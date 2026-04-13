# Thread Pool and Future Guidance

Use this file when the problem involves executors, queueing, async task execution, `Future`, or `CompletableFuture` design.

## Core ideas

- Thread pools are capacity-management tools, not speed multipliers by default.
- Pool sizing depends on workload shape: CPU-bound, I/O-bound, blocking, bursty, or mixed.
- `CompletableFuture` helps composition, but can hide ownership, timeout, and failure-flow complexity.
- Queue growth is often a more useful signal than thread count alone.

## Practical reasoning

When diagnosing pool problems, ask:
- what kind of work runs in the pool?
- does the pool mix blocking and non-blocking tasks?
- is latency caused by queueing, contention, or downstream slowness?
- are async chains losing observability or timeout control?

## Warning

Do not increase pool size first when the real problem is blocking I/O, dependency slowness, or unbounded submission.
