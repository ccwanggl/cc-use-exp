---
name: cc-java-dev
description: Java 与 Spring 开发规范，适用于异常处理、集合、并发、服务分层和测试；不负责 review、debug 或运维流程。
---

# CC Java Dev

在编辑或审查 Java、Spring 代码时使用本技能，重点处理分层、异常、集合、并发和测试。

不要用于：

- 正式 review 或 fix/debug 工作流
- 运维风险判断
- 语言无关的通用边界控制

## 核心规则

- 代码结构优先清晰、职责单一。
- 异常处理要保留业务语义和上下文。
- 集合和对象的可变性要明确。
- 并发代码要显式管理线程池和共享状态。
- 测试优先覆盖行为和边界分支。

---

## 第三方 API HTTP 客户端选型

| 规则 | 说明 |
|------|------|
| ❌ 避免 `RestTemplate` 默认客户端调用国内平台 API | 默认 `HttpURLConnection` 的 POST 请求与微信/支付宝等 CDN 存在兼容性问题（已知触发 412/403） |
| ✅ 优先用 `java.net.http.HttpClient`（JDK 11+） | 现代 HTTP 客户端，无 CDN 兼容性问题 |
| ✅ 或配置 `HttpComponentsClientHttpRequestFactory` | 让 RestTemplate 底层走 Apache HttpClient |

**诊断特征**：HTTP 错误 + body 为空 + response headers 极简（只有 Connection/Content-Length）= CDN 层拦截，不是 API 本身的响应。同一 API 的 GET 正常但 POST 异常时，优先怀疑 HTTP 客户端兼容性。

## 按需展开

- 风格：`references/style.md`
- Spring：`references/spring.md`
- 异常：`references/exceptions.md`
- 集合：`references/collections.md`
- 并发：`references/concurrency.md`
- 测试：`references/testing.md`
- HTTP 客户端选型：`references/http-client.md`
