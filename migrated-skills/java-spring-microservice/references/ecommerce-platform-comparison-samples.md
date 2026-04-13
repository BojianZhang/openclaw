# E-commerce Platform Comparison Samples

Use this file when the user needs to compare two different Java shopping-platform evolution styles rather than study one project in isolation.

This reference compares two user-provided samples:
- 乐SHOP: modular shopping platform with `shop-common`, `shop-manager`, `shop-portal`, `shop-rpc`, `shop-sso`, `shop-order`, Redis, Elasticsearch, payment, SMS, cloud storage
- 易购商城: traditional Java mall with `ego-common`, `ego-manager`, `ego-portal`, `ego-rpc`, `ego-sso`, `ego-order`, Dubbo + ZooKeeper, Solr, cart, order/payment, registration/verification, RabbitMQ

## Why this comparison matters

The two projects are similar enough to compare, but different enough to teach architecture judgment.
They help answer:
- how different Java commerce stacks express similar module boundaries
- how search, RPC, payment, verification, and support capabilities appear in different project styles
- how to explain "traditional modular mall" vs "modular Spring Boot commerce platform" without collapsing them into one story

## Shared structural pattern

Both samples converge on a stable core boundary set:
- shared/common module
- manager/admin module
- portal/user-facing module
- rpc/contract module
- sso/identity module
- order module

This is important.
It means the core commerce-platform boundaries are relatively stable even when the stack and supporting capabilities differ.

## Key differences

### 1. RPC and service-collaboration flavor
**乐SHOP**
- stronger Spring Boot modular-platform feel
- Dubbo appears, but the overall project framing is more like capability-by-capability platform evolution

**易购商城**
- much more explicitly classic Java modular mall style
- Dubbo + ZooKeeper teaching path is central
- `ego-rpc` is especially visible as a contract seam

### 2. Search capability choice
**乐SHOP**
- Elasticsearch

**易购商城**
- Solr / SolrJ

Architectural lesson:
- search capability is stable as a need
- the engine can differ by stack era and ecosystem preference
- do not overfit the business explanation to one search product name

### 3. User-flow emphasis
**乐SHOP**
- platform growth emphasized through portal/manager/SSO/order and later payment/SMS/cloud-storage support

**易购商城**
- stronger teaching emphasis on product management, search, SSO, cart, order, payment, registration, verification, and MQ integration

Architectural lesson:
- 易购商城 highlights the classic shopping flow chain more explicitly
- 乐SHOP highlights platform capability accretion more explicitly

### 4. Cart visibility
**乐SHOP**
- cart is less foregrounded in the extracted stage summaries

**易购商城**
- cart is explicit as its own stage and capability

Architectural lesson:
- cart deserves to be treated as a backend state capability, not only a frontend feature

### 5. Payment/verification support narrative
**乐SHOP**
- payment and SMS arrive as staged support capabilities around a more modern Spring Boot modular platform

**易购商城**
- payment, registration, captcha/Geetest, mail, and RabbitMQ are taught more explicitly as traditional mall capability expansions

## Comparison-friendly answer model

A strong comparison answer can say:
1. both projects stabilize around portal / manager / sso / order / common / rpc boundaries
2. 乐SHOP is better for understanding modern modular platform capability growth
3. 易购商城 is better for understanding classic Java mall architecture with Dubbo + ZooKeeper + Solr + cart/order/payment teaching flow
4. search technology and RPC style differ, but the underlying commerce-domain boundaries remain recognizable

## How to choose which sample to reference

### Prefer 乐SHOP when the user asks about
- staged platform capability growth
- Redis / ES / payment / SMS / cloud-storage capability timing
- modular shopping-platform boundary thinking in a more Spring Boot–style context

### Prefer 易购商城 when the user asks about
- Dubbo + ZooKeeper in a mall project
- Solr in a traditional Java commerce stack
- cart/order/payment/registration/RabbitMQ as classic mall feature progression
- why `rpc` is a first-class module in older Java mall systems

## Output guidance

When comparing:
- start with shared boundaries
- then explain stack/style differences
- then explain which sample is better evidence for the user's current question
- avoid claiming one sample is simply "better" than the other; they illuminate different tradeoffs and eras

## Source notes

Distilled from the user's 乐SHOP and 易购商城 project directories and progression patterns.
