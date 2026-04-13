# InnoDB Core

Use this file when explanation needs storage-engine fundamentals.

## Key ideas

- Index organization affects lookup cost.
- Transactions and isolation are performance topics, not only correctness topics.
- MVCC improves concurrency, but does not remove all lock or history costs.
- Long transactions create pressure beyond their own business logic.

## Practical reasoning

When diagnosing InnoDB behavior, think about:
- primary key and secondary index access paths
- clustered index vs secondary index lookup cost
- lock duration
- transaction scope
- hot-row contention
- write amplification from schema or index choices
- redo, undo, and MVCC costs when transaction behavior is heavy
