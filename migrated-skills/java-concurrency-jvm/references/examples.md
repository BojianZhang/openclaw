# Examples

## Example 1: Visibility vs mutual exclusion

User asks:
- `volatile` 和 `synchronized` 到底怎么选？

Expected response shape:
1. Distinguish visibility from mutual exclusion.
2. Explain that `volatile` does not make compound updates atomic.
3. Recommend the simplest safe primitive for the real shared-state pattern.

## Example 2: Thread pool misuse

User asks:
- 线程池开大一点是不是就更快？

Expected response shape:
1. Push back on thread-count folklore.
2. Explain queueing, blocking, context switching, and resource contention.
3. Recommend sizing by workload type, not optimism.

## Example 3: Async orchestration confusion

User asks:
- `CompletableFuture` 写起来很灵活，但为什么系统更难排查了？

Expected response shape:
1. Explain async composition complexity.
2. Point out observability, timeout propagation, and error-handling risks.
3. Recommend bounded async structure instead of uncontrolled chaining.
