---
name: java-concurrency-jvm
description: Explain and troubleshoot Java concurrency semantics, thread coordination, memory visibility, synchronization, AQS-based primitives, thread pools, and CompletableFuture orchestration. Use when working on Java multithreading, JMM, lock behavior, deadlock, race conditions, shared-state correctness, executor design, or async coordination problems. Prefer this skill for concurrency model and correctness questions; prefer `java-jvm-performance` when the primary question is runtime metrics, GC, OOM, CPU, latency, or evidence-driven performance diagnosis.
---

# Java Concurrency JVM

## Goal

Explain, review, and troubleshoot Java concurrency behavior with emphasis on thread coordination, memory visibility, locking, thread-pool usage, async execution, and practical concurrency design.

## Scope

In scope:
- Java Memory Model basics
- `synchronized`, `volatile`, CAS, and AQS-style primitives
- thread safety and shared-state reasoning
- deadlock, race condition, visibility, ordering, and atomicity issues
- lock contention and coordination issues
- thread pools and async execution patterns
- `Future` and `CompletableFuture` usage tradeoffs
- concurrency design mistakes that affect correctness or coordination
- thread-model and executor-model design problems

Out of scope unless directly relevant:
- GC-heavy JVM tuning as the main topic
- OOM, Full GC, heap sizing, metaspace, or profiling-led performance diagnosis
- MySQL or Redis optimization
- Spring Boot project structure without concurrency focus
- HTTP/TCP timeout chains or transport-layer failure analysis

## Workflow

1. Clarify whether the user needs concept explanation, bug diagnosis, correctness reasoning, or concurrency design advice.
2. Separate correctness problems from throughput symptoms.
3. Name the likely concurrency layer first: shared state, visibility, ordering, locking, pool sizing, blocking I/O in the wrong executor, or async orchestration.
4. Prefer simple and explicit concurrency reasoning over clever abstractions.
5. Explain tradeoffs before recommending more threads, more async work, or more coordination primitives.
6. If the primary issue is runtime evidence such as GC, CPU, heap pressure, latency, or dumps, hand off to `java-jvm-performance`.

## When To Read References

Read `references/concurrency-foundations.md` when the user needs simpler foundation-level explanations before heavier concurrency analysis.
Read `references/concurrency-core.md` for chapter-level concurrency fundamentals and terminology.
Read `references/java-concurrency-in-practice.md` when the user needs a fuller deep-summary background beyond the lighter foundations and QA material.
Read `references/intro-java-multithreading.md` when the user needs a simpler deep-summary bridge from concurrency basics into heavier reasoning.
Read `references/jmm-and-sync.md` when the problem needs visibility, ordering, atomicity, or synchronization reasoning.
Read `references/thread-pool-and-future.md` when the issue involves executors, queueing, `Future`, or `CompletableFuture` design.
Read `references/concurrency-checklist.md` for troubleshooting under contention, blocking, or thread-pool saturation.
Read `references/concurrency-qa.md` for reusable concise answers to common concurrency questions.
Read `references/examples.md` for concrete explanation and troubleshooting response patterns.
Read `references/anti-patterns.md` when guarding against over-threading, misuse of `volatile`, or overly loose async design.

## Output Expectations

When answering:
1. State the concurrency problem clearly.
2. Explain the relevant mechanism.
3. Point out the likely failure or contention source.
4. Recommend the smallest safe improvement.
5. Mention correctness and observability risks when relevant.

Prefer concurrency-model clarity over generic performance folklore.
