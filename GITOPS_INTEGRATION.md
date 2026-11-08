# GitOps 与 Higress 整合方案

> 承接《SCG_MIGRATION_PLAN.md》：该计划 W2 产出的"路由/插件 YAML 存档"正好作为本方案的 Git 仓库种子；
> W4 的"配置变更演练"从 100 次手工变更升级为 100 个 Git PR。
> 适用前提：K8s 部署模式（Helm 安装）。Higress 所有配置皆K8s 资源——这是 GitOps 整合的根基。

---

## 一、为什么 Higress 天然适配 GitOps

Higress 没有私有配置文件/配置数据库，**全部配置即 K8s 资源**，GitOps 工具（Argo CD/Flux）天然可管：

| 配置对象 | K8s 资源 | GitOps 管理方式 |
|---|---|---|
| 路由规则 | `Ingress` / Gateway API `HTTPRoute` | 直接纳管 ✅ |
| 网关全局配置（连接数等） | ConfigMap `higress-config` | ⚠️ Helm lookup 合并式管理，见 4.3 |
| 插件启用+参数+镜像版本 | `WasmPlugin`（extensions.higress.io） | 直接纳管 ✅ |
| 注册中心/服务来源 | `McpBridge`（networking.higress.io） | 直接纳管 ✅ |
| 协议转换 | `Http2Rpc`（networking.higress.io） | 直接纳管 ✅ |
| Envoy 级精细控制（逃生舱） | `EnvoyFilter` | 直接纳管，但慎用 |
| TLS 证书 | `Secret` / cert-manager `Certificate` | 见 4.4，绝不进明文 Git |
| Higress 自身安装 | Helm release | Argo 声明式 Helm 纳管 ✅ |

且 Higress 的热更新特性与 GitOps 是**互补增强**：Argo sync → CR 变更 → 控制面秒级 xDS 推送 → 生效，**全程无进程重启、不断长连接**。回滚 = `git revert` + sync，秒级生效——这比 SCG 时代"回滚要重启、变更断连接"的体验高一个量级。

## 二、推荐架构（Argo CD 为主）

选型建议：**Argo CD**（UI 友好、团队从零上手快，与"对项目不熟"的背景匹配）；纯拉取式团队可选 Flux。核心流转：

```
开发提 PR（路由/插件配置变更）
   → CI 静态校验（kustomize build + kubeconform CRD schema 校验 + 服务端 dry-run）
   → 合并进 Git 仓库（唯一事实源）
   → Argo CD：dev 自动 sync / prod 手动 sync + 变更窗口
   → 集群内 CR 变更
   → Higress Controller 翻译 → xDS 热推送 → Gateway 生效（无重启）
```

配置仓库结构（kustomize base + overlays 多环境晋升）：

```
gateway-config-repo/
├── base/
│   ├── mcpbridge/        # 注册中心数据源（nacos/eureka/consul/zk）
│   ├── routes/           # Ingress / HTTPRoute（SCG 迁移的主战场）
│   ├── wasmplugins/      # 插件启用+配置+镜像 tag
│   ├── tls/              # cert-manager Certificate / Issuer
│   └── envoyfilters/     # 逃生舱，默认空
├── overlays/
│   ├── dev/              # autoSync=true, selfHeal=true（练手环境随意造）
│   ├── staging/          # autoSync=true, 镜像晋升的第一站
│   └── prod/             # 手动 sync + sync window（变更窗口管控）
└── bootstrap/            # Argo Application（app-of-apps 自举）
```

## 三、必须处理好的三个冲突点（整合成败关键）

### 3.1 Higress Console 与 Git 的"双事实源"冲突 ⭐ 最重要

Console（8001）白屏编辑路由/插件时，是**直接改集群里的 CR**——GitOps 视角这就是"漂移"（drift）。策略必须二选一，推荐前者：

**策略 A（推荐）：Git 为唯一事实源，Console 降级为观测台**
- Console 只用其监控/Grafana/Prometheus 视图；配置变更一律走 PR
- dev 环境：Argo `selfHeal=true`——白屏改动自动被回滚，倒逼走 Git
- prod 环境：`selfHeal=false` + 漂移告警——允许"破窗"紧急白屏救火，但告警要求事后补 PR（break-glass 流程）

**策略 B：按域划分**——Console 管"探索性/演示"配置，Git 管生产配置。不建议，边界会慢慢失守。

### 3.2 prune（孤儿资源回收）要分级开

Console 早期创建的资源（如演示路由）没有 Git 对应物，`prune=true` 会被 Argo **直接删除**，引发事故：
- 初始纳管阶段：`prune=false`，先 Git 化全部存量（`argocd app manifests` / console 导出），对齐后再开
- 纳管完成后：dev/staging 开 prune，prod 谨慎开 + `ignoreDifferences`（如 console 加的 label）
- **WasmPlugin 的 `spec.url` 镜像 tag 用 `ignoreDifferences` 是错误示范，别用**——tag 必须受 Git 管控

### 3.3 插件镜像版本晋升（与常规 GitOps 最大的差异点）

`WasmPlugin.spec.url` 是 `oci://registry/.../插件名:tag` 形式——**不在 Pod spec 里，Argo Image Updater 探测不到**，无法自动跟 tag。落地流程：

1. 插件源码改动（如 SCG 迁移的自定义 Filter）→ CI 构建 `plugin.wasm` → 推镜像仓（tag 取自插件目录的 `VERSION` 文件）
2. **手动（或脚本自动）提 PR**：更新 overlays 中 `wasmplugins/xxx.yaml` 的 `spec.url` tag
3. PR 合并 → staging 自动 sync → 验证 → prod 手动 sync 晋升
4. 规则：**禁用 `latest`/浮动 tag**（GitOps 可审计性要求 tag 可追溯），插件 CI 遵循仓库约定（参与官方批量构建需 `VERSION` 以 `-alpha` 结尾，见 AGENTS.md）

## 四、专项细节

### 4.1 sync wave 依赖序

```
wave 0: namespace / CRD（由 Helm 层管，不进 Argo prune 范围）
wave 1: McpBridge（服务来源）+ cert-manager 资源
wave 2: WasmPlugin（依赖镜像可拉取）
wave 3: Ingress / HTTPRoute（依赖前面就绪）
```
用 kustomize annotation `argocd.argoproj.io/sync-wave` 标注。

### 4.2 10 万 QPS 生产环境的变更安全栏

- **prod 手动 sync + sync window**（如仅工作日 10:00-16:00 可 sync，避开大促封网）
- 每次变更 PR 强制附**影响面说明**（哪些路由/插件受影响）
- 回滚演练 = `git revert` + 一次 sync（第 4 周演练时纳入：100 个 PR 中故意掺 3 个"故障回滚"）
- 大批量变更分批：先合 McpBridge+少量路由 → 观测 P99/错误率 → 再放量（Argo sync 本身不重启进程，风险在配置语义错误而非连接中断）

### 4.3 `higress-config` ConfigMap：不要让 Argo 直接纳管

Helm 模板用 `lookup` 合并既有 data——意味着它被 Helm release"部分所有"。正确姿势：
- **网关全局配置的变更走 Helm values**（`connectionLimits` 等），即"Argo 管理声明式 Helm release"（`source: helm, valuesFiles`），而不是单独把 ConfigMap 拉进 kustomize
- Console 写入此 ConfigMap 的全局配置项，迁移时一次性"导出→固化为 Helm values"

### 4.4 证书与密钥

- TLS 证书：首选 **cert-manager + Let's Encrypt**（Higress 官方支持自动签发续期），Git 里只放 `Certificate`/`Issuer` 声明
- 注册中心凭据等 Secret：Sealed Secrets / SOPS / External Secrets Operator 任选，**明文 Secret 不进 Git**
- 注意 McpBridge 里引用的凭据也是 Secret，走同一通道

### 4.5 提前在 CI 拦截配置错误（比"发布后回滚"便宜 100 倍）

在 PR 流水线里：
1. `kustomize build overlays/<env> | kubeconform -schema-location <CRD schema>`——CRD 字段名写错当场红
2. server-side dry-run（`kubectl apply --dry-run=server`）——RBAC/quota/字段约束问题提前暴露
3. 沉淀"配置冒烟集"：对变更涉及的路由跑固定 curl 断言（可复用 SCG 迁移的冒烟脚本），进 dev 集群自动执行
4. 高价值加分项：把仓库的 golden 测试思路搬过来——关键路由在 CI 用 `test/e2e/conformance` 的思路做轻量断言

### 4.6 非 K8s（standalone）模式说明

若用 higress-standalone（纯 Docker/主机部署），配置是本地文件而非 CRD，标准 K8s GitOps 不适用——只能做"Git 仓库存配置文件 + 部署侧拉取"的类 GitOps。**既然要做 GitOps，建议直接选 K8s 部署模式**，这也是与 SCG 迁移计划（Helm 安装）一致的方向。

## 五、与一个月迁移计划的衔接

| 原计划节点 | GitOps 化调整 |
|---|---|
| W2 Day 3-4 白屏迁移+导出 YAML | **直接改为"写 overlays YAML 提 PR"**，白屏只做即时验证；产出物天然就是 GitOps 仓库 v1.0 |
| W2 冒烟验证 | CI 冒烟集同步建设（4.5 节） |
| W3 插件开发 | 插件 CI 增加"推镜像 + 提 tag 晋升 PR"两个 job |
| W4 配置变更演练（100 次） | 改为 100 个 PR 流水验证，掺 3 个回滚演练 |
| W4 灰度切流 | **切流本身也是 Git 变更**（前置 LB 权重仍需外部执行，但路由级灰度可走 overlay 参数） |

新增工作量评估：GitOps 基建（Argo 安装、仓库骨架、CI 校验）约 3~4 人日，W2 内吸收；对 W3/W4 的影响是把原本"手工变更"变成"提 PR"，净成本≈0，且把灰度期的"配置错误"风险大幅前移。

## 六、风险清单

| 风险 | 对策 |
|---|---|
| Console 白屏改动与 Git 漂移打架 | 策略 A + selfHeal 分级 + 破窗流程（3.1） |
| prune 误删存量资源 | 纳管期 prune=false，对齐后再开（3.2） |
| WasmPlugin tag 无法自动更新（非 Pod spec） | 接受手动 PR 晋升，禁浮动 tag（3.3） |
| `higress-config` 双属（Helm lookup + Console 写入） | 走 Helm values 通道，不单独纳管（4.3） |
| prod 误 sync 大变更 | 手动 sync + sync window + 分批合并 |
| 团队 GitOps 经验为零 | Argo CD UI 降低门槛；dev 环境先跑两周"随意造"建立直觉 |

---

## 七、Argo CD 落地清单（确认选型后的具体实施）

### 7.1 安装初始化（半天）

```bash
kubectl create namespace argocd
kubectl apply -n argocd -k https://github.com/argocd/argocd-cd/manifests/core  # 或官方 helm chart
argocd admin initial-password -n argocd        # 拿初始密码，立刻改掉
# ingress 暴露 UI：直接复用 Higress 给 argocd-server 配一条路由（吃自己的狗粮）
```

### 7.2 app-of-apps 自举（放进配置仓库 `bootstrap/`）

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: higress-gateway-config
  namespace: argocd
spec:
  project: higress
  source:
    repoURL: https://git.example.com/team/gateway-config.git
    targetRevision: main
    path: bootstrap/apps      # 该目录下放各环境 Application
  destination:
    server: https://kubernetes.default.svc
    namespace: argocd
  syncPolicy:
    automated: { selfHeal: true }    # bootstrap 自身自动同步
```

### 7.3 三环境 Application 模板（策略差异即第四节规则的落地）

**dev（自动同步 + 自愈 + prune）**：
```yaml
spec:
  syncPolicy:
    automated: { prune: true, selfHeal: true }   # 白屏改动被自动回滚
    syncOptions: [ CreateNamespace=true, ApplyOutOfSyncOnly=true ]
```

**staging（自动同步，但不开 selfHeal）**：
```yaml
spec:
  syncPolicy:
    automated: { prune: true, selfHeal: false }  # 允许临时热修，靠告警追补 PR
```

**prod（手动 sync + 变更窗口）**：
```yaml
spec:
  syncPolicy:
    syncOptions: [ Prune=false ]    # 纳管期 prune 关闭；存量对齐后改 true
  ignoreDifferences: []            # 按需补充，勿放 WasmPlugin 的 url tag
```
变更窗口用 `AppProject` 的 `syncWindows`（如 `kind: Mon-Fri 10:00-16:00, allow: true`）。

### 7.4 sync wave 依赖序（kustomize 注解）

```yaml
metadata:
  annotations:
    argocd.argoproj.io/sync-wave: "-1"   # McpBridge / cert-manager
    argocd.argoproj.io/sync-wave: "0"    # WasmPlugin
    argocd.argoproj.io/sync-wave: "1"    # Ingress / HTTPRoute
```

### 7.5 漂移与失败告警（对应 3.1 破窗流程）

`argocd-notifications-cm` 里配两个 trigger：
- `on-sync-failed`：sync 失败（CI 没拦住的配置错误）→ 群告警
- 自定义 `on-out-of-sync`：`when: app.status.sync.status == 'OutOfSync'` 且持续 10 分钟 → 告警（dev 意味着 selfHeal 在打回白屏改动；prod 意味着有人破窗救火，**触发"24h 内补 PR"流程**）

### 7.6 常用命令速查

| 场景 | 命令 |
|---|---|
| 提交前看差异 | `argocd app diff higress-prod` |
| 手动触发晋升 | `argocd app sync higress-prod`（prod 每次都从 UI/CLI 显式执行） |
| 回滚 | **`git revert` + sync**（不要依赖 `argocd app rollback`——它已被官方标记弃用，且会脱离 Git 状态） |
| 纳管存量资源导出 | `argocd app manifests` / `kubectl get ingress,wasmplugin,mcpbridge -A -o yaml` 去污后入库 |
| 查看合并结果 | `kustomize build overlays/prod`（本地与 CI 各跑一遍） |

### 7.7 与 Higress Helm release 的关系（对应 4.3）

Higress 安装本身也用 Argo 管理：Application 的 source 直接指向 higress helm chart（`source.helm.valuesFiles`），网关全局配置变更 = 修改 values 文件提 PR。**这样 `higress-config` ConfigMap 由 Helm 渲染，Console/手工对它的直接修改才会被完整暴露为漂移。**
