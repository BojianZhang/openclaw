---
name: java-jvm-performance
description: Analyze and improve Java JVM runtime behavior and application performance with evidence-first diagnosis. Use when diagnosing or optimizing GC, OOM, Full GC, heap or non-heap memory, JVM parameters, CPU spikes, latency, throughput, profiling signals, dump analysis, or runtime bottlenecks in backend services. Prefer this skill when the primary question is runtime symptoms and observability evidence; prefer `java-concurrency-jvm` when the primary question is JMM semantics, lock design, shared-state correctness, thread coordination, or CompletableFuture / executor usage.
---

# Java JVM Performance

## Goal

Diagnose and improve JVM runtime behavior with evidence-first analysis. Focus on memory, GC, JVM parameters, latency, throughput, runtime symptoms, and practical troubleshooting in Java backend services.

## Scope

In scope:
- GC behavior and collector tradeoffs
- OOM, memory pressure, heap and metaspace issues
- Full GC diagnosis
- JVM tuning basics and parameter reasoning
- performance bottleneck analysis driven by metrics, dumps, traces, or profiling
- CPU spikes, latency jitter, throughput collapse, and allocation pressure
- thread blockage or contention when it appears as a runtime performance symptom
- observability signals for CPU, memory, GC, threads, and latency

Out of scope unless directly relevant:
- JMM semantics, lock design, or shared-state correctness as the main topic
- MySQL and Redis deep tuning
- Spring Boot layering and code structure refactoring
- transport-layer HTTP/TCP diagnosis without JVM-side runtime evidence

## Workflow

1. Clarify the symptom: slow response, high CPU, frequent GC, OOM, startup memory issue, thread blockage, or throughput drop.
2. Separate signal from guesswork. Ask what metrics, logs, dumps, traces, or monitoring evidence exist.
3. Identify which runtime area is most likely involved: heap, GC, threads, native memory, allocation rate, blocking, or CPU hot paths.
4. Prefer diagnosis before parameter tweaking.
5. Explain tradeoffs when suggesting tuning changes.
6. Recommend small controlled changes instead of broad JVM flag dumps.
7. If the real core is concurrency semantics, executor design, or shared-state coordination, hand off to `java-concurrency-jvm`.

## When To Read References

- Read `references/jvm-checklist.md` for structured troubleshooting.
- Read `references/jvm-oom-and-fullgc.md` for OOM and heavy GC scenarios.
- Read `references/jvm-tuning-qa.md` for reusable tuning Q&A patterns.
- Read `references/understanding-jvm-core.md` for core runtime concepts.
- Read `references/java-performance-core.md` when performance analysis extends beyond GC.
- Read `references/java-performance.md` for deeper optimization guidance.
- Read `references/java-vm-in-practice.md` when the user needs an additional runtime-oriented deep summary beyond the core checklist and QA materials.
- Read `references/understanding-the-jvm.md` when the user needs a broader conceptual deep summary to pair with practical runtime diagnosis.
- Read `references/concurrency-jvm-qa.md` when performance symptoms intersect with locking, thread pools, or concurrency behavior.
- Read `references/examples.md` when the user needs concrete diagnosis or tuning response patterns.
- Read `references/anti-patterns.md` when guarding against evidence-free tuning or oversized flag dumps.

## Output Expectations

When answering:
1. Name the likely runtime problem.
2. List the minimum evidence needed.
3. Give the most likely causes in priority order.
4. Suggest a stepwise diagnosis path.
5. Recommend the smallest safe tuning or remediation changes.
6. Mention tradeoffs and rollback considerations.

Prefer evidence-driven tuning over folklore.
