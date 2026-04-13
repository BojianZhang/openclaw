# Microservice Project Evolution Sample

Use this file when the user is asking not just about isolated Spring Cloud components, but about how a teaching or real-world microservice project grows version by version.

This reference is distilled from the user's 乐Z家 project snapshots across multiple numbered stages.

## Why this sample matters

Unlike component-only demos, this project shows a more realistic growth pattern:
- shared base modules appear first
- gateway and registry appear early
- business services are added incrementally by feature
- infra/data modules (MongoDB, Redis, RabbitMQ) become shared capabilities
- message-driven modules appear later, not at the beginning
- frontend shell exists alongside backend service growth

That makes it valuable as a project-evolution reference rather than a component-definition reference.

## Stage-by-stage module growth

### Stage 1 snapshot
Modules visible:
- `lzj-eureka`
- `lzj-gateway`
- `lzj-banner`
- `lzj-mongodb`
- `lzj-pojo`
- `lzj-commons`

Interpretation:
- project starts with a thin microservice base platform
- gateway and registry exist early
- common/base/data modules are separated before business richness appears
- this is a platform-first baseline rather than a feature-rich product stage

### Stage 2 snapshot
New business modules appear:
- `lzj-hot-product`
- `lzj-recommendation`

Interpretation:
- business capability starts with homepage/product-discovery style services
- the project grows by adding focused feature services on top of shared infra

### Stage 3 snapshot
New modules appear:
- `lzj-comment`
- `lzj-product-details`
- `lzj-redis`
- `lzj-search`

Interpretation:
- richer read-side/product-detail capability is added
- Redis and search enter when read/query experience becomes more complex
- comments and details indicate vertical business capability split, not generic technical slicing

### Stage 4 snapshot
New modules appear:
- `lzj-buytime`
- `lzj-login`
- `lzj-sendyzm`

Interpretation:
- user/account/login and purchase-timing flows enter later
- SMS/verification capability is introduced as a dedicated service rather than buried inside login code
- time-sensitive purchase logic becomes its own bounded capability

### Stage 5 snapshot
New modules appear:
- `lzj-rabbitmq`
- `lzj-buyaction-message-producer`
- `lzj-buyaction-message-consumer`
- `lzj-order`

Interpretation:
- order/business transaction flow is added later, after discovery/detail/login groundwork exists
- messaging is introduced at the point where action decoupling becomes useful
- RabbitMQ support is modularized rather than hand-coded inside one service

## What this project teaches about growth order

A useful growth sequence from this sample is:
1. base platform + shared modules
2. early discovery/read-side business services
3. richer query/detail/search/cache layers
4. login/verification/time-sensitive action services
5. order flow + messaging-based decoupling

This is much more realistic than starting day one with every distributed-system component switched on.

## Module role categories

### Platform modules
- `lzj-eureka`
- `lzj-gateway`

### Shared library / support modules
- `lzj-commons`
- `lzj-pojo`
- `lzj-banner`

### Data integration modules
- `lzj-mongodb`
- `lzj-redis`
- `lzj-rabbitmq`

### Business capability modules
- `lzj-hot-product`
- `lzj-recommendation`
- `lzj-product-details`
- `lzj-comment`
- `lzj-buytime`
- `lzj-login`
- `lzj-sendyzm`
- `lzj-order`

### Message workflow modules
- `lzj-buyaction-message-producer`
- `lzj-buyaction-message-consumer`

## Architectural lessons worth reusing

### 1. Shared support modules come before business explosion
The sample creates `commons`, `pojo`, and data-support modules before many business services appear.
This is useful when the team needs a stable internal baseline.

### 2. Business services grow by vertical capability
The project does not only split by technical layer. It gradually adds business-facing modules like recommendation, details, comments, login, and order.

### 3. Data technologies appear when the business need becomes visible
- MongoDB appears early as a dedicated support module
- Redis appears when richer read/query/performance concerns show up
- RabbitMQ appears later when order/action decoupling starts to matter

### 4. Messaging is introduced late enough to solve a visible problem
This matches good staged architecture practice.

### 5. Frontend and backend evolve together
The project also ships a Vue frontend shell, which means backend capability growth is tied to real page/use-case flow rather than abstract service decomposition alone.

## How to use this reference in answers

Use this sample when the user asks questions like:
- how should a microservice project grow over time?
- should I create all services up front?
- when do Redis / MQ / login / order services usually enter?
- how do I split business services gradually?
- how do shared modules and business modules coexist in a teaching or starter project?

## Output guidance

When answering from this sample:
1. explain the stage-by-stage module evolution
2. separate platform/shared/data/business/message modules
3. show that later-stage modules answer visible business needs
4. warn against introducing everything at once

## Source notes

Distilled from the user's 乐Z家 project directories across stage 1 to stage 5, including both backend multi-module Maven structure and Vue frontend shell presence.
