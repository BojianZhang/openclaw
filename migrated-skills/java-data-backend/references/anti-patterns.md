# Anti-Patterns

## Do not optimize SQL without execution evidence

Always prefer EXPLAIN, latency, row-scan evidence, and lock context over guesswork.

## Do not add indexes blindly

Indexes improve some reads while increasing write and storage cost.

## Do not use Redis as a hand-wavy performance fix

Cache design must state freshness, invalidation, and failure behavior clearly.

## Do not ignore application-side causes

Connection pools, ORM query shape, retries, and chatty repository usage often dominate the issue.

## Do not promise perfect consistency casually

Be explicit about stale windows, invalidation ownership, and failure tradeoffs.
