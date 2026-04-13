# Microservices Practice

Use this file when deciding whether to split services, how to define boundaries, or how to reason about service governance.

## Decision rule

Do not split because microservices sound modern. Split when change boundaries, team ownership, scaling needs, or operational isolation justify it.

## Core questions

Ask:
- what business capability is actually separate?
- what data ownership boundary exists?
- what deployment or scaling pain exists today?
- what operational cost will service splitting introduce?

## Common mistakes

- splitting too early
- creating chatty synchronous dependencies
- unclear ownership of shared data
- underestimating observability and failure-handling costs

## Practical guidance

- first ask whether the current pain is really an architecture problem or just a code-organization problem
- prefer clear business boundaries over technical layering boundaries
- keep synchronous calls limited and purposeful
- define timeout, retry, fallback, idempotency, and backpressure behavior intentionally
- design service interfaces to reduce coupling, not just move it across the network

## Strong reminder

A clear monolith is often a better intermediate target than premature microservice splitting.
