# MySQL Troubleshooting Checklist

Use this checklist when a Java backend shows slow SQL, lock waits, high database latency, unstable throughput, or transaction anomalies.

## 1. Identify the dominant symptom

Classify the problem first:
- single slow query
- many queries slowed at once
- lock wait or deadlock
- CPU pressure on MySQL
- replication delay if relevant
- timeout from application side

## 2. Confirm evidence

Collect what is available:
- slow query log
- execution plan
- query text with parameters
- row counts and cardinality assumptions
- lock wait information
- database CPU, IOPS, and buffer pool metrics
- application latency metrics

Do not optimize SQL blindly without plan or workload evidence.

## 3. Check query shape

Review:
- full table scans
- wrong join order
- functions applied on indexed columns
- range conditions and sorting
- pagination style
- N+1 query behavior from application code
- whether `WHERE`, `ORDER BY`, and `GROUP BY` align with the intended index order
- whether temporary tables, filesort, or heavy back-to-table lookups dominate cost

## 4. Check indexing assumptions

Ask:
- does an appropriate index exist?
- is the index selective enough?
- is the query using leftmost prefix correctly?
- are stats stale or distribution skewed?

## 5. Check transaction and locking behavior

Review:
- transaction duration
- lock hold time
- gap locks or next-key locking where relevant
- isolation level choice
- hot rows or hot keys

## 6. Separate DB issues from app issues

Possible app-side causes:
- connection pool saturation
- excessive retry logic
- ORM-generated inefficient SQL
- too-chatty data access patterns
- transaction scope too broad

## 7. Fix smallest high-impact cause first

Prefer:
- query rewrite
- index correction
- narrowing transaction scope
- reducing row scans
- batching or caching where justified

## 8. Measure after change

Check:
- latency improvement
- rows examined
- lock wait reduction
- CPU or IOPS impact
- regression risk for write path
