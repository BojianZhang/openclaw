# Seckill Write-Path Patterns

Use this file when the user needs deeper reasoning about the write path in a flash-sale / seckill system: stock deduction pressure, anti-oversell controls, Redis pre-checks, MQ admission, idempotency, and final order persistence.

This reference complements `seckill-architecture-patterns.md` by focusing specifically on the hot write path.

## Why the write path is the hard part

In seckill systems, the hardest moment is not page display but the instant many users attempt the same stock-consuming action.
A good explanation should separate:
- request admission
- stock judgment
- duplicate-order prevention
- order creation
- final consistency handling

## Canonical write-path model

A practical explanation path is:
1. user request arrives with validated identity/session
2. security/protection checks happen first (hidden path, captcha, rate limit)
3. fast stock / repeat-purchase pre-check happens in Redis or equivalent fast path
4. accepted request is queued or marked for asynchronous handling
5. consumer or controlled handler executes order creation and stock persistence logic
6. user queries result / order detail later

The key idea: not every request should become an immediate synchronous database write.

## Pattern 1: Fast reject before expensive write

Use when discussing why Redis matters.

Core idea:
- reject obviously invalid requests early
- avoid letting every request fall through to DB stock deduction logic

Typical fast-reject reasons:
- no stock left
- user already purchased
- request frequency too high
- invalid path/captcha/session

Good explanation:
- Redis is often used here because the cost of a quick reject is far lower than a full transactional write attempt

## Pattern 2: Duplicate purchase prevention

A seckill answer should mention duplicate-order prevention explicitly.

Typical reasoning:
- after user identity is confirmed, the system must avoid one user repeatedly creating the same seckill order
- this can be checked in a fast path first, then confirmed in persistent storage/order records

Do not answer only with "lock". The real issue is repeat purchase semantics, not only mutual exclusion wording.

## Pattern 3: Async admission with MQ

Use when the question becomes "why use MQ in seckill".

Core idea:
- decouple user request admission from heavy order persistence
- transform burst writes into controllable downstream throughput

A practical answer should mention:
- MQ smooths spikes
- consumer throughput can be controlled
- user may receive a pending/queued result rather than immediate success
- order creation becomes part of a managed backend pipeline

Do not present MQ as magic. It introduces eventual consistency, retry, and duplicate-consumption concerns.

## Pattern 4: Final order persistence and stock confirmation

The write path usually still needs a final authoritative persistence step.
Even when Redis or MQ stands in front, the system still needs:
- stock confirmation / deduction in persistent storage
- order record creation
- duplicate-order confirmation
- failure handling and result status

Good explanation:
- Redis and MQ reduce pressure and shape traffic
- they do not replace the need for final authoritative business records

## Pattern 5: Idempotency and repeat consumption awareness

Once MQ enters the path, idempotency matters more.
A strong answer can say:
- message delivery or consumer retry can cause repeated handling attempts
- order creation and stock deduction logic need idempotent guards
- user-order uniqueness and processing-state checks help prevent repeated effects

Even if the sample project does not implement every advanced guard in a textbook-perfect way, the interview answer should show awareness.

## Pattern 6: Result query instead of synchronous certainty

A realistic seckill system often shifts the user experience from:
- "I click and get final success instantly"
to
- "I click, the request is admitted, then I query or receive final result"

This is important because asynchronous admission changes API contract expectations.

## Anti-oversell answer framing

When asked "how do you prevent oversell?", a good restrained answer is:
1. reduce invalid requests before they touch the core write path
2. pre-check stock and duplicate-purchase conditions in a fast path
3. use queued/controlled order handling when burst pressure is high
4. keep final stock/order persistence authoritative
5. add idempotent and duplicate-order guards around the final write path

Avoid claiming perfect zero-risk oversell prevention unless the system design truly justifies it.

## Common mistakes in seckill answers

### Mistake 1: saying "just use Redis"
Redis is one layer, not the whole write path.

### Mistake 2: saying "just use MQ"
MQ smooths spikes but does not itself solve final consistency.

### Mistake 3: ignoring duplicate-user purchase control
Repeat-order semantics matter as much as raw stock count.

### Mistake 4: ignoring result-query design
Async admission changes what the frontend/user can expect immediately.

## Output guidance

When answering:
1. describe the write path as a sequence
2. separate pre-check, queueing, and final persistence
3. explain where oversell risk is reduced
4. explain where idempotency becomes necessary
5. avoid claiming stronger guarantees than the design actually provides

## Source notes

Distilled from the user's 双11秒杀 materials and `seckill-demo` code signals such as Redis config, RabbitMQ sender/receiver, `SeckillMessage`, access limiting, login/session handling, and order/seckill controllers.
