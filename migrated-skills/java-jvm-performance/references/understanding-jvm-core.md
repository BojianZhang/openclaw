# JVM Core Concepts

Use this file when an explanation needs runtime fundamentals, not just tuning tips.

## Runtime areas to reason about

Focus on these practical buckets:
- heap: ordinary object storage
- thread stacks: method calls and per-thread execution state
- metaspace: class metadata
- code cache and native or direct memory when relevant

A good diagnosis names which memory area is under pressure before discussing OOM or tuning.

## Classloading matters too

Classloading issues often surface in containers, plugin systems, hot-reload paths, and dynamic-proxy-heavy frameworks. When the symptom is metaspace growth or startup inconsistency, inspect classloader behavior, not just heap charts.

## Heap thinking

The key questions are:
- how fast are objects allocated?
- how long do they survive?
- what proportion becomes long-lived?

Most GC problems are not about GC alone. They are about allocation and survival patterns.

## GC thinking

GC is a tradeoff system, not a magic cleanup button.

Reason about:
- pause time
- throughput impact
- collector suitability
- object lifetime distribution
- memory headroom

## Thread and runtime interaction

Performance symptoms often sit between JVM and code behavior:
- too many threads increase scheduling and stack memory costs
- lock contention inflates latency without obvious memory pressure
- thread pool mis-sizing can look like JVM slowness

## Evidence-first rule

When explaining JVM issues, always connect theory to observable signals:
- heap chart
- pause chart
- CPU trend
- thread state
- latency metrics

Theory without evidence is guesswork.
