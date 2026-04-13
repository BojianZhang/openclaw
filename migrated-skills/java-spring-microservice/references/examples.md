# Examples

## Example 1: Spring Boot startup failure

User asks:
- Spring Boot 项目启动失败，日志一堆异常，应该怎么定位？

Expected response shape:
1. Find the first meaningful root cause.
2. Ask for active profiles, config source, and dependency changes.
3. Separate config, bean wiring, dependency, and environment causes.
4. Recommend the smallest clear correction first.

## Example 2: Should we split a service?

User asks:
- 这个订单系统越来越大，要不要拆成微服务？

Expected response shape:
1. Push the discussion toward business boundary and ownership.
2. Ask about deployment cadence, team ownership, and scaling pain.
3. Explain the operational cost of splitting.
4. Give a phased split or a “do not split yet” answer when justified.

## Example 3: Outbound RPC instability

User asks:
- 服务间调用经常超时，应该从哪几层看？

Expected response shape:
1. Check timeout, retry, fallback, and dependency shape.
2. Separate client config, downstream latency, and network path issues.
3. Explain retry amplification and synchronous fan-out risk.
4. Recommend a bounded troubleshooting order.
