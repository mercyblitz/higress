# Higress GitHub Issues 分类清单

> 生成时间：2026-11-06 ｜ 数据源：GitHub REST API 全量开放 issues（非 PR）
> 范围：[#2345](https://github.com/higress-group/higress/issues/2345) ~ [#5313](https://github.com/higress-group/higress/issues/5313)（2025-01 至 2026-11 创建），共 **755** 个开放 issue
> 分类方法：基于标题 + 标签的规则化归类（启发式，一 issue 一主类）；类型与领域为两个独立维度

## 一、总览

### 按类型

| 类型 | 数量 | 占比 |
|---|---|---|
| issue-spec (Proposal/Design) | 217 | 28% |
| Bug 报告 | 146 | 19% |
| 功能请求/咨询 | 374 | 49% |
| 文档 | 11 | 1% |
| 测试/e2e | 5 | 0% |
| 安全/缺陷披露 | 2 | 0% |

### 按领域

| 领域 | 数量 | 占比 |
|---|---|---|
| AI 网关插件 (ai-*) | 232 | 30% |
| MCP 生态 | 116 | 15% |
| 通用插件（非 AI） | 54 | 7% |
| 核心网关（控制面/数据面） | 44 | 5% |
| 安全/认证/流量治理插件 | 67 | 8% |
| 插件机制/扩展框架 | 28 | 3% |
| 服务注册中心 | 31 | 4% |
| 部署/安装/升级 | 30 | 3% |
| 可观测性 | 3 | 0% |
| Console 控制台 | 7 | 0% |
| hgctl CLI | 25 | 3% |
| 测试 | 2 | 0% |
| 文档 | 2 | 0% |
| 其他/未分类 | 114 | 15% |

> 观察要点见文末「四、结构性观察」。

## 二、分领域明细

### AI 网关插件 (ai-*)（232）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5313](https://github.com/higress-group/higress/issues/5313) | 2026-11-06 | issue-spec (Proposal/Design) | Design: ai-proxy Claude 流式状态隔离与 Vertex 覆盖 \|\| Design: ai-proxy Claude streaming state isolation and Vertex coverage |
| [#5310](https://github.com/higress-group/higress/issues/5310) | 2026-11-05 | issue-spec (Proposal/Design) | Proposal: ai-proxy Claude 流式转换状态按请求隔离 \|\| Proposal: ai-proxy Claude streaming conversion status isolated by request |
| [#5308](https://github.com/higress-group/higress/issues/5308) | 2026-11-05 | issue-spec (Proposal/Design) | Design: Original-format priority and no-space fallback in parseSSEResponse |
| [#5290](https://github.com/higress-group/higress/issues/5290) | 2026-10-31 | issue-spec (Proposal/Design) | [Proposal] ai-proxy: report Gemini thoughtsTokenCount as completion_tokens_details.reasoning_tokens |
| [#5285](https://github.com/higress-group/higress/issues/5285) | 2026-10-31 | issue-spec (Proposal/Design) | [Proposal] Add Desearch engine to the ai-search plugin |
| [#5279](https://github.com/higress-group/higress/issues/5279) | 2026-10-29 | Bug 报告 | ai-load-balancer: global_inflight_enabled 开启后所有请求 503 cluster_not_found |
| [#5272](https://github.com/higress-group/higress/issues/5272) | 2026-10-27 | issue-spec (Proposal/Design) | Proposal: ai-proxy 重试成功的响应绕过后续插件，ai-statistics 记录不到 model / token \|\| Proposal: ai-proxy retries successful responses to bypass subsequent plug-ins, and ai-statistics cannot record model / token |
| [#5271](https://github.com/higress-group/higress/issues/5271) | 2026-10-27 | 功能请求/咨询 | ai-token-ratelimit / ai-quota：流式 SSE 的 usage 事件跨 chunk 到达时可能漏记 token |
| [#5262](https://github.com/higress-group/higress/issues/5262) | 2026-10-27 | issue-spec (Proposal/Design) | Design: ai-data-masking tool arguments masking |
| [#5256](https://github.com/higress-group/higress/issues/5256) | 2026-10-24 | issue-spec (Proposal/Design) | Proposal: Configurable reasoning_content passback in ai-proxy's Claude-to-Chat conversion |
| [#5254](https://github.com/higress-group/higress/issues/5254) | 2026-10-23 | issue-spec (Proposal/Design) | Proposal: ai-proxy Qwen provider silently drops max_completion_tokens in non-compatible mode |
| [#5245](https://github.com/higress-group/higress/issues/5245) | 2026-10-23 | Bug 报告 | ai-proxy: Vertex native conversion loses parallel tool calls and mispairs results |
| [#5241](https://github.com/higress-group/higress/issues/5241) | 2026-10-22 | issue-spec (Proposal/Design) | Design: ai-intent bodyless-request bypass |
| [#5240](https://github.com/higress-group/higress/issues/5240) | 2026-10-22 | issue-spec (Proposal/Design) | Proposal: let ai-intent pass bodyless requests without classification |
| [#5213](https://github.com/higress-group/higress/issues/5213) | 2026-10-21 | 功能请求/咨询 | ai-data-masking: tool arguments bypass the deny/restore masking pipeline |
| [#5212](https://github.com/higress-group/higress/issues/5212) | 2026-10-21 | issue-spec (Proposal/Design) | Design: ai-data-masking-openai-stream-termination |
| [#5210](https://github.com/higress-group/higress/issues/5210) | 2026-10-21 | issue-spec (Proposal/Design) | Proposal: ai-data-masking OpenAI stream termination |
| [#5177](https://github.com/higress-group/higress/issues/5177) | 2026-10-20 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-statistics |
| [#5166](https://github.com/higress-group/higress/issues/5166) | 2026-10-20 | Bug 报告 | ai-proxy: firstByteTimeout does not take effect in Higress 2.2.4/2.2.5 |
| [#5162](https://github.com/higress-group/higress/issues/5162) | 2026-10-19 | issue-spec (Proposal/Design) | Design: ai-load-balancer-inflight-counter-leak |
| [#5161](https://github.com/higress-group/higress/issues/5161) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: compensate the ai-load-balancer least-request counter on failure paths |
| [#5160](https://github.com/higress-group/higress/issues/5160) | 2026-10-19 | Bug 报告 | ai-load-balancer: the Redis least-request counter leaks a permanent +1 when host override fails |
| [#5159](https://github.com/higress-group/higress/issues/5159) | 2026-10-19 | issue-spec (Proposal/Design) | Design: ai-load-balancer-cluster-metrics-mode-validation |
| [#5158](https://github.com/higress-group/higress/issues/5158) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: validate the required `mode` of the ai-load-balancer cluster_metrics policy |
| [#5157](https://github.com/higress-group/higress/issues/5157) | 2026-10-19 | Bug 报告 | ai-load-balancer cluster_metrics: an unknown or missing 'mode' silently falls back to random routing |
| [#5156](https://github.com/higress-group/higress/issues/5156) | 2026-10-19 | issue-spec (Proposal/Design) | Design: ai-endpoint-picker-kv-cache-negative-utilization |
| [#5155](https://github.com/higress-group/higress/issues/5155) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: reject an unusable negative KV-cache utilisation in ai-endpoint-picker |
| [#5154](https://github.com/higress-group/higress/issues/5154) | 2026-10-19 | 功能请求/咨询 | ai-endpoint-picker: a negative KV-cache utilisation is accepted as the best possible signal |
| [#5153](https://github.com/higress-group/higress/issues/5153) | 2026-10-19 | issue-spec (Proposal/Design) | Design: ai-agent-outputparser-panic |
| [#5152](https://github.com/higress-group/higress/issues/5152) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: harden ai-agent outputParser against malformed model output |
| [#5151](https://github.com/higress-group/higress/issues/5151) | 2026-10-19 | Bug 报告 | ai-agent: outputParser panics on malformed model output (nil error deref and single code fence) |
| [#5150](https://github.com/higress-group/higress/issues/5150) | 2026-10-19 | Bug 报告 | [Bug] ai-data-masking drops terminal finish_reason and [DONE] on OpenAI streams |
| [#5148](https://github.com/higress-group/higress/issues/5148) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level stream member in ai-proxy |
| [#5146](https://github.com/higress-group/higress/issues/5146) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-security-guard |
| [#5143](https://github.com/higress-group/higress/issues/5143) | 2026-10-18 | Bug 报告 | ai-json-resp: omitting optional jsonSchema rejects requests with HTTP 500 |
| [#5141](https://github.com/higress-group/higress/issues/5141) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-cache |
| [#5139](https://github.com/higress-group/higress/issues/5139) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-history |
| [#5137](https://github.com/higress-group/higress/issues/5137) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-search |
| [#5135](https://github.com/higress-group/higress/issues/5135) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: reject request bodies with a duplicated top-level messages member in ai-context-limit and ai-prompt-decorator |
| [#5134](https://github.com/higress-group/higress/issues/5134) | 2026-10-18 | issue-spec (Proposal/Design) | Design: remove ai-intent request-content logging |
| [#5133](https://github.com/higress-group/higress/issues/5133) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: remove ai-intent request-content logging |
| [#5130](https://github.com/higress-group/higress/issues/5130) | 2026-10-18 | issue-spec (Proposal/Design) | Design: correct ai-security-guard consumer-service examples |
| [#5129](https://github.com/higress-group/higress/issues/5129) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: correct ai-security-guard consumer-service examples |
| [#5127](https://github.com/higress-group/higress/issues/5127) | 2026-10-17 | 功能请求/咨询 | ai-intent logs every user's question and the full LLM request body at Info level |
| [#5117](https://github.com/higress-group/higress/issues/5117) | 2026-10-16 | issue-spec (Proposal/Design) | Design: ai-token-ratelimit-header-ip-parse-panic |
| [#5115](https://github.com/higress-group/higress/issues/5115) | 2026-10-16 | issue-spec (Proposal/Design) | Proposal: ai-cache-allquestions-key-unambiguous |
| [#5098](https://github.com/higress-group/higress/issues/5098) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: ai-image-reader-preserve-image-order |
| [#5097](https://github.com/higress-group/higress/issues/5097) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: reject non-RSA service-account keys in ai-proxy vertex credentials instead of panicking |
| [#5095](https://github.com/higress-group/higress/issues/5095) | 2026-10-15 | issue-spec (Proposal/Design) | Design: preserve conversation semantics in ai-proxy dify provider (Proposal [#5093](https://github.com/higress-group/higress/issues/5093)) |
| [#5093](https://github.com/higress-group/higress/issues/5093) | 2026-10-15 | issue-spec (Proposal/Design) | [Proposal] ai-proxy: dify provider loses multi-turn conversation semantics (query construction & conversation_id continuity) \|\| 【提案】ai-proxy 的 dify provider 多轮对话语义丢失（query 构建 与 conversation_id 连续性） |
| [#5090](https://github.com/higress-group/higress/issues/5090) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: reduce ai-statistics streaming append allocations |
| [#5087](https://github.com/higress-group/higress/issues/5087) | 2026-10-14 | 功能请求/咨询 | ai-data-masking zeroes float usage counters on merge and emits the accumulated usage on only one rewritten event |
| [#5084](https://github.com/higress-group/higress/issues/5084) | 2026-10-14 | Bug 报告 | ai-data-masking panics on non-UTF-8 streaming bodies shorter than the byte window and on empty streaming responses |
| [#5073](https://github.com/higress-group/higress/issues/5073) | 2026-10-12 | 功能请求/咨询 | ai-proxy: token retries discard customSettings overrides and defaults |
| [#5063](https://github.com/higress-group/higress/issues/5063) | 2026-10-12 | 文档 | docs(ai-security-guard): EN README configuration table missing securityToken option |
| [#5062](https://github.com/higress-group/higress/issues/5062) | 2026-10-12 | 文档 | docs(ai-proxy): EN README Vertex tables document nonexistent vertexGeminiSafetySetting field (silently ignored) |
| [#5051](https://github.com/higress-group/higress/issues/5051) | 2026-10-09 | issue-spec (Proposal/Design) | Design: model-mapper-llm-mock-e2e |
| [#5050](https://github.com/higress-group/higress/issues/5050) | 2026-10-09 | issue-spec (Proposal/Design) | Design: ai-proxy-responses-api-mcp-tool-calling |
| [#5010](https://github.com/higress-group/higress/issues/5010) | 2026-10-08 | issue-spec (Proposal/Design) | Design: ai-proxy-hot-update-failopen-404 |
| [#5009](https://github.com/higress-group/higress/issues/5009) | 2026-10-08 | issue-spec (Proposal/Design) | Proposal: ai-proxy-hot-update-failopen-404 |
| [#5001](https://github.com/higress-group/higress/issues/5001) | 2026-10-06 | issue-spec (Proposal/Design) | Proposal: Prefer exact category matches in ai-intent |
| [#4988](https://github.com/higress-group/higress/issues/4988) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: keep image numbering stable under out-of-order OCR responses in ai-image-reader ([#4987](https://github.com/higress-group/higress/issues/4987)) |
| [#4987](https://github.com/higress-group/higress/issues/4987) | 2026-10-04 | 功能请求/咨询 | ai-image-reader: out-of-order OCR responses swap image numbering in the LLM prompt |
| [#4985](https://github.com/higress-group/higress/issues/4985) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: fall back to the raw question when zhToUnicode fails in ai-intent ([#4978](https://github.com/higress-group/higress/issues/4978)) |
| [#4983](https://github.com/higress-group/higress/issues/4983) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: tolerate message-less choices in ai-json-resp history assembly ([#4976](https://github.com/higress-group/higress/issues/4976)) |
| [#4980](https://github.com/higress-group/higress/issues/4980) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: reject malformed header IP values in ai-token-ratelimit instead of panicking ([#4973](https://github.com/higress-group/higress/issues/4973)) |
| [#4978](https://github.com/higress-group/higress/issues/4978) | 2026-10-04 | 功能请求/咨询 | ai-intent: zhToUnicode error is swallowed and the user's entire question is replaced with an empty string |
| [#4976](https://github.com/higress-group/higress/issues/4976) | 2026-10-04 | 功能请求/咨询 | ai-json-resp: nil *chatMessage dereference in SaveBodyToHistMsg when the last choice has no message |
| [#4973](https://github.com/higress-group/higress/issues/4973) | 2026-10-04 | Bug 报告 | ai-token-ratelimit: ParseIP panics on a header value starting with "]" (slice bounds out of range) |
| [#4961](https://github.com/higress-group/higress/issues/4961) | 2026-10-03 | Bug 报告 | fix(ai-proxy): gemini streaming conversion drops functionCall (non-streaming twin fixed in 7b275a1) |
| [#4960](https://github.com/higress-group/higress/issues/4960) | 2026-10-03 | Bug 报告 | fix(ai-proxy): claude streaming conversion panics on events without a delta field (wasm VM crash) |
| [#4957](https://github.com/higress-group/higress/issues/4957) | 2026-10-03 | issue-spec (Proposal/Design) | Proposal: bypass bodyless requests in ai-intent instead of pausing indefinitely ([#4922](https://github.com/higress-group/higress/issues/4922)) |
| [#4953](https://github.com/higress-group/higress/issues/4953) | 2026-10-03 | issue-spec (Proposal/Design) | Proposal: prevent ai-quota completion requests from remaining paused after synchronous Redis GET failure ([#4874](https://github.com/higress-group/higress/issues/4874)) |
| [#4941](https://github.com/higress-group/higress/issues/4941) | 2026-10-03 | 功能请求/咨询 | ai-search: web_search_options permanently overwrites the plugin searchRewrite config |
| [#4939](https://github.com/higress-group/higress/issues/4939) | 2026-10-02 | 文档 | Document DemonRoute as the openaiCustomUrl worked example (ai-proxy) |
| [#4931](https://github.com/higress-group/higress/issues/4931) | 2026-10-02 | 功能请求/咨询 | ai-search: rewrite replies are matched with a substring test, so real searches are skipped |
| [#4929](https://github.com/higress-group/higress/issues/4929) | 2026-10-02 | 功能请求/咨询 | ai-search: Elasticsearch query body is assembled without JSON escaping |
| [#4927](https://github.com/higress-group/higress/issues/4927) | 2026-10-02 | Bug 报告 | ai-cache: DashVector query response panics on non-string fields |
| [#4924](https://github.com/higress-group/higress/issues/4924) | 2026-10-02 | 文档 | docs(hgctl): fix AI route comment spelling |
| [#4922](https://github.com/higress-group/higress/issues/4922) | 2026-10-02 | 功能请求/咨询 | ai-intent: bodyless requests pause without a bypass path |
| [#4914](https://github.com/higress-group/higress/issues/4914) | 2026-10-01 | 文档 | docs(ai-security-guard): EN README config table is missing the securityToken option |
| [#4913](https://github.com/higress-group/higress/issues/4913) | 2026-10-01 | 文档 | docs(ai-proxy): EN README Vertex tables document a non-existent config field (vertexGeminiSafetySetting → geminiSafetySetting) |
| [#4909](https://github.com/higress-group/higress/issues/4909) | 2026-10-01 | issue-spec (Proposal/Design) | Design: route bodyless ai-history queries through an identity lookup |
| [#4908](https://github.com/higress-group/higress/issues/4908) | 2026-10-01 | issue-spec (Proposal/Design) | Proposal: make the documented bodyless ai-history query return cached history |
| [#4907](https://github.com/higress-group/higress/issues/4907) | 2026-10-01 | 功能请求/咨询 | ai-history: bodyless GET query cannot return cached history |
| [#4906](https://github.com/higress-group/higress/issues/4906) | 2026-10-01 | issue-spec (Proposal/Design) | Design: ai-load-balancer-sglang-metrics |
| [#4901](https://github.com/higress-group/higress/issues/4901) | 2026-09-30 | Bug 报告 | ai-history plugin has three panic bugs: negative cnt slice out of bounds + two naked type assertions |
| [#4897](https://github.com/higress-group/higress/issues/4897) | 2026-09-30 | issue-spec (Proposal/Design) | Design: Treat negative ai-history count parameters as invalid input in the shared query parser |
| [#4896](https://github.com/higress-group/higress/issues/4896) | 2026-09-30 | issue-spec (Proposal/Design) | Design: Validate Chroma query-response dimensions before nested indexing in ai-cache |
| [#4894](https://github.com/higress-group/higress/issues/4894) | 2026-09-30 | Bug 报告 | ai-proxy: hunyuan streaming chunk converter panics on frames without Choices - raw native frames leak to OpenAI clients |
| [#4893](https://github.com/higress-group/higress/issues/4893) | 2026-09-30 | issue-spec (Proposal/Design) | Proposal: model-mapper-llm-mock-e2e |
| [#4891](https://github.com/higress-group/higress/issues/4891) | 2026-09-30 | issue-spec (Proposal/Design) | Proposal: ai-load-balancer-sglang-metrics |
| [#4890](https://github.com/higress-group/higress/issues/4890) | 2026-09-30 | issue-spec (Proposal/Design) | Proposal: ai-proxy-responses-api-mcp-tool-calling |
| [#4883](https://github.com/higress-group/higress/issues/4883) | 2026-09-30 | 功能请求/咨询 | ai-proxy: modelMapping with overlapping wildcard keys is non-deterministic per request - same model randomly maps to different targets |
| [#4876](https://github.com/higress-group/higress/issues/4876) | 2026-09-29 | Bug 报告 | ai-proxy: hunyuan original-protocol chat silently drops native fields (MaxTokens, Stop, ...) - token limits ignored; embeddings impossible with native creds + OpenAI protocol |
| [#4874](https://github.com/higress-group/higress/issues/4874) | 2026-09-29 | Bug 报告 | Bug: ai-quota leaves completion requests paused when Redis GET dispatch fails synchronously |
| [#4859](https://github.com/higress-group/higress/issues/4859) | 2026-09-29 | Bug 报告 | ai-proxy: bedrock provider does not detect /anthropic/v1/messages under protocol: original - request mis-routed to wrong AWS endpoint and auth |
| [#4850](https://github.com/higress-group/higress/issues/4850) | 2026-09-29 | Bug 报告 | [wasm][ai-proxy] 高频配置更新下，AI 路由出现按请求比例的静默 fail-open 404（upstream path 前缀丢失），伴随 [#3920](https://github.com/higress-group/higress/issues/3920) 的 VM 泄漏指纹 \|\| Silent per-request fail-open 404s on AI routes under frequent config updates, with the VM leak signature of [#3920](https://github.com/higress-group/higress/issues/3920) |
| [#4839](https://github.com/higress-group/higress/issues/4839) | 2026-09-29 | Bug 报告 | ai-proxy: cohere provider does not recognize /v1/rerank under protocol: original (request skipped as unsupported path) |
| [#4838](https://github.com/higress-group/higress/issues/4838) | 2026-09-29 | Bug 报告 | ai-proxy: groq provider does not recognize /openai/v1/responses under protocol: original (request skipped as unsupported path) |
| [#4836](https://github.com/higress-group/higress/issues/4836) | 2026-09-29 | Bug 报告 | ai-proxy: baidu provider does not recognize /v2/embeddings under protocol: original (request skipped as unsupported path) |
| [#4827](https://github.com/higress-group/higress/issues/4827) | 2026-09-28 | Bug 报告 | model-router silently ignores multipart writer.Close error |
| [#4823](https://github.com/higress-group/higress/issues/4823) | 2026-09-28 | Bug 报告 | ai-quota query parsing panics on empty values and uses wrong error variable for Redis failures |
| [#4804](https://github.com/higress-group/higress/issues/4804) | 2026-09-28 | issue-spec (Proposal/Design) | Proposal: prevent negative ai-history counts from panicking ([#4336](https://github.com/higress-group/higress/issues/4336)) |
| [#4803](https://github.com/higress-group/higress/issues/4803) | 2026-09-28 | issue-spec (Proposal/Design) | Proposal: prevent malformed Chroma responses from panicking ai-cache ([#4334](https://github.com/higress-group/higress/issues/4334)) |
| [#4799](https://github.com/higress-group/higress/issues/4799) | 2026-09-28 | issue-spec (Proposal/Design) | Proposal: Provider-level session affinity for AI routing |
| [#4783](https://github.com/higress-group/higress/issues/4783) | 2026-09-27 | issue-spec (Proposal/Design) | Proposal: sync model-router EN README with shipped autoRouting documentation |
| [#4751](https://github.com/higress-group/higress/issues/4751) | 2026-09-23 | 功能请求/咨询 | 关于使用ai-load-balancer的endpoint_metrics策略遇到的一些问题 \|\| Some problems encountered when using the endpoint_metrics strategy of ai-load-balancer |
| [#4740](https://github.com/higress-group/higress/issues/4740) | 2026-09-20 | 功能请求/咨询 | CNCF AI Technical Community Group Discussion/Presentation |
| [#4736](https://github.com/higress-group/higress/issues/4736) | 2026-09-20 | issue-spec (Proposal/Design) | Proposal: send the required `Authorization: Bearer` prefix from the ai-proxy `ai360` and `github` providers |
| [#4731](https://github.com/higress-group/higress/issues/4731) | 2026-09-19 | Bug 报告 | [ai-proxy] Tool and content fields are dropped when converting between OpenAI, Claude and Gemini |
| [#4724](https://github.com/higress-group/higress/issues/4724) | 2026-09-18 | issue-spec (Proposal/Design) | Design: Responses content extraction in ai-statistics ([#3581](https://github.com/higress-group/higress/issues/3581)) |
| [#4719](https://github.com/higress-group/higress/issues/4719) | 2026-09-17 | issue-spec (Proposal/Design) | Design: Preserve API identity across ai-proxy retry transforms ([#4396](https://github.com/higress-group/higress/issues/4396)) |
| [#4718](https://github.com/higress-group/higress/issues/4718) | 2026-09-17 | issue-spec (Proposal/Design) | Proposal: Preserve resolved API identity in ai-proxy retries ([#4396](https://github.com/higress-group/higress/issues/4396)) |
| [#4717](https://github.com/higress-group/higress/issues/4717) | 2026-09-17 | Bug 报告 | AI 模型路由插件model-router里面的自动匹配模型多模态不支持的问题 \|\| The automatic matching model multi-modality in the AI model routing plug-in model-router does not support the problem |
| [#4716](https://github.com/higress-group/higress/issues/4716) | 2026-09-17 | 功能请求/咨询 | [ai-proxy] qwen provider 多模态请求仅支持 qwen-vl 前缀模型，其他多模态模型报 InvalidParameter \|\| [ai-proxy] qwen provider multi-modal request only supports qwen-vl prefix model, other multi-modal models report InvalidParameter |
| [#4710](https://github.com/higress-group/higress/issues/4710) | 2026-09-16 | issue-spec (Proposal/Design) | Design: isolate model-router auto-routing text to the final user message |
| [#4709](https://github.com/higress-group/higress/issues/4709) | 2026-09-16 | issue-spec (Proposal/Design) | Design: configurable model-router auto-routing trigger model ID |
| [#4707](https://github.com/higress-group/higress/issues/4707) | 2026-09-16 | issue-spec (Proposal/Design) | Proposal: prevent model-router auto routing from reusing stale text across user turns |
| [#4706](https://github.com/higress-group/higress/issues/4706) | 2026-09-16 | issue-spec (Proposal/Design) | Proposal: make model-router auto-routing trigger model ID configurable |
| [#4610](https://github.com/higress-group/higress/issues/4610) | 2026-08-27 | 功能请求/咨询 | 使用AI负载均衡插件（ai-load-balancer）发现一些问题 |
| [#4605](https://github.com/higress-group/higress/issues/4605) | 2026-08-26 | 功能请求/咨询 | [RFC] Make auto-routing model ID customizable in model-router plugin |
| [#4600](https://github.com/higress-group/higress/issues/4600) | 2026-08-26 | issue-spec (Proposal/Design) | Design: Isolate ai-image-reader DashScope provider configuration per plugin config |
| [#4599](https://github.com/higress-group/higress/issues/4599) | 2026-08-26 | Bug 报告 | ai-token-ratelimit and frontend-gray Wasm plugins panic on malformed Cookie header and fail open, bypassing AI token rate limiting and gray-release routing |
| [#4575](https://github.com/higress-group/higress/issues/4575) | 2026-08-18 | issue-spec (Proposal/Design) | Proposal: Preserve ai-image-reader source image order across OCR callbacks |
| [#4565](https://github.com/higress-group/higress/issues/4565) | 2026-08-18 | Bug 报告 | [bug] ai-statistics: Gemini streaming path streamGenerateContent?alt=sse model name resolves to UNKNOWN |
| [#4559](https://github.com/higress-group/higress/issues/4559) | 2026-08-17 | issue-spec (Proposal/Design) | Proposal: AI JSON 响应的 Provider 感知结构化输出策略 |
| [#4558](https://github.com/higress-group/higress/issues/4558) | 2026-08-17 | issue-spec (Proposal/Design) | Proposal: AI 会话上下文版本化与工具调用历史 |
| [#4557](https://github.com/higress-group/higress/issues/4557) | 2026-08-17 | issue-spec (Proposal/Design) | Proposal: AI 缓存有效性与命中可观测性 |
| [#4551](https://github.com/higress-group/higress/issues/4551) | 2026-08-16 | 功能请求/咨询 | proposal(ai): establish a semantic control plane for AI routes |
| [#4546](https://github.com/higress-group/higress/issues/4546) | 2026-08-16 | 功能请求/咨询 | proposal(ai-image-reader): add an OpenAI-compatible vision provider |
| [#4545](https://github.com/higress-group/higress/issues/4545) | 2026-08-16 | 功能请求/咨询 | bug(ai-image-reader): preserve source image order across OCR callbacks |
| [#4544](https://github.com/higress-group/higress/issues/4544) | 2026-08-16 | 功能请求/咨询 | fix(ai-proxy): retry/health check 未应用 providerDomain \|\| fix(ai-proxy): retry/health check providerDomain is not applied |
| [#4540](https://github.com/higress-group/higress/issues/4540) | 2026-08-16 | Bug 报告 | ai-image-reader: DashScope apiKey stored in package-global state leaks across provider instances |
| [#4535](https://github.com/higress-group/higress/issues/4535) | 2026-08-15 | issue-spec (Proposal/Design) | Proposal: 修复 ai-image-reader DashScope 配置跨实例覆盖 \|\| Proposal: Isolate ai-image-reader DashScope provider configuration per plugin config |
| [#4523](https://github.com/higress-group/higress/issues/4523) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: 修复 ai-cache embedding provider 配置跨实例覆盖 \|\| Proposal: Isolate ai-cache embedding provider configuration per plugin config |
| [#4446](https://github.com/higress-group/higress/issues/4446) | 2026-08-12 | issue-spec (Proposal/Design) | Proposal: Add native latency histograms and an in-flight gauge to ai-statistics |
| [#4445](https://github.com/higress-group/higress/issues/4445) | 2026-08-12 | issue-spec (Proposal/Design) | Proposal: Preserve structured AI response semantics on ai-cache hits |
| [#4424](https://github.com/higress-group/higress/issues/4424) | 2026-08-11 | Bug 报告 | [ai-statistics 插件] Codex /v1/responses 请求流式响应，解析 model 与 token 消耗失败 \|\| [ai-statistics plug-in] Codex /v1/responses requests streaming response, parsing model and token consumption fails |
| [#4396](https://github.com/higress-group/higress/issues/4396) | 2026-08-10 | 功能请求/咨询 | ai-proxy retries non-chat requests with Chat Completions transforms |
| [#4336](https://github.com/higress-group/higress/issues/4336) | 2026-08-08 | Bug 报告 | ai-history panics on negative history count parameters |
| [#4335](https://github.com/higress-group/higress/issues/4335) | 2026-08-08 | Bug 报告 | ai-agent panics when OpenAPI servers are missing |
| [#4334](https://github.com/higress-group/higress/issues/4334) | 2026-08-08 | Bug 报告 | ai-cache panics on malformed Chroma query responses |
| [#4323](https://github.com/higress-group/higress/issues/4323) | 2026-08-08 | 功能请求/咨询 | ai-proxy omits system_fingerprint field in streaming responses, breaking older go-openai SDK versions |
| [#4301](https://github.com/higress-group/higress/issues/4301) | 2026-08-07 | Bug 报告 | bug(ai-proxy): malformed multimodal fields can panic content parsing |
| [#4290](https://github.com/higress-group/higress/issues/4290) | 2026-08-07 | issue-spec (Proposal/Design) | Design: GIE 显式 BuiltIn ai-endpoint-picker 与 External EPP 兼容 \|\| Design: GIE explicit BuiltIn ai-endpoint-picker compatible with External EPP |
| [#4289](https://github.com/higress-group/higress/issues/4289) | 2026-08-07 | issue-spec (Proposal/Design) | Proposal: GIE 显式集成 ai-endpoint-picker 并默认兼容 External EPP \|\| Proposal: GIE explicitly integrates ai-endpoint-picker and is compatible with External EPP by default |
| [#4272](https://github.com/higress-group/higress/issues/4272) | 2026-08-06 | 功能请求/咨询 | fix: Claude response cache token propagation to OpenAI format |
| [#4267](https://github.com/higress-group/higress/issues/4267) | 2026-08-05 | 功能请求/咨询 | ai-statistics: hard-coded 100 MiB request-body buffer causes 413 for non-AI multipart uploads |
| [#4233](https://github.com/higress-group/higress/issues/4233) | 2026-07-31 | 功能请求/咨询 | ai-proxy Wasm plugin NACK prevents dynamic HTTPS/TLS listener updates |
| [#4214](https://github.com/higress-group/higress/issues/4214) | 2026-07-27 | 功能请求/咨询 | [ai-proxy] Claude→OpenAI conversion leaves a non-leading system message, rejected by strict backends ("System message must be at the beginning.") |
| [#4201](https://github.com/higress-group/higress/issues/4201) | 2026-07-24 | 功能请求/咨询 | AI路由的重试插件和全局路由超时配置问题 \|\| AI routing retry plug-in and global routing timeout configuration issues |
| [#4173](https://github.com/higress-group/higress/issues/4173) | 2026-07-20 | Bug 报告 | ai-statistics配置defaultConfig里的attributes不生效 |
| [#4157](https://github.com/higress-group/higress/issues/4157) | 2026-07-17 | Bug 报告 | ai-data-masking 插件开启后立即 OOM 崩溃 \|\| ai-data-masking OOM crashes immediately after the plug-in is enabled |
| [#4133](https://github.com/higress-group/higress/issues/4133) | 2026-07-13 | Bug 报告 | AI路由不支持一个https(忽略ssl证书校验的前提), 一个http进行负载均衡 \|\| AI routing does not support an https (ignoring the premise of ssl certificate verification), an http for load balancing |
| [#4089](https://github.com/higress-group/higress/issues/4089) | 2026-07-07 | 功能请求/咨询 | [ai-proxy] responses协议通过源码看到已经支持apikey亲和性选择了，希望messages协议也添加该支持 \|\| [ai-proxy] The responses protocol already supports apikey affinity selection through the source code. I hope the messages protocol will also add this support. |
| [#4082](https://github.com/higress-group/higress/issues/4082) | 2026-07-06 | Bug 报告 | [ai-proxy] 插件在进行 Anthropic Messages -> OpenaiChatCompletions 协议转换中会导致结构错误 |
| [#4072](https://github.com/higress-group/higress/issues/4072) | 2026-07-06 | issue-spec (Proposal/Design) | [Proposal] optimize ai-token-ratelimit & cluster-key-rate-limit config UX, docs, and dev notes |
| [#4067](https://github.com/higress-group/higress/issues/4067) | 2026-07-05 | Bug 报告 | ai-token-ratelimit 插件不生效：配置正确但从不连接 Redis（cx_total/cx_connect_fail 恒为 0，WasmPlugin config_fail 持续增长） \|\| ai-token-ratelimit plug-in does not take effect: the configuration is correct but never connects to Redis (cx_total/cx_connect_fail is always 0, WasmPlugin config_fail continues to grow) |
| [#4021](https://github.com/higress-group/higress/issues/4021) | 2026-06-25 | Bug 报告 | ai-context-limit plugin image build fails because BPE vocabulary is missing |
| [#4018](https://github.com/higress-group/higress/issues/4018) | 2026-06-24 | 功能请求/咨询 | 希望 ai-statistics 插件默认支持 use_default_attributes=true + 自定义attributes \|\| I hope the ai-statistics plug-in supports use_default_attributes=true + custom attributes by default |
| [#3992](https://github.com/higress-group/higress/issues/3992) | 2026-06-17 | Bug 报告 | model-mapper: service constraint silently skips matching on McpBridge-based AI routes |
| [#3970](https://github.com/higress-group/higress/issues/3970) | 2026-06-15 | 功能请求/咨询 | ai-statistics 是否可以增加自定义 label？ \|\| ai-statistics Is it possible to add custom labels? |
| [#3949](https://github.com/higress-group/higress/issues/3949) | 2026-06-10 | 功能请求/咨询 | AI服务提供者的支持Codex OAuth认证吗？ \|\| Does the AI ​​service provider support Codex OAuth authentication? |
| [#3944](https://github.com/higress-group/higress/issues/3944) | 2026-06-10 | 功能请求/咨询 | ai-proxy：Higress integrates with the Claude model on AWS Bedrock and exposes the Anthropic protocol (/v1/messages) externally. The ai-proxy internally uses the bedrock-mantle endpoint but reported an error. \| 对接AWS Bedrock上面的Claude模型，Higress对外暴露Anthropic协议（/v1/messages），ai-proxy内部使用bedrock-mantle端点报错 |
| [#3934](https://github.com/higress-group/higress/issues/3934) | 2026-06-08 | 功能请求/咨询 | ai-proxy: Claude provider hardcodes Host header to api.anthropic.com, ignoring claudeCustomUrl |
| [#3931](https://github.com/higress-group/higress/issues/3931) | 2026-06-08 | 功能请求/咨询 | 目前使用AI网关，每隔几天就会出现由于内存问题，导致进程不可用，需要重启 \|\| I am currently using the AI gateway, and every few days there will be a memory problem that causes the process to be unavailable and needs to be restarted. |
| [#3926](https://github.com/higress-group/higress/issues/3926) | 2026-06-05 | Bug 报告 | AI路由管理里的降级服务配置后不生效 \|\| The downgrade service in AI routing management does not take effect after configuration |
| [#3915](https://github.com/higress-group/higress/issues/3915) | 2026-06-04 | 功能请求/咨询 | Higress AI 开源网关是否可提供类似 LiteLLM 的 Organization / Team / User 多级租户管理模型 \|\| Can the Higress AI open source gateway provide an Organization / Team / User multi-level tenant management model similar to LiteLLM? |
| [#3912](https://github.com/higress-group/higress/issues/3912) | 2026-06-03 | 功能请求/咨询 | AI网关管理创建的DB MCP服务连不上 \|\| The DB MCP service created by AI gateway management cannot be connected. |
| [#3892](https://github.com/higress-group/higress/issues/3892) | 2026-05-27 | 功能请求/咨询 | ai-proxy启动报错 |
| [#3880](https://github.com/higress-group/higress/issues/3880) | 2026-05-26 | Bug 报告 | AI缓存插件不支持cache+vector同时生效 \|\| The AI cache plug-in does not support cache+vector taking effect at the same time. |
| [#3843](https://github.com/higress-group/higress/issues/3843) | 2026-05-18 | 功能请求/咨询 | 什么时候能支持  Claude API兼容模式 \|\| When can Claude API compatibility mode be supported? |
| [#3841](https://github.com/higress-group/higress/issues/3841) | 2026-05-17 | 功能请求/咨询 | Support OpenAI Responses API affinity across multiple providers/deployments |
| [#3840](https://github.com/higress-group/higress/issues/3840) | 2026-05-17 | 功能请求/咨询 | Support provider-level session affinity for AI Route / ai-proxy |
| [#3819](https://github.com/higress-group/higress/issues/3819) | 2026-05-13 | 功能请求/咨询 | ai-statistics请求超过100MB报错 413 Payload Too Large \|\| ai-statistics request exceeds 100MB and reports error 413 Payload Too Large |
| [#3814](https://github.com/higress-group/higress/issues/3814) | 2026-05-12 | Bug 报告 | ai-statistics 插件在处理流式 LLM 响应时会导致 WASM OOM 和 503 错误 |
| [#3812](https://github.com/higress-group/higress/issues/3812) | 2026-05-12 | 功能请求/咨询 | The ai-proxy plugin loses reasoning_content when converting Claude format to OpenAI format |
| [#3763](https://github.com/higress-group/higress/issues/3763) | 2026-04-28 | 功能请求/咨询 | AI路由功能——目标模型 \|\| AI routing function-target model |
| [#3752](https://github.com/higress-group/higress/issues/3752) | 2026-04-24 | 功能请求/咨询 | ai-proxy support OPENAI /v1/responses/compact |
| [#3740](https://github.com/higress-group/higress/issues/3740) | 2026-04-21 | Bug 报告 | Bug: ai-load-balancer plugin hangs on requests without body (GET/HEAD/DELETE), causing 504 timeout |
| [#3732](https://github.com/higress-group/higress/issues/3732) | 2026-04-17 | 功能请求/咨询 | model-mapper config overwritten when multiple upstreams share the same provider |
| [#3725](https://github.com/higress-group/higress/issues/3725) | 2026-04-16 | 功能请求/咨询 | ai-proxy: Should illegal providers affect legitimate providers during the startup phase |
| [#3703](https://github.com/higress-group/higress/issues/3703) | 2026-04-11 | 功能请求/咨询 | Envoy 生成的 x-forwarded-proto 对部分 LLM API 造成了干扰 |
| [#3693](https://github.com/higress-group/higress/issues/3693) | 2026-04-09 | Bug 报告 | AI路由配置了请求认证未生效 \|\| AI routing configured request authentication does not take effect |
| [#3678](https://github.com/higress-group/higress/issues/3678) | 2026-04-03 | 功能请求/咨询 | higress作为AI网关代理doubao大模型时调用返回异常 \|\| higress returns exception when called when acting as AI gateway proxy doubao large model |
| [#3633](https://github.com/higress-group/higress/issues/3633) | 2026-03-22 | 功能请求/咨询 | 希望 AI 路由能请求并显示提供商额度 \|\| Hope AI routing can request and display provider quota |
| [#3615](https://github.com/higress-group/higress/issues/3615) | 2026-03-18 | 功能请求/咨询 | AI Agent 工具调用未执行：LLM 正确输出 Thought + Action，但无 Observation |
| [#3589](https://github.com/higress-group/higress/issues/3589) | 2026-03-13 | 功能请求/咨询 | 希望ai-statistics插件可以支持完整message以json格式输出 \|\| Hope the ai-statistics plug-in can support the complete message output in json format |
| [#3581](https://github.com/higress-group/higress/issues/3581) | 2026-03-10 | 功能请求/咨询 | ai-statistics插件支持Azure OpenAI的/v1/responses接口采集LLM返回内容 \|\| ai-statistics plug-in supports Azure OpenAI’s /v1/responses interface to collect LLM return content |
| [#3473](https://github.com/higress-group/higress/issues/3473) | 2026-02-12 | 功能请求/咨询 | 同一个模型多个AI服务提供商如何hash路由 \|\| How to hash route multiple AI service providers for the same model |
| [#3407](https://github.com/higress-group/higress/issues/3407) | 2026-01-29 | 功能请求/咨询 | ai-load-balancer插件不太好用 \|\| ai-load-balancer plug-in is not easy to use |
| [#3392](https://github.com/higress-group/higress/issues/3392) | 2026-01-26 | 功能请求/咨询 | ai-load-balancer 考虑支持 SGLang 吗？ \|\| ai-load-balancer Consider supporting SGLang? |
| [#3308](https://github.com/higress-group/higress/issues/3308) | 2026-01-07 | Bug 报告 | ai-data-masking deny_words 在处理llm的content的时候不生效 \|\| ai-data-masking deny_words does not take effect when processing the content of llm |
| [#3246](https://github.com/higress-group/higress/issues/3246) | 2025-12-22 | 功能请求/咨询 | ai-token-ratelimit命中多条限流规则后(rule_items)，是否可以基于所有命中规则判定最终的限流结果 \|\| ai-token-ratelimit After hitting multiple current limiting rules (rule_items), can the final current limiting result be determined based on all hit rules? |
| [#3214](https://github.com/higress-group/higress/issues/3214) | 2025-12-11 | 功能请求/咨询 | AI统计插件可以实现cached token的用量统计吗？ \|\| Can the AI statistics plug-in realize usage statistics of cached token? |
| [#3203](https://github.com/higress-group/higress/issues/3203) | 2025-12-08 | 功能请求/咨询 | AI网关是否支持基于指标自动负载均衡到后端不同推理服务 \|\| Does the AI gateway support automatic load balancing to different back-end inference services based on indicators? |
| [#3197](https://github.com/higress-group/higress/issues/3197) | 2025-12-05 | 功能请求/咨询 | 配置多个Azure OpenAI为provider时，配置路由做负载均衡，使用流式调用，容易报错invalid_request_error \|\| When configuring multiple Azure OpenAI as providers, configuring routes for load balancing and using streaming calls, it is easy to report an invalid_request_error error. |
| [#3189](https://github.com/higress-group/higress/issues/3189) | 2025-12-03 | Bug 报告 | openai自定义协议配置多个模型动态转换没有生效 \|\| openai custom protocol configuration multiple model dynamic conversion does not take effect |
| [#3174](https://github.com/higress-group/higress/issues/3174) | 2025-11-27 | 功能请求/咨询 | 请求响应转换插件不支持AI路由么？ \|\| Doesn’t the request-response conversion plug-in support AI routing? |
| [#3158](https://github.com/higress-group/higress/issues/3158) | 2025-11-20 | 功能请求/咨询 | ai-security-guard don't support streaming response |
| [#3147](https://github.com/higress-group/higress/issues/3147) | 2025-11-18 | 功能请求/咨询 | AI路由配置能接入语音模型吗 \|\| Can the AI ​​routing configuration be connected to the speech model? |
| [#3146](https://github.com/higress-group/higress/issues/3146) | 2025-11-18 | 功能请求/咨询 | AI-Proxy对接Gemini接口，需要支持generationConfig参数 \|\| AI-Proxy connects to the Gemini interface and needs to support the generationConfig parameter |
| [#3141](https://github.com/higress-group/higress/issues/3141) | 2025-11-17 | Bug 报告 | AI配额管理无法使用 \|\| AI quota management cannot be used. |
| [#3115](https://github.com/higress-group/higress/issues/3115) | 2025-11-12 | 功能请求/咨询 | AI路由管理-AI JSON格式化问题 |
| [#3087](https://github.com/higress-group/higress/issues/3087) | 2025-11-04 | 功能请求/咨询 | 希望AI网关管理-MCP管理提供插件支持 \|\| Hope that AI Gateway Management-MCP Management provides plug-in support |
| [#3086](https://github.com/higress-group/higress/issues/3086) | 2025-11-04 | 功能请求/咨询 | ai-proxy插件更新镜像后报错 |
| [#3055](https://github.com/higress-group/higress/issues/3055) | 2025-10-27 | Bug 报告 | 普通路由/test1使用重写插件,重写为/v1/chat/completions后,curl可以返回200状态码。使用AI路由直接curl 10.58.230.60:8080/v1/chat/completions,返回404。无法解决。 \|\| Ordinary route /test1 uses the rewrite plug-in. After rewriting to /v1/chat/completions, curl can return the 200 status code. Use AI routing to directly curl 10.58.230.60:8080/v1/chat/completions and return 404. Can't be solved. |
| [#3036](https://github.com/higress-group/higress/issues/3036) | 2025-10-21 | Bug 报告 | AI提示词模板properties传json报错 \|\| AI prompt word template properties report error when passing json |
| [#3020](https://github.com/higress-group/higress/issues/3020) | 2025-10-16 | 功能请求/咨询 | Feature Request: Implement A2AS (Agent-to-Agent Security) Framework for AI Gateway |
| [#3017](https://github.com/higress-group/higress/issues/3017) | 2025-10-16 | 功能请求/咨询 | AI提示词插件 配置显示问题 \|\| AI prompt word plug-in configuration display problem |
| [#2960](https://github.com/higress-group/higress/issues/2960) | 2025-09-25 | 功能请求/咨询 | transform配额ai-quota插件的处理问题 \|\| =Problem of the transformation quota ai-quota plug-in |
| [#2954](https://github.com/higress-group/higress/issues/2954) | 2025-09-25 | Bug 报告 | AI提示词模板插件不支持流式使用 \|\| =AI prompt word template plugin does not support streaming use |
| [#2949](https://github.com/higress-group/higress/issues/2949) | 2025-09-23 | 功能请求/咨询 | 欢迎大家参加Higress AI 网关开发挑战赛，赢取20万元奖金 |
| [#2918](https://github.com/higress-group/higress/issues/2918) | 2025-09-15 | Bug 报告 | ai-token-rate-limit 在响应体 Content-Type 是 application/json 时，且响应体数据过大时，会无法获取到 Token 数据 \|\| ai-token-rate-limit When the response body Content-Type is application/json, and the response body data is too large, the Token data will not be obtained. |
| [#2900](https://github.com/higress-group/higress/issues/2900) | 2025-09-10 | 功能请求/咨询 | extended ai-proxy CustomSettings |
| [#2857](https://github.com/higress-group/higress/issues/2857) | 2025-09-02 | 功能请求/咨询 | ai-statistics插件没有llm_first_token_duration指标 |
| [#2855](https://github.com/higress-group/higress/issues/2855) | 2025-09-02 | 功能请求/咨询 | Feature: AI wasm load balancer 在非K8s 场景支持 多实例智能路由？（比如 STATIC Ips） |
| [#2798](https://github.com/higress-group/higress/issues/2798) | 2025-08-20 | 功能请求/咨询 | ai-proxy (or ai-statistics) integration with websockets |
| [#2756](https://github.com/higress-group/higress/issues/2756) | 2025-08-13 | 功能请求/咨询 | ai-proxy插件创建问题 \|\| =Ai-proxy plugin creation problem |
| [#2733](https://github.com/higress-group/higress/issues/2733) | 2025-08-08 | 功能请求/咨询 | ai-statistics 记录流式请求分配过多的内存 \|\| ai-statistics Record streaming requests allocate too much memory |
| [#2718](https://github.com/higress-group/higress/issues/2718) | 2025-08-05 | 测试/e2e | Implement Google Cloud Vertex LLM mock server & e2e test case |
| [#2717](https://github.com/higress-group/higress/issues/2717) | 2025-08-05 | 测试/e2e | Implement Amazon Bedrock LLM mock server & e2e test case |
| [#2708](https://github.com/higress-group/higress/issues/2708) | 2025-08-04 | Bug 报告 | AI路由中使用了前缀时无法正常转发到后端服务 \|\| =The prefix cannot be forwarded to the backend service normally when using prefix in AI routing |
| [#2607](https://github.com/higress-group/higress/issues/2607) | 2025-07-16 | 功能请求/咨询 | AI路由插件是不是会丢弃不在白名单内的请求头信息 \|\| Will the AI routing plugin discard request header information that is not on the whitelist? |
| [#2487](https://github.com/higress-group/higress/issues/2487) | 2025-06-24 | 功能请求/咨询 | 本地部署测试，使用AI配额策略时，更新配额提示stream timeout, 查看配额正常 \|\| Local deployment test. When using the AI ​​quota strategy, update the quota prompts stream timeout, check the quota normally |
| [#2483](https://github.com/higress-group/higress/issues/2483) | 2025-06-23 | 功能请求/咨询 | Extend ai-proxy Plugin to Support OpenAI Response API Protocol with Remote MCP Server Tool Calling |
| [#2482](https://github.com/higress-group/higress/issues/2482) | 2025-06-23 | Bug 报告 | [ai-statistics ai 统计]  代理 阿里百炼应用时，无法正常统计token |
| [#2464](https://github.com/higress-group/higress/issues/2464) | 2025-06-19 | 功能请求/咨询 | 关于AI Token 限流插件的深度探究——希望有技术人员能认真阅读并理解互相讨论 \|\| In-depth exploration of AI Token current limit plug-in-I hope some technicians can read carefully and understand and discuss with each other |
| [#2428](https://github.com/higress-group/higress/issues/2428) | 2025-06-16 | 功能请求/咨询 | [model-mapper] 支持通过正则匹配与替换目标模型 \|\| [model-mapper] supports regular matching and replacement of target models |
| [#2359](https://github.com/higress-group/higress/issues/2359) | 2025-06-02 | Bug 报告 | 【ai-search】联网搜索插件配置开头引用时会导致流式请求输出被截断 \|\| 【ai-search】The streaming request output will be truncated when referenced at the beginning of the network search plug-in configuration. |
| [#2345](https://github.com/higress-group/higress/issues/2345) | 2025-05-29 | 功能请求/咨询 | [ai-proxy] 希望能将 provider 的 capabilities 配置化 \|\| [ai-proxy] Hope to configure the capabilities of the provider |

### MCP 生态（116）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5301](https://github.com/higress-group/higress/issues/5301) | 2026-11-04 | issue-spec (Proposal/Design) | [Design] Wanlianku MCP adapter: seven tools, isolated consumer tokens and verification plan |
| [#5300](https://github.com/higress-group/higress/issues/5300) | 2026-11-04 | issue-spec (Proposal/Design) | [Proposal] Add Wanlianku MCP marketplace integration with per-consumer credentials |
| [#5297](https://github.com/higress-group/higress/issues/5297) | 2026-11-04 | issue-spec (Proposal/Design) | Proposal: add the Fax for Agents MCP server to the MCP marketplace |
| [#5296](https://github.com/higress-group/higress/issues/5296) | 2026-11-03 | 文档 | docs: mcp-server README.md (CN) contains unresolved conflict markers since [#5029](https://github.com/higress-group/higress/issues/5029) |
| [#5295](https://github.com/higress-group/higress/issues/5295) | 2026-11-02 | 功能请求/咨询 | mcp路由支持配置其他插件 \|\| mcp routing supports configuring other plug-ins |
| [#5281](https://github.com/higress-group/higress/issues/5281) | 2026-10-29 | issue-spec (Proposal/Design) | Design: Unify Modern/Legacy MCP business compatibility \|\| 统一 Modern/Legacy MCP 业务兼容策略 |
| [#5280](https://github.com/higress-group/higress/issues/5280) | 2026-10-29 | issue-spec (Proposal/Design) | Proposal: Unify Modern/Legacy MCP business compatibility \|\| 统一 Modern/Legacy MCP 业务兼容策略 |
| [#5278](https://github.com/higress-group/higress/issues/5278) | 2026-10-28 | issue-spec (Proposal/Design) | Proposal: BrewPage MCP marketplace integration intake and approval |
| [#5261](https://github.com/higress-group/higress/issues/5261) | 2026-10-26 | issue-spec (Proposal/Design) | Design: Stateless modern MCP instructions passthrough \|\| 无状态透传 modern MCP 服务端指引 |
| [#5235](https://github.com/higress-group/higress/issues/5235) | 2026-10-22 | 功能请求/咨询 | higress all in one mcp tool能支持暴露上游的uri吗？ |
| [#5234](https://github.com/higress-group/higress/issues/5234) | 2026-10-22 | 功能请求/咨询 | higress all in one v2.2.4镜像的key-auth和mcp-server插件版本没覆盖v2.2.3的 |
| [#5198](https://github.com/higress-group/higress/issues/5198) | 2026-10-20 | Bug 报告 | MCP server tools/call fails with a local 308 redirect when the domain enables Force HTTPS (ssl-redirect on MCP server Ingress) |
| [#5049](https://github.com/higress-group/higress/issues/5049) | 2026-10-09 | 功能请求/咨询 | mcp-session: live SSE session is split across old/new Redis after mcpServer.redis hot update |
| [#5012](https://github.com/higress-group/higress/issues/5012) | 2026-10-08 | issue-spec (Proposal/Design) | Design: Restore MCP proxy main-request forwarding \|\| 恢复 MCP 代理主请求转发与旧配置兼容性 |
| [#5011](https://github.com/higress-group/higress/issues/5011) | 2026-10-08 | issue-spec (Proposal/Design) | Proposal: Restore MCP proxy routing and header compatibility \|\| 恢复 MCP 代理转发与请求头兼容性 |
| [#5002](https://github.com/higress-group/higress/issues/5002) | 2026-10-06 | issue-spec (Proposal/Design) | Proposal: Close tool-search Milvus clients on server retirement |
| [#4879](https://github.com/higress-group/higress/issues/4879) | 2026-09-29 | Bug 报告 | mcp-session: SSE fragment cache dropped at endStream + unbounded cache growth |
| [#4788](https://github.com/higress-group/higress/issues/4788) | 2026-09-28 | 功能请求/咨询 | Streamable HTTP MCP session requests reach different upstream Pods, causing intermittent 404 / `Session terminated` |
| [#4778](https://github.com/higress-group/higress/issues/4778) | 2026-09-27 | issue-spec (Proposal/Design) | Design: Optional BM25 and dense hybrid retrieval for MCP Tool Search |
| [#4777](https://github.com/higress-group/higress/issues/4777) | 2026-09-27 | issue-spec (Proposal/Design) | Proposal: Add optional BM25 and dense hybrid retrieval to MCP Tool Search |
| [#4735](https://github.com/higress-group/higress/issues/4735) | 2026-09-20 | issue-spec (Proposal/Design) | Proposal: return a clear error when an OpenAPI spec converts to zero MCP tools instead of panicking in hgctl |
| [#4684](https://github.com/higress-group/higress/issues/4684) | 2026-09-11 | issue-spec (Proposal/Design) | Design: Request-scoped auto protocol detection for mcp-server \|\| mcp-server 请求级 auto 协议探测设计 |
| [#4683](https://github.com/higress-group/higress/issues/4683) | 2026-09-11 | issue-spec (Proposal/Design) | Proposal: Add opt-in auto protocol detection to mcp-server \|\| mcp-server 增加可选的 auto 协议探测 |
| [#4636](https://github.com/higress-group/higress/issues/4636) | 2026-09-02 | 功能请求/咨询 | higress 有做 MCP 网关的计划吗？目前看着是做了插件做协议转换，后面会不会做多租户管理，配置 MCP-server。 \|\| Does higress have any plans to become an MCP gateway? At present, it seems that a plug-in is used for protocol conversion. Will multi-tenant management and MCP-server be configured later? |
| [#4621](https://github.com/higress-group/higress/issues/4621) | 2026-08-31 | issue-spec (Proposal/Design) | Design: Decouple mcp-server schema validation from REST tool compatibility \|\| 解耦 mcp-server Schema 校验与 REST 工具兼容路径 |
| [#4587](https://github.com/higress-group/higress/issues/4587) | 2026-08-23 | issue-spec (Proposal/Design) | Design: honor non-zero Redis database in mcp-session |
| [#4586](https://github.com/higress-group/higress/issues/4586) | 2026-08-23 | issue-spec (Proposal/Design) | Proposal: honor non-zero Redis database in mcp-session |
| [#4555](https://github.com/higress-group/higress/issues/4555) | 2026-08-16 | 功能请求/咨询 | proposal(mcp): add declarative MCPRoute governance |
| [#4549](https://github.com/higress-group/higress/issues/4549) | 2026-08-16 | 功能请求/咨询 | proposal(mcp): implement delta generation for control-plane resources |
| [#4548](https://github.com/higress-group/higress/issues/4548) | 2026-08-16 | 功能请求/咨询 | proposal(tool-search): reuse RAG vector-store providers and add Qdrant |
| [#4507](https://github.com/higress-group/higress/issues/4507) | 2026-08-14 | Bug 报告 | Higress 2.2.3 gateway 在 source-derived `nacos-mcp-registry` 配置 + 直接 POST initialize（无前置 GET /sse、`match_list: []`）路径上 OOM/SIGABRT 崩溃 \|\| Higress 2.2.3 gateway OOM/SIGABRT crash on source-derived `nacos-mcp-registry` configuration + direct POST initialize (no prepended GET /sse, `match_list: []`) path |
| [#4477](https://github.com/higress-group/higress/issues/4477) | 2026-08-13 | 功能请求/咨询 | mcp-server remote registry load-balances off-by-one, last instance never selected |
| [#4470](https://github.com/higress-group/higress/issues/4470) | 2026-08-13 | issue-spec (Proposal/Design) | Proposal: Expand MCP OAuth security and extension ecosystem \|\| 完善 MCP OAuth 安全与扩展生态 |
| [#4469](https://github.com/higress-group/higress/issues/4469) | 2026-08-13 | issue-spec (Proposal/Design) | Proposal: Support multi-round interactions and long-running tasks in the MCP gateway \|\| 支持 MCP 网关多轮交互与长任务 |
| [#4468](https://github.com/higress-group/higress/issues/4468) | 2026-08-13 | issue-spec (Proposal/Design) | Proposal: Deepen MCP schema and tool-level policy governance \|\| 深化 MCP Schema 与工具级策略治理 |
| [#4467](https://github.com/higress-group/higress/issues/4467) | 2026-08-13 | issue-spec (Proposal/Design) | Proposal: Evolve MCP protocol negotiation and cross-version interoperability \|\| 完善 MCP 协议能力协商与跨版本互操作 |
| [#4459](https://github.com/higress-group/higress/issues/4459) | 2026-08-12 | Bug 报告 | Data race and nil pointer panics in mcp-session Redis client and SSE handler |
| [#4431](https://github.com/higress-group/higress/issues/4431) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Keep mcp-session Redis state coherent across route merges |
| [#4429](https://github.com/higress-group/higress/issues/4429) | 2026-08-11 | 功能请求/咨询 | 如何在一个mcp server 中对接来自不同域名的api \|\| How to connect APIs from different domain names in an mcp server |
| [#4405](https://github.com/higress-group/higress/issues/4405) | 2026-08-10 | Bug 报告 | Concurrent map access panic in nacos MCP registry crashes Envoy worker |
| [#4395](https://github.com/higress-group/higress/issues/4395) | 2026-08-10 | 功能请求/咨询 | mcp-session ignores configured non-zero Redis database |
| [#4340](https://github.com/higress-group/higress/issues/4340) | 2026-08-08 | 功能请求/咨询 | MCP Session reverses the Redis requirement for user-level servers |
| [#4322](https://github.com/higress-group/higress/issues/4322) | 2026-08-08 | Bug 报告 | MCP SSE proxy panics on missing/mistyped context values in streaming response callbacks |
| [#4274](https://github.com/higress-group/higress/issues/4274) | 2026-08-06 | issue-spec (Proposal/Design) | Implement: MCP 2026 Tools Baseline for the WASM MCP Server \|\| 实现 WASM MCP Server 的 MCP 2026 Tools Baseline |
| [#4271](https://github.com/higress-group/higress/issues/4271) | 2026-08-06 | issue-spec (Proposal/Design) | Design: Dual-era MCP protocol core and proxy bridge for MCP 2026-07-28 \|\| MCP 2026-07-28 双代际协议内核与代理桥接设计 |
| [#4246](https://github.com/higress-group/higress/issues/4246) | 2026-08-01 | issue-spec (Proposal/Design) | Proposal: Adapt the mcp-server framework to MCP 2026-07-28 \|\| mcp-server 框架适配 MCP 2026-07-28 |
| [#4228](https://github.com/higress-group/higress/issues/4228) | 2026-07-29 | 功能请求/咨询 | MCP 最新协议的支持 \|\| MCP latest protocol support |
| [#4181](https://github.com/higress-group/higress/issues/4181) | 2026-07-22 | 功能请求/咨询 | higress能否支持mcp标准原生的prompts方法 |
| [#4081](https://github.com/higress-group/higress/issues/4081) | 2026-07-06 | Bug 报告 | higress 配置nacos将存量api接口转换成mcp 调用的时候频繁出现503 \|\| higress Configure nacos to convert the stock api interface into mcp. 503 frequently appears when calling. |
| [#4033](https://github.com/higress-group/higress/issues/4033) | 2026-06-29 | Bug 报告 | Higress（2.2.3版本）配置直接路由MCP无法获取工具 \|\| Higress (version 2.2.3) configures direct routing MCP and cannot obtain the tool |
| [#4004](https://github.com/higress-group/higress/issues/4004) | 2026-06-23 | Bug 报告 | Higress 2.2.2 从 Nacos3 读取 MCP tool 配置时，inputSchema 中 type: object 的参数及其 required 声明丢失 \|\| Higress 2.2.2 When reading MCP tool configuration from Nacos3, the parameters of type: object in inputSchema and their required declaration are lost |
| [#3946](https://github.com/higress-group/higress/issues/3946) | 2026-06-10 | 功能请求/咨询 | 来源于Nacos的HTTP-TO-MCP服务，tools/list输出部分缺少outputschema部分 \|\| HTTP-TO-MCP service from Nacos, the tools/list output part lacks the outputschema part |
| [#3945](https://github.com/higress-group/higress/issues/3945) | 2026-06-10 | Bug 报告 | [Bug] Higress-AI网关管理-MCP管理 添加路径时 /sse 保存后变成 //sse |
| [#3917](https://github.com/higress-group/higress/issues/3917) | 2026-06-04 | 功能请求/咨询 | Large MCP tools/call responses cause persistent Envoy anonymous RSS growth |
| [#3822](https://github.com/higress-group/higress/issues/3822) | 2026-05-13 | Bug 报告 | MCP无法读取响应体的header \|\| MCP cannot read the header of the response body |
| [#3802](https://github.com/higress-group/higress/issues/3802) | 2026-05-08 | Bug 报告 | MCP插件配置保存后YMAL格式错误 \|\| YMAL format error after saving the MCP plug-in configuration |
| [#3787](https://github.com/higress-group/higress/issues/3787) | 2026-05-05 | 功能请求/咨询 | [MCP] Add On-Page.ai SEO MCP |
| [#3698](https://github.com/higress-group/higress/issues/3698) | 2026-04-10 | 功能请求/咨询 | 在并发高的场景下使用mcpclient去获取tool list会出现获取不精准的情况 \|\| When using mcpclient to obtain tool list in high concurrency scenarios, the acquisition may be inaccurate. |
| [#3697](https://github.com/higress-group/higress/issues/3697) | 2026-04-10 | 功能请求/咨询 | 在并发高的场景下使用mcpclient去获取tool list会出现获取不精准的情况 \|\| When using mcpclient to obtain tool list in high concurrency scenarios, the acquisition may be inaccurate. |
| [#3685](https://github.com/higress-group/higress/issues/3685) | 2026-04-07 | 功能请求/咨询 | [Feature Request] Support MCP Elicitation in mcp-proxy mode |
| [#3634](https://github.com/higress-group/higress/issues/3634) | 2026-03-23 | 功能请求/咨询 | MCP管理，新建同名的MCP服务，直接把之前的覆盖了 \|\| MCP management. Create a new MCP service with the same name and directly overwrite the previous one. |
| [#3568](https://github.com/higress-group/higress/issues/3568) | 2026-03-06 | 功能请求/咨询 | MCP router和MCP工具聚合问题 \|\| MCP router and MCP tool aggregation problem |
| [#3538](https://github.com/higress-group/higress/issues/3538) | 2026-02-27 | 功能请求/咨询 | MCP直接代理模式提供日志详情 \|\| MCP direct proxy mode to provide log details? |
| [#3395](https://github.com/higress-group/higress/issues/3395) | 2026-01-26 | Bug 报告 | 创建mcp server 报错invoke com.alibaba.higress.sdk.model.Route.getName() because "existRoute" is null \|\| Create mcp server and report error invoke com.alibaba.higress.sdk.model.Route.getName() because "existRoute" is null |
| [#3387](https://github.com/higress-group/higress/issues/3387) | 2026-01-24 | 功能请求/咨询 | nacos配置http转mcp，mcp的Authorization怎么透传给http header \|\| nacos configures http to mcp, how does mcp's Authorization pass through to http header? |
| [#3376](https://github.com/higress-group/higress/issues/3376) | 2026-01-21 | Bug 报告 | mcp-server插件配置mcp-proxy类型时，无法代理transport为http且流式返回数据（reponse的content-type: text/event-stream）的mcp server \|\| mcp-server plug-in configures the mcp-proxy type, it cannot proxy the mcp server whose transport is http and the data is returned in a streaming manner (reponse content-type: text/event-stream) |
| [#3373](https://github.com/higress-group/higress/issues/3373) | 2026-01-21 | Bug 报告 | 使用Higress Nacos 以及spring ai alibaba无法访问MCP Server，报错404 \|\| Using Higress Nacos and spring ai alibaba, the MCP Server cannot be accessed and error 404 is reported. |
| [#3328](https://github.com/higress-group/higress/issues/3328) | 2026-01-14 | 功能请求/咨询 | 期望streamable类型mcp可以根据session id路由到固定节点 \|\| It is expected that the streamable type MCP can be routed to a fixed node based on the session id. |
| [#3315](https://github.com/higress-group/higress/issues/3315) | 2026-01-09 | 功能请求/咨询 | 创建MCP管理，能否自动加载openapi  swagger的/v3/api-docs \|\| Create MCP management, can it automatically load openapi swagger's /v3/api-docs |
| [#3282](https://github.com/higress-group/higress/issues/3282) | 2025-12-30 | 功能请求/咨询 | MCP插件支持将代理的现存的多个MCP server的工具可选重组为新的MCP Server \|\| MCP plug-in supports the tool of optionally reorganizing multiple existing MCP servers of the agent into a new MCP Server |
| [#3281](https://github.com/higress-group/higress/issues/3281) | 2025-12-30 | 功能请求/咨询 | Cannot view mcp tools via direct route |
| [#3248](https://github.com/higress-group/higress/issues/3248) | 2025-12-22 | 功能请求/咨询 | native mcp服务可以给不通的订阅者  开放不通的权限范围 \|\| native mcp service can open unreachable permission ranges to unreachable subscribers |
| [#3247](https://github.com/higress-group/higress/issues/3247) | 2025-12-22 | 功能请求/咨询 | 新增每个mcp服务 订阅者的监控（监控粒度到订阅者级别） \|\| Add monitoring of each mcp service subscriber (monitoring granularity to subscriber level) |
| [#3242](https://github.com/higress-group/higress/issues/3242) | 2025-12-21 | Bug 报告 | higress配置直接路由MCP时，对于/xxx/sse这种路径，经过higress转发，message路径会变成 /xxx/xxx/message?session=...导致404错误 |
| [#3151](https://github.com/higress-group/higress/issues/3151) | 2025-11-19 | Bug 报告 | Nacos的Mcp-server无法在Higress里面进行添加 \|\| Nacos' Mcp-server cannot be added in Higress |
| [#3081](https://github.com/higress-group/higress/issues/3081) | 2025-10-31 | 功能请求/咨询 | nginx-migration-mcp 插件沙箱工具 \|\| nginx-migration-mcp plug-in sandbox tool |
| [#3080](https://github.com/higress-group/higress/issues/3080) | 2025-10-31 | 功能请求/咨询 | nginx-migration-mcp 插件在 Higress 下效果验证和优化 |
| [#3064](https://github.com/higress-group/higress/issues/3064) | 2025-10-28 | 功能请求/咨询 | higress + nacos 存量API转MCP，tool list获取成功，调用工具时报错404 \|\| higress + nacos Convert existing API to MCP, tool list is obtained successfully, error 404 is reported when calling the tool |
| [#3035](https://github.com/higress-group/higress/issues/3035) | 2025-10-21 | 功能请求/咨询 | ReOrganize mcp servers feature |
| [#3034](https://github.com/higress-group/higress/issues/3034) | 2025-10-21 | 功能请求/咨询 | API转MCP是否有需要一定要用YAML配置 \|\| If you need to convert API to MCP, you must use YAML configuration |
| [#3033](https://github.com/higress-group/higress/issues/3033) | 2025-10-21 | Bug 报告 | 使用“MCP 管理”直接路由 sse，客户端无法访问 \|\| Use "MCP Management" to route sse directly, the client cannot access it |
| [#2999](https://github.com/higress-group/higress/issues/2999) | 2025-10-13 | 功能请求/咨询 | [Enhancement] Add an mcp smart router |
| [#2924](https://github.com/higress-group/higress/issues/2924) | 2025-09-15 | 功能请求/咨询 | Higress 的Gateway 支持 MCP Client对Mcp Server tools的请求信息 |
| [#2902](https://github.com/higress-group/higress/issues/2902) | 2025-09-11 | 功能请求/咨询 | openapi-to-mcp场景下https服务访问报错 \|\| = The https service access error in openapi-to-mcp scenario |
| [#2885](https://github.com/higress-group/higress/issues/2885) | 2025-09-08 | 功能请求/咨询 | 关于配置mcp的问题 \|\| about configuring mcp |
| [#2877](https://github.com/higress-group/higress/issues/2877) | 2025-09-05 | 功能请求/咨询 | Register MCP Endpoint Back To Nacos |
| [#2874](https://github.com/higress-group/higress/issues/2874) | 2025-09-05 | 功能请求/咨询 | MCP管理要像路由配置一样，支持配置使用各种策略插件 \|\| MCP management should be like routing configuration, and supports configuration and use various policy plug-ins. |
| [#2856](https://github.com/higress-group/higress/issues/2856) | 2025-09-02 | 功能请求/咨询 | 使用nacos+higress 将存量API转换为MCP访问 /mcp/{mcp-server-name}/sse 能正常连接，但是调用tool时有一定几率出现 -32602 Tool not allowed  报错 \|\| Use nacos+higress to convert the existing API to MCP access /mcp/{mcp-server-name}/sse to connect normally, but there is a certain chance of a tool when calling -32602 Tool not allowed Report an error |
| [#2846](https://github.com/higress-group/higress/issues/2846) | 2025-08-31 | 功能请求/咨询 | 请教下，mcp的security认证信息没传到后端呢？ \|\| Please help me, has the mcp security authentication information not been transmitted to the backend? |
| [#2802](https://github.com/higress-group/higress/issues/2802) | 2025-08-21 | 功能请求/咨询 | higress 代理restful api和nacos 服务中转mcp ,迫切希望支持mcp 分组tags 可以归类统一管理mcp \|\| =higress agent restful API and nacos service transfer mcp, and I urgently hope to support mcp grouping tags, which can be classified and managed mcp |
| [#2785](https://github.com/higress-group/higress/issues/2785) | 2025-08-19 | 功能请求/咨询 | OpenAPI-to-MCP后端认证需要支持配置默认认证而不是逐个工具配置认证方式 \|\| OpenAPI-to-MCP backend authentication needs to support configuration of default authentication rather than configuring authentication method by tool. |
| [#2784](https://github.com/higress-group/higress/issues/2784) | 2025-08-19 | 功能请求/咨询 | 在OpenAPI-to-MCP场景下，需要支持透传客户端请求的http header \|\| In OpenAPI-to-MCP scenario, it is necessary to support http header that transmits the request from the client. |
| [#2749](https://github.com/higress-group/higress/issues/2749) | 2025-08-12 | 功能请求/咨询 | higress v2.1.4 nacos registry 同步MCP requestTemplate.security无效 \|\| higress v2.1.4 nacos registry Synchronous MCP requestTemplate.security is invalid |
| [#2747](https://github.com/higress-group/higress/issues/2747) | 2025-08-12 | 功能请求/咨询 | higress mcp插件yaml中，args设置问题 \|\| Higress mcp plugin yaml, args setting problem |
| [#2741](https://github.com/higress-group/higress/issues/2741) | 2025-08-11 | Bug 报告 | bug-python写的mcp-server并且注册到nacos上，higress无法通过nacos发现mcp-server \|\| = Bug-python and registered with nacos. Higress cannot discover mcp-server through nacos |
| [#2738](https://github.com/higress-group/higress/issues/2738) | 2025-08-10 | 功能请求/咨询 | database mcp server for Oracle |
| [#2692](https://github.com/higress-group/higress/issues/2692) | 2025-07-31 | 功能请求/咨询 | 希望访问mcp服务时，支持客户点和服务端弹性伸缩扩容及ip改变也不影响正常访问 \|\| I hope that when accessing mcp services, the elastic scaling and expansion of client points and servers will not affect normal access. |
| [#2642](https://github.com/higress-group/higress/issues/2642) | 2025-07-22 | 功能请求/咨询 | Mcp Server插件配置项优化 \|\| Mcp Server Plug-in Configuration Item Optimization |
| [#2632](https://github.com/higress-group/higress/issues/2632) | 2025-07-21 | 功能请求/咨询 | skyline-monitor-api-service  Error POSTing to endpoint (HTTP 404): {"timestamp":1753084573852,"status":404,"error":"Not Found","path":"/mcp/skyline-monitor-api-service"} |
| [#2606](https://github.com/higress-group/higress/issues/2606) | 2025-07-16 | 功能请求/咨询 | 关于MCP管理，服务类型为DB时，端口不会获取服务来源  ip:port, port始终为80 |
| [#2582](https://github.com/higress-group/higress/issues/2582) | 2025-07-11 | 功能请求/咨询 | MCP管理配置后端服务展示中，没有Port信息，如果有多个port没办法进行区分 \|\| In the display of the MCP management configuration backend service, there is no port information. If there are multiple ports, it is impossible to distinguish them. |
| [#2570](https://github.com/higress-group/higress/issues/2570) | 2025-07-10 | 功能请求/咨询 | nacos3中添加了mcp配置，改完配置后到生效的时间较慢 \|\| The mcp configuration has been added to nacos3. The time it takes to take effect after the configuration is changed is slower. |
| [#2556](https://github.com/higress-group/higress/issues/2556) | 2025-07-08 | 功能请求/咨询 | Doris MCP Support |
| [#2549](https://github.com/higress-group/higress/issues/2549) | 2025-07-07 | 功能请求/咨询 | MCP实例太多导致wasmplugin CR过大，报错：etcdserver: request is too large \|\| Too many MCP instances cause wasmplugin CR to be too large, and an error is reported: etcdserver: request is too large |
| [#2540](https://github.com/higress-group/higress/issues/2540) | 2025-07-03 | 功能请求/咨询 | MCP透传认证问题 |
| [#2539](https://github.com/higress-group/higress/issues/2539) | 2025-07-03 | 功能请求/咨询 | 2.1.5 MCP管理 编辑后提交失败 \|\| 2.1.5 MCP Management Submission failed after editing |
| [#2512](https://github.com/higress-group/higress/issues/2512) | 2025-06-27 | 功能请求/咨询 | Higress调用nacos托管MCP后端报错，报“no route match for URL” \|  Higress encountered an error when invoking the MCP backend managed by Nacos, reporting "no route match for URL". |
| [#2481](https://github.com/higress-group/higress/issues/2481) | 2025-06-22 | Bug 报告 | 开启mcpServer会导致websocket连接后无法发送消息并30秒后自动断开连接 \|\| Opening mcpServer will cause the websocket to fail to send messages after connection and will automatically disconnect after 30 seconds. |
| [#2467](https://github.com/higress-group/higress/issues/2467) | 2025-06-19 | 功能请求/咨询 | Does the [Key Authentication] Plugin for Higress support controlling MCP requests to Nacos StreamableHTTP? |
| [#2465](https://github.com/higress-group/higress/issues/2465) | 2025-06-19 | 功能请求/咨询 | [Feature]希望mcp-server插件使用文档中使用示例更丰富一些 \|\| [Feature] I hope the usage examples in the mcp-server plug-in usage documentation are more abundant |
| [#2454](https://github.com/higress-group/higress/issues/2454) | 2025-06-18 | 功能请求/咨询 | [Feature&Question] higress mcp 能否支持配置全局参数 \|\| [Feature&Question] hues mcp can support configuring global parameters |
| [#2453](https://github.com/higress-group/higress/issues/2453) | 2025-06-18 | 功能请求/咨询 | mcp server tool级别权限管控 \|\| =mcp server tool level permission control |
| [#2436](https://github.com/higress-group/higress/issues/2436) | 2025-06-17 | 功能请求/咨询 | 在服务来源配置Nacos 3.x ，报错，controller日志报错：List mcp server configs for page size 1, page number 50 null %!v(MISSING) \|\| Configure Nacos 3.x in the service source, report an error, controller log error: List mcp server configs for page size 1, page number 50 null %!v(MISSING) |
| [#2416](https://github.com/higress-group/higress/issues/2416) | 2025-06-14 | 功能请求/咨询 | higress2.13 nacos3.0.0 配置带参数的MCP get请求，参数带不上 \|\| higress2.13 nacos3.0.0 configures MCP get request with parameters, but the parameters cannot be brought with them. |
| [#2370](https://github.com/higress-group/higress/issues/2370) | 2025-06-04 | 功能请求/咨询 | higress创建数据来源，选择nacos3类型 mcp服务，创建后服务列表无对应服务 \|\| higress creates data source, select the Nacos3 type mcp service, and there is no corresponding service in the service list after creation. |
| [#2367](https://github.com/higress-group/higress/issues/2367) | 2025-06-04 | 功能请求/咨询 | 提供可以调用dubbo服务的MCP Server \|\| Provides MCP Server that can call dubbo services |

### 通用插件（非 AI）（54）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5269](https://github.com/higress-group/higress/issues/5269) | 2026-10-27 | 功能请求/咨询 | [Question] frontend-gray: should localStorageGrayKey initialize a missing cookie? |
| [#5268](https://github.com/higress-group/higress/issues/5268) | 2026-10-27 | Bug 报告 | [BUG] frontend-gray: rewrite.host bypasses skippedByHeaders for non-HTML requests |
| [#5267](https://github.com/higress-group/higress/issues/5267) | 2026-10-27 | issue-spec (Proposal/Design) | Design: Honor documented frontend-gray storeMaxAge |
| [#5266](https://github.com/higress-group/higress/issues/5266) | 2026-10-27 | issue-spec (Proposal/Design) | Proposal: Honor documented frontend-gray storeMaxAge |
| [#5247](https://github.com/higress-group/higress/issues/5247) | 2026-10-23 | 功能请求/咨询 | [Bug investigation] 2.2.4 批量更新路由和插件时 controller CPU 升高，gateway 配置延迟生效 |
| [#5207](https://github.com/higress-group/higress/issues/5207) | 2026-10-20 | Bug 报告 | bug: OPA plugin can leave a request paused when DispatchHttpCall fails synchronously |
| [#5202](https://github.com/higress-group/higress/issues/5202) | 2026-10-20 | issue-spec (Proposal/Design) | Design: api-workflow-join-sibling-dispatch |
| [#5200](https://github.com/higress-group/higress/issues/5200) | 2026-10-20 | issue-spec (Proposal/Design) | Proposal: api-workflow-join-sibling-dispatch |
| [#5189](https://github.com/higress-group/higress/issues/5189) | 2026-10-20 | 功能请求/咨询 | api-workflow: waiting for a join skips sibling branches and stalls valid DAGs |
| [#5164](https://github.com/higress-group/higress/issues/5164) | 2026-10-19 | issue-spec (Proposal/Design) | Design: log-request-response: response status code logging condition |
| [#5163](https://github.com/higress-group/higress/issues/5163) | 2026-10-19 | issue-spec (Proposal/Design) | Proposal: log-request-response: add response status code condition for logging |
| [#5132](https://github.com/higress-group/higress/issues/5132) | 2026-10-18 | issue-spec (Proposal/Design) | Design: repair the request-block local-build walkthrough |
| [#5131](https://github.com/higress-group/higress/issues/5131) | 2026-10-18 | issue-spec (Proposal/Design) | Proposal: repair the request-block local-build walkthrough |
| [#5113](https://github.com/higress-group/higress/issues/5113) | 2026-10-16 | issue-spec (Proposal/Design) | Proposal: geo-ip-strip-client-supplied-geo-headers |
| [#5101](https://github.com/higress-group/higress/issues/5101) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: request-validation-validate-non-object-bodies |
| [#5100](https://github.com/higress-group/higress/issues/5100) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: de-graphql-validate-variable-types |
| [#5099](https://github.com/higress-group/higress/issues/5099) | 2026-10-15 | issue-spec (Proposal/Design) | Proposal: log-request-response-publish-head-once |
| [#4994](https://github.com/higress-group/higress/issues/4994) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: stop logging full request bodies at Info in request-block ([#4993](https://github.com/higress-group/higress/issues/4993)) |
| [#4979](https://github.com/higress-group/higress/issues/4979) | 2026-10-04 | 功能请求/咨询 | jsonrpc-converter: truncateString cuts UTF-8 runes in half — invalid UTF-8 forwarded in x-envoy-* headers |
| [#4977](https://github.com/higress-group/higress/issues/4977) | 2026-10-04 | 功能请求/咨询 | log-request-response: streamed bodies larger than maxSize log the tail, overwriting the head |
| [#4975](https://github.com/higress-group/higress/issues/4975) | 2026-10-04 | 功能请求/咨询 | de-graphql: non-String GraphQL variables are concatenated raw — JSON injection and invalid JSON in the upstream body |
| [#4974](https://github.com/higress-group/higress/issues/4974) | 2026-10-04 | 功能请求/咨询 | request-validation: object body schema is bypassed by valid-JSON non-object bodies (array/string/number) |
| [#4956](https://github.com/higress-group/higress/issues/4956) | 2026-10-03 | issue-spec (Proposal/Design) | Proposal: preserve response metadata when gw-error-format body matching fails ([#4851](https://github.com/higress-group/higress/issues/4851)) |
| [#4851](https://github.com/higress-group/higress/issues/4851) | 2026-09-29 | Bug 报告 | Bug: gw-error-format rewrites status and headers before response-body match |
| [#4825](https://github.com/higress-group/higress/issues/4825) | 2026-09-28 | Bug 报告 | response-cache naked type assertion can panic on non-string context value |
| [#4779](https://github.com/higress-group/higress/issues/4779) | 2026-09-27 | 文档 | docs(frontend-gray): CN README documents injection.body field as "after" but code reads "last" |
| [#4672](https://github.com/higress-group/higress/issues/4672) | 2026-09-09 | issue-spec (Proposal/Design) | Design: Restore cached upstream status on response-cache hits |
| [#4670](https://github.com/higress-group/higress/issues/4670) | 2026-09-09 | issue-spec (Proposal/Design) | Proposal: Restore the cached upstream status code on response-cache hits |
| [#4664](https://github.com/higress-group/higress/issues/4664) | 2026-09-09 | 功能请求/咨询 | 使用qwen3guard插件 针对输入请求做检测的时候 当被拦截后 返回自定义内容的时候 在dify这种平台里面 看不到自定义内容，从工作流里面看是 空值 的问题以及解决方案呢？这个是否是因为非流式输出和流式输出导致的？ \|\| Use the qwen3guard plug-in to detect input requests and return custom content after being intercepted. In a platform likedify I can’t see the custom content, but it looks like a null value in the workflow, and what’s the solution? Is this caused by non-streaming output and streaming output? |
| [#4634](https://github.com/higress-group/higress/issues/4634) | 2026-09-02 | issue-spec (Proposal/Design) | Proposal: Harden the managed plugin release pipeline (layout unification, migration preflight, approval simplification) |
| [#4601](https://github.com/higress-group/higress/issues/4601) | 2026-08-26 | 功能请求/咨询 | replay-protection 插件对带请求体（POST）的请求存在重放漏放风险 |
| [#4556](https://github.com/higress-group/higress/issues/4556) | 2026-08-16 | issue-spec (Proposal/Design) | Proposal: 统一插件 Manifest 与校验器 |
| [#4447](https://github.com/higress-group/higress/issues/4447) | 2026-08-12 | issue-spec (Proposal/Design) | Proposal: Let api-workflow start without a body and consume path/query inputs |
| [#4392](https://github.com/higress-group/higress/issues/4392) | 2026-08-10 | 功能请求/咨询 | [response-cache] Cached non-200 responses are replayed as HTTP 200 |
| [#4360](https://github.com/higress-group/higress/issues/4360) | 2026-08-08 | 功能请求/咨询 | [replay-protection] Invalid nonce and Redis ranges are accepted |
| [#4358](https://github.com/higress-group/higress/issues/4358) | 2026-08-08 | 功能请求/咨询 | [response-cache] Invalid Redis timeout and port settings are accepted |
| [#4356](https://github.com/higress-group/higress/issues/4356) | 2026-08-08 | 功能请求/咨询 | [api-workflow] Callback response headers contain empty entries |
| [#4350](https://github.com/higress-group/higress/issues/4350) | 2026-08-08 | Bug 报告 | [bug] transformer plugin panics on bare type assertions when headers/querys context is nil |
| [#4341](https://github.com/higress-group/higress/issues/4341) | 2026-08-08 | 功能请求/咨询 | cache-control accepts invalid and overflowing expires values |
| [#4180](https://github.com/higress-group/higress/issues/4180) | 2026-07-22 | 功能请求/咨询 | 2.1.11版本没有插件配置 2.2.x版本占用配置过高 \|\| The 2.1.11 version has no plug-in configuration. The 2.2.x version occupies too high a configuration. |
| [#4035](https://github.com/higress-group/higress/issues/4035) | 2026-06-30 | 功能请求/咨询 | CORS plugin issue [#1743](https://github.com/higress-group/higress/issues/1743) implementation coordination |
| [#3993](https://github.com/higress-group/higress/issues/3993) | 2026-06-18 | 功能请求/咨询 | 插件缓存如何配置 \|\| How to configure the plug-in cache |
| [#3889](https://github.com/higress-group/higress/issues/3889) | 2026-05-27 | 功能请求/咨询 | 意图识别插件 \|\| Intent recognition plug-in |
| [#3824](https://github.com/higress-group/higress/issues/3824) | 2026-05-14 | 功能请求/咨询 | 2.1.11版本在未使用插件情况下经常出现敏感词屏蔽情况 \|\| Version 2.1.11 often blocks sensitive words without using plug-ins. |
| [#3635](https://github.com/higress-group/higress/issues/3635) | 2026-03-23 | 功能请求/咨询 | 希望插件页面增加使用说明，插件市场能够开放第三方插件 \|\| I hope that the plug-in page will add usage instructions and the plug-in market will open third-party plug-ins. |
| [#3629](https://github.com/higress-group/higress/issues/3629) | 2026-03-20 | 功能请求/咨询 | db-log-pusher插件代码为什么没有合并呢？ |
| [#3537](https://github.com/higress-group/higress/issues/3537) | 2026-02-27 | 功能请求/咨询 | OPA plugin returns bad argument |
| [#3464](https://github.com/higress-group/higress/issues/3464) | 2026-02-09 | 功能请求/咨询 | 有没有插件支持higress-gateway的日志直接输出到sls \|\| Is there any plug-in that supports higress-gateway's logs being output directly to sls? |
| [#3382](https://github.com/higress-group/higress/issues/3382) | 2026-01-22 | 功能请求/咨询 | 优化插件使用secret占位逻辑 \|\| Optimize plug-in to use secret placeholder logic |
| [#3333](https://github.com/higress-group/higress/issues/3333) | 2026-01-15 | 功能请求/咨询 | Feature Request: Support reusable plugin configurations and config sets with flexible order |
| [#3009](https://github.com/higress-group/higress/issues/3009) | 2025-10-15 | 功能请求/咨询 | Higress AI配额管理插件问题 |
| [#2936](https://github.com/higress-group/higress/issues/2936) | 2025-09-18 | 功能请求/咨询 | 插件ai配额为啥请求一次配额数减少了20次 \|\| Why is the number of requested quotas for plug-in ai quota reduced by 20 times |
| [#2840](https://github.com/higress-group/higress/issues/2840) | 2025-08-29 | 功能请求/咨询 | ai插件支持 OpenTelemetry 链路追踪头传播 \|\| =ai plug-in supports OpenTelemetry link tracking header propagation |
| [#2634](https://github.com/higress-group/higress/issues/2634) | 2025-07-21 | 功能请求/咨询 | 如何在插件的parseConfig中发送异步请求获取外部配置进行加载？ \|\| How to send an asynchronous request in the parseConfig of the plugin to get external configuration for loading? |

### 核心网关（控制面/数据面）（44）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5222](https://github.com/higress-group/higress/issues/5222) | 2026-10-22 | issue-spec (Proposal/Design) | [Design] Fix translate workflow short SHA pin |
| [#5221](https://github.com/higress-group/higress/issues/5221) | 2026-10-22 | issue-spec (Proposal/Design) | [Proposal] Fix translate workflow short SHA pin |
| [#5094](https://github.com/higress-group/higress/issues/5094) | 2026-10-15 | 功能请求/咨询 | Higress普通路由做一个简单的http请求，有如下问题，请给看看 \|\| Higress ordinary routing makes a simple http request. If you have the following questions, please take a look. |
| [#5053](https://github.com/higress-group/higress/issues/5053) | 2026-10-10 | 功能请求/咨询 | 413 Payload Too Large 精确卡在 262144 字节：请求两次经过 Envoy 过滤链时触发 （别名域名 → rewrite.host → 绕回同一网关） |
| [#5045](https://github.com/higress-group/higress/issues/5045) | 2026-10-08 | issue-spec (Proposal/Design) | Design: support watching multiple ingressClasses (Proposal [#5044](https://github.com/higress-group/higress/issues/5044)) |
| [#5044](https://github.com/higress-group/higress/issues/5044) | 2026-10-08 | issue-spec (Proposal/Design) | Proposal: support watching multiple ingressClasses |
| [#4997](https://github.com/higress-group/higress/issues/4997) | 2026-10-05 | 功能请求/咨询 | [跟进 [#2920](https://github.com/higress-group/higress/issues/2920)] 多副本 controller 生成的 listener 字节不一致导致反复 in-place 更新并强杀长连接 \|\| Follow-up to [#2920](https://github.com/higress-group/higress/issues/2920): byte-different listeners across controller replicas cause repeated in-place updates and killed long-lived connections |
| [#4986](https://github.com/higress-group/higress/issues/4986) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: truncate x-envoy-* header values on rune boundaries ([#4979](https://github.com/higress-group/higress/issues/4979)) |
| [#4849](https://github.com/higress-group/higress/issues/4849) | 2026-09-29 | 功能请求/咨询 | Canary routes lose adjacency with their base when a Prefix / catch-all route coexists with other path types |
| [#4772](https://github.com/higress-group/higress/issues/4772) | 2026-09-26 | Bug 报告 | Bug: rejected Gateway listeners incorrectly report Programmed=True |
| [#4631](https://github.com/higress-group/higress/issues/4631) | 2026-09-02 | 功能请求/咨询 | 对接gateway httproute状态异常，但配置其实已经下发成功 |
| [#4594](https://github.com/higress-group/higress/issues/4594) | 2026-08-25 | Bug 报告 | AI负载均衡策略无法把请求转到路径不是以/v1开头的上游服务 |
| [#4519](https://github.com/higress-group/higress/issues/4519) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: 修复 HTTPRoute 单规则多 InferencePool backendRefs 的 endpoint-picker 配置覆盖 \|\| Proposal: Prevent endpoint-picker config overwrite for multiple InferencePool backendRefs in one HTTPRoute rule |
| [#4425](https://github.com/higress-group/higress/issues/4425) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Preserve same-named ListenerSet outputs across namespaces |
| [#4409](https://github.com/higress-group/higress/issues/4409) | 2026-08-10 | Bug 报告 | Data race and connection pool leak in gorm DBClient crashes Envoy worker |
| [#4321](https://github.com/higress-group/higress/issues/4321) | 2026-08-08 | issue-spec (Proposal/Design) | Design: Higress Sandbox Gateway control plane, routing, and provider adapters \|\| Higress Sandbox Gateway 控制面、路由与 Provider Adapter 设计 |
| [#3930](https://github.com/higress-group/higress/issues/3930) | 2026-06-05 | Bug 报告 | The first fallback, doubao-seed-1-8, succeeded 22 times (returned 200) but also failed 24 times (returned 429). When it also returns 429, Envoy's max_internal_redirects defaults to 1, which does not allow |
| [#3913](https://github.com/higress-group/higress/issues/3913) | 2026-06-04 | 功能请求/咨询 | HIgress是否能支持Nginx-ingress的SSI特性 \|\| Can HIgress support the SSI feature of Nginx-ingress? |
| [#3900](https://github.com/higress-group/higress/issues/3900) | 2026-06-01 | 功能请求/咨询 | httproute代理多个服务时是否有健康检查机制 \|\| Does httproute have a health check mechanism when proxying multiple services? |
| [#3751](https://github.com/higress-group/higress/issues/3751) | 2026-04-24 | Bug 报告 | 【bug】higress 中包含特殊符号复杂的header 值这是无效；且有复杂值，重启gateway 后 直接无法匹配路由 \|\| [bug] higress contains special symbols and complex header values, which is invalid; and there are complex values. After restarting the gateway, the route cannot be matched directly. |
| [#3628](https://github.com/higress-group/higress/issues/3628) | 2026-03-20 | 功能请求/咨询 | higress gateway pod中的istio worker的cpu使用为什么不能自动伸缩？ |
| [#3617](https://github.com/higress-group/higress/issues/3617) | 2026-03-18 | Bug 报告 | upstream-hash-by does not take effect in Higress 2.2.0, final Envoy cluster still uses LEAST_REQUEST |
| [#3616](https://github.com/higress-group/higress/issues/3616) | 2026-03-18 | 功能请求/咨询 | 在路由里配置的路径 包含 ** 时，整个Higress不可用了 所有请求都是404 路由配置blackhole了 \|\| When the path configured in the routing contains **, the entire Higress is unavailable. All requests are 404. The routing configuration is blackhole. |
| [#3452](https://github.com/higress-group/higress/issues/3452) | 2026-02-04 | Bug 报告 | 一致性 Hash、Cookie 亲和不生效，配置未下发到 Envoy(V2.1.9) \|\| Consistency Hash and Cookie affinity do not take effect, and the configuration is not sent to Envoy (V2.1.9) |
| [#3299](https://github.com/higress-group/higress/issues/3299) | 2026-01-06 | 功能请求/咨询 | How can I set the request body size for a specific route in Higress, such as a route used for file uploads? |
| [#3269](https://github.com/higress-group/higress/issues/3269) | 2025-12-26 | 功能请求/咨询 | Higress的gateway，在AI侧是否也有像Ingress一样能力的会话保持功能 |
| [#3245](https://github.com/higress-group/higress/issues/3245) | 2025-12-22 | 功能请求/咨询 | 在路由配置的页面增加筛选功能 \|\| Add filtering function to routing configuration page |
| [#3219](https://github.com/higress-group/higress/issues/3219) | 2025-12-13 | Bug 报告 | 多 API-Key 负载均衡导致异步视频模型关联接口调用失败 \|\| Multiple API-Key load balancing causes asynchronous video model associated interface call to fail |
| [#3183](https://github.com/higress-group/higress/issues/3183) | 2025-12-03 | 功能请求/咨询 | 海量路由加载时间较长 \|\| It takes a long time to load massive routes |
| [#3180](https://github.com/higress-group/higress/issues/3180) | 2025-11-29 | 功能请求/咨询 | higress envoy filters.http.geoip不能使用 |
| [#3170](https://github.com/higress-group/higress/issues/3170) | 2025-11-26 | 功能请求/咨询 | 可以为envoy_cluster_采集指标增加自定义参数功能吗 \|\| Can you add custom parameters to envoy_cluster_collection indicators? |
| [#3157](https://github.com/higress-group/higress/issues/3157) | 2025-11-20 | 功能请求/咨询 | ingressClass 参数是否可以支持指定多个ingressclass \|\| ingressClass Whether the parameter can support specifying multiple ingressclasses |
| [#3117](https://github.com/higress-group/higress/issues/3117) | 2025-11-12 | 功能请求/咨询 | 如何将http请求header中的api_key作为标签添加到envoy_xxx(如：envoy_http_downstream_rq)指标中 \|\| How to add the api_key in the http request header as a label to the envoy_xxx (such as: envoy_http_downstream_rq) indicator |
| [#3068](https://github.com/higress-group/higress/issues/3068) | 2025-10-28 | 功能请求/咨询 | 2.1.3版本higress-gateway的envoy进程持续增长触发pod oom |
| [#2972](https://github.com/higress-group/higress/issues/2972) | 2025-09-30 | 功能请求/咨询 | higress-controller 2.0.2频繁空指针重启 \|\| higress-controller 2.0.2 Frequent null pointer restart |
| [#2946](https://github.com/higress-group/higress/issues/2946) | 2025-09-23 | 功能请求/咨询 | 【开放原子大赛】智能路由方向数据集使用说明 \|\| [Open Atomic Competition] Instructions for using intelligent routing direction dataset |
| [#2878](https://github.com/higress-group/higress/issues/2878) | 2025-09-05 | 功能请求/咨询 | 是否可以支持路由下线的功能 \|\| Is it possible to support the function of offline routing? |
| [#2845](https://github.com/higress-group/higress/issues/2845) | 2025-08-31 | 功能请求/咨询 | 开启envoy cache filter后一段时间，cpu使用率跑满 |
| [#2603](https://github.com/higress-group/higress/issues/2603) | 2025-07-16 | 功能请求/咨询 | 如何调整controller的日志等级 \|\| How to adjust the log level of the controller |
| [#2505](https://github.com/higress-group/higress/issues/2505) | 2025-06-26 | 功能请求/咨询 | 支持模型负载均衡与故障转移 \|\| Support model load balancing and failover |
| [#2490](https://github.com/higress-group/higress/issues/2490) | 2025-06-24 | Bug 报告 | 模型路由转发会带上请求头transfer-encoding:chunked，如果模型不支持会导致报错 \|\| Model routing forwarding will bring the request header transfer-encoding:chunked. If the model does not support it, it will cause an error. |
| [#2468](https://github.com/higress-group/higress/issues/2468) | 2025-06-19 | 功能请求/咨询 | 一条路由代理多个固定地址的服务，如何设置健康检查和故障转移？ \|\| A single route proxy service with multiple fixed addresses. How to set up health checks and failover? |
| [#2386](https://github.com/higress-group/higress/issues/2386) | 2025-06-10 | 功能请求/咨询 | nginx ingress 默认监听了 80 和 443 端口，ingress 全局配置 force-ssl-redirect，将http 重定向到 https。higress 是否有相关配置 |
| [#2357](https://github.com/higress-group/higress/issues/2357) | 2025-05-31 | 功能请求/咨询 | 如何监控higress配置的路由对应的后端服务是否正常？ \|\| How to monitor whether the backend service corresponding to the route configured by higress is normal? |

### 安全/认证/流量治理插件（67）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5298](https://github.com/higress-group/higress/issues/5298) | 2026-11-04 | 安全/缺陷披露 | Security: Higress v2.2.5 Gateway still ships Envoy 1.36.10, which is affected by CVE-2026-111497 |
| [#5274](https://github.com/higress-group/higress/issues/5274) | 2026-10-28 | 功能请求/咨询 | OIDC: requests with a body may reach upstream without X-Forwarded-Access-Token during session refresh |
| [#5119](https://github.com/higress-group/higress/issues/5119) | 2026-10-16 | 功能请求/咨询 | Higress 请求带有认证的后端服务接口，是否有相应方案？ \|\| Higress requests a backend service interface with authentication. Is there a corresponding solution? |
| [#4993](https://github.com/higress-group/higress/issues/4993) | 2026-10-04 | 功能请求/咨询 | request-block: entire request body is logged at Info level on every request (leftover demo code in a security plugin) |
| [#4992](https://github.com/higress-group/higress/issues/4992) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: delete only the exactly-named token cookie in jwt-auth ([#4991](https://github.com/higress-group/higress/issues/4991)) |
| [#4991](https://github.com/higress-group/higress/issues/4991) | 2026-10-04 | Bug 报告 | jwt-auth: deleteCookie drops every cookie whose name starts with the token cookie name |
| [#4990](https://github.com/higress-group/higress/issues/4990) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: authenticate every configured basic-auth consumer and allow colon passwords ([#4989](https://github.com/higress-group/higress/issues/4989)) |
| [#4989](https://github.com/higress-group/higress/issues/4989) | 2026-10-04 | Bug 报告 | basic-auth: duplicate usernames silently last-consumer-wins — a configured consumer's valid credential gets 401; passwords containing ":" cannot be configured (RFC 7617) |
| [#4820](https://github.com/higress-group/higress/issues/4820) | 2026-09-28 | Bug 报告 | ext-auth header iteration can panic on malformed entries |
| [#4771](https://github.com/higress-group/higress/issues/4771) | 2026-09-25 | issue-spec (Proposal/Design) | Proposal: expose WAF transaction and interruption metrics |
| [#4693](https://github.com/higress-group/higress/issues/4693) | 2026-09-12 | issue-spec (Proposal/Design) | Design: workload-identity-auth-for-bedrock-and-vertex |
| [#4692](https://github.com/higress-group/higress/issues/4692) | 2026-09-12 | issue-spec (Proposal/Design) | Design: ingress-scoped-letsencrypt-certificates |
| [#4691](https://github.com/higress-group/higress/issues/4691) | 2026-09-12 | issue-spec (Proposal/Design) | Proposal: workload-identity-auth-for-bedrock-and-vertex |
| [#4690](https://github.com/higress-group/higress/issues/4690) | 2026-09-12 | issue-spec (Proposal/Design) | Proposal: ingress-scoped-letsencrypt-certificates |
| [#4677](https://github.com/higress-group/higress/issues/4677) | 2026-09-10 | 功能请求/咨询 | Implement: ext-auth: cache auth results, decide allow/deny from response content, and forward response fields upstream |
| [#4676](https://github.com/higress-group/higress/issues/4676) | 2026-09-10 | issue-spec (Proposal/Design) | Design: ext-auth: cache auth results, decide allow/deny from response content, and forward response fields upstream |
| [#4675](https://github.com/higress-group/higress/issues/4675) | 2026-09-10 | issue-spec (Proposal/Design) | Proposal: ext-auth: cache auth results, decide allow/deny from response content, and forward response fields upstream |
| [#4647](https://github.com/higress-group/higress/issues/4647) | 2026-09-05 | issue-spec (Proposal/Design) | Design: distinguish synchronous continuation from asynchronous resume in ext-auth |
| [#4646](https://github.com/higress-group/higress/issues/4646) | 2026-09-05 | issue-spec (Proposal/Design) | Proposal: prevent ext-auth duplicate forwarding on synchronous fail-open errors |
| [#4633](https://github.com/higress-group/higress/issues/4633) | 2026-09-02 | 功能请求/咨询 | 同一个 443 端口，域名 A (TLSRoute‑Passthrough 四层透传) + 域名 B (Ingress‑HTTPS 网关解密终止 TLS) 如何共存 |
| [#4527](https://github.com/higress-group/higress/issues/4527) | 2026-08-14 | issue-spec (Proposal/Design) | Design: fail fast during certificate server initialization |
| [#4526](https://github.com/higress-group/higress/issues/4526) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: propagate certificate server initialization errors |
| [#4355](https://github.com/higress-group/higress/issues/4355) | 2026-08-08 | 功能请求/咨询 | [basic-auth] Earlier credential is rejected when consumers share a username |
| [#4251](https://github.com/higress-group/higress/issues/4251) | 2026-08-03 | issue-spec (Proposal/Design) | Implement: optimize ratelimit-plugin config UX, docs, and dev notes |
| [#4221](https://github.com/higress-group/higress/issues/4221) | 2026-07-28 | Bug 报告 | server.passthroughAuthHeader 配置不生效 \|\| server.passthroughAuthHeader configuration does not take effect |
| [#4203](https://github.com/higress-group/higress/issues/4203) | 2026-07-24 | Bug 报告 | Gateway fails cold start: ssl-passthrough Ingress generates TLS context without certificate |
| [#4172](https://github.com/higress-group/higress/issues/4172) | 2026-07-20 | 功能请求/咨询 | ext-auth认证失败，返回403 bad argument \|\| ext-auth authentication failed, returning 403 bad argument |
| [#4159](https://github.com/higress-group/higress/issues/4159) | 2026-07-17 | 功能请求/咨询 | 官方文档中增加消费者认证访问 \|\| Add consumer authentication access in the official document |
| [#4134](https://github.com/higress-group/higress/issues/4134) | 2026-07-13 | 功能请求/咨询 | [Feature] 网关支持根据安全检测结果自动将流量路由到不同模型 \|\| [Feature] The gateway supports automatically routing traffic to different models based on security detection results |
| [#4049](https://github.com/higress-group/higress/issues/4049) | 2026-07-03 | 功能请求/咨询 | 域名配置+请求认证返回404 \|\| Domain name configuration + request authentication returns 404 |
| [#3941](https://github.com/higress-group/higress/issues/3941) | 2026-06-09 | Bug 报告 | bug: OIDC plugin ignores skip_oidc_discovery=true, always attempts discovery http_call first |
| [#3908](https://github.com/higress-group/higress/issues/3908) | 2026-06-03 | Bug 报告 | [Bug] cluster-key-rate-limit 插件偶尔出现 redis 连接及解析报错 \|\| [Bug] The cluster-key-rate-limit plug-in occasionally displays redis connection and parsing errors. |
| [#3884](https://github.com/higress-group/higress/issues/3884) | 2026-05-27 | 功能请求/咨询 | 基于key的本地限流插件 测试 限流和配置不符合 \|\| Key-based local current limiting plug-in test current limiting and configuration do not match |
| [#3850](https://github.com/higress-group/higress/issues/3850) | 2026-05-20 | Bug 报告 | [Bug] HTTP/3 (QUIC) requests return 403 when using go-waf-plugin, while HTTP/1.1 works normally |
| [#3744](https://github.com/higress-group/higress/issues/3744) | 2026-04-23 | Bug 报告 | [BUG] 关于前端灰度(frontend-gray)插件的一些问题 \|\| [BUG] Some issues about the frontend-gray plug-in |
| [#3709](https://github.com/higress-group/higress/issues/3709) | 2026-04-14 | 功能请求/咨询 | 2.2.1：SSL routines:OPENSSL_internal:CERTIFICATE_VERIFY_FAILED:TLS_error_end \|\| 2.2.1: SSL routines:OPENSSL_internal:CERTIFICATE_VERIFY_FAILED:TLS_error_end |
| [#3661](https://github.com/higress-group/higress/issues/3661) | 2026-03-31 | Bug 报告 | 把这个WAF插件打开后，Gateway的pod重启一直失败，关闭WAF插件后才能启动成功 \|\| After turning on this WAF plug-in, Gateway's pod restart fails. It can only be started successfully after turning off the WAF plug-in. |
| [#3619](https://github.com/higress-group/higress/issues/3619) | 2026-03-18 | Bug 报告 | X-HI-ORIGINAL-AUTH header is send to provider，there is security threat |
| [#3593](https://github.com/higress-group/higress/issues/3593) | 2026-03-14 | 功能请求/咨询 | 消费者管理是否能够增加一个分组功能，然后路由里可以按组授权 \|\| Can consumer management add a grouping function, and then the routing can be authorized by group? |
| [#3560](https://github.com/higress-group/higress/issues/3560) | 2026-03-04 | Bug 报告 | Redis错误: NOAUTH Authentication required. \|\| Redis error: NOAUTH Authentication required. |
| [#3419](https://github.com/higress-group/higress/issues/3419) | 2026-01-31 | Bug 报告 | key-auth插件运行一段时间后偶尔失效 \|\| key-auth plug-in occasionally fails after running for a period of time |
| [#3309](https://github.com/higress-group/higress/issues/3309) | 2026-01-08 | 功能请求/咨询 | Plan and timeline for JWT / OAuth2 authentication support |
| [#3227](https://github.com/higress-group/higress/issues/3227) | 2025-12-18 | 功能请求/咨询 | 提高higress全局限流的可靠性与性能 \|\| Improve the reliability and performance of higress full flow limiting |
| [#3215](https://github.com/higress-group/higress/issues/3215) | 2025-12-12 | 功能请求/咨询 | 使用redis进行全局限流时redis连接池可配置 \|\| The redis connection pool can be configured when using redis for global flow restriction. |
| [#3111](https://github.com/higress-group/higress/issues/3111) | 2025-11-11 | 功能请求/咨询 | 使用key-auth插件，在路由中配置上较多消费者时，会出现CPU内存大幅上涨，甚至导致gateway出现OOM |
| [#3103](https://github.com/higress-group/higress/issues/3103) | 2025-11-07 | 功能请求/咨询 | 使用自签证书功能，higress创建的80接口对应的证书应答会被对应域名的路由拦击，优先级不是最高 \|\| Using the self-signed certificate function, the certificate response corresponding to the 80 interface created by higress will be blocked by the route of the corresponding domain name, and the priority is not the highest |
| [#3102](https://github.com/higress-group/higress/issues/3102) | 2025-11-07 | 功能请求/咨询 | 开启WAF 插件后，正常识别工具，但是监控没有相关的WAF指标数据 \|\| After turning on the WAF plug-in, the tool is recognized normally, but there is no relevant WAF indicator data for monitoring. |
| [#3053](https://github.com/higress-group/higress/issues/3053) | 2025-10-27 | Bug 报告 | 启用基于key集群限流，redis密码配置错误时，会导致higress响应慢 \|\| Enable key-based cluster current limiting, and when the redis password is configured incorrectly, higress will respond slowly. |
| [#2994](https://github.com/higress-group/higress/issues/2994) | 2025-10-11 | 功能请求/咨询 | higress基于key集群限流判断优化 \|\| higress is optimized based on key cluster current limiting judgment |
| [#2993](https://github.com/higress-group/higress/issues/2993) | 2025-10-11 | 功能请求/咨询 | waf插件能否默认提供一些常用的OWASP CRS规则 \|\| Can the waf plug-in provide some commonly used OWASP CRS rules by default? |
| [#2974](https://github.com/higress-group/higress/issues/2974) | 2025-09-30 | 功能请求/咨询 | higress基于key集群限流模块redis连接问题 |
| [#2963](https://github.com/higress-group/higress/issues/2963) | 2025-09-26 | 功能请求/咨询 | higress配置"基于key集群限流"报错问题 \|\| =Higress configuration "current limit based on key cluster" error problem |
| [#2944](https://github.com/higress-group/higress/issues/2944) | 2025-09-23 | 功能请求/咨询 | OIDC 插件使用 cookie_secret 加密身份令牌导致 _oauth_proxy Cookie 过大 \|\| OIDC plugin uses cookie_secret to encrypt the identity token, causing the _oauth_proxy cookie to be too large |
| [#2901](https://github.com/higress-group/higress/issues/2901) | 2025-09-10 | 功能请求/咨询 | go ext-auth with custom message |
| [#2834](https://github.com/higress-group/higress/issues/2834) | 2025-08-28 | 功能请求/咨询 | higress开启Coraza waf后性能衰退很大，QPS只有之前的5% \|\| Higress After turning on Coraza waf, the performance declined greatly, and the QPS was only 5% of the previous ones. |
| [#2742](https://github.com/higress-group/higress/issues/2742) | 2025-08-11 | 功能请求/咨询 | higress是否支持国密tls通信 \|\| Does Higress support national secret tls communication |
| [#2728](https://github.com/higress-group/higress/issues/2728) | 2025-08-07 | Bug 报告 | ingress里超过3级的域名，cert-manager获取ssl证书后，会遇到higress-gateway不实时更新ssl证书的问题 \|\| Domain names in iningress that exceed level 3, after cert-manager obtains the ssl certificate, it will encounter the problem that higress-gateway does not update the ssl certificate in real time. |
| [#2720](https://github.com/higress-group/higress/issues/2720) | 2025-08-06 | Bug 报告 | 集群限流插件不支持grpc请求配置status code \|\| The cluster current limit plug-in does not support grpc request configuration status code |
| [#2643](https://github.com/higress-group/higress/issues/2643) | 2025-07-22 | 功能请求/咨询 | ext-auth认证报错 |
| [#2629](https://github.com/higress-group/higress/issues/2629) | 2025-07-21 | 功能请求/咨询 | 基于cluster-key-rate-limit修改lua脚本实现滑动时间窗口 \|\| Modify the lua script based on cluster-key-rate-limit to implement the sliding time window |
| [#2530](https://github.com/higress-group/higress/issues/2530) | 2025-07-01 | 功能请求/咨询 | 是否可以支持自定义端口开启 ssl，并配置自签证书，443 仍使用 ca 证书 \|\| Is it possible to support the custom port to enable SSL and configure a self-signed certificate, 443 still uses the ca certificate |
| [#2519](https://github.com/higress-group/higress/issues/2519) | 2025-06-30 | 功能请求/咨询 | [key_auth] 使用 key_auth 插件对 ingress/domain 授权 consumer 遇到的问题 |
| [#2518](https://github.com/higress-group/higress/issues/2518) | 2025-06-30 | 功能请求/咨询 | [key_auth] 认证插件适配多种认证场景 \|\| [key_auth] The authentication plug-in is suitable for multiple authentication scenarios |
| [#2479](https://github.com/higress-group/higress/issues/2479) | 2025-06-22 | 功能请求/咨询 | 请问后续的oauth2插件是否会支持授权码模式？ \|\| Will the subsequent oauth2 plug-in support the authorization code mode? |
| [#2470](https://github.com/higress-group/higress/issues/2470) | 2025-06-19 | 功能请求/咨询 | 为 OAuth2 插件增加 OAuth 2.1 规范的授权码模式支持 \|\| Added the authorization code mode support for the OAuth 2.1 specification to the OAuth2 plug-in |
| [#2455](https://github.com/higress-group/higress/issues/2455) | 2025-06-18 | 功能请求/咨询 | Discussion: extending cluster-key-rate-limit filter |
| [#2365](https://github.com/higress-group/higress/issues/2365) | 2025-06-04 | 功能请求/咨询 | JWT插件 claims_to_headers 配置问题 \|\| JWT plugin claims_to_headers configuration issues |

### 插件机制/扩展框架（28）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5059](https://github.com/higress-group/higress/issues/5059) | 2026-10-12 | 测试/e2e | e2e: add testcases for the nginx-rewrite-compatible wasmplugin |
| [#5058](https://github.com/higress-group/higress/issues/5058) | 2026-10-11 | issue-spec (Proposal/Design) | Proposal: ExtProc CR——以插件化 filter chain 的方式开放 Envoy ext_proc 数据面扩展 \|\| Proposal: ExtProc CR — user-facing out-of-process plugin chains on Envoy ext_proc |
| [#4857](https://github.com/higress-group/higress/issues/4857) | 2026-09-29 | Bug 报告 | One WasmPlugin CR with a missing wasm file breaks ALL routes on the gateway (500 / NFCF), not just its own |
| [#4784](https://github.com/higress-group/higress/issues/4784) | 2026-09-28 | 功能请求/咨询 | AgentCert / agent-trust verification as a Wasm plugin or ext_authz — would it fit? |
| [#4748](https://github.com/higress-group/higress/issues/4748) | 2026-09-22 | 功能请求/咨询 | Feature request: 确认 WasmPlugin 的 RuntimeError 恢复支持与 FAIL_RELOAD 贡献方向 |
| [#4733](https://github.com/higress-group/higress/issues/4733) | 2026-09-20 | issue-spec (Proposal/Design) | Design: exercise ext-auth endpoint modes and match policies in Wasm E2E |
| [#4732](https://github.com/higress-group/higress/issues/4732) | 2026-09-20 | issue-spec (Proposal/Design) | Proposal: add runtime E2E coverage for the ext-auth Wasm plugin |
| [#4657](https://github.com/higress-group/higress/issues/4657) | 2026-09-08 | 功能请求/咨询 | Wasm SDK LogDebugf formats disabled debug messages |
| [#4606](https://github.com/higress-group/higress/issues/4606) | 2026-08-26 | Bug 报告 | [Bug] wasm 插件 StopIterationNoBuffer 暂停 + 下游 ext_proc 异步恢复导致流式单帧响应空 body \|\| [Bug] wasm plug-in StopIterationNoBuffer pause + downstream ext_proc asynchronous recovery causes streaming single frame response to empty body |
| [#4529](https://github.com/higress-group/higress/issues/4529) | 2026-08-15 | issue-spec (Proposal/Design) | Proposal: make Wasm plugin OCI layouts Envoy-verifiable before promotion |
| [#4521](https://github.com/higress-group/higress/issues/4521) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: 修复 macOS Bash 3.2 下 WASM 批量构建脚本的 mapfile 失败 \|\| Proposal: Make the WASM batch-build script safe with macOS Bash 3.2 |
| [#4433](https://github.com/higress-group/higress/issues/4433) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Bind targeted Wasm e2e tests to the locally built artifact |
| [#4393](https://github.com/higress-group/higress/issues/4393) | 2026-08-10 | 功能请求/咨询 | Multiple InferencePool rules in one HTTPRoute share the last ext_proc config |
| [#4264](https://github.com/higress-group/higress/issues/4264) | 2026-08-04 | 功能请求/咨询 | Extract shared SSE framing utility into wasm-go/pkg/sseframe |
| [#4032](https://github.com/higress-group/higress/issues/4032) | 2026-06-29 | 功能请求/咨询 | Unexpected number of active Wasm VMs and created after restarting higress container |
| [#3977](https://github.com/higress-group/higress/issues/3977) | 2026-06-15 | 功能请求/咨询 | cluster_hash/cluster_metrics: missing controller-side integration, requires manual EnvoyFilter to work |
| [#3844](https://github.com/higress-group/higress/issues/3844) | 2026-05-18 | Bug 报告 | wasmPlugins 配置不生效 \|\| wasmPlugins configuration does not take effect |
| [#3821](https://github.com/higress-group/higress/issues/3821) | 2026-05-13 | 功能请求/咨询 | 优化：移除对 EnvoyFilter CRD 的强依赖，避免与 Istio 版本冲突 \|\| Optimization: Remove strong dependence on EnvoyFilter CRD to avoid conflicts with Istio versions |
| [#3808](https://github.com/higress-group/higress/issues/3808) | 2026-05-11 | Bug 报告 | 使用标准 Go 1.26 + wasip1 构建 WASM 插件时，遇到 `nottinygc` CGO 依赖错误： \|\| When building the WASM plugin using standard Go 1.26 + wasip1, I encountered a `nottinygc` CGO dependency error: |
| [#3276](https://github.com/higress-group/higress/issues/3276) | 2025-12-29 | 功能请求/咨询 | wasm-go插件构建失败 \|\| wasm-go plugin build failed |
| [#3012](https://github.com/higress-group/higress/issues/3012) | 2025-10-15 | 功能请求/咨询 | wasm插件日志单独输出在独立文件 \|\| wasm plug-in log is output in a separate file |
| [#2705](https://github.com/higress-group/higress/issues/2705) | 2025-08-03 | Bug 报告 | wasm-go transformer map 来源为 headers 或 querys 时不符合预期 \|\| =wasm-go transformer map does not meet expectations when it comes from headers or querys |
| [#2559](https://github.com/higress-group/higress/issues/2559) | 2025-07-08 | 功能请求/咨询 | Feature Request: Support Alibaba Cloud Service Mesh (ASM) via EnvoyFilterTemplate |
| [#2510](https://github.com/higress-group/higress/issues/2510) | 2025-06-27 | 功能请求/咨询 | Suggestion: Display Detailed Error Information in WASM Plugin CRD Events |
| [#2495](https://github.com/higress-group/higress/issues/2495) | 2025-06-25 | 功能请求/咨询 | wasm插件返回内容时能否支持流时传输 \|\| Can the wasm plug-in support streaming when returning content |
| [#2461](https://github.com/higress-group/higress/issues/2461) | 2025-06-19 | 功能请求/咨询 | 在wasmPlugin中，可不可以把httproute写入matchrules的ingress字段，然后对应的规则在指定的httproute上生效？ \|\| In wasmPlugin, can httpproute be written into the ingress field of matchrules, and then the corresponding rules take effect on the specified httpproute? |
| [#2447](https://github.com/higress-group/higress/issues/2447) | 2025-06-17 | 功能请求/咨询 | Automatically builds Wasm plugins when plugin-related files are modified in a pull request |
| [#2354](https://github.com/higress-group/higress/issues/2354) | 2025-05-30 | 功能请求/咨询 | go-wasm插件如何实现从另一个源分片下载文件后再分片返回客户端 \|\| How to implement the go-wasm plug-in to download the file from another source shard and then return to the client through sharding. |

### 服务注册中心（31）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5217](https://github.com/higress-group/higress/issues/5217) | 2026-10-22 | 功能请求/咨询 | Higress与Nacos3版本兼容的问题 |
| [#4999](https://github.com/higress-group/higress/issues/4999) | 2026-10-05 | issue-spec (Proposal/Design) | Design: finalize failed registry replacement without deleting other registries' data |
| [#4998](https://github.com/higress-group/higress/issues/4998) | 2026-10-05 | issue-spec (Proposal/Design) | Proposal: retire stale discovery data after registry replacement fails |
| [#4832](https://github.com/higress-group/higress/issues/4832) | 2026-09-28 | Bug 报告 | registry/nacos/address: TestBackup fails under -race due to a data race in the test |
| [#4831](https://github.com/higress-group/higress/issues/4831) | 2026-09-28 | 功能请求/咨询 | registry/nacos: weights below 0.5 become 0 in generated ServiceEntry endpoints |
| [#4830](https://github.com/higress-group/higress/issues/4830) | 2026-09-28 | Bug 报告 | registry/nacos: v1 watcher drops instance metadata when the protocol key is absent |
| [#4756](https://github.com/higress-group/higress/issues/4756) | 2026-09-23 | issue-spec (Proposal/Design) | Design: restore-registry-watcher-status-wiring |
| [#4755](https://github.com/higress-group/higress/issues/4755) | 2026-09-23 | issue-spec (Proposal/Design) | Proposal: restore-registry-watcher-status-wiring |
| [#4671](https://github.com/higress-group/higress/issues/4671) | 2026-09-09 | issue-spec (Proposal/Design) | Design: Fix registry reconcile readiness goroutine leak |
| [#4669](https://github.com/higress-group/higress/issues/4669) | 2026-09-09 | issue-spec (Proposal/Design) | Proposal: Fix the goroutine leak in registry reconcile readiness wait |
| [#4538](https://github.com/higress-group/higress/issues/4538) | 2026-08-16 | 功能请求/咨询 | Higress 2.2.3 Standalone Compose 使用 Nacos 存储时，删除 Ingress 后 Gateway RDS 路由残留 \|\| Higress 2.2.3 When Standalone Compose uses Nacos storage, the Gateway RDS route remains after deleting Ingress. |
| [#4520](https://github.com/higress-group/higress/issues/4520) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: Nacos v2 更换 namingClient 后重放已有服务订阅 \|\| Proposal: Replay Nacos v2 service subscriptions after namingClient replacement |
| [#4432](https://github.com/higress-group/higress/issues/4432) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Interpret Eureka retry delay in milliseconds |
| [#4426](https://github.com/higress-group/higress/issues/4426) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Close every Eureka HTTP response body |
| [#4423](https://github.com/higress-group/higress/issues/4423) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Isolate ZooKeeper retry state per watched service |
| [#4415](https://github.com/higress-group/higress/issues/4415) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: Preserve IPv6 Dubbo providers discovered through ZooKeeper |
| [#4398](https://github.com/higress-group/higress/issues/4398) | 2026-08-10 | 功能请求/咨询 | /registry/watcherStatus always returns 404 because IngressStore is not wired |
| [#4397](https://github.com/higress-group/higress/issues/4397) | 2026-08-10 | Bug 报告 | Registry readiness timeout leaks a waiter goroutine |
| [#4394](https://github.com/higress-group/higress/issues/4394) | 2026-08-10 | 功能请求/咨询 | Failed registry replacement leaves stale services in the discovery cache |
| [#4390](https://github.com/higress-group/higress/issues/4390) | 2026-08-10 | 功能请求/咨询 | Consul registry keeps stale endpoints when all instances become unhealthy |
| [#4339](https://github.com/higress-group/higress/issues/4339) | 2026-08-08 | 功能请求/咨询 | Image builds misparse tags when the registry has a port |
| [#4006](https://github.com/higress-group/higress/issues/4006) | 2026-06-23 | 功能请求/咨询 | Controller 自动生成 VirtualService 时重写路径固定为 /，未读取 nacos 配置的 remoteServerConfig.exportPath \|\| Controller automatically generates VirtualService, the rewrite path is fixed to /, and the remoteServerConfig.exportPath of nacos configuration is not read. |
| [#3876](https://github.com/higress-group/higress/issues/3876) | 2026-05-25 | 功能请求/咨询 | 服务来源支持 Eureka 集群配置 \|\| Service source supports Eureka cluster configuration |
| [#3737](https://github.com/higress-group/higress/issues/3737) | 2026-04-20 | 功能请求/咨询 | 通过higress可以请求到nacos上不健康的实例 \|\| You can request unhealthy instances on nacos through higress |
| [#3326](https://github.com/higress-group/higress/issues/3326) | 2026-01-14 | 功能请求/咨询 | higress最新版和nacos3.1.1兼容日志报错 \|\| The latest version of higress is compatible with nacos3.1.1 log error |
| [#3112](https://github.com/higress-group/higress/issues/3112) | 2025-11-11 | 功能请求/咨询 | 在higress+Nacos部署模式下，使用key-auth插件，当配置的数量达到一定程度之后，key-auth插件对应的配置数据超过了Nacos单条数据的长度限制导致报错 \|\| In higress+Nacos deployment mode, use the key-auth plug-in. When the number of configurations reaches a certain level, the configuration data corresponding to the key-auth plug-in exceeds the length limit of Nacos single data, resulting in an error. |
| [#2896](https://github.com/higress-group/higress/issues/2896) | 2025-09-10 | Bug 报告 | 使用eureka作为服务发现来源时，服务中最后一个节点下线时无法清理该节点信息 \|\| When using eureka as the source of service discovery, the information of the node cannot be cleaned when the last node in the service is offline. |
| [#2895](https://github.com/higress-group/higress/issues/2895) | 2025-09-10 | 功能请求/咨询 | 使用eureka作为服务发现来源时，未找到配置服务列表全量刷新及单个服务刷新间隔时间配置 \|\| When using eureka as the source of service discovery, no configuration service list is found to be fully refreshed and the interval time configuration of single service refresh |
| [#2894](https://github.com/higress-group/higress/issues/2894) | 2025-09-10 | Bug 报告 | 使用eureka作为服务注册中心时，服务列表无法过滤非up状态的服务节点 \|\| When using eureka as the service registration center, the service list cannot filter service nodes in non-up states. |
| [#2821](https://github.com/higress-group/higress/issues/2821) | 2025-08-25 | 功能请求/咨询 | higress-registry.cn-hangzhou.cr.aliyuncs.com/higress/all-in-one:latest start failed!!! |
| [#2369](https://github.com/higress-group/higress/issues/2369) | 2025-06-04 | 功能请求/咨询 | Nacos配置获取实例BUG \|\| Nacos configuration get instance bug |

### 部署/安装/升级（30）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5076](https://github.com/higress-group/higress/issues/5076) | 2026-10-13 | Bug 报告 | plugin-server 镜像升级后历史插件目录缺失，导致既有 WasmPlugin URL 无法保持兼容 \|\| plugin-server After the image upgrade, the historical plug-in directory is missing, resulting in the existing WasmPlugin URL being unable to remain compatible. |
| [#4749](https://github.com/higress-group/higress/issues/4749) | 2026-09-23 | issue-spec (Proposal/Design) | Proposal: expose Agent APIs through a standalone A2A conversion plugin |
| [#4688](https://github.com/higress-group/higress/issues/4688) | 2026-09-11 | issue-spec (Proposal/Design) | Proposal: responses-api-deployment-affinity |
| [#4662](https://github.com/higress-group/higress/issues/4662) | 2026-09-08 | issue-spec (Proposal/Design) | Design: Envoy 1.36.4 → 1.36.10 security upgrade — merge resolution, pin set, and red/green verification |
| [#4626](https://github.com/higress-group/higress/issues/4626) | 2026-09-01 | issue-spec (Proposal/Design) | Proposal: Upgrade Higress v2.2.4 Envoy to 1.36.6 \|\| 将 Higress v2.2.4 的 Envoy 升级至 1.36.6 |
| [#4591](https://github.com/higress-group/higress/issues/4591) | 2026-08-24 | Bug 报告 | 镜像升级到最新版本后，添加AI路由时提示错误409 |
| [#4567](https://github.com/higress-group/higress/issues/4567) | 2026-08-18 | issue-spec (Proposal/Design) | Proposal: Normalize fresh-install local-docker version metadata |
| [#4534](https://github.com/higress-group/higress/issues/4534) | 2026-08-15 | issue-spec (Proposal/Design) | Design: Synchronize local-docker version metadata after a successful upgrade |
| [#4514](https://github.com/higress-group/higress/issues/4514) | 2026-08-14 | Bug 报告 | Panic bugs: nil map write in triggerRollout, empty slice in accessDockerCompose, empty Hosts in convertServiceEntry |
| [#4416](https://github.com/higress-group/higress/issues/4416) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: Keep persisted local-docker version in sync after upgrade |
| [#4292](https://github.com/higress-group/higress/issues/4292) | 2026-08-07 | 功能请求/咨询 | Implement: o11y logging 功能组开关与外部 Loki 推送（helm/core）(design [#4291](https://github.com/higress-group/higress/issues/4291)) \|\| Implement: o11y logging function group switch and external Loki push (helm/core) (design [#4291](https://github.com/higress-group/higress/issues/4291)) |
| [#4291](https://github.com/higress-group/higress/issues/4291) | 2026-08-07 | issue-spec (Proposal/Design) | Design: o11y logging 功能组开关与外部 Loki 推送（helm/core）(proposal [#4250](https://github.com/higress-group/higress/issues/4250)) \|\| Design: o11y logging function group switch and external Loki push (helm/core) (proposal [#4250](https://github.com/higress-group/higress/issues/4250)) |
| [#4179](https://github.com/higress-group/higress/issues/4179) | 2026-07-22 | 功能请求/咨询 | Higress all-in-one v2.2.3 Envoy CPU 飙升至 1000%+ 导致网关不可用 |
| [#4150](https://github.com/higress-group/higress/issues/4150) | 2026-07-16 | 功能请求/咨询 | image pull err |
| [#4126](https://github.com/higress-group/higress/issues/4126) | 2026-07-11 | 功能请求/咨询 | feat(helm): decouple gateway Promtail access-log shipping from the bundled o11y stack + configurable Loki URL |
| [#3842](https://github.com/higress-group/higress/issues/3842) | 2026-05-18 | Bug 报告 | helm 安装 2.2.1 版本出现错误 \|\| helm An error occurred while installing version 2.2.1 |
| [#3796](https://github.com/higress-group/higress/issues/3796) | 2026-05-07 | 功能请求/咨询 | 使用higress all-in-one镜像文件部署服务，存在JAVA语言方向以下高/中/低危漏洞问题，麻烦跟进修复 \|\| When using the higress all-in-one image file deployment service, there are high/medium/low risk vulnerabilities in the JAVA language direction. Please follow up and fix them. |
| [#3795](https://github.com/higress-group/higress/issues/3795) | 2026-05-07 | 功能请求/咨询 | 使用higress all-in-one镜像文件部署服务，存在GO语言方向以下高/中/低危漏洞问题，麻烦跟进修复 \|\| When using the higress all-in-one image file deployment service, there are high/medium/low risk vulnerabilities in the GO language direction. Please follow up and fix them. |
| [#3749](https://github.com/higress-group/higress/issues/3749) | 2026-04-23 | 功能请求/咨询 | Helm: controller RBAC templates ignore controller.rbac.create toggle & gateway missing cluster-level RBAC toggle |
| [#3712](https://github.com/higress-group/higress/issues/3712) | 2026-04-14 | 功能请求/咨询 | 2.2.1环境上使用helm安装Istio CRD失败 \|\| The installation of Istio CRD using helm in the 2.2.1 version environment failed |
| [#3553](https://github.com/higress-group/higress/issues/3553) | 2026-03-02 | 功能请求/咨询 | all-in-one部署版本v2.1.11  在连接过多时,envoy进程退出，且没有重新启动 |
| [#3377](https://github.com/higress-group/higress/issues/3377) | 2026-01-21 | 功能请求/咨询 | RAG 插件是否可以支持非阿里云的向量检索后端（私有化部署场景） \|\| Can the RAG plug-in support non-Alibaba Cloud vector retrieval backends (private deployment scenario) |
| [#3332](https://github.com/higress-group/higress/issues/3332) | 2026-01-15 | 功能请求/咨询 | Install failed & no health upstream |
| [#3331](https://github.com/higress-group/higress/issues/3331) | 2026-01-15 | 功能请求/咨询 | Feature Request: Publish WasmPlugin Images in Kubernetes ImageVolume-Compatible Format |
| [#3207](https://github.com/higress-group/higress/issues/3207) | 2025-12-09 | Bug 报告 | 使用all in one 的方式部署服务，swagger的request Body不显示参数 |
| [#3140](https://github.com/higress-group/higress/issues/3140) | 2025-11-17 | Bug 报告 | wasm oci 镜像如何私有化-在私有化部署中无法下载wasm 镜像 \|\| How to privatize the wasm oci image - the wasm image cannot be downloaded in privatized deployment |
| [#3030](https://github.com/higress-group/higress/issues/3030) | 2025-10-19 | 功能请求/咨询 | all-in-one报错 |
| [#2879](https://github.com/higress-group/higress/issues/2879) | 2025-09-06 | Bug 报告 | 部署多个higress的时候无法修改gatewayclass的name和controllerName \|\| When deploying multiple higresses, the name and controllerName of gatewayclass cannot be modified. |
| [#2548](https://github.com/higress-group/higress/issues/2548) | 2025-07-07 | Bug 报告 | 我想将higress 2.1.4版本部署到k8s 1.18版本中（没办法升级），环境不允许安装helm，有办法可以部署吗？ \|\| I want to deploy higress 2.1.4 version to k8s 1.18 version (no way to upgrade), the environment does not allow helm to be installed. Is there a way to deploy? |
| [#2466](https://github.com/higress-group/higress/issues/2466) | 2025-06-19 | 功能请求/咨询 | higress 部署阿里云OV通配符证书 tls访问失败 \|\| higress Deploy Alibaba Cloud OV wildcard certificate TLS access failed |

### 可观测性（3）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5215](https://github.com/higress-group/higress/issues/5215) | 2026-10-21 | 功能请求/咨询 | WasmPlugin update convergence: request for a supported readiness / observability contract |
| [#4183](https://github.com/higress-group/higress/issues/4183) | 2026-07-23 | 功能请求/咨询 | v2.2.3版本可以使用responses格式请求模型，普罗米修斯的端点 /stats/prometheus 里面统计不到responses格式的token数量。 |
| [#3653](https://github.com/higress-group/higress/issues/3653) | 2026-03-27 | 功能请求/咨询 | prometheus对 v1/message 接口的计数统计 \|\| Prometheus’s counting statistics for the v1/message interface |

### Console 控制台（7）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5081](https://github.com/higress-group/higress/issues/5081) | 2026-10-14 | Bug 报告 | [Bug] Higress v2.2.0 控制台切换域名证书后不生效，需重启网关 \|\| [Bug] Higress v2.2.0 console does not take effect after switching the domain name certificate, and the gateway needs to be restarted |
| [#4609](https://github.com/higress-group/higress/issues/4609) | 2026-08-27 | 功能请求/咨询 | Does Console support displaying Ingress routes created via kubectl across all namespaces? |
| [#3746](https://github.com/higress-group/higress/issues/3746) | 2026-04-23 | 功能请求/咨询 | Guided Higress install mission in KubeStellar Console |
| [#3677](https://github.com/higress-group/higress/issues/3677) | 2026-04-02 | 功能请求/咨询 | higress-console v2.2.0 不能在控制台页面上创建和管理httproute配置 \|\| higress-console v2.2.0 httproute configuration cannot be created and managed on the console page |
| [#3004](https://github.com/higress-group/higress/issues/3004) | 2025-10-14 | 功能请求/咨询 | higress-console底层的Spring-Core依赖存在安全漏洞 |
| [#2644](https://github.com/higress-group/higress/issues/2644) | 2025-07-22 | 功能请求/咨询 | Higress控制台支持阿里云百炼海外接入点 \|\| =Higress console supports Alibaba Cloud Bailian Overseas Access Point |
| [#2444](https://github.com/higress-group/higress/issues/2444) | 2025-06-17 | 功能请求/咨询 | Higress console 配置 secret 时如果是缺省 namespace 格式的话 controller 处理会报错 \|\| Higress console When configuring secret, if the controller handles the default namespace format, the controller will report an error. |

### hgctl CLI（25）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5229](https://github.com/higress-group/higress/issues/5229) | 2026-10-22 | issue-spec (Proposal/Design) | Proposal: Honor the selected namespace in hgctl plugin install |
| [#5228](https://github.com/higress-group/higress/issues/5228) | 2026-10-22 | issue-spec (Proposal/Design) | Proposal: Preserve caller-owned hgctl plugin build output on failure |
| [#4923](https://github.com/higress-group/higress/issues/4923) | 2026-10-02 | 文档 | docs(hgctl): fix prerequisite spelling in agent comments |
| [#4911](https://github.com/higress-group/higress/issues/4911) | 2026-10-01 | issue-spec (Proposal/Design) | Proposal: honor default-No confirmation in hgctl install, uninstall, and upgrade ([#4905](https://github.com/higress-group/higress/issues/4905)) |
| [#4905](https://github.com/higress-group/higress/issues/4905) | 2026-10-01 | 功能请求/咨询 | hgctl: install, uninstall and upgrade do not cancel on Enter or lowercase n |
| [#4898](https://github.com/higress-group/higress/issues/4898) | 2026-09-30 | issue-spec (Proposal/Design) | Design: Validate malformed Envoy config dumps in hgctl gateway-config |
| [#4885](https://github.com/higress-group/higress/issues/4885) | 2026-09-30 | 功能请求/咨询 | hgctl: agent deploy ignores --agentrun when selecting the deployment target |
| [#4805](https://github.com/higress-group/higress/issues/4805) | 2026-09-28 | issue-spec (Proposal/Design) | Proposal: validate malformed Envoy config dumps in hgctl ([#4333](https://github.com/higress-group/higress/issues/4333)) |
| [#4737](https://github.com/higress-group/higress/issues/4737) | 2026-09-20 | issue-spec (Proposal/Design) | Proposal: restart Higress after `hgctl upgrade --quiet` instead of silently keeping the old version running |
| [#4641](https://github.com/higress-group/higress/issues/4641) | 2026-09-03 | issue-spec (Proposal/Design) | Design: hgctl-ci-unit-tests |
| [#4550](https://github.com/higress-group/higress/issues/4550) | 2026-08-16 | 功能请求/咨询 | proposal(hgctl): add Rust WASM support to plugin build |
| [#4547](https://github.com/higress-group/higress/issues/4547) | 2026-08-16 | 功能请求/咨询 | proposal(hgctl): add resource-aware gateway Config Dump diff |
| [#4525](https://github.com/higress-group/higress/issues/4525) | 2026-08-14 | issue-spec (Proposal/Design) | Design: use Kubernetes ParseQuantity for hgctl resource validation |
| [#4524](https://github.com/higress-group/higress/issues/4524) | 2026-08-14 | issue-spec (Proposal/Design) | Proposal: use canonical Kubernetes resource quantity validation in hgctl |
| [#4512](https://github.com/higress-group/higress/issues/4512) | 2026-08-14 | Bug 报告 | hgctl panics: naked type assertion in GlobalConfAsker.Ask() and entries[0] without length check in ParseLatestVersion |
| [#4452](https://github.com/higress-group/higress/issues/4452) | 2026-08-12 | issue-spec (Proposal/Design) | Proposal: Default hgctl Envoy dashboard lookups to higress-system |
| [#4418](https://github.com/higress-group/higress/issues/4418) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: Honor and resolve explicit targets in hgctl dashboard envoy |
| [#4417](https://github.com/higress-group/higress/issues/4417) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: Make hgctl dashboard port forwarding report startup failures reliably |
| [#4403](https://github.com/higress-group/higress/issues/4403) | 2026-08-10 | issue-spec (Proposal/Design) | Design: preserve hgctl profile discovery errors |
| [#4402](https://github.com/higress-group/higress/issues/4402) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: preserve hgctl profile discovery errors |
| [#4391](https://github.com/higress-group/higress/issues/4391) | 2026-08-10 | 功能请求/咨询 | hgctl upgrade and uninstall hide profile discovery errors as not installed |
| [#4338](https://github.com/higress-group/higress/issues/4338) | 2026-08-08 | Bug 报告 | hgctl profile validation drops resource defaults and normalization |
| [#4333](https://github.com/higress-group/higress/issues/4333) | 2026-08-08 | Bug 报告 | hgctl gateway-config panics on malformed Envoy config dumps |
| [#4332](https://github.com/higress-group/higress/issues/4332) | 2026-08-08 | 功能请求/咨询 | Clarify production reachability of hgctl's PDB conflict resolver |
| [#3639](https://github.com/higress-group/higress/issues/3639) | 2026-03-24 | Bug 报告 | 使用hgctl部署无法指定pvc的sc |

### 测试（2）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#4829](https://github.com/higress-group/higress/issues/4829) | 2026-09-28 | 测试/e2e | e2e: CompareResponse never compares text/plain response bodies |
| [#4362](https://github.com/higress-group/higress/issues/4362) | 2026-08-08 | 测试/e2e | E2E test documentation points to removed conformance paths |

### 文档（2）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5061](https://github.com/higress-group/higress/issues/5061) | 2026-10-12 | 文档 | docs(ip-restriction): README config example uses mixed-case header name x-real-iP |
| [#4780](https://github.com/higress-group/higress/issues/4780) | 2026-09-27 | 文档 | docs(ip-restriction): example uses wrong header name casing (x-real-iP → x-real-ip) |

### 其他/未分类（114）

| # | 日期 | 类型 | 标题 |
|---|---|---|---|
| [#5307](https://github.com/higress-group/higress/issues/5307) | 2026-11-05 | issue-spec (Proposal/Design) | Proposal: Preserve original SSE data parsing and add a no-space fallback |
| [#5258](https://github.com/higress-group/higress/issues/5258) | 2026-10-24 | issue-spec (Proposal/Design) | Proposal: Limit requests in flight per consumer, header or model |
| [#5257](https://github.com/higress-group/higress/issues/5257) | 2026-10-24 | issue-spec (Proposal/Design) | Proposal: Opt-in active health checks for backend services |
| [#4984](https://github.com/higress-group/higress/issues/4984) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: log the first maxSize bytes of streamed bodies exactly once ([#4977](https://github.com/higress-group/higress/issues/4977)) |
| [#4982](https://github.com/higress-group/higress/issues/4982) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: type-check non-String GraphQL variables before building the upstream body ([#4975](https://github.com/higress-group/higress/issues/4975)) |
| [#4981](https://github.com/higress-group/higress/issues/4981) | 2026-10-04 | issue-spec (Proposal/Design) | Proposal: validate valid-JSON non-object bodies against the configured schema ([#4974](https://github.com/higress-group/higress/issues/4974)) |
| [#4818](https://github.com/higress-group/higress/issues/4818) | 2026-09-28 | Bug 报告 | ToInputSchema panics on nil input and silently ignores marshal/unmarshal errors |
| [#4816](https://github.com/higress-group/higress/issues/4816) | 2026-09-28 | Bug 报告 | Naked type assertion in cloneSchemaSnapshot can panic |
| [#4770](https://github.com/higress-group/higress/issues/4770) | 2026-09-24 | issue-spec (Proposal/Design) | Design: merge configured and request query parameters in redirects |
| [#4769](https://github.com/higress-group/higress/issues/4769) | 2026-09-24 | issue-spec (Proposal/Design) | Proposal: merge configured and request query parameters in redirects |
| [#4750](https://github.com/higress-group/higress/issues/4750) | 2026-09-23 | issue-spec (Proposal/Design) | Design: A2A to Agent API conversion and kind verification |
| [#4742](https://github.com/higress-group/higress/issues/4742) | 2026-09-21 | 功能请求/咨询 | /v1/responses接口的input、output内容目前没有记录到ai_log中 \|\| /v1/responses interface are currently not recorded in ai_log. |
| [#4725](https://github.com/higress-group/higress/issues/4725) | 2026-09-18 | issue-spec (Proposal/Design) | Design: Integer/Short Dubbo string parameter conversion ([#3659](https://github.com/higress-group/higress/issues/3659)) |
| [#4723](https://github.com/higress-group/higress/issues/4723) | 2026-09-18 | issue-spec (Proposal/Design) | Proposal: make multi-model fallback progress through backup models ([#3930](https://github.com/higress-group/higress/issues/3930)) |
| [#4722](https://github.com/higress-group/higress/issues/4722) | 2026-09-18 | issue-spec (Proposal/Design) | Proposal: support Integer and Short Dubbo string parameters ([#3659](https://github.com/higress-group/higress/issues/3659)) |
| [#4721](https://github.com/higress-group/higress/issues/4721) | 2026-09-18 | issue-spec (Proposal/Design) | Proposal: collect Responses API answer and summary text ([#3581](https://github.com/higress-group/higress/issues/3581)) |
| [#4667](https://github.com/higress-group/higress/issues/4667) | 2026-09-09 | issue-spec (Proposal/Design) | Design: preserve stream mode in Qwen3Guard input-denial responses |
| [#4666](https://github.com/higress-group/higress/issues/4666) | 2026-09-09 | issue-spec (Proposal/Design) | Proposal: honor streaming requests when Qwen3Guard blocks input |
| [#4574](https://github.com/higress-group/higress/issues/4574) | 2026-08-18 | Bug 报告 | 默认的通义千问服务提供者不支持response API ? \|\| The default Tongyi Qianwen service provider does not support response API? |
| [#4553](https://github.com/higress-group/higress/issues/4553) | 2026-08-16 | 功能请求/咨询 | proposal(ai): unify GenAI telemetry and cost/budget semantics |
| [#4434](https://github.com/higress-group/higress/issues/4434) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Use one Kind cluster name throughout Gateway API conformance |
| [#4419](https://github.com/higress-group/higress/issues/4419) | 2026-08-11 | issue-spec (Proposal/Design) | Proposal: Preserve integer-valued RAG Milvus mapping parameters |
| [#4401](https://github.com/higress-group/higress/issues/4401) | 2026-08-10 | issue-spec (Proposal/Design) | Proposal: HiMarket enterprise MaaS control plane powered by Higress \|\| 基于 Higress 的 HiMarket 企业 MaaS 控制面 |
| [#4359](https://github.com/higress-group/higress/issues/4359) | 2026-08-08 | 功能请求/咨询 | setup_env.sh loops forever for KUBECONFIG with a trailing separator |
| [#4357](https://github.com/higress-group/higress/issues/4357) | 2026-08-08 | 功能请求/咨询 | [qwen3guard] Oversized timeout and body limits wrap to uint32 |
| [#4349](https://github.com/higress-group/higress/issues/4349) | 2026-08-08 | issue-spec (Proposal/Design) | Implement: A2A protocol-aware data plane parity milestone \|\| A2A 协议感知数据面对等能力实现 |
| [#4348](https://github.com/higress-group/higress/issues/4348) | 2026-08-08 | issue-spec (Proposal/Design) | Design: Higress A2A protocol-aware gateway data plane and integrations \|\| Higress A2A 协议感知网关数据面与集成设计 |
| [#4345](https://github.com/higress-group/higress/issues/4345) | 2026-08-08 | issue-spec (Proposal/Design) | Design: Agent-assisted contribution gate and runtime verification policy |
| [#4344](https://github.com/higress-group/higress/issues/4344) | 2026-08-08 | issue-spec (Proposal/Design) | Proposal: Require issue-spec governance for materially agent-assisted PRs |
| [#4326](https://github.com/higress-group/higress/issues/4326) | 2026-08-08 | issue-spec (Proposal/Design) | Proposal: Higress A2A protocol-aware gateway \|\| Higress A2A 协议感知网关 |
| [#4325](https://github.com/higress-group/higress/issues/4325) | 2026-08-08 | issue-spec (Proposal/Design) | Proposal: Higress Agent behavior guardrails \|\| Higress Agent 行为护栏 |
| [#4324](https://github.com/higress-group/higress/issues/4324) | 2026-08-08 | issue-spec (Proposal/Design) | Proposal: Higress Agent Session gateway capabilities \|\| Higress Agent Session 网关能力 |
| [#4319](https://github.com/higress-group/higress/issues/4319) | 2026-08-08 | issue-spec (Proposal/Design) | Proposal: Higress Sandbox Gateway and multi-provider abstraction \|\| Higress Sandbox Gateway 与多 Sandbox Provider 抽象 |
| [#4297](https://github.com/higress-group/higress/issues/4297) | 2026-08-07 | issue-spec (Proposal/Design) | Proposal: Higress 内置直连 vLLM ZMQ KVEvents 的精确缓存感知调度 |
| [#4280](https://github.com/higress-group/higress/issues/4280) | 2026-08-06 | issue-spec (Proposal/Design) | [Proposal] 建立 Higress GIE v1.1.0-v1.5.0 Conformance 基线与兼容性补齐计划 |
| [#4250](https://github.com/higress-group/higress/issues/4250) | 2026-08-03 | issue-spec (Proposal/Design) | Proposal: o11y 套件按 logging / metrics 功能分组独立开关 + Promtail 外部 Loki 推送地址 \|\| Proposal: The o11y suite is grouped by logging/metrics function independent switches + Promtail external Loki push address |
| [#4169](https://github.com/higress-group/higress/issues/4169) | 2026-07-20 | 功能请求/咨询 | Bedrock cache write tokens are conflated with cache reads in protocol-converted usage |
| [#4145](https://github.com/higress-group/higress/issues/4145) | 2026-07-15 | 功能请求/咨询 | higress2.1.9下游downstream_remote_disconnect后网关没有获取到token相关数据 \|\| higress2.1.9 After downstream downstream_remote_disconnect, the gateway did not obtain token related data. |
| [#4044](https://github.com/higress-group/higress/issues/4044) | 2026-07-01 | Bug 报告 | downstream idle timeout设置为999后，非流式的post请求到180s还是会报504 stream idle timeout \|\| Downstream idle timeout is set to 999, non-streaming post requests will still report 504 stream idle timeout at 180s. |
| [#4029](https://github.com/higress-group/higress/issues/4029) | 2026-06-26 | 功能请求/咨询 | support grpc-web |
| [#4026](https://github.com/higress-group/higress/issues/4026) | 2026-06-26 | 功能请求/咨询 | stats_config新增监控指标tag \|\| stats_config adds monitoring indicator tag |
| [#4001](https://github.com/higress-group/higress/issues/4001) | 2026-06-22 | 安全/缺陷披露 | [CVE-2025-48924]以及其他漏洞 \|\| [CVE-2025-48924] and other vulnerabilities |
| [#3972](https://github.com/higress-group/higress/issues/3972) | 2026-06-15 | 功能请求/咨询 | 支持一种官方的多集群 Higress 配置共享/同步方案 \|\| Supports an official multi-cluster Higress configuration sharing/synchronization solution |
| [#3960](https://github.com/higress-group/higress/issues/3960) | 2026-06-12 | Bug 报告 | 无法把headers 中的自定义参数带入 body中设置默认值 \|\| Cannot bring custom parameters in headers into body to set default values |
| [#3957](https://github.com/higress-group/higress/issues/3957) | 2026-06-11 | 功能请求/咨询 | Anthropic在stream=false下bug \|\| Anthropic bug under stream=false |
| [#3948](https://github.com/higress-group/higress/issues/3948) | 2026-06-10 | 功能请求/咨询 | higress with gpustack not balance very perfect in qwen3-embedding-8b |
| [#3936](https://github.com/higress-group/higress/issues/3936) | 2026-06-08 | 功能请求/咨询 | 后端模型双协议支持 \|\| Backend model dual protocol support |
| [#3887](https://github.com/higress-group/higress/issues/3887) | 2026-05-27 | 功能请求/咨询 | 国模多协议多地址适配 \|\| national model multi-protocol and multi-address adaptation can be realized within one supplier |
| [#3833](https://github.com/higress-group/higress/issues/3833) | 2026-05-15 | 功能请求/咨询 | Track OpenSSF Best Practices badge to Passing level |
| [#3809](https://github.com/higress-group/higress/issues/3809) | 2026-05-11 | 功能请求/咨询 | Clarify and extend native Anthropic Messages API support across providers |
| [#3794](https://github.com/higress-group/higress/issues/3794) | 2026-05-07 | 功能请求/咨询 | ExternalName service 不再被支持 \|\| ExternalName service is no longer supported |
| [#3780](https://github.com/higress-group/higress/issues/3780) | 2026-04-30 | 功能请求/咨询 | Migrate personal fork dependencies to higress-group organization |
| [#3747](https://github.com/higress-group/higress/issues/3747) | 2026-04-23 | 功能请求/咨询 | Health Checks for Server availability |
| [#3729](https://github.com/higress-group/higress/issues/3729) | 2026-04-17 | Bug 报告 | higress不支持阿里云多模态向量模型 \|\| higress does not support Alibaba Cloud's multi-modal vector model |
| [#3716](https://github.com/higress-group/higress/issues/3716) | 2026-04-15 | 功能请求/咨询 | himarket跟higress的用户数据监控疑难问题 |
| [#3665](https://github.com/higress-group/higress/issues/3665) | 2026-03-31 | Bug 报告 | [Bug] http_dubbo_transcoder uses CONNECT method, causing HTTP Keep-Alive connections to be non-reusable and severely degrading performance |
| [#3662](https://github.com/higress-group/higress/issues/3662) | 2026-03-31 | 功能请求/咨询 | 开了监控之后， 内存占用持续增加，一直增加到溢出，然后反复重启 \|\| After turning on monitoring, the memory usage continues to increase until it overflows, and then restarts repeatedly |
| [#3659](https://github.com/higress-group/higress/issues/3659) | 2026-03-29 | 功能请求/咨询 | [Feature] http_dubbo_transcoder: extend convertStringToTypeValue to support more Java types (Integer, Short, Float, Date, BigDecimal, Set) |
| [#3641](https://github.com/higress-group/higress/issues/3641) | 2026-03-24 | 功能请求/咨询 | Higress Http2Rpc List<DTO> 元素为 null |
| [#3626](https://github.com/higress-group/higress/issues/3626) | 2026-03-20 | 功能请求/咨询 | 什么时候能添加body-size参数，整体都可以，就唯独少这一个参数 为什么不实现呢 \|\| When can the body-size parameter be added? Everything is fine except for this one parameter. Why not implement it? |
| [#3621](https://github.com/higress-group/higress/issues/3621) | 2026-03-19 | 功能请求/咨询 | 支持管理多个 namespaces \|\| Supports management of multiple namespaces |
| [#3613](https://github.com/higress-group/higress/issues/3613) | 2026-03-17 | 功能请求/咨询 | 监控不到模型的第一次请求&模型token计量数量不准&token计量数会上下浮动 \|\| The first request of the model cannot be monitored & the model token measurement number is inaccurate & the token measurement number will fluctuate up and down |
| [#3592](https://github.com/higress-group/higress/issues/3592) | 2026-03-13 | Bug 报告 | http转dubbo时，RpcContext如果存在大写时无法传递 \|\| When converting http to dubbo, RpcContext cannot be passed if it exists in uppercase letters. |
| [#3552](https://github.com/higress-group/higress/issues/3552) | 2026-03-02 | 功能请求/咨询 | higress gateway pod突然卡死导致网关不可用 \|\| higress gateway pod suddenly got stuck, causing the gateway to become unavailable. |
| [#3388](https://github.com/higress-group/higress/issues/3388) | 2026-01-26 | Bug 报告 | higress是不是无法监测到ragflow配置的模型使用的情况 \|\| Is higress unable to monitor the use of models configured by ragflow? |
| [#3329](https://github.com/higress-group/higress/issues/3329) | 2026-01-14 | 功能请求/咨询 | Add load balancing mechanism Peak EWMA |
| [#3294](https://github.com/higress-group/higress/issues/3294) | 2026-01-05 | 功能请求/咨询 | Realtime model supported in Higress |
| [#3239](https://github.com/higress-group/higress/issues/3239) | 2025-12-19 | 功能请求/咨询 | HTTPS的443 端口问题 \|\| HTTPS port 443 problem |
| [#3224](https://github.com/higress-group/higress/issues/3224) | 2025-12-16 | 功能请求/咨询 | logrotate invaliad when .Values.global.liteMetrics is true |
| [#3222](https://github.com/higress-group/higress/issues/3222) | 2025-12-15 | 功能请求/咨询 | redis突然链接不上去了，higress稳定性是不是不够啊 \|\| redis suddenly failed to connect. Is higress not stable enough? |
| [#3216](https://github.com/higress-group/higress/issues/3216) | 2025-12-12 | Bug 报告 | himarket接入higress网关Model API不带端口号导致不可用 \|\| himarket access higress gateway Model API does not have a port number and is unavailable |
| [#3208](https://github.com/higress-group/higress/issues/3208) | 2025-12-09 | 功能请求/咨询 | 根据消费者维度统计模型调用情况 \|\| Statistical model calls based on consumer dimensions |
| [#3194](https://github.com/higress-group/higress/issues/3194) | 2025-12-04 | 功能请求/咨询 | 支持：转发时请求头顺序可控 \|\| Support: The order of request headers can be controlled when forwarding |
| [#3169](https://github.com/higress-group/higress/issues/3169) | 2025-11-26 | Bug 报告 | 大模型调用180秒后固定触发504 gateway timeout \|\| will be reported and 504 gateway timeout will be triggered 180 seconds after the large model is called. |
| [#3154](https://github.com/higress-group/higress/issues/3154) | 2025-11-20 | 功能请求/咨询 | 请问如何让higress可以传达真实的客户端IP给到服务 \|\| How can higress convey the real client IP to the service? |
| [#3107](https://github.com/higress-group/higress/issues/3107) | 2025-11-10 | 功能请求/咨询 | 内网如何使用higress \|\| How to use higress in the intranet |
| [#3098](https://github.com/higress-group/higress/issues/3098) | 2025-11-06 | 功能请求/咨询 | 希望网关链路追踪增加自定义标签功能 \|\| I hope gateway link tracking will add custom label functionality |
| [#3077](https://github.com/higress-group/higress/issues/3077) | 2025-10-31 | 功能请求/咨询 | Feature: Agent-Transparent Context Compression for Multi-Turn Conversations |
| [#3007](https://github.com/higress-group/higress/issues/3007) | 2025-10-14 | 功能请求/咨询 | higress 启用 opentelemert 链路，如何在链路中增加扩展参数？ \|\| higress enables opentelemert link, how to add extended parameters to the link? |
| [#3003](https://github.com/higress-group/higress/issues/3003) | 2025-10-14 | 功能请求/咨询 | 基于IP访问控制优化建议 \|\| Optimization suggestions based on IP access control |
| [#2995](https://github.com/higress-group/higress/issues/2995) | 2025-10-11 | 功能请求/咨询 | 【Bug/功能请求】当 x-mse-consumer 等请求头值包含中文时，需要支持自动编码或提供处理机制 \|\| [Bug/Function Request] When request header values ​​such as x-mse-consumer contain Chinese, it is necessary to support automatic encoding or provide a processing mechanism |
| [#2975](https://github.com/higress-group/higress/issues/2975) | 2025-10-01 | 功能请求/咨询 | 关于一个很早之前的功能的提问 \|\| Ask a question about a long time ago function. |
| [#2971](https://github.com/higress-group/higress/issues/2971) | 2025-09-29 | 功能请求/咨询 | 获取input_token和out_token的数量 \|\| Get the number of input_token and out_token |
| [#2966](https://github.com/higress-group/higress/issues/2966) | 2025-09-26 | 功能请求/咨询 | 在loki中，如何将消费者也关联到日志中去 \|\| In loki, how to associate consumers into logs |
| [#2958](https://github.com/higress-group/higress/issues/2958) | 2025-09-25 | 功能请求/咨询 | Higress 对接Dubbo服务，报错：Cannot parse RpcResult type from buffer |
| [#2947](https://github.com/higress-group/higress/issues/2947) | 2025-09-23 | 功能请求/咨询 | Higress 对接 Dubbo 服务, 报错 can not transcode the request because the given param not match the type |
| [#2929](https://github.com/higress-group/higress/issues/2929) | 2025-09-17 | 功能请求/咨询 | Higress代理大模型接口tokenize报404 |
| [#2919](https://github.com/higress-group/higress/issues/2919) | 2025-09-15 | 功能请求/咨询 | higress 日志如何获取namespce 字段 |
| [#2911](https://github.com/higress-group/higress/issues/2911) | 2025-09-12 | Bug 报告 | higress 接入skywalking不生效 |
| [#2909](https://github.com/higress-group/higress/issues/2909) | 2025-09-11 | 功能请求/咨询 | higress到upstream的TCP建连超时时间已知默认是10秒，有什么方便的办法可以自定义修改这个建连超时时间吗？ \|\| The TCP connection timeout from higress to upstream is known to be 10 seconds by default. Is there any convenient way to customize and modify the connection timeout time? |
| [#2886](https://github.com/higress-group/higress/issues/2886) | 2025-09-08 | 功能请求/咨询 | Higress在使用Redis时的高可用性问题 \|\| High availability issues with Higress when using Redis |
| [#2881](https://github.com/higress-group/higress/issues/2881) | 2025-09-06 | Bug 报告 | higress-gateway访问一段时间后出现 503 no_healthy_upstream |
| [#2853](https://github.com/higress-group/higress/issues/2853) | 2025-09-01 | 功能请求/咨询 | 同时设置了配额和降级，配额不足时依然请求成功，请求到了降级服务 |
| [#2835](https://github.com/higress-group/higress/issues/2835) | 2025-08-28 | 功能请求/咨询 | higress-gateway启动速度太慢，长达4分钟 |
| [#2819](https://github.com/higress-group/higress/issues/2819) | 2025-08-25 | 功能请求/咨询 | 如何自定义higress暴露出的直方图的桶？ \|\| How to customize the bucket of the histogram exposed by higress? |
| [#2811](https://github.com/higress-group/higress/issues/2811) | 2025-08-22 | Bug 报告 | 503 upstream_reset_before_response_started{connection_termination} 有人遇到过么？ \|\| 503 upstream_reset_before_response_started{connection_termination} Has anyone encountered it? |
| [#2792](https://github.com/higress-group/higress/issues/2792) | 2025-08-19 | Bug 报告 | higress调用本地模型服务503 \|\| higress calls local model service 503 |
| [#2789](https://github.com/higress-group/higress/issues/2789) | 2025-08-19 | 功能请求/咨询 | 控制面板中 tokens 有小数点，另外每次刷新数字都会有变化 \|\| The tokens in the control panel has a decimal point, and the number will change every time you refresh it. |
| [#2774](https://github.com/higress-group/higress/issues/2774) | 2025-08-16 | 功能请求/咨询 | 支持网关与后端服务之间的连接池的配置 |
| [#2765](https://github.com/higress-group/higress/issues/2765) | 2025-08-15 | 功能请求/咨询 | 关于“服务来源”的建议 \|\| Suggestions on "Source of Service" |
| [#2763](https://github.com/higress-group/higress/issues/2763) | 2025-08-15 | 功能请求/咨询 | redis client报错 \|\| redis client reported error |
| [#2734](https://github.com/higress-group/higress/issues/2734) | 2025-08-08 | 功能请求/咨询 | 🚀欢迎大家参与“直通乌镇”Higress开源竞技挑战赛 \|\| 🚀Welcome everyone to participate in the "Straight to Wuzhen" Higress Open Source Competition Challenge |
| [#2714](https://github.com/higress-group/higress/issues/2714) | 2025-08-05 | 功能请求/咨询 | 自动发现多k8s集群 \|\| Automatically discover multiple k8s clusters |
| [#2682](https://github.com/higress-group/higress/issues/2682) | 2025-07-29 | 功能请求/咨询 | 设置websocket代理40秒就自动断开 \|\| Set the websocket proxy automatically disconnects in 40 seconds |
| [#2640](https://github.com/higress-group/higress/issues/2640) | 2025-07-22 | Bug 报告 | golang  ctx.SetRequestBodyBufferLimit() 对 wrapper.HttpClient 不起作用 \|\| golang ctx.SetRequestBodyBufferLimit() does not work for wrapper.HttpClient |
| [#2618](https://github.com/higress-group/higress/issues/2618) | 2025-07-18 | 功能请求/咨询 | 基于 KEY Auto 配置AI Quota Management报错 |
| [#2590](https://github.com/higress-group/higress/issues/2590) | 2025-07-14 | 功能请求/咨询 | ai_log日志字段缺失 \|\| = ai_log log field is missing |
| [#2587](https://github.com/higress-group/higress/issues/2587) | 2025-07-12 | 功能请求/咨询 | Support restoring original request headers when triggering fallback |
| [#2565](https://github.com/higress-group/higress/issues/2565) | 2025-07-09 | 功能请求/咨询 | higress多层代理日志中consumer异常问题 \|\| = Consumer exception problem in higress multi-layer proxy log |
| [#2555](https://github.com/higress-group/higress/issues/2555) | 2025-07-08 | 功能请求/咨询 | higress-gateway POD启动失败 \|\| higress-gateway POD failed to start |
| [#2486](https://github.com/higress-group/higress/issues/2486) | 2025-06-24 | 功能请求/咨询 | consumer日志和 metrics 增强 \|\| =consumer logs and metrics enhancements |
| [#2474](https://github.com/higress-group/higress/issues/2474) | 2025-06-20 | Bug 报告 | Higress 连接本地 vllm 大模型偶发 503 和 502 |
| [#2473](https://github.com/higress-group/higress/issues/2473) | 2025-06-20 | 功能请求/咨询 | 监控面板指标异常 |
| [#2456](https://github.com/higress-group/higress/issues/2456) | 2025-06-18 | 功能请求/咨询 | 日志过大导致loki OOM \|\| The log is too large and causes loki OOM |

## 三、分类型索引（数量Top）

### issue-spec (Proposal/Design)（217）

issue-spec 工作流条目（Proposal/Design 配对），按领域分布：

| 领域 | 数量 |
|---|---|
| AI 网关插件 (ai-*) | 82 |
| MCP 生态 | 26 |
| 通用插件（非 AI） | 19 |
| 核心网关（控制面/数据面） | 8 |
| 安全/认证/流量治理插件 | 14 |
| 插件机制/扩展框架 | 6 |
| 服务注册中心 | 11 |
| 部署/安装/升级 | 8 |
| hgctl CLI | 14 |
| 其他/未分类 | 29 |

### Bug 报告（146）

（该类型最新 15 条示例，完整清单见分领域明细）

- [#5279](https://github.com/higress-group/higress/issues/5279)（2026-10-29，AI 网关插件 (ai-*)）：ai-load-balancer: global_inflight_enabled 开启后所有请求 503 cluster_not_found
- [#5268](https://github.com/higress-group/higress/issues/5268)（2026-10-27，通用插件（非 AI））：[BUG] frontend-gray: rewrite.host bypasses skippedByHeaders for non-HTML requests
- [#5245](https://github.com/higress-group/higress/issues/5245)（2026-10-23，AI 网关插件 (ai-*)）：ai-proxy: Vertex native conversion loses parallel tool calls and mispairs results
- [#5207](https://github.com/higress-group/higress/issues/5207)（2026-10-20，通用插件（非 AI））：bug: OPA plugin can leave a request paused when DispatchHttpCall fails synchronously
- [#5198](https://github.com/higress-group/higress/issues/5198)（2026-10-20，MCP 生态）：MCP server tools/call fails with a local 308 redirect when the domain enables Force HTTPS (ssl-redirect on MCP server Ingress)
- [#5166](https://github.com/higress-group/higress/issues/5166)（2026-10-20，AI 网关插件 (ai-*)）：ai-proxy: firstByteTimeout does not take effect in Higress 2.2.4/2.2.5
- [#5160](https://github.com/higress-group/higress/issues/5160)（2026-10-19，AI 网关插件 (ai-*)）：ai-load-balancer: the Redis least-request counter leaks a permanent +1 when host override fails
- [#5157](https://github.com/higress-group/higress/issues/5157)（2026-10-19，AI 网关插件 (ai-*)）：ai-load-balancer cluster_metrics: an unknown or missing 'mode' silently falls back to random routing
- [#5151](https://github.com/higress-group/higress/issues/5151)（2026-10-19，AI 网关插件 (ai-*)）：ai-agent: outputParser panics on malformed model output (nil error deref and single code fence)
- [#5150](https://github.com/higress-group/higress/issues/5150)（2026-10-19，AI 网关插件 (ai-*)）：[Bug] ai-data-masking drops terminal finish_reason and [DONE] on OpenAI streams
- [#5143](https://github.com/higress-group/higress/issues/5143)（2026-10-18，AI 网关插件 (ai-*)）：ai-json-resp: omitting optional jsonSchema rejects requests with HTTP 500
- [#5084](https://github.com/higress-group/higress/issues/5084)（2026-10-14，AI 网关插件 (ai-*)）：ai-data-masking panics on non-UTF-8 streaming bodies shorter than the byte window and on empty streaming responses
- [#5081](https://github.com/higress-group/higress/issues/5081)（2026-10-14，Console 控制台）：[Bug] Higress v2.2.0 控制台切换域名证书后不生效，需重启网关 \|\| [Bug] Higress v2.2.0 console does not take effect after switching the domain name certificate, and the gateway needs to be restarted
- [#5076](https://github.com/higress-group/higress/issues/5076)（2026-10-13，部署/安装/升级）：plugin-server 镜像升级后历史插件目录缺失，导致既有 WasmPlugin URL 无法保持兼容 \|\| plugin-server After the image upgrade, the historical plug-in directory is missing, resulting in the existing WasmPlugin URL being unable to remain compatible.
- [#4991](https://github.com/higress-group/higress/issues/4991)（2026-10-04，安全/认证/流量治理插件）：jwt-auth: deleteCookie drops every cookie whose name starts with the token cookie name

### 功能请求/咨询（374）

（该类型最新 15 条示例，完整清单见分领域明细）

- [#5295](https://github.com/higress-group/higress/issues/5295)（2026-11-02，MCP 生态）：mcp路由支持配置其他插件 \|\| mcp routing supports configuring other plug-ins
- [#5274](https://github.com/higress-group/higress/issues/5274)（2026-10-28，安全/认证/流量治理插件）：OIDC: requests with a body may reach upstream without X-Forwarded-Access-Token during session refresh
- [#5271](https://github.com/higress-group/higress/issues/5271)（2026-10-27，AI 网关插件 (ai-*)）：ai-token-ratelimit / ai-quota：流式 SSE 的 usage 事件跨 chunk 到达时可能漏记 token
- [#5269](https://github.com/higress-group/higress/issues/5269)（2026-10-27，通用插件（非 AI））：[Question] frontend-gray: should localStorageGrayKey initialize a missing cookie?
- [#5247](https://github.com/higress-group/higress/issues/5247)（2026-10-23，通用插件（非 AI））：[Bug investigation] 2.2.4 批量更新路由和插件时 controller CPU 升高，gateway 配置延迟生效
- [#5235](https://github.com/higress-group/higress/issues/5235)（2026-10-22，MCP 生态）：higress all in one mcp tool能支持暴露上游的uri吗？
- [#5234](https://github.com/higress-group/higress/issues/5234)（2026-10-22，MCP 生态）：higress all in one v2.2.4镜像的key-auth和mcp-server插件版本没覆盖v2.2.3的
- [#5217](https://github.com/higress-group/higress/issues/5217)（2026-10-22，服务注册中心）：Higress与Nacos3版本兼容的问题
- [#5215](https://github.com/higress-group/higress/issues/5215)（2026-10-21，可观测性）：WasmPlugin update convergence: request for a supported readiness / observability contract
- [#5213](https://github.com/higress-group/higress/issues/5213)（2026-10-21，AI 网关插件 (ai-*)）：ai-data-masking: tool arguments bypass the deny/restore masking pipeline
- [#5189](https://github.com/higress-group/higress/issues/5189)（2026-10-20，通用插件（非 AI））：api-workflow: waiting for a join skips sibling branches and stalls valid DAGs
- [#5154](https://github.com/higress-group/higress/issues/5154)（2026-10-19，AI 网关插件 (ai-*)）：ai-endpoint-picker: a negative KV-cache utilisation is accepted as the best possible signal
- [#5127](https://github.com/higress-group/higress/issues/5127)（2026-10-17，AI 网关插件 (ai-*)）：ai-intent logs every user's question and the full LLM request body at Info level
- [#5119](https://github.com/higress-group/higress/issues/5119)（2026-10-16，安全/认证/流量治理插件）：Higress 请求带有认证的后端服务接口，是否有相应方案？ \|\| Higress requests a backend service interface with authentication. Is there a corresponding solution?
- [#5094](https://github.com/higress-group/higress/issues/5094)（2026-10-15，核心网关（控制面/数据面））：Higress普通路由做一个简单的http请求，有如下问题，请给看看 \|\| Higress ordinary routing makes a simple http request. If you have the following questions, please take a look.

### 文档（11）

（该类型最新 15 条示例，完整清单见分领域明细）

- [#5296](https://github.com/higress-group/higress/issues/5296)（2026-11-03，MCP 生态）：docs: mcp-server README.md (CN) contains unresolved conflict markers since [#5029](https://github.com/higress-group/higress/issues/5029)
- [#5063](https://github.com/higress-group/higress/issues/5063)（2026-10-12，AI 网关插件 (ai-*)）：docs(ai-security-guard): EN README configuration table missing securityToken option
- [#5062](https://github.com/higress-group/higress/issues/5062)（2026-10-12，AI 网关插件 (ai-*)）：docs(ai-proxy): EN README Vertex tables document nonexistent vertexGeminiSafetySetting field (silently ignored)
- [#5061](https://github.com/higress-group/higress/issues/5061)（2026-10-12，文档）：docs(ip-restriction): README config example uses mixed-case header name x-real-iP
- [#4939](https://github.com/higress-group/higress/issues/4939)（2026-10-02，AI 网关插件 (ai-*)）：Document DemonRoute as the openaiCustomUrl worked example (ai-proxy)
- [#4924](https://github.com/higress-group/higress/issues/4924)（2026-10-02，AI 网关插件 (ai-*)）：docs(hgctl): fix AI route comment spelling
- [#4923](https://github.com/higress-group/higress/issues/4923)（2026-10-02，hgctl CLI）：docs(hgctl): fix prerequisite spelling in agent comments
- [#4914](https://github.com/higress-group/higress/issues/4914)（2026-10-01，AI 网关插件 (ai-*)）：docs(ai-security-guard): EN README config table is missing the securityToken option
- [#4913](https://github.com/higress-group/higress/issues/4913)（2026-10-01，AI 网关插件 (ai-*)）：docs(ai-proxy): EN README Vertex tables document a non-existent config field (vertexGeminiSafetySetting → geminiSafetySetting)
- [#4780](https://github.com/higress-group/higress/issues/4780)（2026-09-27，文档）：docs(ip-restriction): example uses wrong header name casing (x-real-iP → x-real-ip)
- [#4779](https://github.com/higress-group/higress/issues/4779)（2026-09-27，通用插件（非 AI））：docs(frontend-gray): CN README documents injection.body field as "after" but code reads "last"

### 测试/e2e（5）

（该类型最新 15 条示例，完整清单见分领域明细）

- [#5059](https://github.com/higress-group/higress/issues/5059)（2026-10-12，插件机制/扩展框架）：e2e: add testcases for the nginx-rewrite-compatible wasmplugin
- [#4829](https://github.com/higress-group/higress/issues/4829)（2026-09-28，测试）：e2e: CompareResponse never compares text/plain response bodies
- [#4362](https://github.com/higress-group/higress/issues/4362)（2026-08-08，测试）：E2E test documentation points to removed conformance paths
- [#2718](https://github.com/higress-group/higress/issues/2718)（2025-08-05，AI 网关插件 (ai-*)）：Implement Google Cloud Vertex LLM mock server & e2e test case
- [#2717](https://github.com/higress-group/higress/issues/2717)（2025-08-05，AI 网关插件 (ai-*)）：Implement Amazon Bedrock LLM mock server & e2e test case

### 安全/缺陷披露（2）

（该类型最新 15 条示例，完整清单见分领域明细）

- [#5298](https://github.com/higress-group/higress/issues/5298)（2026-11-04，安全/认证/流量治理插件）：Security: Higress v2.2.5 Gateway still ships Envoy 1.36.10, which is affected by CVE-2026-111497
- [#4001](https://github.com/higress-group/higress/issues/4001)（2026-06-22，其他/未分类）：[CVE-2025-48924]以及其他漏洞 \|\| [CVE-2025-48924] and other vulnerabilities

## 四、结构性观察

1. **AI 插件是 issue 绝对主体**：AI 网关插件 232 个 + MCP 生态 116 个，合计约占开放 issue 的 46%——与 Higress "AI 网关"的产品定位一致，也印证了 ai-* 系插件是高频开发区（升级需谨慎）。
2. **issue-spec 工作流已被社区大规模采用**：217 个 Proposal/Design 条目，且 Proposal/Design 严格配对（见 [#5280](https://github.com/higress-group/higress/issues/5280)/[#5281](https://github.com/higress-group/higress/issues/5281) 等模式）——与 AGENTS.md 的 AI 门禁政策互为表里。
3. **Bug 报告 146 个**，高度集中在插件层（panic/静默失败/流式处理），控制面 bug 占比低——数据支持"内核稳、插件层需盯"的判断。
4. 存量 issue 积压较大（755 个开放，最早可追溯至 2025 年初的 HEP）——提新 issue 前务必搜索去重（CONTRIBUTING 也如此要求）；认领老 issue 前先确认其描述是否仍适用于当前版本。
