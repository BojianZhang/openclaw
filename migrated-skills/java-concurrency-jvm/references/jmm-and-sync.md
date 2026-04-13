# JMM and Synchronization

Use this file when a question needs Java Memory Model reasoning rather than only API-level advice.

## Core ideas

- Visibility, ordering, and atomicity are different concerns.
- `volatile` helps visibility and ordering for simple shared state, but does not make compound actions atomic.
- `synchronized` provides both mutual exclusion and visibility boundaries.
- CAS-style primitives reduce some lock usage, but they do not eliminate contention or complexity.

## Practical reasoning

When diagnosing concurrency behavior, ask:
- is shared state mutable?
- do multiple threads update the same value?
- is the issue visibility, mutual exclusion, ordering, or contention?
- would a simpler confinement strategy remove the problem entirely?

## Warning

Do not start with low-level primitives if the real fix is reducing shared mutable state.
