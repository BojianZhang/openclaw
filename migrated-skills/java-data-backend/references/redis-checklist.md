# Redis Troubleshooting Checklist

Use this checklist when cache latency rises, hit ratio drops, memory pressure appears, or cache consistency problems affect a Java service.

## 1. Classify the main problem

Common categories:
- cache miss rate too high
- hot key pressure
- memory pressure or eviction
- stale data
- penetration, breakdown, or avalanche
- timeout or connection issues

## 2. Confirm evidence

Collect:
- hit ratio trend
- key eviction signals
- memory usage trend
- command latency
- hot key or big key evidence
- application timeout and retry behavior
- cache read/write traffic pattern

## 3. Check key and data design

Review:
- key naming and namespace
- key cardinality
- TTL policy
- object size
- whether large payloads are being serialized repeatedly

## 4. Check failure patterns

Ask:
- is the problem caused by cache misses or cache invalidation bugs?
- are many keys expiring together?
- is one hot key dominating traffic?
- is the app amplifying load through retries?
- is this really a Redis problem, or is SQL, network, or thread-pool behavior being misdiagnosed as cache pain?

Common failure classes to name explicitly:
- penetration
- breakdown
- avalanche
- stale-data inconsistency

## 5. Check consistency strategy

Review:
- cache-aside or write-through style
- invalidation timing
- double-write ordering
- acceptable stale window
- fallback behavior during cache failure

## 6. Check Java integration issues

Possible causes:
- serializer overhead
- connection pool saturation
- timeout settings too aggressive or too lax
- missing local protection for hot keys
- no degradation path when Redis is unhealthy

## 7. Apply smallest useful fix

Prefer:
- targeted TTL adjustment
- hot key protection
- invalidation correction
- payload reduction
- fallback or rate-limiting improvement

## 8. Recheck impact

Measure:
- hit ratio
- latency
- eviction rate
- backend database pressure
- stale-data risk
