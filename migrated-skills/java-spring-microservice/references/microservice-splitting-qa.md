# Microservice Splitting Q&A

## When should I split a service?

Split when business ownership, scaling behavior, deployment cadence, or fault isolation clearly benefit. Do not split because a codebase merely feels large.

## What is the biggest mistake in splitting?

Moving coupling from code into network calls. If the new services still need constant synchronous coordination, you may have redistributed the monolith without improving it.

## Should each service own its own database?

Prefer clear data ownership. Shared database access across many services usually hides boundary problems and makes evolution harder.

## Is synchronous RPC always bad?

No. It is bad when overused, chatty, or unsupported by timeout, retry, and fallback discipline.

## What is the first question before splitting?

Ask whether the main pain is team or deployment scale, or whether the real problem is still unclear boundaries inside a monolith. If the latter is true, clean up the monolith first.
