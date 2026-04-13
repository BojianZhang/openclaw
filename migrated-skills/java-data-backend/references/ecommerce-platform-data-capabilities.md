# E-commerce Platform Data Capabilities

Use this file when the user is discussing how a Java e-commerce platform gradually introduces Redis cache, Elasticsearch search, SSO/session storage, order persistence, payment state handling, SMS verification support, and cloud-storage-backed assets.

This reference is distilled from the user's 乐SHOP project stages.

## Why this sample matters

Unlike a single-topic demo, this project shows how data and integration capabilities are introduced as the shopping platform grows:
- cloud object storage
- Redis caching
- Elasticsearch search
- SSO/session support
- order persistence
- payment integration
- SMS verification support

That makes it useful for explaining when and why a business platform adds supporting data capabilities.

## Capability-by-capability interpretation

### 1. Cloud storage capability
Stage topic:
- 七牛云存储

Interpretation:
- asset/file storage becomes a first-class platform need once the shopping platform starts managing product/media resources
- storage integration is a supporting capability, not the core shopping domain itself

Good answer angle:
- use cloud storage when local file handling no longer fits asset distribution, reliability, or operations needs

### 2. Redis cache capability
Stage topic:
- Redis缓存

Code/dependency signals:
- `spring-boot-starter-data-redis`
- `commons-pool2`
- Redis dependencies appear in multiple modules such as portal, manager, sso, order

Interpretation:
- Redis is not attached to only one module; it supports several high-frequency platform flows
- in a shopping platform, Redis often supports:
  - hot data caching
  - session/token-related data
  - temporary state / quick lookup
  - reducing DB pressure for portal/order-adjacent flows

### 3. Elasticsearch search capability
Stage topic:
- ElasticSearch

Dependency signals:
- `elasticsearch`
- `elasticsearch-rest-client`
- `elasticsearch-rest-high-level-client`

Interpretation:
- search enters when plain database query/search is no longer enough for the portal user experience
- ES is a support engine for product retrieval/search experience, not a replacement for all system data storage

### 4. SSO capability
Stage topic:
- 单点登录

Module signal:
- `shop-sso`
- Redis dependency appears in SSO-related module

Interpretation:
- identity/session/token concerns are treated as a dedicated capability
- Redis often naturally supports high-frequency session or token access paths

A good answer should frame SSO as identity capability plus state access optimization, not just a login page.

### 5. Order capability
Stage topic:
- 订单实现

Module signal:
- `shop-order`
- MyBatis, MySQL, PageHelper, Redis, Dubbo-related dependencies coexist

Interpretation:
- order is treated as a business domain with its own persistence needs
- Redis near the order module suggests caching/state acceleration around order flows
- the order domain sits close to payment but should not be collapsed into payment handling itself

### 6. Payment capability
Stage topic:
- 支付实现

Dependency signal:
- Alipay SDK

Interpretation:
- payment is introduced after order capability exists
- this reflects a good commerce design sequence: order domain first, then payment integration
- payment integration should be explained as an external transactional capability adjacent to order state, not as a generic utility

### 7. SMS verification capability
Stage topic:
- 短信验证

Dependency signals:
- Tencent cloud SMS SDK
- AMQP / RabbitMQ dependencies in later portal stage

Interpretation:
- SMS verification is a support capability around identity/security or high-value user actions
- if MQ enters nearby, a useful reasoning pattern is that verification or notification workflows may benefit from asynchronous integration rather than purely inline synchronous logic

## Cross-cutting architecture lessons

### Lesson 1: Supporting capabilities arrive after business pressure appears
This project introduces Redis, ES, payment, SMS, and cloud storage gradually instead of starting with all of them on day one.

### Lesson 2: Data capabilities should be explained by business need
- Redis -> hot data/session/state pressure
- ES -> search experience
- payment SDK -> transaction closure
- SMS -> verification and notification path
- cloud storage -> media/resource management

### Lesson 3: Order and payment are adjacent but different
A strong answer separates:
- order persistence and order lifecycle
- external payment integration and payment-state callback/closure

### Lesson 4: SSO is not merely frontend login
SSO usually implies shared identity/session/token handling across multiple platform surfaces.

## How to answer from this reference

Use this when the user asks:
- why does a shopping platform need Redis/ES/payment/SMS?
- when should these capabilities be introduced?
- how do order, payment, SSO, and search relate in platform design?
- how do support capabilities differ from core business domains?

A strong answer should:
1. state the business problem first
2. map the capability to the relevant module or flow
3. explain why it appears at that project stage
4. avoid portraying every support technology as a top-level domain

## Source notes

Distilled from the user's 乐SHOP stage topics and module dependencies across portal, manager, sso, order, and related platform modules.
