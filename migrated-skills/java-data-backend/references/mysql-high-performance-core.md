# MySQL High Performance Core

Use this file when explanation needs mechanism-level guidance for MySQL performance.

## Core ideas

- Query shape matters as much as indexing.
- Rows examined matters more than SQL looking short.
- Read and write tradeoffs matter when adding indexes.
- Tail latency often comes from scans, sorts, joins, and lock waits, not just average CPU.

## Investigation order

1. Understand the access pattern.
2. Check execution plan.
3. Check row volume and selectivity.
4. Check locking and transaction scope.
5. Check whether the app is causing chatty access.

Remember the practical hierarchy:
- SQL shape and access path usually matter before parameter tuning
- indexing is about query patterns, not column collection
- replication, sharding, and caching are not substitutes for basic query correctness
