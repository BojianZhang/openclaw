# E-commerce Redis, Search, Order, and Payment Patterns

Use this file when the user needs a deeper implementation-oriented explanation of how Redis, Elasticsearch, order persistence, payment integration, and SSO/session support fit together in a modular Java shopping platform.

This reference extends the 乐SHOP-derived platform references with a more implementation-facing lens.

## 1. Redis in a shopping platform is multi-role, not single-purpose

In the sample dependencies, Redis appears near multiple business-facing modules such as portal, manager, SSO, and order.
That suggests a practical architecture lesson:
- Redis is not only for "homepage cache"
- Redis is a shared high-frequency support capability for several flows

### Common Redis roles in this kind of platform
- hot data caching for portal/user-facing reads
- identity/session/token-related fast access around SSO
- temporary state acceleration around order-adjacent flows
- reducing repeated DB pressure on high-frequency queries

A strong answer should explain the role by module and flow, not just say "Redis improves performance".

## 2. Elasticsearch is a search capability, not a universal storage replacement

The project introduces Elasticsearch as a distinct stage after the platform and cache capability are already in place.
That indicates a healthy sequence:
- first get the platform working
- then improve retrieval/search experience with a dedicated search engine

### Good explanation
Elasticsearch is most valuable when product retrieval/search experience, fuzzy matching, filtering, ranking, or search-specific query behavior outgrow basic database queries.

### Weak explanation
"We used ES because it is faster than MySQL."

A better answer is:
- MySQL remains authoritative for transactional/product source data
- ES improves search-facing experience and query shape

## 3. SSO and Redis naturally interact

The sample puts SSO beside Redis dependency support.
A useful interpretation is:
- identity state is frequently read and checked
- fast state access matters for login/session/token workflows
- Redis often supports these high-frequency identity checks better than repeatedly hitting the relational source of truth

Do not reduce SSO to login UI. It is an identity-state capability.

## 4. Order is a business truth boundary

The presence of a distinct `shop-order` module is important.
A good architecture explanation should say:
- order captures the platform's internal business transaction truth
- order state flow and order persistence belong together conceptually
- payment is adjacent, but external to that truth in a different way

### Typical order-side concerns
- order creation
- order query
- order status progression
- order persistence
- coordination with identity and payment result

## 5. Payment is an external transactional integration boundary

The sample introduces Alipay after the order module exists.
This gives a strong architectural lesson:
- order first
- payment integration second

That is healthier than treating payment SDK code as if it were the origin of the business process.

### Good answer framing
- order is the platform's internal transaction intent
- payment integration handles external settlement interaction
- payment callbacks/results must be mapped back into internal order state

## 6. SMS verification is a support capability around trust/risk/identity

The sample introduces Tencent SMS after payment and order capabilities are already present.
This suggests SMS is not a foundational domain module, but a support capability attached to high-value identity or transaction flows.

Typical roles:
- login verification
- registration/identity confirmation
- sensitive operation verification
- transaction-adjacent trust reinforcement

## 7. Cloud storage is a resource capability, not a shopping domain

Qiniu appears early as a stage topic.
A good explanation is:
- shopping platforms quickly need image/media/resource management
- cloud storage solves asset-hosting/distribution concerns
- it supports business flows like product publishing, not the domain logic of orders or login itself

## 8. A practical capability relationship chain

A useful way to explain the platform is:
1. portal/manager drive user and operator flows
2. SSO provides identity/session capability
3. Redis accelerates hot/stateful access around those flows
4. ES improves product retrieval/search experience
5. order captures business transaction truth
6. payment closes transactions externally
7. SMS/cloud storage act as supporting verification/resource capabilities

This is much stronger than listing technology names.

## Common mistakes

### Mistake 1: saying Redis is just for caching product lists
It often supports SSO/session and order-adjacent state too.

### Mistake 2: saying ES replaces MySQL
ES usually serves search experience, not transactional truth.

### Mistake 3: mixing order and payment into one module boundary
Payment is adjacent to order, but conceptually distinct.

### Mistake 4: treating SMS or cloud storage as core commerce domains
They are important, but usually support capabilities.

## Output guidance

When answering:
1. separate core business domains from support capabilities
2. explain why each capability appears at that stage
3. show module-to-capability mapping
4. avoid turning all technologies into first-class business domains

## Source notes

Distilled from the user's 乐SHOP project stages, module layout, and module dependency progression across portal, manager, sso, order, search, payment, SMS, and cloud storage capabilities.
