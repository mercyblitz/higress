# Higress 社区已有架构/迁移方案调研（GitHub Issues）

> 调研时间：2026-11-06，范围：higress-group/higress 全量 issues（含 HEP = Higress Enhancement Proposal）
> 目的：为 SCG 迁移计划找官方已有方案，避免重复造轮子，识别可借力/可贡献的点。

## 一、SCG 迁移线（与本项目直接相关）⭐

### [#521](https://github.com/higress-group/higress/issues/521) [HEP] support smooth migration from Spring Cloud Gateway（OPEN，追踪清单）
官方 SCG 迁移总纲，其进度清单本身就是权威的差距地图：
- ✅ 服务发现：Done（Nacos/Eureka/Zookeeper/Consul）——与我们附录 D 的三环境判断一致
- ◐ GatewayFilters：部分完成（见 [#519](https://github.com/higress-group/higress/issues/519)）
- ❌ Java 扩展（即 SCG 自定义 Filter 的 Java 生态兼容，未做）
- ❌ 配置转换工具：[#522](https://github.com/higress-group/higress/issues/522)（见下）
- ❌ Golden path 文档

### [#519](https://github.com/higress-group/higress/issues/519) higress 对 SCG 常用插件的支持情况梳理（OPEN）
**官方版 SCG Filter → Higress 能力映射表**（AddRequestHeader→策略配置/Transform、AddRequestParameter→Transform 插件……）。
→ **用途：W1 功能盘点时用它与我们的映射表（迁移计划第二节）交叉验证**，官方表更权威。

### [#522](https://github.com/higress-group/higress/issues/522) 实现 SCG application.yaml → Ingress 配置转换工具（OPEN，未实现）
官方计划中的转换工具，**至今无人实现**。
→ 两个含义：① 我们的 W2 手工迁移没有捷径，计划不变；② **这是一个理想的开源贡献机会**（Go/工具型、有官方 issue 背书、与我们自用需求完全重合——先自用再贡献，符合"早期胜利"路线）。

### [#774](https://github.com/higress-group/higress/issues/774) SCG 迁移到 MSE Higress 最佳实践（OPEN）
能力对标文档（Route/Predicate/Filter 三要素 → 路由/匹配规则/插件映射），我们映射表的数据源之一，已引用。

## 二、Nginx/其他网关迁移线（方法论可借鉴）

### [#548](https://github.com/higress-group/higress/issues/548) [HEP] Higress Smooth Migration（OPEN，伞 issue）
官方迁移工程全景：from Nginx + **from SCG** + Ingress→Gateway API 三条线。是我们方案的"官方版上层结构"。

### [#526](https://github.com/higress-group/higress/issues/526)/[#527](https://github.com/higress-group/higress/issues/527) Nginx 平滑迁移 HEP + 配置转换文档 / [#247](https://github.com/higress-group/higress/issues/247)/[#248](https://github.com/higress-group/higress/issues/248) Nginx Ingress & Istio Ingress Gateway step-by-step 文档需求
Nginx 线同样有"配置转换工具 + golden path 文档"的规划，但与 [#522](https://github.com/higress-group/higress/issues/522) 一样均未落地。

### [#3080](https://github.com/higress-group/higress/issues/3080)/[#3081](https://github.com/higress-group/higress/issues/3081) nginx-migration-mcp 插件沙箱工具（OPEN）⭐ 思路值得借鉴
社区在做 **nginx.conf → wasm 插件的自动转换工具**（含 Lua→wasm-go 代码生成器 convert_lua_to_wasm，正在优化错误处理/日志模板）。
→ **对你们的启发**：SCG 自定义 Filter 迁移（C 类）可借鉴此模式——把"手工翻译 Java Filter"变成"模板化代码生成"，尤其适合批量相似的 Filter。

## 三、架构方案类（HEP 中的架构演进路线）

| Issue | 方案 | 状态 | 与本项目相关性 |
|---|---|---|---|
| [#233](https://github.com/higress-group/higress/issues/233) [HEP] Gateway API 支持 | Ingress → Gateway API 双轨 | OPEN（已实现大半，README 已列一致性实现） | 我们用 Gateway API HTTPRoute 时的依据 |
| [#312](https://github.com/higress-group/higress/issues/312) [HEP] 非 K8s standalone 部署 | K8s 外部署的统一配置模型 | **CLOSED（已落地为 higress-standalone）** | 附录 D.0 的"VM 部署"分支确认有官方形态支撑 |
| [#738](https://github.com/higress-group/higress/issues/738) [HEP] LLM API proxy 与管理 | AI 网关起点 | CLOSED（ai-proxy 全家桶的现状源头） | 背景知识 |
| [#5058](https://github.com/higress-group/higress/issues/5058) ExtProc CR 提案 | **以 Envoy ext_proc 开放进程外插件链**（与 Wasm 并行的第二条扩展路） | OPEN Proposal | ⭐ C 类插件的备选机制：比 wasm 性能上限更高（无沙箱开销）、无语言限制；关注其落地 |
| [#4319](https://github.com/higress-group/higress/issues/4319)/[#4321](https://github.com/higress-group/higress/issues/4321) Sandbox Gateway | 多 Provider 抽象（proposal+design 配对） | OPEN | AI sandbox 场景，暂无需求 |
| [#316](https://github.com/higress-group/higress/issues/316) Consumer 管理 / [#535](https://github.com/higress-group/higress/issues/535) API Portal | 消费者/API 门户 | OPEN | 若后续需要 API 全生命周期管理可追踪 |
| [#940](https://github.com/higress-group/higress/issues/940) [HEP] More LLM Providers | 模型生态扩展 | OPEN | ai-proxy 生态背景 |

## 四、issue-spec 工作流观察（对贡献方式的影响）

社区当前用 **Proposal Issue + Design Issue 配对**承载架构方案（如 [#5280](https://github.com/higress-group/higress/issues/5280)/[#5281](https://github.com/higress-group/higress/issues/5281) MCP 兼容、[#4319](https://github.com/higress-group/higress/issues/4319)/[#4321](https://github.com/higress-group/higress/issues/4321) Sandbox Gateway、[#5307](https://github.com/higress-group/higress/issues/5307)/[#5308](https://github.com/higress-group/higress/issues/5308) SSE 解析），并有严格命名约定（`Proposal:` / `Design:` 前缀、issue-spec/ 标签）。结合 AGENTS.md 的 AI 门禁：
→ 我们若贡献 [#522](https://github.com/higress-group/higress/issues/522) 转换工具或 ExtProc 试点，**必须先提 Proposal Issue 并获维护者批准**——工具型贡献同样适用。

## 五、对我们计划的结论与调整

| 发现 | 影响 |
|---|---|
| [#519](https://github.com/higress-group/higress/issues/519) 官方映射表存在 | W1 盘点：用官方表交叉校验我们的映射表（半小时） |
| [#522](https://github.com/higress-group/higress/issues/522) 转换工具未实现 | W2 手工迁移计划不变；新增可选项：把转换工具作为第一个正式开源贡献（自用驱动，排 W3-W4 之后） |
| [#3080](https://github.com/higress-group/higress/issues/3080) 配置→插件代码生成思路 | C 类 Filter 迁移时评估"模板化生成"而非逐个手写 |
| [#312](https://github.com/higress-group/higress/issues/312) standalone 已落地 | 附录 D.0 的 VM 部署分支确认可行，无需新增调研 |
| [#5058](https://github.com/higress-group/higress/issues/5058) ExtProc CR | 记入 C 类插件的技术备选清单（性能敏感的 Filter 等 ExtProc 落地） |
| HEP 均为"计划"而非"成品" | 官方迁移工具链（转换器/文档）普遍未落地——**我们的方案没有错过任何现成轮子**，反而处处是贡献机会 |

> 综合判断：社区的"迁移方案"目前停留在 **HEP 规划 + 最佳实践文档** 层面，自动化工具基本未实现。我们的迁移计划不但不重复，反而是把 [#521](https://github.com/higress-group/higress/issues/521)/[#548](https://github.com/higress-group/higress/issues/548) 的规划在真实场景中走通——过程中产出的转换脚本、映射校验、golden path 笔记都有反哺社区的价值。
