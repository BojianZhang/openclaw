# Examples

## Example 1: Slow query diagnosis

User asks:
- 这个列表接口越来越慢，怀疑是 MySQL 慢查询，先怎么排？

Expected response shape:
1. Separate DB latency from application latency.
2. Ask for SQL text, EXPLAIN, rows examined, and traffic shape.
3. Explain likely causes: scan, sort, join, lock wait, or N+1 access.
4. Suggest the smallest likely fix first.

## Example 2: Redis consistency concern

User asks:
- 更新数据库以后再删缓存，这种方案会不会有脏数据？

Expected response shape:
1. Explain cache-aside consistency tradeoff.
2. State that perfect consistency is uncommon.
3. Discuss invalidation ordering, retries, and stale window.
4. Recommend a bounded-risk design, not a magical guarantee.

## Example 3: Index choice

User asks:
- 这个查询条件有 4 个字段，索引应该怎么建？

Expected response shape:
1. Start from real access pattern, not column count alone.
2. Consider filter order, selectivity, sort order, and write cost.
3. Warn against blind over-indexing.
4. Recommend validating with execution plan.
