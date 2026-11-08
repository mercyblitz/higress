# Higress 新人入职计划

> 为有丰富开发经验、但初次接触云原生网关技术栈（Istio/Envoy/Wasm）的工程师定制。
> 仓库：higress-group/higress（CNCF Sandbox 项目，Go 控制面 + Envoy 数据面 + 多语言 Wasm 插件）

---

## Phase 1 — Foundation（第 1 周）

### 1.1 环境搭建（预计 1~2 天）

**前置依赖：**

| 工具 | 要求 | 用途 |
|---|---|---|
| Go | ≥ 1.26（以 `go.mod` 为准） | 控制面、wasm-go 插件 |
| Docker Desktop | 最新，分配 ≥ 8GB 内存 | all-in-one 体验、kind 集群、e2e |
| kind + kubectl | kind ≥ 0.20 | e2e 测试环境 |
| Helm | v3 | 安装 Higress |
| TinyGo | 可选 | wasm 插件本地构建（Docker 构建方式可不用） |
| protoc / buf | 可选 | 仅改动 API 定义时需要（`make gen-api`） |

**Step 1：先体验产品（30 分钟，强烈建议先做）**

不需要编译任何东西，直接跑官方 all-in-one 镜像，建立对产品形态的直觉：

```bash
mkdir higress && cd higress
docker run -d --rm --name higress-ai -v ${PWD}:/data \
  -p 8001:8001 -p 8080:8080 -p 8443:8443 \
  higress-registry.cn-hangzhou.cr.aliyuncs.com/higress/all-in-one:latest
```

- 8001 = 控制台 UI（先浏览一遍：路由、插件市场、服务来源）
- 8080 = 网关 HTTP 入口

**Step 2：Fork + Clone + 开发准备**

```bash
# Fork 后克隆你自己的仓库
git clone git@github.com:<your-username>/higress.git
cd higress
git remote add upstream git@github.com:higress-group/higress.git
git remote set-url --push upstream no-ping

# 拉取 istio/envoy 子模块并整理依赖（首次较慢，下载量大）
make prebuild && go mod tidy
```

**Step 3：验证构建**

```bash
go build ./...          # 控制面全量编译
cd plugins/wasm-go
PLUGIN_NAME=request-block make local-build   # 本地构建一个最简单的 Go 插件
```

### 1.2 常见问题排查（Troubleshooting）

| 症状 | 原因与解法 |
|---|---|
| 子模块拉取超时/失败 | `make prebuild` 拉取 istio/envoy 子模块体积大。国内网络给 git 配置代理；或浅克隆 `git clone --depth 1`。也可用 `BUILD_WITH_CONTAINER=true make build` 走容器化构建，绕开本地环境差异 |
| 拉镜像超时 | 换官方镜像源：北美 `higress-registry.us-west-1.cr.aliyuncs.com`，东南亚 `higress-registry.ap-southeast-7.cr.aliyuncs.com` |
| e2e 起不来/kind OOM | Docker Desktop 内存调到 8GB+；先 `make delete-cluster` 清理残留 kind 集群再重跑 |
| `local-build` 报错 GOOS 不支持 | 必须用仓库自带的 Makefile 目标（它自动设置 `GOOS=wasip1 GOARCH=wasm -buildmode=c-shared`），不要手敲 `go build` |
| 插件 CI 不编译你的插件 | 批量构建脚本只编译 `VERSION` 文件以 `-alpha` 结尾的 wasm-go 插件——改插件时把 VERSION 改成如 `1.0.0-alpha` |

### 1.3 必读文档（按此优先级顺序）

1. **`README.md`** —— 项目定位：AI 原生 API 网关 + MCP Server 托管 + Ingress 控制器（1 小时）
2. **`docs/architecture.md`** + 官网开发者指南（https://higress.cn/en/docs/latest/dev/architecture/）—— 控制面如何把 Ingress/Gateway API 翻译成 Envoy 配置（核心！）
3. **`CONTRIBUTING_EN.md`** —— 分支模型、提交规范、`changes/` 目录约定、测试要求
4. **`AGENTS.md``（仓库根目录）+ `docs/developers/agent-assisted-contributions.md`** —— **如果你会用 AI 编程工具（大概率会），这条是硬性门禁**：AI 实质性参与的贡献必须先获得维护者批准的 Proposal Issue + Design Issue 才能动手实现；仅拼写/标点/空白/格式类纯文档修正可豁免
5. **`plugins/README.md` + `plugins/wasm-go/README.md`** —— 插件框架与贡献流程
6. **`test/README_CN.md`** —— e2e 测试体系（Ingress/Gateway API 一致性 + WasmPlugin 测试）

**背景补课（针对新栈，每天 1 小时即可，边做边学）：**
- Istio 流量管理基础概念（VirtualService/DestinationRule 是理解 `pkg/ingress` 的前提）
- Envoy HTTP filter 生命周期（理解插件在请求链路中的位置）
- proxy-wasm ABI 基本概念（理解 WASM 插件为何能热更新）
- Kubernetes Gateway API（Higress 是一致性实现，未来方向）

---

## Phase 2 — Exploration（第 2~3 周）

### 2.1 代码地图（按重要性排序）

```
cmd/higress/          控制面入口
pkg/bootstrap/        控制面启动装配
pkg/ingress/          Ingress/Gateway API → Istio/Envoy 配置翻译（最核心）
pkg/                  cert、config、kube 等支撑包
api/                  CRD 定义（extensions/v1alpha1 如 WasmPlugin）
registry/             服务发现集成（nacos/consul/eureka/zookeeper...）
plugins/wasm-go/extensions/   ~59 个 Go WASM 插件（ai-* 是重头戏，每个是独立 Go module）
plugins/wasm-rust|wasm-cpp|  其他语言插件
hgctl/                CLI 工具（独立 Go module）
test/e2e/conformance/ 一致性/e2e 测试
```

### 2.2 动手实验（由浅入深，每个都是一次"跑通"的胜利）

1. **读懂一个最小插件的完整链路**：`plugins/wasm-go/extensions/request-block/`（逻辑最简单）→ 再看 `key-auth`。跟踪：CRD 配置如何传入插件 → `OnPluginStart` → HTTP 处理回调
2. **跑控制面单测**：`go test ./pkg/ingress/...`，打开 `-run` 跑几个用例，观察 golden 文件（`*.golden`）机制——这是理解配置翻译行为的捷径
3. **在 all-in-one 环境里手工装一个 WasmPlugin**：参照 `plugins/README.md` 里的 YAML，把 request-block 配上你的路由，验证请求被拦截——打通"配置 → 生效"的全链路体感
4. **跑一个单插件 e2e**：
   ```bash
   PLUGIN_NAME=request-block TEST_SHORTNAME=<某个用例> make higress-wasmplugin-test-skip-docker-build
   ```
   然后照着 `test/e2e/conformance/tests/` 里的现有用例（如 `httproute-simple-same-namespace.go` + `.yaml`）给自己练习：为某个还没覆盖的场景写一个测试
5. **选一个 ai-* 插件深读**（建议 `ai-proxy`，它是项目核心卖点）：看 README 配置 → main.go 流程 → provider 抽象

### 2.3 新手任务推荐（当前真实开放的 issue，按建议顺序）

**⭐ 首选：[#5296](https://github.com/higress-group/higress/issues/5296) — 修复 mcp-server 中文 README 中遗留的合并冲突标记**
- `plugins/wasm-go/extensions/mcp-server/README.md` 里有 4 处 `<<<<<<< HEAD` / `=======` / `>>>>>>>` 冲突标记（约 112、290、318、326 行）
- 纯文档格式修复，**按项目政策可豁免 AI 门禁 issue-spec 流程**；工作量半天内，能完整走一遍"认领 → 修复 → PR → CI → 合并"全流程
- 记得按规范在 `changes/` 目录加一个说明 md 文件
- ⚠️ 动手前先在 issue 下留言认领，并确认没有已关联的 PR

**次选（带 good first issue 标签，动手前同样先确认未被认领）：**
- **[#1734](https://github.com/higress-group/higress/issues/1734) — 实现 ollama e2e 测试用例**：适合练手 e2e 体系，顺带理解 ai-proxy
- **[#1725](https://github.com/higress-group/higress/issues/1725) — 实现 azure e2e 测试用例**：同上
- **[#1514](https://github.com/higress-group/higress/issues/1514) / [#1022](https://github.com/higress-group/higress/issues/1022)**：偏功能讨论，可先参与讨论练表达
- ⚠️ [#3207](https://github.com/higress-group/higress/issues/3207)（good first issue 标签）评论区显示已有人在做，别撞车

**备选策略**：用 `gh issue list -R higress-group/higress --label "level/easy"` 找标记为 easy 的 issue；或者直接挑一个你读代码时发现的小 bug / 缺测试的场景（CONTRIBUTING 明确欢迎"发现错别字就修、缺测试就补"）。

---

## Phase 3 — Integration（第 4 周起）

### 3.1 团队流程速查

- **提交信息**：`docs:` / `feature:` / `bugfix:` / `refactor:` / `test:` 前缀，信息要显式
- **每次 PR**：在 `changes/` 下新建 md 简述变更；按 PR 模板填写
- **分支**：一切 PR 面向 `main` 分支
- **测试硬性要求**：新 Wasm 插件单测覆盖率 ≥30%（CI 强制）；改动代码 patch 覆盖率 ≥50%（Codecov 强制）；bug 修复必须带回归测试
- **⚠️ AI 协作门禁（对你尤其重要）**：只要 AI 工具实质性参与（设计/实现/测试/PR 撰写），就必须先走 issue-spec：Proposal Issue → 维护者批准 → Design Issue → 批准 → 才能实现。PR 中必须声明 AI 参与并披露提示词。**在提任何实质代码 PR 之前，把 `docs/developers/agent-assisted-contributions.md` 完整读一遍**

### 3.2 早期胜利路线（建议节奏）

1. **第 4 周**：完成 [#5296](https://github.com/higress-group/higress/issues/5296) 或一个 easy 文档 PR，拿到第一个合并（建立肌肉记忆 + CI 熟悉度）
2. **第 4~5 周**：认领一个小型 bug 修复（推荐从单个插件入手，如 ai-token-ratelimit / frontend-gray 相关的近期 issue，影响面小、验证路径清晰）；若用 AI 辅助修复，则按门禁先提 Proposal/Design
3. **第 5~6 周**：给某个插件补单元测试或 e2e 用例（同时满足覆盖率要求，一举两得）
4. **第 6 周后**：提一个自己的小型功能/enhancement Proposal，完整走一遍 issue-spec 设计流程——这是走向深度贡献的分水岭

### 3.3 融入社区

- 加入 Discord（README 有链接），每月社区会议见 `MEETINGS.md`——例会是最快的"刷脸"方式
- 回答别人 issue 里的疑问、review 他人 PR，都算贡献（CONTRIBUTING 原话："任何帮助都是贡献"）
- 遵循 CNCF 行为准则；安全问题走 `SECURITY.md` 私密流程，绝不公开讨论

### 3.4 学习资源清单

- 官网文档（使用 + 开发双视角）：https://higress.cn/docs/latest/
- 插件市场（看生态全貌）：https://higress.cn/en/plugin/
- Wasm Go SDK（插件 API 真正的定义处）：https://github.com/higress-group/wasm-go
- Istio 官方文档（流量管理章节）
- Envoy 官方文档（HTTP filters 概念即可）
- 仓库内 `docs/developers/` 下所有文档（篇幅不大，全读）

---

## 检查点

| 时间 | 你应该能做到 |
|---|---|
| 第 1 周末 | 本地跑起 all-in-one + 控制面编译通过 + 读完前 4 篇必读文档 |
| 第 3 周末 | 讲清"Ingress YAML 如何变成 Envoy 配置"整条链路；跑通至少一个 e2e 用例；认领了第一个 issue |
| 第 4 周末 | 第一个 PR 已提交（文档类） |
| 第 6 周末 | 第一个代码 PR（bug 修复或测试）在 review 中；理解 AI 门禁流程 |

> 核心原则：**动手优先于阅读**。每读一个概念，立刻去代码/运行环境里找到它的对应物。
