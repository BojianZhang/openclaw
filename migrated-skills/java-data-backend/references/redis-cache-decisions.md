# Redis Cache Decision Guide

Use this file when choosing cache strategy or diagnosing cache-related design tradeoffs.

## Core questions

Ask before designing cache behavior:
1. What data is expensive enough to cache?
2. How stale can the data be?
3. What happens if Redis is unavailable?
4. Is the access pattern uniform or hot-key heavy?
5. Is read amplification or write amplification the bigger problem?

## Common strategy choices

### Cache-aside
Use when:
- application controls reads and writes
- some staleness is acceptable
- simplicity matters

Risks:
- invalidation bugs
- race windows around write and delete

### Write-through or write-behind
Use when:
- cache must stay closer to write path
- consistency requirements are tighter

Risks:
- more operational complexity
- failure handling becomes more subtle

### TTL-based caching
Use when:
- exact freshness is not required
- content is naturally periodic or approximate

Risks:
- synchronized expiry storms
- stale windows if TTL is too long

## Failure patterns to defend against

### Penetration
- use null caching where safe
- validate bad keys early
- add rate limiting or bloom filters if justified

### Breakdown
- protect hot keys
- use refresh or mutex techniques when necessary
- avoid one key becoming the whole service bottleneck

### Avalanche
- randomize TTLs
- degrade gracefully
- avoid synchronized mass expiry

## Decision rule

Use Redis when there is real hotspot read pressure, acceptable bounded staleness, and a data-access pattern that benefits from caching.

Do not rush to Redis when the root cause is actually SQL shape, indexing, network latency, or thread-pool behavior.

Prefer the simplest strategy that satisfies freshness and load goals. Do not add cache complexity unless the backend pressure or latency profile justifies it.
