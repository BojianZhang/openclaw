# Redis Core

Use this file when explanation needs cache and Redis mechanism fundamentals.

## Key ideas

- Redis is fast because it keeps operations simple and memory-resident, but memory is finite and operational tradeoffs matter.
- Cache design is mostly about traffic shape, staleness tolerance, and failure handling.
- Hot keys, big keys, serializer overhead, and expiry behavior often dominate real-world issues.

## Practical reasoning

When diagnosing Redis-backed systems, think about:
- access skew
- key and data-structure fit for the business scenario
- TTL distribution
- fallback pressure on the database
- payload size
- timeout and retry amplification
- eviction and memory-policy side effects
