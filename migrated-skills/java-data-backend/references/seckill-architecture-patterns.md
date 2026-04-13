# Seckill Architecture Patterns

Use this file when the user is discussing flash-sale / seckill systems, high-concurrency e-commerce purchase flows, stock deduction pressure, Redis pre-checks, MQ async order handling, or anti-oversell design.

This reference is distilled from the user's 双11秒杀 demo materials and code.

## Why this sample matters

This project is not mainly about microservice splitting.
It is about high-concurrency transactional pressure around a single business event:
- login/session sharing
- goods list/detail pages
- seckill action
- order details
- pressure testing
- page/service optimization
- MQ-based async processing
- interface security
- rate limiting

That makes it ideal for backend data/concurrency architecture discussion.

## Core problem framing

The course material repeatedly frames seckill around three themes:
- **read pressure**: many users reading the same hot data
- **write pressure**: many users attempting the same stock deduction/order creation
- **protection**: preventing the system from collapsing under abnormal or abusive traffic

A good answer should not reduce seckill to "just use Redis".

## Common optimization layers shown in the sample

### 1. Distributed session / login handling
The materials explicitly include:
- distributed session
- user login
- shared session

Code signals:
- `UserArgumentResolver`
- `UserContext`
- cookie utilities
- login controller and user service

Interpretation:
- user identity/session extraction is moved out of repetitive controller plumbing
- request identity handling becomes infrastructure-like, not hand-written per endpoint

### 2. Page optimization and cache-first read path
The materials explicitly include:
- page optimization
- cache
- staticization / static-resource optimization

Config signals in code:
- aggressive static resource caching
- resource chain / compressed resource settings
- Thymeleaf usage with cache control choices

Interpretation:
- hot read paths should be reduced before users even hit the deepest dynamic path
- staticization and cache headers are part of seckill design, not cosmetic frontend tuning

### 3. Redis as hot-path coordination layer
Code signals:
- Redis config
- connection pool tuning
- likely stock/result/session use around seckill flow

Interpretation:
- Redis acts as a pressure absorber for hot-path state and quick checks
- in seckill discussion, Redis often sits in front of or alongside the relational write path

### 4. MQ as async order-processing buffer
Code signals:
- `MQSender`
- `MQReceiver`
- `SeckillMessage`
- RabbitMQ config with consumer concurrency/prefetch/retry

Interpretation:
- user request admission and final order processing are decoupled
- MQ is used to smooth write spikes and serialize business handling more safely
- prefetch and consumer concurrency are part of the throughput/backpressure story

### 5. Interface protection layer
Materials explicitly include:
- hidden seckill path
- captcha
- interface rate limiting

Code signals:
- `AccessLimit`
- `AccessLimitInterceptor`
- validation helpers

Interpretation:
- security is not only auth; it is traffic shaping and anti-abuse gating
- hidden paths, captcha, and rate limiting reduce invalid traffic before it reaches core stock logic

### 6. Pressure testing as design feedback
Materials explicitly include:
- JMeter introduction
- custom variables
- formal pressure testing

Interpretation:
- performance design is not theoretical; pressure testing is part of the architecture loop
- seckill optimization should be explained together with measurement, not as slogan-only design

## High-value architecture lessons

### Lesson 1: Seckill is a pipeline, not one SQL statement
A robust answer usually describes:
1. request entry and identity/session handling
2. anti-abuse / rate-limit / captcha checks
3. fast-path cache or Redis pre-check
4. async admission via MQ when needed
5. final order creation and stock confirmation
6. result polling or detail query

### Lesson 2: Read optimization and write optimization are different problems
- page/static/cache optimization reduces hot reads
- stock/order/MQ/Redis design handles hot writes

### Lesson 3: Protection logic is part of the architecture
Hidden paths, captcha, and interface rate limiting are not decorations. They are system-protection layers.

### Lesson 4: MQ should solve a visible spike-absorption problem
Do not answer as if RabbitMQ is mandatory for all shopping systems. In this sample it matters because a flash-sale write burst is the core problem.

## How to answer from this reference

Use when the user asks:
- how do you design a seckill/flash-sale system?
- why use Redis in seckill?
- why use MQ in seckill?
- how do you prevent oversell / collapse / abusive traffic?
- what does seckill optimization usually include besides inventory deduction?

A strong answer should:
1. define the pressure model (read/write/protection)
2. explain the admission path
3. explain Redis/MQ/security roles separately
4. mention pressure testing and result measurement

## Source notes

Distilled from the user's 双11秒杀 solution PDFs and `seckill-demo` codebase, including Redis, RabbitMQ, login/session sharing, page optimization, interface security, and pressure testing topics.
