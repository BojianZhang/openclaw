# Concurrency Troubleshooting Checklist

Use this checklist when a Java service shows race conditions, thread blockage, pool saturation, or concurrency-driven throughput collapse.

## 1. Identify the problem class

Classify first:
- wrong result or inconsistent state
- latency under concurrency
- thread pool saturation
- deadlock or thread blockage
- runaway async task growth

## 2. Confirm evidence

Collect what is available:
- thread dumps
- queue length and rejection signals
- pool size and active thread count
- latency under concurrency vs single-request behavior
- lock or contention evidence
- timeout and downstream dependency behavior

## 3. Separate correctness from capacity

Ask:
- is shared state wrong?
- or is work just piling up?
- or are blocking dependencies making threads wait?

## 4. Check shared-state design

Review:
- mutable shared objects
- compound updates without synchronization
- unclear ownership of state
- unsafe publication or stale-read patterns

## 5. Check thread-pool design

Review:
- workload type in each pool
- queueing strategy
- blocking calls in general-purpose pools
- retry loops or polling patterns

## 6. Change the smallest useful thing

Prefer:
- clearer state ownership
- narrower synchronization
- bounded async fan-out
- pool separation by workload type
- better timeout and backpressure rules
