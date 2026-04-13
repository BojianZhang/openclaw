# Seckill Cache and Protection Patterns

Use this file when the user is asking about hot-read reduction, page optimization, distributed session, hidden paths, captcha, access limiting, or how to protect a seckill system before the write path is even reached.

This reference complements `seckill-architecture-patterns.md` and `seckill-write-path-patterns.md` by focusing on pre-write protection and read-side optimization.

## Why this layer matters

Many seckill failures happen before inventory logic becomes the problem.
If the system allows too many wasteful or abusive requests through, the core write path is overwhelmed no matter how carefully stock deduction is designed.

## Pattern 1: Shared login/session as infrastructure

The materials explicitly include distributed session and shared session.
Code signals include:
- `UserArgumentResolver`
- `UserContext`
- cookie utilities
- login/user controllers and services

Interpretation:
- login/session extraction is treated as reusable infrastructure
- request handlers do not repeatedly parse identity by hand
- user context becomes a prerequisite for protected purchase paths

## Pattern 2: Hot-read reduction via page and resource optimization

The materials explicitly include:
- page optimization
- cache
- staticization / static resource separation

Config signals include:
- static resource cache settings
- compressed resource support
- Thymeleaf cache control choices

Interpretation:
- not every request should render dynamic pages from scratch
- static/resource-layer tuning is part of seckill architecture because it reduces wasteful hot reads

## Pattern 3: Hidden seckill path

A good answer should mention hidden-path style gating.
Purpose:
- reduce naive scripted abuse
- avoid exposing the hottest action endpoint as a predictable fixed address

Important nuance:
- hidden path is a friction layer, not a complete security solution

## Pattern 4: Captcha as anti-abuse gate

Captcha matters when the project needs to distinguish normal users from large-scale scripted traffic.
In a seckill context, it helps protect the hottest path before the order pipeline is flooded.

Important nuance:
- captcha improves protection but increases user friction
- use it where attack risk justifies the cost

## Pattern 5: Access limiting / rate limiting

Code signals include:
- `AccessLimit`
- `AccessLimitInterceptor`

Interpretation:
- some request-rate policy is enforced before the core business action proceeds
- this is an admission-control layer, not merely a logging feature

A strong answer should explain:
- rate limiting protects the system from repeated abuse and accidental storms
- it should be applied before deep business handling where possible

## Pattern 6: Fast failure is part of user-experience design

In seckill systems, fast rejection can be better than slow uncertain waiting.
Examples:
- no stock
- invalid request
- too frequent request
- not logged in / invalid session

This is not only system protection; it is also user-path clarity under pressure.

## Layered protection model

A clean layered answer can be:
1. user identity/session layer
2. hidden path / captcha layer
3. access limiting layer
4. cache/static/hot-read reduction layer
5. fast stock/repeat check layer
6. async write pipeline layer

This shows the user understands that protection happens in multiple rings.

## Common mistakes

### Mistake 1: jumping straight to DB stock deduction
That skips all the pre-write protection layers.

### Mistake 2: treating cache only as performance tuning
In seckill, cache and staticization are part of admission protection too.

### Mistake 3: treating captcha or hidden paths as sufficient alone
They help, but they do not replace limiters, session control, and backend protection.

## Output guidance

When answering:
1. separate read optimization from write optimization
2. explain how protection reduces invalid traffic before the hot path
3. mention both user experience and system stability
4. position hidden paths/captcha/rate limit as layered safeguards, not silver bullets

## Source notes

Distilled from the user's 双11秒杀 PDFs and code signals including static-resource config, distributed session/login handling, `AccessLimit` interception, and security/optimization topics.
