# Java Performance Core

Use this file when the problem is broader than JVM flags and involves end-to-end Java performance behavior.

## Performance dimensions

Always distinguish:
- latency
- throughput
- CPU efficiency
- memory efficiency
- tail behavior under load

Optimizing one may hurt another.

## Common false assumptions

- High latency does not automatically mean GC.
- High CPU does not automatically mean business logic is efficient.
- More threads do not automatically mean more throughput.
- Lower average latency does not guarantee better tail latency.

## Priority order for investigation

1. Confirm the slow thing and when it happens.
2. Check whether the bottleneck is CPU, memory, lock contention, I/O, or downstream dependency.
3. Identify whether the issue is steady-state or burst-driven.
4. Tune only after narrowing the dominant factor.

## Practical levers

Depending on evidence, improvement may come from:
- reducing allocations
- batching or streaming differently
- limiting concurrency
- resizing pools correctly
- reducing serialization overhead
- improving cache hit behavior
- tuning JVM memory and collector settings

A reliable optimization loop is:
1. measure
2. form a hypothesis
3. validate with evidence
4. review whether the gain is real and worth the complexity

JVM flags are only one lever in the system.
