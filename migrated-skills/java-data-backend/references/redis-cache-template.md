# Redis Cache Template

Use this template pattern when introducing or reviewing Redis caching in a Java service.

## Intent

Add caching without hiding consistency assumptions.

## Structure guidance

- Keep cache ownership explicit.
- Name keys predictably.
- Centralize TTL and invalidation policy.
- Define fallback behavior for cache miss and cache outage.

## Practical rules

- Do not let cache access scatter across unrelated classes.
- Avoid silent stale-data behavior.
- Protect hot keys when traffic is bursty.
- Monitor hit ratio and backend load together.
- Prefer database write followed by cache invalidation over naive direct double-write in common cache-aside flows.
