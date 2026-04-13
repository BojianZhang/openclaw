# Microservice Call Patterns

Use this file when the issue is not just protocol mechanics but service-to-service communication design.

## Core ideas

- Every synchronous call adds latency and failure surface.
- Fan-out multiplies downstream variance.
- Retry without budget control creates cascading load.
- Observability is part of the design, not an afterthought.

## Practical reasoning

When reviewing call patterns, ask:
- how many hops are in the common path?
- what happens when one downstream call slows down?
- are timeouts nested sensibly?
- are retries bounded and visible?
- should some interaction be async instead of synchronous?

## Warning

Do not move coupling from code into chatty service networks and call that improvement.
