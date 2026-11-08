# Higress 严重 Bug Issues 清单（精选）

> 从 755 个开放 issue（2026-11-06 快照）中，按**影响面 × 描述完整度**精选的严重缺陷。
> 标注 ⭐ 的与我们迁移方案直接相关；标注 ✅ 的正文已逐条核验（含复现条件/版本）。
> 配套：全量分类见 `ISSUES_CLASSIFICATION.md`；处置建议见文末。

## 一、网关级故障（影响面最大，升级前必查）⚠️

### [#4857](https://github.com/higress-group/higress/issues/4857) ✅ 一个损坏的 WasmPlugin CR 打挂整个网关
- **现象**：单个 WasmPlugin 的 url 指向不存在的 wasm 文件，**所有路由**（包括没挂插件的路由）全部 500（`response_flags: NFCF`）
- **影响面**：全网关；爆炸半径远超"单个插件失败"的预期（违背 Wasm 沙箱隔离设计意图）
- **复现版本**：v2.2.4 官方镜像，`volumeWasmPlugins=true` 挂载卷方式
- ⭐ **与我们相关**：GitOps 批量下发 WasmPlugin 时，一个 tag 写错 = 全站故障。W4 演练应包含"故意下发坏插件 CR"用例，验证当前版本行为

### [#4997](https://github.com/higress-group/higress/issues/4997) ✅ 多副本 controller 生成字节不一致 listener → 周期性强杀长连接
- **现象**：多个 controller 副本对同一配置生成**字节不一致**的 listener；网关每次 `MaxConnectionAge`（默认约 30 分钟）重连落到另一副本时，Envoy 判定"配置变了" → in-place filter chain 重建 → **周期性批量 502 / SSE 流式中断**
- **根因**：[#2920](https://github.com/higress-group/higress/issues/2920) 的跟进——[#2931](https://github.com/higress-group/higress/issues/2931) 只用 ECDS 规避了 mcp-server 一个 filter，**任何 patch value 含 map 的 EnvoyFilter 都会复现**
- ⭐⭐ **与我们直接冲突**：我们是多副本 controller + 长连接（SSE）场景，且附录 A/C 会手写含 map 的 EnvoyFilter（tracing、access log）——**正是该 bug 的复现条件**。对策：① 跟踪该 issue 修复版本；② 我们手写的 EnvoyFilter 上线后必须观测是否有周期性 DC（response_flags=DC）尖刺；③ 迁移期内 controller 单副本可规避（与附录 B "controller 不横向扩"一致）

### [#4507](https://github.com/higress-group/higress/issues/4507) 网关 OOM/SIGABRT 崩溃（nacos-mcp-registry + 直接 POST initialize）
- 特定配置路径（无前置 GET /sse、`match_list: []`）触发网关进程级 OOM/崩溃，v2.2.3。进程崩溃级别，非插件级

### [#4157](https://github.com/higress-group/higress/issues/4157) / [#3814](https://github.com/higress-group/higress/issues/3814) ✅ 插件导致 WASM OOM
- **[#4157](https://github.com/higress-group/higress/issues/4157)**：ai-data-masking 开启后**立即 OOM 崩溃**
- **[#3814](https://github.com/higress-group/higress/issues/3814)**：ai-statistics 处理流式 LLM 响应时 WASM 堆内存耗尽（日志实证 `runtime: out of memory... 1GB in use`）+ 503，v2.2.1
- 共性：流式响应是 WASM 内存放大器；AI 插件 + 大流量流式场景上线前必须压测插件内存行为

### [#4405](https://github.com/higress-group/higress/issues/4405) / [#4409](https://github.com/higress-group/higress/issues/4409) / [#4459](https://github.com/higress-group/higress/issues/4459) Envoy worker 崩溃三连（并发缺陷）
- **[#4405](https://github.com/higress-group/higress/issues/4405)**：nacos MCP registry 并发 map 读写 panic → **crash Envoy worker**
- **[#4409](https://github.com/higress-group/higress/issues/4409)**：gorm DBClient 数据竞争 + 连接池泄漏 → crash Envoy worker
- **[#4459](https://github.com/higress-group/higress/issues/4459)**：mcp-session Redis 客户端数据竞争 + nil panic
- 共性：Go 并发经典缺陷（未加锁 map / data race），集中在 golang-filter（mcp 系）；命中即 worker 崩溃

## 二、安全/认证类（敏感流量必查）🔒

### [#4599](https://github.com/higress-group/higress/issues/4599) ✅ 恶意 Cookie 头使限流/灰度插件 panic 且 **fail-open**（有 GHSA 安全通告）
- **现象**：`Cookie: mykey`（键名匹配但缺 `=`）触发 `strings.Split(pair, "=")[1]` 越界 panic；**panic 后 fail-open**：AI token 限流与灰度路由**双双被绕过**
- **影响**：攻击者可构造恶意 Cookie 绕过限流（成本攻击面）和灰度隔离；已上报安全通告 GHSA-2fcr-xqjj-m5pp
- ⭐ **与我们相关**：来自 Kong 的公网流量会原样透传 Cookie——上线前确认所用版本已修（同类问题曾报 jwt-auth）

### [#5274](https://github.com/higress-group/higress/issues/5274) OIDC 会话刷新期请求**不带访问令牌**直达上游
- 带 body 的请求在 session refresh 窗口可能**缺少 X-Forwarded-Access-Token 就转发上游**——若上游信任该头做鉴权，等于认证旁路窗口
- ⭐ 我们映射表里 OIDC → oidc 插件，若迁移含 OAuth2/TokenRelay 语义，此 issue 必须纳入验证

### [#5213](https://github.com/higress-group/higress/issues/5213) ai-data-masking 工具参数绕过脱敏管道
- MCP/工具调用参数不经过 deny/restore 脱敏——**敏感数据明文出境**。用 AI 网关 + 脱敏的场景属 P0 级

### [#4975](https://github.com/higress-group/higress/issues/4975) de-graphql：GraphQL 变量未转义直接拼接 → **JSON 注入**
- 非 String 变量原文拼进上游 body，构造恶意输入可注入/破坏上游 JSON

### [#4989](https://github.com/higress-group/higress/issues/4989) ✅ basic-auth 用户名重复静默覆盖 + 冒号密码不可配置
- 两个 consumer 同名时"后者生效"，**先配置者的合法凭证反被 401**；含 `:` 的密码无法配置（违反 RFC 7617）——认证配置语义陷阱

### 其他认证/校验类
- **[#4973](https://github.com/higress-group/higress/issues/4973)** ai-token-ratelimit ParseIP 对畸形 header 值 panic（`]` 开头即触发）
- **[#4991](https://github.com/higress-group/higress/issues/4991)** jwt-auth 登出时误删所有前缀同名的 cookie（殃及业务会话）
- **[#4974](https://github.com/higress-group/higress/issues/4974)** request-validation 对合法 JSON 但非 object 的 body（数组/字符串）校验被绕过
- **[#4876](https://github.com/higress-group/higress/issues/4876)** ai-proxy hunyuan 原生协议丢弃 MaxTokens/Stop——**token 上限失效**（成本失控）
- **[#5127](https://github.com/higress-group/higress/issues/5127) / [#4993](https://github.com/higress-group/higress/issues/4993)** ai-intent / request-block 以 Info 级记录**完整用户请求体**（隐私合规风险，安全插件里的演示代码残留）

## 三、静默错误路由/流量错乱（最难排查）🔀

### [#4850](https://github.com/higress-group/higress/issues/4850) ✅ 高频配置更新下 AI 路由**按比例静默 fail-open 404**
- **现象**：生产环境（2.2.4，3 副本，20 worker，10 个 Wasm filter），Console API 每 30s~5min 调整权重 → 数天累积后 **~3.9% 的请求静默 fail-open 404**（upstream path 前缀丢失），伴随 [#3920](https://github.com/higress-group/higress/issues/3920) 的 VM 泄漏指纹
- ⭐ **与我们相关**：我们规划了"压测中批量变更 100 次配置"的演练（W4）——该 issue 说明**高频配置变更 × Wasm ECDS 是已知雷区**；演练必须覆盖长时间（数天级）变更累积，而非一次性批量

### [#4883](https://github.com/higress-group/higress/issues/4883) modelMapping 通配符重叠 → 同一模型随机映射到不同目标
- 配置语义未定义（map 遍历序不确定），同一请求随机路由到不同模型——**确定性缺失**，对计费/测试都是灾难

### [#4849](https://github.com/higress-group/higress/issues/4849) Canary 路由与基础路由失去邻接关系
- Prefix/兜底路由与其他路径类型共存时，灰度路由匹配关系错乱——**灰度语义错误 = 流量放错版本**

### [#4831](https://github.com/higress-group/higress/issues/4831) Nacos 权重 < 0.5 的实例在 ServiceEntry 中权重归零
- 注册权重被静默抹成 0：小权重实例**收不到任何流量**且无告警。⭐ 注册中心翻译层的静默失真， Consul 同类风险需在 W2 验证（权重/元数据透传）

### [#5279](https://github.com/higress-group/higress/issues/5279) ai-load-balancer 开启 global_inflight 后所有请求 503 cluster_not_found
- 配置项与集群名生成互斥——开一个功能全站 503

### MCP 会话类三连（AI 网关场景）
- **[#4788](https://github.com/higress-group/higress/issues/4788)** Streamable HTTP 会话请求分散到不同上游 pod → 间歇性 404 / `Session terminated`
- **[#4879](https://github.com/higress-group/higress/issues/4879)** SSE 分片缓存在 endStream 丢弃 + 无界增长
- **[#5049](https://github.com/higress-group/higress/issues/5049)** Redis 热更新把活跃 SSE 会话劈到新旧两个 Redis 上

### 其他
- **[#4044](https://github.com/higress-group/higress/issues/4044)** ⭐ downstream idleTimeout 设 999 仍在 180s 报 504 stream idle timeout——**超时语义与文档不符**，与我们"层级递减超时预算"（附录 D.1）直接相关，配置超时前先实测
- **[#5053](https://github.com/higress-group/higress/issues/5053)** 请求两次经过过滤链（别名域名→rewrite.host 绕回）时精确卡 262144 字节 413
- **[#3665](https://github.com/higress-group/higress/issues/3665)** http_dubbo_transcoder 使用 CONNECT 方法导致 Keep-Alive 连接不可复用，**性能严重劣化**

## 四、功能失效/配置不生效（知晓即可）📋

- **[#5081](https://github.com/higress-group/higress/issues/5081)** Console 切换域名证书不生效，需重启网关（v2.2.0）⭐ 证书运维相关
- **[#4067](https://github.com/higress-group/higress/issues/4067)** ai-token-ratelimit 配置正确但从不连 Redis（config_fail 持续增长）——**安全功能静默失效**
- **[#5166](https://github.com/higress-group/higress/issues/5166)** firstByteTimeout 在 2.2.4/2.2.5 不生效
- **[#5157](https://github.com/higress-group/higress/issues/5157)** cluster_metrics 模式缺失/拼错时**静默回退随机路由**
- **[#4004](https://github.com/higress-group/higress/issues/4004)** Nacos3 读取 MCP tool 配置时 inputSchema 的 object 参数及 required 丢失
- **[#5076](https://github.com/higress-group/higress/issues/5076)** plugin-server 镜像升级后历史插件目录缺失，既有 WasmPlugin URL 全部失效 ⭐ GitOps 插件 tag 晋升相关
- **[#5234](https://github.com/higress-group/higress/issues/5234)** all-in-one v2.2.4 镜像的 key-auth/mcp-server 插件版本**低于** v2.2.3（升级即回退）
- **[#4221](https://github.com/higress-group/higress/issues/4221) / [#4173](https://github.com/higress-group/higress/issues/4173) / [#3926](https://github.com/higress-group/higress/issues/3926)** passthroughAuthHeader / ai-statistics attributes / AI 路由降级服务——配置后不生效类

## 五、处置建议（纳入我们的计划）

| 动作 | 触发条件 | 对应 issue |
|---|---|---|
| **升级版本前查此清单** | 任何 Higress 版本变更 | 全部（尤其一、三类） |
| W4 演练加"坏插件 CR"用例 | 验证 [#4857](https://github.com/higress-group/higress/issues/4857) 在当前版本的行为 | [#4857](https://github.com/higress-group/higress/issues/4857) |
| 手写 EnvoyFilter 上线后监控 DC 尖刺 | 我们必然手写（tracing/access log） | [#4997](https://github.com/higress-group/higress/issues/4997) ⭐⭐ |
| 认证链路渗透用例（畸形 Cookie/OIDC 刷新窗口） | 上线安全插件前 | [#4599](https://github.com/higress-group/higress/issues/4599)、[#5274](https://github.com/higress-group/higress/issues/5274) |
| 长时高频配置变更 soak（数天级） | 替代一次性批量演练 | [#4850](https://github.com/higress-group/higress/issues/4850) |
| 超时/权重等翻译语义实测 | W2 配置迁移时 | [#4044](https://github.com/higress-group/higress/issues/4044)、[#4831](https://github.com/higress-group/higress/issues/4831) |
| 订阅这些 issue 的修复版本 | 日常 | 在 GitOps 仓库建 tracked 清单 |

> 历史参考（已关闭但具警示价值）：[#4034](https://github.com/higress-group/higress/issues/4034)（插件死循环 CPU 100%）、[#3920](https://github.com/higress-group/higress/issues/3920)（Wasm VM 泄漏，[#4850](https://github.com/higress-group/higress/issues/4850) 的关联根因）——说明插件层缺陷可升级为网关级故障，但均在社区响应后修复。
