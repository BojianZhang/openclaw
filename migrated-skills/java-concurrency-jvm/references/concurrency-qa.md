# Concurrency Q&A

## When should I use `volatile`?

Use `volatile` for simple shared state where visibility matters and compound atomic updates are not required.

## When should I use `synchronized`?

Use `synchronized` when both mutual exclusion and visibility are required around shared mutable state.

## Is `CompletableFuture` always better than blocking code?

No. It is better only when asynchronous composition is justified and still observable, bounded, and maintainable.

## Does a larger thread pool always improve throughput?

No. More threads can increase queueing noise, context switching, lock contention, and downstream pressure.

## What is the first question in concurrency debugging?

First ask whether the problem is state correctness, contention, pool capacity, or blocking dependency behavior.
