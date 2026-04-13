# OOM and Full GC Decision Guide

Use this guide when the service shows OutOfMemoryError, repeated Full GC, long GC pauses, or heap pressure symptoms.

## Scenario 1: Repeated Full GC with no OOM yet

Possible causes:
- old generation retention pressure
- allocation bursts faster than reclamation
- oversized caches or in-memory buffers
- large batch processing windows
- too-small heap for traffic shape

What to check first:
- old gen occupancy trend
- object survival pattern
- whether Full GC recovers enough space
- GC pause frequency and duration
- whether latency drops only during low traffic

Likely direction:
- reduce retention
- reduce allocation bursts
- review cache sizes
- verify heap sizing and collector fit

## Scenario 2: Java heap space OOM

Possible causes:
- true memory leak
- expected working set larger than heap
- unbounded collection or cache
- request fan-out creating too many live objects
- deserialization or batch object explosion

What to check first:
- heap dump
- dominator tree
- top retained object graphs
- whether retained objects are business data, cache entries, or framework artifacts

Likely direction:
- fix retention path
- cap data structures
- stream or batch differently
- resize heap only after understanding retention

## Scenario 3: Metaspace OOM

Possible causes:
- dynamic class generation growth
- classloader leak
- repeated hot reload behavior
- proxy generation accumulation

What to check first:
- class count trend
- classloader retention
- framework or plugin behavior

Likely direction:
- fix classloader lifecycle
- reduce dynamic generation churn
- resize metaspace only as a secondary move

## Scenario 4: Container killed before JVM OOM

Possible causes:
- off-heap or native memory growth
- direct buffers
- thread stacks
- container limit smaller than JVM assumptions

What to check first:
- container memory limit
- RSS vs heap usage
- direct memory settings
- thread count

Likely direction:
- align JVM sizing with container limits
- review native memory usage
- reduce thread count or direct buffers if needed

## Decision rule

If Full GC or OOM appears, do not jump straight to larger heap.

Ask first:
1. Is memory retained unexpectedly?
2. Is allocation rate the real problem?
3. Is environment sizing mismatched?
4. Is workload shape the root cause?

Quick triage shortcut:
- Full GC stays high after reclaim: suspect retention, leak, or oversized caches
- Traffic spike causes jitter: inspect allocation bursts, thread pools, batch jobs, and cache behavior
- Metaspace OOM: inspect classloading, dynamic proxies, and hot-reload patterns
- Too many threads: inspect pool sizing, blocking waits, and stuck external calls

Heap increase can hide the symptom without fixing the cause.
