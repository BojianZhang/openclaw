# E-commerce RPC, Search, Cart, and Order Patterns

Use this file when the user needs a backend-focused explanation of how a traditional Java shopping platform uses RPC, Solr search, Redis, cart flows, SSO state, order creation, payment adjacency, and MQ-assisted workflows.

This reference is distilled from the user's 易购商城 materials.

## Why this sample matters

This project represents a classic modular Java commerce stack rather than a pure Spring Cloud sample.
Its architecture combines:
- multi-module Maven structure
- portal / manager / sso / order / rpc boundaries
- Dubbo + ZooKeeper service collaboration
- Redis state/cache support
- Solr search
- shopping cart flow
- order + payment
- registration/verification + MQ extension

That makes it especially useful for explaining older but still common commerce-platform design patterns.

## 1. RPC layer as contract and collaboration seam

Module signal:
- `ego-rpc`

Dependency signals:
- Dubbo
- ZooKeeper / zkclient

Interpretation:
- RPC is treated as a collaboration boundary rather than hidden ad hoc calls
- portal, sso, and order do not need to know every implementation detail directly
- Dubbo + ZooKeeper expresses a classic service contract / service registration style in older Java commerce systems

Good explanation:
- use RPC to stabilize service interaction boundaries across modules
- avoid turning RPC interfaces into a second copy of business implementation

## 2. Solr as search capability

Stage signal:
- homepage menu implementation + Solr search engine
- dedicated `SolrJDemo`

Interpretation:
- search becomes important after the basic portal is in place
- Solr is introduced to improve search-facing retrieval and query experience
- search is an experience capability, not the system of record for transactional truth

Good answer:
- DB remains authoritative for transactional/product source data
- Solr improves retrieval/search behavior for user-facing portal flows

## 3. Redis as support for state and hot access

Stage signals:
- Redis intro and installation
- master-slave switching and Spring Data Redis

Interpretation:
- Redis is important enough to deserve dedicated teaching around HA/read-write considerations
- in this kind of platform Redis is not only generic cache; it often supports:
  - SSO/session/token state
  - portal hot data
  - cart-related temporary/high-frequency access
  - pressure reduction around repeated reads

Good answer:
- Redis should be explained by flow and state type, not only as a performance buzzword

## 4. Cart as a distinct user-state capability

Stage signal:
- shopping cart implementation and cart list features

Interpretation:
- cart is not just a tiny UI feature; it is a user-state domain with its own storage and retrieval pattern
- cart often sits between browsing and order creation
- cart-related data is a strong candidate for fast-access support because it is user-specific, high-frequency, and mutable

Good answer:
- cart should be described as an intermediate transaction-intent state rather than only a table or page

## 5. Order as business transaction truth

Stage signal:
- order implementation appears before payment is fully integrated

Interpretation:
- the platform first establishes internal order truth
- order creation, order state, and order query are separated from payment integration

Good answer:
- order owns internal business transaction lifecycle
- payment is attached later as external settlement interaction

## 6. Payment as external closure, not order replacement

Stage signal:
- dedicated payment implementation
- separate `ego-alipay`

Interpretation:
- payment integration is external-facing and should map results back into order state
- this is a strong reason to keep order and payment conceptually separate

## 7. Registration / verification / MQ support

Stage signals:
- registration
- email sending
- captcha / Geetest
- RabbitMQ integration

Interpretation:
- identity/trust enhancement grows after the basic platform and order flow exist
- MQ appears as a support mechanism for decoupled registration/notification/message handling rather than being mandatory from day one

Good answer:
- registration verification and messaging should be explained as support workflows around identity and user activation, not as core shopping-domain truth

## 8. A practical user-flow chain

A useful way to explain the platform is:
1. portal provides browse/search entry
2. SSO handles identity/session state
3. Redis accelerates high-frequency state and hot reads
4. cart captures user purchase intent before order
5. order captures transaction truth
6. payment closes the transaction externally
7. registration/verification/MQ support user onboarding and trust workflows

## Common mistakes

### Mistake 1: treating cart as just a frontend concern
Cart is a real backend state/intent capability.

### Mistake 2: treating Solr as a database replacement
Solr supports search experience, not transactional truth.

### Mistake 3: treating Dubbo as only a dependency name
It should be explained as a service interaction style and contract boundary.

### Mistake 4: mixing order and payment into one boundary
Payment closes the order externally; it does not replace order truth.

## Output guidance

When answering:
1. explain the user/business flow first
2. map RPC/search/cache/cart/order/payment to the right stage of that flow
3. separate core domain truth from support capabilities
4. explain why these capabilities appear gradually in the project

## Source notes

Distilled from the user's 易购商城 day08-day14 materials, including Dubbo+ZooKeeper, Solr search, SSO, cart, order, payment, registration, validation, and RabbitMQ integration stages.
