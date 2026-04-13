# Anti-Patterns

## Do not add threads as a default fix

More threads often increase contention, queueing noise, and resource pressure.

## Do not confuse visibility with atomicity

`volatile` is not a substitute for real synchronization of compound actions.

## Do not overcomplicate async flows

If async composition makes ownership, timeout, and failure handling unclear, the design is probably too loose.

## Do not explain concurrency only in theory

Always connect JMM, locks, and pools back to actual Java code paths and runtime symptoms.
