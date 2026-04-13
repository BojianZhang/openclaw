# MySQL Index Q&A

## Why does MySQL ignore an index?

Possible reasons:
- the index is not selective enough
- the query shape defeats index usage
- a function or transformation is applied to the indexed column
- the optimizer estimates a scan as cheaper
- the predicate does not align with the leftmost prefix of a composite index

## Is more indexing always better?

No. Extra indexes increase write cost, storage usage, and maintenance overhead. Add indexes for real query patterns, not for aesthetic completeness.

## How should I think about composite indexes?

Think in terms of actual filter and sort order. The best composite index matches the common access pattern, not just all columns involved.

## Why can a query still be slow even with an index?

Because slowness may come from:
- poor selectivity
- sorting or temporary tables
- join expansion
- row lookup cost after index scan
- lock waits
- returning too much data

## How should I design an index?

Design around the real access pattern, not the table structure alone. Start from the common filters, sort order, grouping pattern, and whether covering the query is worth the write cost.
