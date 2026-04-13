# JVM Tuning Q&A

## When should I tune the JVM?

Tune only when there is evidence of runtime pain such as high pause times, frequent Full GC, OOM risk, poor throughput, or memory-pressure symptoms. Do not tune because a flag set looks "more advanced."

## Is increasing heap always the first fix?

No. A larger heap may reduce GC frequency, but it can also increase pause cost and hide retention problems. Diagnose allocation and retention first.

## How should I think about GC tuning?

Treat GC tuning as a workload fit problem:
- What is the allocation rate?
- How long do objects live?
- Is latency or throughput more important?
- Are pauses rare but long, or frequent but short?

Pick changes that match the workload, not internet folklore.

## What evidence matters most before tuning?

The minimum useful evidence usually includes:
- heap usage trend
- GC log behavior
- pause distribution
- CPU trend
- request latency trend
- thread or lock symptoms if relevant

## How do I reason about high latency?

Do not assume GC first. High latency may come from:
- lock contention
- thread pool exhaustion
- downstream I/O
- serialization overhead
- logging overhead
- CPU saturation
- GC pauses

Find which of these dominates before tuning.

## What is a safe tuning style?

Safe tuning means:
- one meaningful change at a time
- measurable before/after comparison
- rollback path
- no cargo-cult flag bundles

## When should I ask for heap dump or thread dump?

Ask for a heap dump when retention, OOM, or unexplained memory growth is central.
Ask for thread dumps when latency, thread blockage, deadlock, or CPU hotspots suggest concurrency or blocking issues.

## Where should JVM tuning start?

Start by separating JVM-local symptoms from non-JVM causes such as database latency, downstream network calls, or thread-model problems. Use the checklist and runtime evidence before touching flags.
