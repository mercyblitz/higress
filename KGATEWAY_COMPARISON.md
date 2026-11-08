# Higress vs KGateway 全面对比

> 背景：为 SCG→Higress 迁移决策做选型校验。对比基于双方案源码/官方文档/第三方评测（2026-11 检索），
> 并结合本项目已确认的部署需求：K8s + Consul Connect Mesh + VM（Consul Registry）三环境、上游腾讯云 Kong、
> 腾讯云 OTel APM、Argo CD GitOps、10 万 QPS、纯开源组件。
> KGateway 快照：前身为 Gloo（Solo.io，2018），2025-03 捐入 CNCF Sandbox，当前 v2.4.x（2026-09 v2.4.5）。

## 一、结论前置（针对你们场景）

**维持 Higress 选型，不建议切换。** 决定性因素是硬需求匹配，不是偏好：

| 你们的硬需求 | Higress | KGateway | 判定 |
|---|---|---|---|
| VM 服务经 Consul Registry 发现 | ✅ 原生 consul watcher（本仓库 `registry/consul` 已核实） | ❌ K8s Gateway API 原生，外部注册中心非一等公民（需自建同步层） | **决定性差异** |
| Consul Connect Mesh 接入 | 需 TG（不原生） | 需 TG（不原生） | 平手 |
| 纯开源（无企业版付费依赖） | ✅ 全部能力开源，含控制台 | ⚠️ 社区版可用，但部分企业能力（细粒度 AI 治理/支持）在 Solo 企业版 | Higress 胜 |
| Go 不熟的团队做插件二开 | ✅ wasm-go 插件模型简单（模板起步 ~200 行），可 AI 辅助 | ⚖️ 策略以 CRD/内置 filter 为主，深度定制走 Go 控制面或 ext_auth 服务，上手面更宽 | Higress 胜 |
| SCG 迁移 | ✅ 官方迁移最佳实践（issue [#774](https://github.com/higress-group/higress/issues/774)）+ transformer 插件对标 | ❌ 无官方 SCG 迁移指引 | Higress 胜 |
| 中文社区/文档 | ✅ | ⚠️ 英文为主 | Higress 胜 |
| Argo GitOps / 腾讯云 OTel | ✅ 全 CR 化 / 内置 otel tracer | ✅ 官方文档明确支持 Argo CD / OTel | 平手 |

**KGateway 会在以下场景反超**（如果你未来遇到，再重新评估）：纯 K8s 环境且重度依赖 Gateway API 高级特性（route delegation 多团队路由委派、细粒度多租户）、自建 GPU 推理集群需要 inference-aware routing（按 GPU 显存/队列深度路由）、需要英文生态商业支持。

## 二、项目基本面

| 维度 | Higress | KGateway |
|---|---|---|
| 出身 | 阿里内部网关产品开源（2022），CNCF Sandbox | Gloo（Solo.io，2018）→ 2025-03 捐入 CNCF Sandbox |
| 生产历史 | 阿里生产验证（公开表述数十万 QPS），sealos 等公开案例 | 7+ 年生产历史，"billions of API calls"表述，100+ 贡献者 |
| 治理 | CNCF Sandbox | CNCF Sandbox（平手） |
| 许可 | Apache-2.0，全功能开源 + 免费控制台 | Apache-2.0 社区版；Solo 企业版承载高级能力与支持（open-core 模式） |
| 社区重心 | 中文生态为主（国内采用者多） | 欧美生态为主 |
| 发版节奏 | 活跃（2.x 系列） | 活跃（v2.4.x / v2.3.x 双线补丁，2026-09 仍发版） |
| Star/规模 | ~9.7k | ~5.6k |
| 关联项目 | higress-console / wasm-go SDK / openapi-to-mcp | agentgateway（Rust，MCP/A2A，v2.3 起独立） |

## 三、架构与技术栈

| 维度 | Higress | KGateway |
|---|---|---|
| 数据面 | Envoy（higress-group fork） | Envoy（上游） |
| 控制面 | **扩展 Istio pilot**（Go），经 xDS 下发 | **自研 Go 控制面**，直发 xDS |
| 控制面重量 | 较重（带 Istio 依赖，换来 mesh 级能力与 McpBridge 等扩展） | 较轻（无 Istio 依赖，纯 Gateway API 翻译） |
| API 标准 | Ingress（注解体系，兼容大量 nginx-ingress 注解）+ Gateway API | **Gateway API 原生**（K8s Ingress 支持较弱，定位就是 Gateway API 实现） |
| 部署形态 | K8s Helm / all-in-one Docker（standalone，非 K8s 场景） | 仅 K8s（Helm/Argo CD 安装），无私有 standalone 形态 |
| 配置模型 | CR（McpBridge/WasmPlugin）+ Ingress/HTTPRoute + higress-config | Gateway API 资源 + kgateway Policy CRD（TrafficPolicy/AuthPolicy 等） |
| 多租户/路由组织 | 域名/路由级 + 插件匹配 | **route delegation**（路由树委派，平台团队/业务团队分层）、组合策略——设计上更精细 |

**架构小结**：同为 Envoy 数据面，差异全在控制面。Higress 的 Istio 底座是双刃剑——多了依赖与心智负担，但换来了非 K8s 注册中心集成、mesh 邻接能力和更丰富的"翻译层"（本仓库 `pkg/ingress` 的核心价值）。KGateway 更"纯"：Gateway API in、Envoy config out，链路短、概念少。

## 四、扩展机制（对你们二开影响最大）

| 维度 | Higress | KGateway |
|---|---|---|
| 主扩展模型 | **Wasm 插件**（Go/Rust/C++/AssemblyScript），沙箱隔离、热更新、单插件崩溃不挂主进程 | Policy CRD 组合（内置能力声明式拼装）+ 少量出口：ext_proc/ext_auth 对接外部服务、Go 控制面深度改造 |
| 官方插件生态 | ~59 个官方 wasm-go 插件（ai-* 全家桶、transformer、key-rate-limit 等）+ wasm-cpp/rust 内置件 | 内置 policy 覆盖 authn/z/rate-limit/resilience/transformation；生态偏"平台内置"而非"插件市场" |
| 自定义业务逻辑 | 写一个 wasm-go 插件（独立 Go module，模板起步），适合你们 SCG 自定义 Filter 的 C 类迁移 | 场景化：简单转换用 policy CRD；复杂逻辑要么 ext_auth/gRPC 外挂服务，要么改控制面（Go 工程量更大） |
| 热更新 | 插件镜像换 tag 即热生效（Wasm 特性） | 策略变更 xDS 热生效 |
| 二开对 Go 熟练度要求 | 低-中（插件是受限 API 面，SDK 回调式） | 中-高（要动 Go 控制面或维护外挂 ext 服务） |

## 五、服务发现与多环境（你们场景的决定性战场）

| 能力 | Higress | KGateway |
|---|---|---|
| K8s Service | ✅ | ✅ |
| Nacos（v1/v2/v3） | ✅ 原生 watcher（含 namespace/group/鉴权） | ❌ 需自建 |
| **Consul Registry（VM 服务）** | ✅ 原生（datacenter/serviceTag/ACL token/refresh interval，源码已核实） | ❌ 非一等公民；Gateway API BackendObjectKind 限定 K8s 资源，Consul 服务需先以某种形式"K8s 化"（自建同步控制器/手工 ServiceEntry 等价物） |
| Eureka / ZooKeeper | ✅ 原生 | ❌ 同上 |
| 静态/DNS 后端 | ✅（static/dns registry 类型） | ✅（Backend CRD 可写静态后端） |
| Consul Connect mTLS | ❌（需 Terminating Gateway） | ❌（同样需 TG；Envoy 系皆不参与 Connect 平面） |

> 结论：你们的 VM + Consul Registry 需求在 KGateway 上要**额外自建一层同步机制**（把 Consul catalog 翻译成 K8s 资源），这是一个持续运维的隐形组件；Higress 是配置即得。这是本对比中权重最高的一项。

## 六、AI 网关能力（前瞻性维度，你们当前非刚需）

| 能力 | Higress | KGateway |
|---|---|---|
| 多 LLM 提供商统一协议 | ✅ ai-proxy，100+ 模型 | ✅ AI 扩展（需 `aiExtension.enabled`） |
| Inference-aware routing | ✅ Gateway API Inference Extension 一致性实现 | ✅ **招牌能力**（按 GPU 显存/队列深度选 pod） |
| Token 限流/语义缓存/提示词防护 | ✅ ai-token-ratelimit / ai-cache / ai-security-guard 等全开源 | ⚠️ 部分在社区版，企业级治理在 Solo 版 |
| MCP Server 托管 | ✅ 网关内建（mcp-server 插件 + 协议转换 + MCP 市场），另有 openapi-to-mcp 工具 | ⚠️ v2.3 起 MCP/agent 能力移交姊妹项目 agentgateway（Rust 数据面，需独立部署治理） |
| AI 可观测 | ai-statistics（token/模型维度） | AI 指标经 OTel |

**解读**：两者 AI 能力路径不同——Higress 是"单体网关内吃下 AI 流量"，KGateway 是"经典 API 网关 + 独立 agentgateway 分工"。若你们未来 AI 流量成为主体且走 MCP/agent 形态，两边都需要二次架构决策；当前 SCG 迁移场景此项权重低。

## 七、可观测性 / 弹性 / 运维

| 维度 | Higress | KGateway |
|---|---|---|
| OTel 链路 | 内置开关（otel/zipkin/skywalking 三选一，`higress-config` 一行配置，源码已核实） | 官方文档 OTel 集成（同为 Envoy tracer，能力等价，配置面在 CRD） |
| 指标/看板 | 安装自带 Prometheus + Grafana + Console 监控页 | 自行装配（Grafana 官方有 kgateway dashboard 模板） |
| 控制台 UI | ✅ 开源 Console（路由/插件/证书白屏管理） | 社区版无完整管理 UI（企业版侧） |
| 熔断/容错 | outlier detection（语义与 Sentinel 有差，见附录 A.3） | outlier detection + fault injection + retry policy（语义同为 Envoy 原生，与 Sentinel 差异同源） |
| HPA | Chart 内置模板（附录 B 方案基础） | 自写 HPA/KEDA（等价，仅工程量差异） |
| GitOps 契合 | 全 CR 化，Argo 直接管（GITOPS_INTEGRATION.md 已落地） | 官方支持 Argo CD 安装，同为 CR 驱动，等价 |
| 升级 | 控制面/数据面独立升级；插件独立于网关版本 | 2.4 有明确 breaking change 与控制面/数据面兼容矩阵（升级纪律严格，文档完备） |

## 八、性能视角（10 万 QPS 口径）

不做虚构 benchmark 头对头。可站住的判断：

1. **数据面同为 Envoy**——L7 转发吞吐/延迟量级一致，10 万 QPS 对两者都是常规负载（第三方 8C16G 实测 Envoy 21k+ rps/节点，已在迁移计划 1.1 引用）
2. 差异点：
   - **控制面开销**：KGateway 直译链路更短；Higress 多一层 Istio pilot 翻译（大量路由+频繁变更时控制面资源占用更高，issue [#5247](https://github.com/higress-group/higress/issues/5247) 是真实参考）。对数据面 P99 无影响，影响的是"配置生效时延"与控制面成本
   - **插件机制**：Higress 的 Wasm 沙箱有微秒级调用开销（官方对标 SCG 时含插件场景仍领先，见 1.1 节数据）；KGateway policy 多为 Envoy 原生 filter，路径更短。**但你们的自定义 Filter 场景下，KGateway 需走 ext_auth 外挂——引入一次网络 RTT，比 Wasm 本地调用更贵**
   - 真实结论依赖压测：无论选谁，第 2 周的同口径压测流程不变

## 九、逐项评分（你们场景加权）

| 维度 | 权重 | Higress | KGateway | 说明 |
|---|---|---|---|---|
| Consul Registry/VM 接入 | 25% | 9 | 3 | KGateway 需自建同步层，长期运维成本 |
| 开源完整性（无付费依赖） | 15% | 9 | 6 | KGateway open-core，企业能力在企业版 |
| SCG 迁移路径 | 15% | 9 | 4 | 官方最佳实践 + transformer 对标 vs 无指引 |
| 团队 Go 门槛/二开模型 | 10% | 8 | 5 | Wasm 插件受限面 vs 控制面/外挂服务 |
| GitOps/OTel/腾讯云栈 | 10% | 8 | 8 | 平手（方案均已落地 vs 等价可行） |
| Gateway API 纯度/多租户 | 5% | 7 | 9 | KGateway route delegation 设计优秀 |
| 性能（数据面/控制面） | 10% | 8 | 8 | 数据面平手；控制面轻重互有胜负 |
| 社区/文档语言 | 5% | 9 | 6 | 中文生态 vs 欧美生态 |
| 治理成熟度 | 5% | 7 | 8 | KGateway 7 年历史 vs Higress 阿里生产验证 |
| **加权总分** | 100% | **8.4** | **5.4** | 权重可按需调整，但 Consul 项无论怎么降权都是断层差 |

## 十、风险对冲与再评估触发点

即使维持 Higress，建议记录以下"重新评估触发条件"（写入选型决策记录，供未来回溯）：

1. **Consul Connect 后端占比超过 50%** → Higress 的 TG 方案与 KGateway 无差异，但若同时 K8s 化进程加速（VM 服务逐步容器化），Higress 的注册中心优势权重下降，届时重比
2. **AI/agent 流量成为主体**（MCP 网关化） → 双方都要重新架构（Higress mcp-server vs agentgateway），单独立项评估
3. **团队 Go 能力沉淀后追求 Gateway API 深度治理**（多团队路由自治）→ KGateway 的 route delegation 值得再看
4. **Higress 社区活跃度下降/关键 issue 长期无响应** → CNCF Sandbox 双雄同风险等级，关注双方 release cadence

> 若切换成本已沉没前发现本对比有误，及时止损；本对比基于 2026-11 信息，重大版本（Higress 3.x / KGateway 3.x）发布时复核。

---

*引用源：本仓库源码（registry/、pkg/ingress/、helm/）；kgateway GitHub/官方文档与 release notes（v2.4.x）；CNCF 项目页；第三方评测（2026-11 检索）。性能数据引用与迁移计划 1.1 节一致，未引入未经证实的 benchmark。*
