# Slow Query Decision Guide

Use this guide when a Java service suffers from slow SQL or database-driven latency spikes.

## Typical root causes

- missing or ineffective index
- query shape causing large scans or sorts
- bad join pattern
- stale statistics or skewed data distribution
- transaction locking side effects
- too many round trips from application code

## First questions to answer

1. Is one query slow, or many queries slow?
2. Is the slowdown steady or traffic-dependent?
3. Did data volume or distribution change?
4. Is the latency in DB execution, lock wait, or connection acquisition?

## Evidence path

Minimum useful evidence:
- SQL text
- EXPLAIN plan
- rows examined or estimated
- lock wait information if applicable
- application timing around query call

## Likely fix directions

### If index is missing or weak
- add or adjust index
- verify leftmost prefix and selectivity
- avoid redundant overlapping indexes where write cost matters

### If query shape is poor
- reduce selected columns
- rewrite pagination or sorting path
- split overly broad query into safer pieces when necessary

### If locks dominate
- shorten transactions
- reorder writes consistently
- avoid long-running reads inside large transactions
- review isolation level and hot-row patterns

### If app pattern is the problem
- remove N+1 queries
- batch access
- cache carefully when read profile justifies it

## Caution

Quick triage shortcut:
- full scan in `EXPLAIN`: inspect predicates, composite-index order, and statistics
- index exists but query is still slow: inspect back-to-table cost, low selectivity, range scans, sort/group work, and temporary tables
- slowdown is occasional: inspect lock conflicts, large transactions, batch jobs, and connection-pool queueing
- app layer slows too: inspect thread pools and cache behavior, not just MySQL

Do not declare victory after improving average latency alone. Check tail latency and write-path regression too.
