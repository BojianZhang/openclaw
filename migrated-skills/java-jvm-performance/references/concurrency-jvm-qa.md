# Concurrency and JVM Q&A

## Can thread problems look like JVM problems?

Yes. Thread pool exhaustion, lock contention, blocked I/O, or runaway task submission can create latency, CPU pressure, and memory pressure that look like JVM tuning issues.

## When should I suspect thread contention?

Suspect contention when:
- CPU is high but useful throughput does not rise
- many threads sit in BLOCKED or WAITING states
- latency spikes under concurrency, not under single-request tests
- request queues grow while heap looks normal

## Does increasing thread count always improve throughput?

No. Extra threads can increase context switching, stack memory usage, contention, and queueing overhead. More threads often make a saturated system noisier, not faster.

## How do I separate GC pain from lock pain?

Look for:
- GC pause timing vs request latency timing
- thread dump evidence of contention
- CPU hotspot location
- queue growth and rejection patterns

If latency spikes without matching GC pause evidence, look harder at concurrency and downstream blocking.

## What is the practical difference between volatile and synchronized?

`volatile` mainly helps visibility and ordering for simple shared state. `synchronized` provides both mutual exclusion and visibility boundaries. Compound operations like `count++` still need real synchronization or atomic structures.
