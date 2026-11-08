# Spring Cloud Gateway → Higress 二次开发一个月规划

> 定制背景：开发者 Go 不熟练、对本项目不熟悉；目标是把 SCG 功能迁移到 Higress；
> 需要稳定性评估结论 + 10 万 QPS 下的资源对比（比率表达）。
> 配套阅读：仓库根目录 `ONBOARDING.md`（环境搭建与排障细节，本计划不重复）。

---

## 一、先回答你最关心的两个问题（结论前置）

### 1.1 10 万 QPS 资源对比（比率）

**Higress 官方团队实测数据**（Higress Committer 发布，同吞吐量水平对比）：

| 场景 | SCG CPU 开销 | SCG 内存开销 |
|---|---|---|
| 双方均不开插件/Filter | ≈ Higress 的 **3.30 倍** | ≈ Higress 的 **4.88 倍** |
| 双方均开启对应功能（Higress Transformer vs SCG GatewayFilters） | ≈ Higress 的 **2.98 倍** | ≈ Higress 的 **3.19 倍** |

**第三方交叉验证数据**（8C16G，wrk -t4 -c256）：
- Envoy：21,350 req/s，P99 9.1ms，内存 238MB
- SCG：8,240 req/s，P99 42.7ms，内存 486MB
- 即吞吐 ≈ SCG 的 **2.6 倍**，内存 ≈ SCG 的 **1/2**，P99 延迟 ≈ SCG 的 **1/4.7**

**换算到 10 万 QPS 的预估配置**（以 SCG 单节点 4C8G 承载 ~8-10k QPS 的常见生产经验为基准）：

| 方案 | 10 万 QPS 所需节点（4C8G） | 总核数 | 总内存 | 比率（SCG : Higress） |
|---|---|---|---|---|
| SCG 集群 | 13~20 台（需留 GC/长连接余量） | 52~80C | 104~160G | CPU **1 : 0.25~0.33**（约省 2/3 强），内存 **1 : 0.20~0.28**（约省 3/4 强） |
| Higress 集群（建议 N+1） | 4~5 台 | 16~20C | 32~40G | |

> ⚠️ 以上是公开数据的推算，**第 2 周必须用你自己的真实业务报文压测出同口径比率**（方法见 4.2 节）。
> 额外优势：Higress 配置热更新不走进程重启（SCG reload 会断长连接），大促类流量突增场景扩缩容更平滑。

### 1.2 稳定性评估：Higress 不如 SCG 稳吗？

**客观证据（Higress 侧）**：
- 源自阿里内部网关产品，公开表述经过"数十万 QPS"生产验证，现为 CNCF Sandbox 项目
- 数据面 Envoy 是 CNCF 毕业项目，同类的 C++ 网关内核被苹果、Stripe 等大规模使用
- 仓库自带完整 e2e 一致性测试套件（Ingress API / Gateway API / WasmPlugin 三类，`make higress-conformance-test` 等）
- 架构上避免了 SCG 的两个固有稳定性短板：**JVM GC 停顿毛刺**、**配置变更导致的连接中断**（Higress 毫秒级热更新、长连接不断）

**SCG 的"稳"来自哪里**：Spring 生态成熟度高、你团队对它更熟、出问题能改 Java 源码。这三点与网关内核稳定性无关，而是**熟悉度与生态风险**——这正是本计划第 1 周要系统化消除的。

**结论**：内核层面 Higress（Envoy）稳定性不弱于 SCG，且有架构优势；风险主要在"团队 unfamiliarity + 迁移期配置错误"，用 1.3 节的验证矩阵 + 第 4 周的灰度机制兜住。

---

## 二、SCG → Higress 能力映射表（迁移工作量的决定因素）

先盘清你现有 SCG 用了什么，对着下表打勾。**绝大多数能力是"配置迁移"而非"开发"**，真正要写代码的只有自定义 Filter。

| SCG 能力 | Higress 对应 | 迁移方式 |
|---|---|---|
| Route/Predicate（Path/Method/Header/Query 匹配） | Ingress 注解 或 Gateway API HTTPRoute 匹配规则 | 纯配置 |
| `lb://` 服务发现（Nacos/Eureka/Consul/ZK） | `registry/` 原生集成（nacos/consul/eureka/zookeeper/direct）| 配置 McpBridge/Registry 来源 |
| LoadBalancerClientFilter | 路由后端 + Envoy 负载均衡 | 纯配置 |
| AddRequestHeader / RemoveRequestHeader / AddRequestParameter / MapRequestHeader / DedupeResponseHeader 等 | **transformer 插件**（官方对 SCG 专门做过对标） | 插件配置 |
| RewritePath / PrefixPath / StripPrefix | higress.io rewrite 注解 或 nginx-rewrite-compatible 插件 | 纯配置 |
| SetPath / SetStatus / 自定义响应 | custom-response 插件（wasm-cpp） | 插件配置 |
| CORS | cors 插件 或注解 | 插件配置 |
| RequestRateLimiter（Redis 令牌桶） | key-rate-limit / cluster-key-rate-limit（集群限流） | 插件配置 |
| JWT/Key/Basic/HMAC 认证 | jwt-auth / key-auth / basic-auth / hmac-auth 插件 | 插件配置 |
| OAuth2 / OIDC / TokenRelay | oidc 插件 | 插件配置 |
| CircuitBreaker（Resilience4j/Sentinel 熔断） | Envoy outlier detection（DestinationRule 配置）+ 主动健康检查（issue [#5257](https://github.com/higress-group/higress/issues/5257) 在推进） | 配置 + 验证（语义差异详见附录 A.3） |
| Retry | 路由级 retry 策略（超时/重试注解） | 纯配置 |
| Weighted / 灰度分流 | higress.io 灰度注解（按 header/cookie 权重分流） | 纯配置 |
| RequestSize 限制 | 注解（body size limit） | 纯配置 |
| WebSocket / HTTP2 / gRPC 透传 | 原生支持 | 验证即可 |
| ModifyRequestBody / ModifyResponseBody（自定义逻辑） | transformer（简单）/ **wasm-go 自定义插件（复杂逻辑）** | ⭐ 需要开发 |
| 自定义 GlobalFilter（业务逻辑） | **wasm-go 自定义插件**（全局 = 域名级匹配） | ⭐ 需要开发 |
| 限流后 Sentinel 规则联动 | wasm 插件内置逻辑或集群限流 | 需要验证/开发 |

> 参考：官方 issue [#774](https://github.com/higress-group/higress/issues/774)《SpringCloudGateway迁移到MSE Higress最佳实践》含完整能力对标图；
> 官方博客《Wasm 实现 Higress 扩展，性能是 Spring Cloud Gateway 的 3 倍》演示了典型 GatewayFilter 用 transformer 替代。

---

## 三、四周总体节奏

```
W1 打基线        W2 核心迁移+压测      W3 缺口开发(Go)      W4 稳定性+灰度切换
─────────────   ─────────────────   ─────────────────   ─────────────────
环境+功能盘点     服务发现/路由/插件     自定义 wasm-go 插件   soak/故障演练
SCG 基准压测     10万QPS 压测出比率    单测+本地调试        灰度 5%→25%→100%
稳定性评估矩阵    缺口清单确认          Go 定向补课          回滚预案演练
```

---

## 四、每周详细任务

### 第 1 周：基线建立（这是评估的地基）

**目标产出**：SCG 功能清单、SCG 基准性能数据、Higress 环境就绪、稳定性评估矩阵 v1。

**Day 1-2 环境就绪**
1. 按 `ONBOARDING.md` Phase 1 完成：all-in-one 体验 → `make prebuild && go mod tidy` → 控制面编译通过
2. 搭建压测专用 K8s 环境（kind 或真实集群）：
   ```bash
   # helm 方式安装（生产同构，比 all-in-one 更接近真实部署）
   helm install higress -n higress-system higress.io/higress --create-namespace
   ```
3. 压测工具准备：wrk / vegeta（HTTP），后续对比用**同一工具、同一报文、同一后端**

**Day 3 功能盘点（最重要的一天）**
- 导出生产 SCG 全部路由配置（application.yml / 配置中心里的 routes）
- 对照第二节映射表逐条打勾，分成三类：**A 纯配置迁移 / B 插件配置迁移 / C 需开发**
- 产出《SCG 功能迁移清单.xlsx/md》，C 类就是你的二次开发范围（经验上通常只有 2~4 个）

**Day 4-5 SCG 基准压测**
- 用真实业务报文形状（典型 header 数、body 大小、连接复用率）压现有 SCG 集群，记录：单节点极限 QPS、P99、CPU 峰值、RSS 内存
- **这一步是后面所有"比率"的分母，必须先做**

**稳定性评估矩阵 v1（Day 5 交付）**

| 维度 | SCG | Higress | 验证方法（第 4 周执行） |
|---|---|---|---|
| 配置热更新 | 需 reload，断长连接 | xDS 毫秒级推送 | 路由批量变更 1000 次，观测连接数/P99 |
| GC/运行时抖动 | JVM GC 毛刺 | 无 GC（Envoy C++） | 7 天 soak 看 P99 抖动带 |
| 进程崩溃影响 | 整个 JVM 挂 | 插件崩溃仅插件失效，主进程不受影响 | kill -9 插件故障注入 |
| 长连接（SSE/WebSocket） | reload 时断 | 不断 | 压测中滚动变更配置，观测 |
| 生态成熟度/可调试性 | 高（团队熟） | 待建立 | ——团队熟悉度就是最大风险项 |

### 第 2 周：核心迁移 + 10 万 QPS 压测

**Day 1-2 服务发现对接**（SCG 迁移的关键路径）
- 确认现有注册中心（Nacos/Eureka/Consul/ZK 均原生支持），配置 McpBridge 数据来源
- 验证：服务列表同步、实例上下线感知速度（对比 SCG 的刷新周期）

**Day 3-4 路由与插件配置迁移**
- 按清单把 A 类（纯配置）+ B 类（插件配置）全部迁到 Higress，**先在测试 namespace 用控制台白屏操作**，导出 YAML 存档
- 每迁 10 条路由做一次冒烟验证（curl 集合，把 SCG 的集成测试借来用）
- 注意 transformer 的坑：同时处理请求+响应需要挂两个实例（request/response 各一）

**Day 5 首轮 10 万 QPS 压测（产出你的比率）**

压测方法（口径必须与 SCG 基线完全一致）：
```bash
# 同报文、同并发模型、同后端（后端最好是同一组 mock/真实服务）
wrk -t8 -c512 -d300s -s biz.lua http://<higress-gateway>/api/xxx
```
逐级加压：5万 → 8万 → 10万 → 12万（验证余量），记录每档的 CPU/内存/P99，填入模板：

| 指标 | SCG @10万QPS | Higress @10万QPS | 比率 SCG:Higress |
|---|---|---|---|
| 网关总核数 | | | 1 : x |
| 网关总内存 | | | 1 : x |
| P99 延迟 | | | x : 1 |
| P999/P9999 | | | |
| 错误率 | | | |

> 官方参考比率：CPU 1:0.30、内存 1:0.20（无插件）；开插件后 CPU 1:0.34、内存 1:0.31。
> 若你的实测比率偏差超过 2 倍，优先排查：插件数量是否过多、body 是否被缓冲、后端瓶颈。

**Day 5 同时冻结《缺口清单》**：C 类功能的详细需求（输入/输出/错误码/日志要求），第 3 周的开发任务书。

### 第 3 周：自定义插件开发（Go 定向补课 + wasm-go 实战）

**关键认知：二次开发不需要懂 Higress 控制面源码。** 自定义 Filter 全部走 wasm-go 插件——独立 Go module、~200 行起步、只接触 SDK 回调 API，Go 新手的可行切入点。

**Go 定向补课（每天上午 1 小时，只学与插件有关的子集）**
1. Go 语法速通（A Tour of Go 前 10 节足够）：struct/interface、slice/map、error 处理、JSON 解析
2. 不需要：goroutine 深水区、channel 模式、泛型——wasm 插件基本用不到
3. 读 `plugins/wasm-go/extensions/request-block/main.go`（最短完整示例）+ `transformer/`（对标 SCG 的成熟写法）

**开发流程（每个插件）**
```bash
cd plugins/wasm-go/extensions
cp -r request-block my-scg-filter && cd my-scg-filter
# 修改 main.go：OnPluginStart 解析配置 → 解析请求回调里写业务逻辑
# VERSION 改为 1.0.0（自用不必 -alpha，要贡献回社区才需注意 CI 规则）
PLUGIN_NAME=my-scg-filter make build          # 产出 plugin.wasm
```
1. 配置解析参考 `transformer` 的 `parseConfig`；请求头/Query 读写参考 SDK（github.com/higress-group/wasm-go）
2. 每个插件补 `main_test.go`，**覆盖率 ≥30%**（本地跑法：`go test -cover`）
3. 本地调试：all-in-one 环境挂载 wasm 文件 → 控制台配置该插件 → curl 验证
4. 排错抓手：`log-request-response` 插件先挂上，请求/响应一目了然

**开发顺序建议**：先做最简单的一个（比如纯 header 改写）打通全流程，再做逻辑最复杂的那个。
**AI 辅助提示**：内部 fork 自用不受仓库门禁限制，可放心用 AI 辅助写插件；若未来想把这个插件贡献回 higress-group/higress 上游，必须先读 `docs/developers/agent-assisted-contributions.md`（需维护者批准 Proposal/Design Issue）。

### 第 4 周：稳定性验证 + 灰度切换

**Day 1-2 稳定性实测（执行第 1 周的矩阵）**
1. **Soak**：10 万 QPS 的 70% 持续压 24~48h，看内存泄漏（RSS 曲线）与 P99 抖动带
2. **配置变更演练**：压测中执行路由/插件批量变更 100 次，观测长连接是否断、P99 是否尖刺（这是 Higress 相对 SCG 的核心加分项，必须量化记录）
3. **故障注入**：kill gateway pod（验证多副本自愈与客户端重试）、断注册中心连接（验证端点缓存兜底）、插件故意 panic（验证沙箱隔离、主进程不挂）
4. **升级演练**：Higress 版本升级一次，验证热更新无损

**Day 3 灰度切换方案（SCG 不立刻下线）**
```
阶段1 镜像期：真实流量 100% 复制到 Higress（shadow），只记录不返回 → 对比两边日志/错误率 3 天
阶段2 灰度期：5% → 25% → 50% 真实流量切 Higress（按 header/cookie 分流，出问题秒级切回）
阶段3 全量：100%，SCG 冷备 1~2 周后下线
```
- 切流手段：前置 LB 权重，或 DNS，或客户端网关地址配置中心开关
- **回滚预案**：SCG 集群缩容不销毁，保留一键切回能力；每阶段设 SLO 红线（错误率、P99 超过 SCG 基线即回滚）

**Day 4-5 收尾**
- 补齐压测报告：10 万 QPS 比率表 + soak 结论 + 故障演练记录（给管理层的决策材料）
- 运维交接文档：Higress 控制台常用操作、插件发布流程、常见排障（对照 `ONBOARDING.md` 排障表）
- 制定升级策略：跟随社区 release 节奏（关注 issue [#5298](https://github.com/higress-group/higress/issues/5298) 这类安全公告）

---

## 五、风险与对策

| 风险 | 等级 | 对策 |
|---|---|---|
| Go 不熟导致 C 类插件开发延期 | 高 | 插件模板起步 + AI 辅助 + 第 3 周只安排 2~3 个插件；实在不行可先用 transformer 配置组合顶替部分自定义 Filter |
| 团队对 Higress 不熟，配置出错 | 高 | 镜像期对比验证 + 灰度期秒级回滚 + 每阶段冒烟用 SCG 同一套测试 |
| 压测比率不及公开数据 | 中 | 第 2 周首压即发现，留 2 周调优窗口（插件精简、连接缓冲调优、后端直连） |
| 熔断语义与 Resilience4j 不完全一致 | 中 | 第 2 周用故障注入实测 outlier detection 行为；不满足则进 C 类自研清单 |
| 一个月不够全量切换 | 中 | 本计划 1 个月的终点是"灰度期开始"，全量切换+SCG 下线顺延 1~2 周是正常节奏，不属于失败 |

## 六、每周检查点

| 周末 | 交付物 | 通过标准 |
|---|---|---|
| W1 | SCG 功能清单 + SCG 基准压测数据 + Higress 环境就绪 | 压测数据可复现；清单 A/B/C 分类完成 |
| W2 | 配置迁移完成率 100%（A+B 类）+ 你的 10 万 QPS 比率表 + 缺口清单 | 冒烟全过；比率数据成型 |
| W3 | C 类插件全部上线测试环境 + 单测 | 覆盖率 ≥30%；功能验收通过 |
| W4 | soak/故障演练报告 + 灰度方案获批准 + 灰度开始 | 镜像期对比无差异；回滚演练通过 |

---

## 附录 A：腾讯云栈专项（OTel APM / 日志 / Sentinel）

> 本附录基于确认的实际栈：可观测性 = OpenTelemetry（腾讯云 APM 托管）、日志 = Log4j2/Logback、容错 = Alibaba Sentinel。

### A.1 链路追踪：迁移到腾讯云 APM 托管服务

**先说一个决定架构的事实**：腾讯云 APM 遵循 OTLP 协议，接入点形如 `pl-xxx.ap-<region>.apm.tencentcs.com:4317`，鉴权 Token **以 Resource attribute（`token=xxx`）形式随数据传入**，不是 HTTP header。而 Higress 网关侧的 tracing 配置（`higress-config`）只开放 service/port/采样率/超时四个字段——**无法注入 token，网关不能直连腾讯云接入点**。

**因此架构必须是三段式**：

```
Higress Gateway（envoy.tracers.opentelemetry）
  → 集群内自部署 otel-collector（OTLP gRPC :4317）
    → 注入 token resource attribute → 转发腾讯云 APM 接入点
```

collector 核心配置（这层还能顺带做尾部采样，10 万 QPS 下控制 APM 计费与开销）：

```yaml
receivers:
  otlp:
    protocols: { grpc: { endpoint: 0.0.0.0:4317 } }
processors:
  attributes/token:            # 腾讯云 APM 鉴权：token 走 resource attribute
    actions:
      - { key: token, value: "${TENCENT_APM_TOKEN}", action: upsert }
  tail_sampling:               # 建议生产开启：错误/慢请求全采，正常流量按比例
    policies: [...]
exporters:
  otlphttp/apm:
    endpoint: https://pl-xxx.ap-<region>.apm.tencentcs.com
service:
  pipelines:
    traces:
      receivers: [otlp]
      processors: [attributes/token, tail_sampling]
      exporters: [otlphttp/apm]
```

网关侧只需在 `higress-config` 的 tracing 块指向集群内 collector（走 Helm values 提 PR，见 GITOPS_INTEGRATION.md）：
```yaml
tracing:
  enable: true
  sampling: 100.0          # head 采样交给 collector 精细控制
  opentelemetry:
    service: otel-collector.observability.svc.cluster.local
    port: "4317"
```

**业务应用侧：零迁移**。Java 应用继续用腾讯云增强版 OTel javaagent（`-Dotel.resource.attributes=service.name=xxx,token=xxx`），上报路径不动；网关 span 与应用 span 靠 W3C tracecontext 串成全链路，在 APM 同一业务系统下查看。
**若集群在腾讯云 VPC 内，collector 选内网上报**（省流量费 + 免外网暴露）；Token 进 Secret（External Secrets/SOPS 管理），不进 Git。

### A.2 日志：Log4j2/Logback 的迁移边界

**关键认知：业务应用里的 Log4j2/Logback 与网关迁移完全无关，零改动**——包括 OTel appender 往日志里注入 trace_id 的机制。要迁移的只有"网关自身日志"这一小块：

| 迁移对象 | SCG 现状 | Higress 方案 |
|---|---|---|
| 网关访问日志 | logback 配置输出 | Envoy access log（stdout JSON，格式经 EnvoyFilter 定制，`%TRACE_ID%` 可注入与 APM 同 trace_id） |
| 日志采集 | Logback appender 直推 | stdout → Fluent Bit DaemonSet → 腾讯云 CLS（VPC 内网） |
| 自定义 MDC 字段 | logback MDC | access log format 对齐字段名；或注入 span attribute（wasm 插件，参考 examples/custom-span-attribute） |

**注意**：Higress 的 `higress-config` 全局配置不暴露访问日志开关，access log 格式化需要一次**手写 EnvoyFilter**（本方案允许的逃生舱场景之一）。W1 盘点时把现有 CLS 检索语句/告警依赖的字段列出来，EnvoyFilter 格式尽量对齐，避免下游检索/告警全部重写。

### A.3 Sentinel → Higress 容错能力映射（最大语义差异区）

| Sentinel 能力 | Higress 对应 | 差异与动作 |
|---|---|---|
| 网关流控规则（route/API 维度 QPS + 突发） | key-rate-limit（wasm-cpp，单机）/ cluster-key-rate-limit（Redis，集群全局） | Sentinel 默认单机语义→key-rate-limit 平移；依赖全局阈值的规则必须换 cluster 版 |
| 热点参数限流 | key-rate-limit 按 header/cookie/query 维度 | 基本平移，注意 key 提取语法差异 |
| 熔断-异常比例/异常数 | Envoy outlier detection（DestinationRule `consecutive5xx` / `successRate`） | ⚠️ 语义不同：Envoy 是"连续 N 个 5xx"或"成功率窗口"判定+主动探测恢复，无 Sentinel"异常比例持续 M 秒"的滑动窗口语义——**阈值必须按语义重新校准，不能数值照抄** |
| 熔断-慢调用比例（SLOW_REQUEST_RATIO） | 无原生对应 | ⚠️ **已知缺口**：组合"超时+主动健康检查"近似；不满足则进 C 类自研插件清单（W3 评估） |
| 系统自适应保护（Load/RT/线程数） | 不在网关层做 | 范式转变：K8s HPA + 资源 limit + 后端容量规划承接 |
| 授权规则（黑白名单） | ip-restriction 插件 | 基本平移 |
| 限流/熔断后的 fallback 响应 | key-rate-limit 自定义响应 / custom-response 插件 | 对齐原 fallback 报文格式，下游可能依赖 |
| Sentinel Dashboard 动态推规则 | 规则=CR，GitOps PR 声明式 | **范式转变**：若规则持久化在 Nacos，一次性导出转 WasmPlugin/EnvoyFilter YAML；若在 Dashboard 内存里，趁迁移机会清理僵尸规则 |
| Dashboard 实时监控/簇点链路 | Higress Console + Prometheus/Grafana（自带栈） | 看板重建，指标更丰富 |

> 建议动作：W1 盘点时对 Sentinel 规则清单**逐条标注依赖的语义**（单机/全局、比例/连续、流控/熔断），分三列："直接平移 / 阈值重校准 / 缺口自研"。经验上 80%+ 是前两列。

### A.4 对四周计划的增量调整

| 周次 | 新增任务 |
|---|---|
| W1 | 盘点清单扩三项：Sentinel 规则导出（Nacos/内存，按 A.3 三列标注）、SCG 网关 logback 配置与 CLS 依赖字段、腾讯云 APM 接入点/Token/VPC 归属确认 |
| W2 | +1 天：部署 otel-collector（token 注入打通 APM）+ Fluent Bit→CLS + access log EnvoyFilter；压测时直接用 APM 看链路（顺带验证 trace 开销，tail sampling 策略在此定稿） |
| W3 | 慢调用熔断若为硬需求→进 C 类插件；否则记录"超时+健康检查"补偿方案的评审结论 |
| W4 | 故障演练新增四项：① 5xx 注入触发 outlier detection 摘除/恢复 ② 限流触发验证 fallback 响应格式 ③ **kill collector——网关转发必须完全无恙**（Envoy tracer 异步上报，理论无影响，必须实测）④ CLS 断流告警验证 |

### A.5 新增风险

| 风险 | 对策 |
|---|---|
| Sentinel 熔断语义差异导致保护失灵 | W1 三列标注 + W4 5xx 注入实测；阈值重校准而非照抄 |
| collector 成为单点 | 网关转发不依赖它（W4 演练验证）；collector 双副本；token 只在 collector 侧 |
| APM 计费/开销随 10 万 QPS 放大 | tail sampling 在 collector 收口；head sampling 维持 100% 由 tail 决定 |
| CLS 检索/告警字段不兼容 | W1 导出字段依赖清单，access log format 尽量对齐 |

---

## 附录 B：网关自动扩缩容（HPA）方案

### B.1 现状：Helm 内置 CPU 型 HPA

`helm/core` 已提供 gateway 的 HPA 模板（`templates/hpa.yaml`），要求 `gateway.kind=Deployment`，默认关闭。开启方式（走 Helm values 提 PR）：

```yaml
gateway:
  kind: Deployment          # HPA 的硬性前置条件
  autoscaling:
    enabled: true
    minReplicas: 5          # = 10 万 QPS 基线副本数（见 1.1 节 N+1），HPA 只管突发
    maxReplicas: 12
    targetCPUUtilizationPercentage: 60   # 60 而非默认 80：留缓冲应对突发
```

内置模板只支持 CPU 单指标。对 10 万 QPS 生产，建议用 HPA v2 behavior + 自定义指标替换/增强（见 B.3）。

### B.2 分层认知：谁需要扩、谁不能扩

| 组件 | 扩容方式 | 说明 |
|---|---|---|
| **higress-gateway**（数据面） | ✅ HPA 水平扩 | 无状态；但新 pod 需从控制面拉全量 Envoy 配置，冷启动有秒级空窗，**minReplicas 必须常态覆盖基线流量，HPA 只应对突发**，不要指望"从 1 副本扩起来" |
| **higress-controller**（控制面） | ❌ 不横向扩 | 配置翻译单活（leader），扩副本不分工反而抢锁；负载高时（如批量变更路由，参见 issue [#5247](https://github.com/higress-group/higress/issues/5247) 的真实案例）应做 vertical 扩容（加 CPU/内存）+ 优化变更批次 |
| istiod | ❌ 常规不动 | 随 Higress 部署体系管理 |
| 后端业务服务 | 各自 HPA | 网关扩容的前提是后端容量跟上，否则扩网关只是把排队移个位置 |

### B.3 生产建议：自定义指标驱动（CPU 型的局限）

CPU 型的两个盲区：① 长连接场景（SSE/WebSocket/AI 业务）连接数高但 CPU 低，CPU 触发滞后；② 突发流量下 CPU 是"结果"指标，滞后于请求速率。10 万 QPS 级别建议用**请求速率 + 活跃连接**做前瞻指标：

方案 A：**Prometheus Adapter + HPA 自定义指标**（Higress 自带 Prometheus，指标现成）
```yaml
# HPA 追加（gateway 暴露 envoy_http_downstream_rq 等指标于 :15020/stats/prometheus）
metrics:
- type: Pods
  pods:
    metric: { name: envoy_http_downstream_rq_per_pod }   # adapter 聚合规则定义
    target: { type: AverageValue, averageValue: "20000" } # 每副本 2 万 QPS 目标
- type: Resource
  resource:
    name: cpu
    target: { type: Utilization, averageUtilization: 60 } # CPU 保底
```

方案 B：**KEDA**（基于 Prometheus 查询伸缩，配置更直观，天然支持缩容窗口/周期策略——如"夜间低于 30% 才缩"）。二选一，团队不熟 Go/K8s 生态的话 KEDA 上手更快。

### B.4 扩容行为调优（behavior）

```yaml
behavior:
  scaleUp:
    stabilizationWindowSeconds: 0      # 扩容不等待，立即反应
    policies: [{ type: Percent, value: 100, periodSeconds: 30 }]  # 每 30s 最多翻倍
  scaleDown:
    stabilizationWindowSeconds: 600     # 缩容看 10 分钟窗口，防抖动（默认 300s 对网关偏激进）
    policies: [{ type: Pods, value: 1, periodSeconds: 120 }]       # 每次最多减 1 个，慢缩
```

要点：**扩要快、缩要慢**。缩容抖动对网关的伤害（连接迁移、配置重分发）远大于多跑一个副本的成本。

### B.5 缩容与长连接：最容易出事的地方

Envoy pod 收到 SIGTERM 后进入 drain（不再接新连接，存量连接继续服务至排空），因此：

1. **terminationGracePeriodSeconds** 要 ≥ 最长业务连接预期（SSE 长推送场景可能要 300s+；chart 未暴露此参数时用 GitOps overlay 补丁或推上游 PR）
2. **PDB 必须自建**（chart 没有内置 PDB 模板，已确认）：
```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata: { name: higress-gateway, namespace: higress-system }
spec:
  minAvailable: 4        # 永远不少于基线副本数
  selector: { matchLabels: { higress: higress-system-higress-gateway } }
```
3. 缩容/节点维护尽量安排**低峰窗口**（与 GitOps 的 sync window 思路一致）；大促前手动上调 minReplicas（一次 PR 的事）
4. 接受一个现实：**超长连接（如小时级 SSE）无法无损缩容**——要么客户端有重连机制，要么对长连接重的路由域单独部署一组固定副本的 gateway（Higress 支持多 Deployment 模型：Gateway API 每网关独立 Deployment，`enableGatewayAPIDeploymentController`）

### B.6 与 GitOps/已有方案的衔接

- HPA/PDB 都是普通 CR：HPA 走 Helm values 通道；PDB 放 overlays 根目录随 Argo 下发
- min/maxReplicas 变更（如大促调容）= 一个 PR，可审计可回滚
- W4 压测/演练追加两项：① 把 HPA maxReplicas 调小人为触发缩容，观测长连接断连与错误率；② 突发加压验证扩容时延（从触发到新副本就绪接流的全链路时间）

### B.7 快速决策表

| 现象 | 动作 |
|---|---|
| CPU 持续 > 70%、P99 抬升 | 先确认后端是否同步扩了；再查 HPA 是否触发、新 pod 是否卡在配置拉取 |
| CPU 不高但 P99 高、连接堆积 | 自定义指标方案（B.3）；查 idleTimeout/连接缓冲配置 |
| controller CPU 高 | vertical 扩容；查是否批量变更路由（[#5247](https://github.com/higress-group/higress/issues/5247) 模式），分批提交 |
| 缩容后错误率尖刺 | PDB/宽限期问题；或长连接路由 → 固定副本组 |
| 扩容触发但新副本接不到流量 | 检查 readiness（就绪即应接流）与负载均衡健康检查 |

---

## 附录 C：优雅缩容——等待存量请求处理结束

> 承接附录 B.5。目标：缩容时**不丢任何进行中的请求**，存量流处理完毕后才让副本退出。
> 基于 chart 实测事实（`helm/core/templates/_pod.tpl`）：gateway 是 Istio proxy 模式（pilot-agent 随 Envoy 主容器运行），readiness 为 `/healthz/ready:15021`，容器名 `higress-gateway`；**chart 未暴露 `terminationGracePeriodSeconds`，也没有内置 preStop** —— 这两处需要补丁。

### C.1 先理解机制：缩容时实际发生了什么

```
HPA 缩容 → Deployment 删 Pod
  → [preStop 钩子，若配置]                        ← 窗口1在此消解
  → SIGTERM → pilot-agent 触发 Envoy drain：
      · readiness 翻红（/healthz/ready → 503）→ Endpoint 摘除 → 新流量不再路由过来
      · 新连接直接关闭；HTTP/1.1 存量响应自动带 Connection: close，HTTP/2 发 GOAWAY
  → 存量连接上的活跃请求流继续处理直至完成          ← 这就是"等待处理结束"的机制本体
  → 宽限期（terminationGracePeriodSeconds）耗尽且活跃流已清零 → 优雅退出
  → 宽限期耗尽但流未清零 → SIGKILL（丢请求）       ← 窗口2/3在此爆发
```

**关键认知：Envoy 的 drain 天然就是"等存量、拒增量"**。所以方案不需要自己发明"等待"，只需要把三个丢请求窗口补死。

### C.2 三个丢请求窗口与对应补丁

**窗口 1：Endpoint 传播延迟（秒级）**
Pod 被删到所有 kube-proxy/客户端 LB 真正不再路由新流量之间有传播延迟。此期间新请求仍会到达正在排空的 pod——Envoy 会拒绝新连接、且给存量 keep-alive 响应加 `Connection: close`，配合**客户端重试**即可自愈；但要"零失败"，需 preStop sleep 让 pod 以完全健康状态度过传播期。

**窗口 2：宽限期 < 存量流时长**
宽限期耗尽时 Envoy 被 SIGKILL，进行中的流被掐断。必须让 `terminationGracePeriodSeconds ≥ P99.9 请求时长 + 传播窗口 + 余量`。

**窗口 3：无界长连接（SSE/WebSocket 小时级）**
有界宽限期物理上不可能等它结束。这不是配置问题，是架构问题：客户端重连协议（SSE 断线重连是标配）或固定副本组（见 B.5 第 4 点），二选一。

### C.3 落地补丁（GitOps overlay，随 Argo 下发）

chart 未暴露这两个参数，用 kustomize strategic merge patch 补到 gateway Deployment：

```yaml
# overlays/prod/gateway-drain-patch.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: higress-gateway
  namespace: higress-system
spec:
  template:
    spec:
      terminationGracePeriodSeconds: 120    # ≥ P99.9 时长 + 15s 传播 + 余量；压测定值
      containers:
        - name: higress-gateway             # chart 实际容器名（已核实）
          lifecycle:
            preStop:
              exec:
                command: ["sleep", "15"]     # 覆盖 Endpoint 传播延迟，期间正常服务
```

> 配套要求：**客户端/调用方必须有重试**（连接被拒/被 close 后退避重试到其他副本）。你们从 SCG 迁来的业务若已有 Ribbon/重试配置，语义平移即可。
> 若未来给 Higress 上游提 PR 开放这两个参数（`gateway.terminationGracePeriodSeconds` / `gateway.podAnnotations` 方式），patch 可退化为 values——注意该 PR 属于实质功能改动，走 AGENTS.md 的 AI 门禁流程。

### C.4 排空过程可观测

| 观测点 | 方法 |
|---|---|
| 排空进度（活跃流是否清零） | Envoy stat `envoy_http_downstream_rq_active`（:15020/stats/prometheus），排空副本应单调降至 0 |
| Endpoint 摘除时延 | `kubectl -n higress-system get endpoints higress-gateway -w`；与 preStop 时长对照 |
| 排空期失败请求 | access log 过滤该 pod（缩容演练时验证是否为 0） |
| readiness 翻红确认 | `curl <pod-ip>:15021/healthz/ready` 在 SIGTERM 后应 503 |

### C.5 W4 演练脚本（缩容零丢失验收）

1. 部署一个** 60 秒长请求**测试服务（如 `sleep:60` 后端）+ 一个持续压测的短请求客户端
2. 手动把 replicas 从 5 缩到 4（`kubectl scale`，或临时 PR 调 minReplicas）
3. 长请求命中即将退出的副本 → 观察其是否在宽限期内**完整返回 200**（而非 502/连接重置）
4. 短请求客户端统计缩容窗口内的错误率——目标 **0 非必然**，允许的失败应全部来自"无重试客户端撞上新连接拒绝"，据此决定 preStop 时长是否需加大
5. 对 SSE 场景重复 2-4：确认断开的是连接而非请求被掐（客户端重连后流式数据续传）——不行则该路由进固定副本组
6. 记录"从缩容触发到副本完全退出"的实际耗时（= preStop 15s + 排空时长），校准宽限期定值

### C.6 决策速查

| 现象 | 定位 |
|---|---|
| 缩容窗口出现 502/连接重置 | preStop 缺失或过短（窗口 1）；确认客户端有重试 |
| 长请求（>宽限期）被掐 | 宽限期不够（窗口 2）；或本应进固定副本组（窗口 3） |
| 副本退出后仍有请求打进来 | Endpoint 摘除延迟 > preStop 时长；加大 sleep 或查 CNI/外部 LB 健康检查 |
| 缩容后 P99 尖刺 | 排空期残余流量集中到剩余副本；属正常瞬态，stabilization window 已缓解，必要时减慢缩容步长 |

---

## 附录 D：多环境部署拓扑（K8s / Consul Connect / VM + 上游 Kong）

### D.0 目标拓扑与解读

```
客户端 → 腾讯云 Kong（托管边缘网关，TLS/接入/粗粒度管控）
          → Higress（K8s 部署，微服务网关：路由/限流/熔断/插件/可观测）
              ├─ ① K8s 集群服务（原生服务发现）
              ├─ ② Consul Connect Service Mesh（经 Consul Terminating Gateway 接入）
              └─ ③ VM 服务（注册在 Consul Registry，经 Higress Consul watcher 发现）
```

> 解读：三类"部署需求"按**后端服务所在环境**处理——Higress 统一部署在 K8s（本计划主线不变），一个 McpBridge 同时挂多注册中心，路由覆盖三环境。
> 若需求实为"Higress 自身也要部署到 VM"，则该实例走 higress-standalone 形态（独立进程、本地配置），与 K8s 主集群构成双平面——W1 需再确认（当前方案按主解读展开）。

### D.1 上游 Kong（腾讯云托管）的链路协同

Kong 在前改变了几件事，逐项约定：

| 事项 | 约定 |
|---|---|
| 职责切分 | Kong：接入、TLS 终止、API key/配额等**账号级**管控；Higress：路由/灰度/限流熔断/插件/**服务级**治理。避免双网关做重复限流认证（双重扣减、口径打架） |
| 回源地址 | Kong upstream 指向 Higress 的 Service（LoadBalancer/CLB，内网）；健康检查与 Kong 的 upstream health 配置联动 |
| 客户端 IP | Kong 注入 `X-Forwarded-For`，Higress 配置信任并透传（`addXRealIpHeader` 已在 higress-config 暴露）；限流 key 用 XFF 第一跳的需评估代理链可信度 |
| Trace 连续性 | Kong 开 OpenTelemetry 插件（同接你的 otel-collector→腾讯云 APM）；确认其注入 `traceparent` 且 Higress 侧透传 → 全链路一条 trace（否则 Higress 会另起新 trace，链路断两截） |
| 超时/重试预算 | **层级递减**：Kong upstream timeout > Higress 路由超时 > 后端处理时长。重试只在一层做（建议 Higress 层），防重试风暴相乘放大 |
| 配置边界 ⚠️ | Kong 的路由/upstream 配置在腾讯云侧（控制台/云 API），**不在你的 Argo Git 仓库**——Kong↔Higress 的路由映射存在双事实源。约定：Kong 只配"粗路由→Higress"，精细路由全部下沉到 Higress，Kong 侧变更量趋近于零 |
| 压测口径 | 10 万 QPS 压测必须从 Kong 入口打（含 Kong 开销的端到端 P99），而非直打 Higress |

### D.2 环境①：K8s 集群服务（基线，无新增工作）

Higress K8s 部署模式下，同集群 Service 原生可路由（McpBridge 默认来源）。SCG 迁移的 A 类路由直接对接。唯一注意：Kong 进来的流量对 Higress 而言是"南北向内网流量"，`X-Forwarded-For` 已由 Kong 注入。

### D.3 环境②：Consul Connect Service Mesh（本方案的关键约束）

**源码核实**：Higress 的 Consul watcher 是纯目录发现（catalog/health API），选项仅 type/name/domain/port/datacenter/serviceTag/refreshInterval/consulToken——**不参与 Connect mTLS 平面**。因此：

- ❌ 不能：Higress 直连 mesh 内服务（sidecar 只接受 mTLS，Higress 发不出 Connect 握手）
- ✅ 正解：**Consul Terminating Gateway**（Consul 官方为此场景设计的组件）：在 mesh 边界终结 Connect mTLS，对 Higress 暴露普通 HTTP
```
Higress → (普通 HTTP) → Consul Terminating Gateway → (Connect mTLS) → mesh 服务 sidecar
```
- 落地动作：
  1. Consul 侧为每个需要暴露给网关的 service 配置 `terminating-gateway` config entry（指定暴露哪些 service）
  2. TG 的地址（Consul 注册的 TG 实例）作为 Higress 的路由后端——用 McpBridge 的 **static/dns 类型来源**或 consul 来源（TG 自身也注册在 catalog）指向
  3. `ConsulServiceTag` 过滤器（watcher 原生支持）用于区分"暴露给网关"的服务标签，避免全目录吸入
- 语义收益：mesh 内部的服务间治理（intention、mTLS）不经过 Higress，各管各的层；Higress 的熔断/限流照样作用于它到 TG 的这一跳

### D.4 环境③：VM 服务（Consul Registry 发现）

这是 Higress **原生支持最好**的一块（`registry/consul` 就是为此而生）：

```yaml
# McpBridge 追加 registry（与 K8s 来源并列，一个 McpBridge 挂多来源）
registries:
- type: consul
  name: consul-vm            # 服务域名后缀来源：<service>.consul-vm
  domain: consul-vm
  address: <consul-server>:8500
  port: "8500"
  consulDatacenter: dc1
  consulServiceTag: gateway-exposed   # 只吸入打了此标签的 VM 服务，防全目录吸入
  # consulToken 走 Secret（authSecret 名），GitOps 下 Secret 用 SOPS/ESO 管
```
- VM 侧要求：consul agent 正常注册 + **健康检查必须配**（Higress 用 health API，只有 passing 实例会进 Endpoint——摘除/上线跟随 Consul 健康状态，等效于注册中心即健康检查面）
- McpBridge 是 CR：进 GitOps overlays，`sync-wave: -1`（对齐 GITOPS_INTEGRATION.md 4.1）
- 若 VM 服务间也有治理诉求且已上 Consul Connect，统一走 D.3 的 TG；纯注册（无 Connect）则本节直连即可

### D.5 三环境统一治理面

| 能力 | K8s ① | Consul Connect ② | VM@Consul ③ |
|---|---|---|---|
| 服务发现 | 集群原生 | TG 地址（static/dns/consul） | consul watcher（原生） |
| 健康摘除 | K8s readiness | TG/mesh 健康 | Consul health API（原生） |
| 熔断（outlier detection） | ✅ | ✅ 作用于 Higress→TG 跳 | ✅ |
| 灰度/插件/限流 | ✅ 统一在 Higress，与环境无关 | 同左 | 同左 |
| mTLS 到后端 | 集群内可（istio mtls） | 由 Connect 保证（Higress 不感知） | 建议内网安全组/或规划 TLS route |
| Trace 透传 | W3C tracecontext 全链路 | 需 VM 服务自行上报 APM（与附录 A.1 同通道） | 同左 |

### D.6 对计划与风险的增量

**W1 盘点追加**：SCG 后端清单按三环境标注；Consul Connect 的服务清单（哪些要暴露给网关→TG config entry 列表）；Consul 版本/ACL token/datacenter 拓扑确认；Kong 侧当前路由数与超时配置导出。

**W2 追加（+1 天）**：McpBridge 三来源打通；TG config entry 配置并验证 mesh 服务经 Higress 可达；压测改为从 Kong 入口打。

**W4 演练追加**：① Consul 断连——Higress 已拉取的 Endpoint 缓存兜底验证（网关不因注册中心抖动而摘流量）；② TG 实例故障——mesh 服务的熔断行为（等效普通后端）；③ Kong→Higress 全链路 trace 一条线验证（Kong tracing 插件 ↔ Higress ↔ APM）。

| 新增风险 | 对策 |
|---|---|
| Consul Connect 语义被误解为"Higress 支持 Connect"（不支持，源码已证） | D.3 的 TG 方案写入评审结论；对 mesh 侧同学讲清边界 |
| Kong/Higress 双网关配置漂移（两个事实源） | D.1 职责切分：Kong 粗路由冻结，精细路由下沉 Higress |
| Consul 全目录吸入导致路由表膨胀 | consulServiceTag 过滤 + 分 datacenter |
| 双层重试放大故障 | 重试只留一层（Higress），Kong upstream 重试关闭 |
| TG 成为 mesh 流量单点 | TG 多实例（Consul 官方支持）；W4 故障演练覆盖 |
