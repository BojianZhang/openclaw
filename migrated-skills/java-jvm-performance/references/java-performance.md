# Deeper Performance Guidance

Use this file when a user needs more than quick diagnosis and wants a structured path to ongoing performance improvement.

## Evidence ladder

Prefer this sequence:
1. metrics
2. logs
3. GC data
4. thread dumps
5. profiler output
6. heap dump when memory retention is suspected

Each deeper artifact should answer a specific question.

## Tune by bottleneck class

### Memory-bound
Focus on:
- allocation pressure
- object retention
- cache sizing
- collector fit

### CPU-bound
Focus on:
- hotspot methods
- lock contention
- serialization and parsing
- unnecessary retries or polling

### Concurrency-bound
Focus on:
- thread pool saturation
- queue growth
- blocking calls in shared pools
- lock granularity

### I/O-bound
Focus on:
- downstream dependencies
- connection pool sizing
- timeout and retry amplification

## Stop conditions

Stop tuning when:
- the dominant pain is removed
- the next gains are marginal
- complexity rises faster than performance benefit
- the system meets practical latency and throughput targets

Keep perspective on optimization order. In many real systems, architecture, database, cache, I/O, and lock contention improvements return more value than syntax-level micro-optimization.

Performance work should end with clearer evidence and simpler operating assumptions, not just a longer JVM flag string.
