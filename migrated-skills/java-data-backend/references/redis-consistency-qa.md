# Redis Consistency Q&A

## Can cache and database be perfectly consistent?

Usually not in normal application design. Most systems choose bounded inconsistency with clear invalidation rules and failure handling.

## What is the most common mistake in cache consistency?

Assuming cache invalidation is trivial. Ordering bugs, retries, concurrent writes, and delayed deletes often create stale reads.

## Should I delete cache before or after database write?

In many cache-aside designs, update the database first, then invalidate cache. But the real answer depends on concurrency, retry behavior, and stale-read tolerance.

## When is stale data acceptable?

When the business can tolerate a short stale window and the performance gain is worth it. Be explicit about the acceptable window instead of pretending it is zero.

## How do I reduce stale-read risk?

Use:
- clear invalidation ownership
- bounded TTL
- idempotent write flow where possible
- retry logic that does not amplify inconsistency
- hot-key protection where concurrent refresh is likely

## Why do systems get more complicated after adding Redis?

Because cache improves performance by introducing new moving parts: invalidation, warm-up, TTL policy, hot-key protection, eviction behavior, and consistency tradeoffs. Faster systems are often more operationally complex.
