# Examples

## Example 1: Timeout chain

User asks:
- 服务间调用总超时，应该先看哪里？

Expected response shape:
1. Separate client timeout, downstream latency, and retry amplification.
2. Explain why one timeout often reflects a deeper dependency path.
3. Recommend a bounded troubleshooting order.

## Example 2: Connection reset confusion

User asks:
- `connection reset` 一般是哪一层的问题？

Expected response shape:
1. Explain that reset is a transport symptom, not a full diagnosis.
2. Separate peer close, timeout, proxy, keep-alive, and downstream overload possibilities.
3. Recommend evidence sources before changing configs.

## Example 3: Keep-alive and connection pools

User asks:
- keep-alive 和连接池到底怎么影响 Java 服务性能？

Expected response shape:
1. Explain connection reuse and its latency benefits.
2. Explain stale connections, timeout mismatch, and pool exhaustion risks.
3. Tie protocol behavior back to Java client configuration.
