# E-commerce Platform Config and RPC Patterns

Use this file when the user needs configuration and integration-pattern guidance for a modular shopping platform that uses Dubbo, ZooKeeper, Redis, Elasticsearch, Alipay, Tencent SMS, and related support components.

This reference is inspired by the 乐SHOP dependency structure.

## Parent project pattern

The sample shows a classic parent-aggregator pattern:
- top-level `pom` with `packaging=pom`
- shared module registration
- centralized version management
- capability dependencies introduced stage by stage

This is valuable because commerce-platform growth often starts from a stable multi-module parent rather than independent services from day one.

## Shared dependency-management pattern

The parent project centrally manages dependencies for:
- MyBatis
- PageHelper
- MySQL
- Druid
- Qiniu
- Dubbo
- ZooKeeper (`zkclient`)
- Elasticsearch client stack
- Kaptcha
- Alipay SDK
- Tencent SMS SDK

Architectural lesson:
- capability growth is expressed through centralized dependency governance first, then module-specific adoption second

## Dubbo + ZooKeeper interpretation

The sample uses:
- `dubbo-spring-boot-starter`
- `zkclient`

A good explanation pattern is:
- Dubbo acts as the RPC/service-governance interaction style
- ZooKeeper provides coordination/registry support in that ecosystem
- `shop-rpc` indicates service contracts are treated as first-class collaboration seams

Important nuance:
- explain Dubbo as a service-call/contract ecosystem choice, not as a universal architecture answer

## Module-specific dependency pattern

### Portal module
Usually carries:
- web + Freemarker
- MyBatis/PageHelper/MySQL/Druid
- Redis
- common + rpc + sso
- Dubbo/ZK when remote collaboration is involved
- sometimes SMS/MQ or other user-facing support integrations

Interpretation:
- portal is an orchestration-heavy user-facing boundary with several support dependencies

### Manager module
Usually carries:
- Freemarker/web-style admin dependencies
- MyBatis/MySQL/Druid
- Redis
- cloud storage / captcha in relevant stages

Interpretation:
- manager is an admin-facing operational boundary, not just a second copy of portal

### SSO module
Usually carries:
- common + MyBatis/MySQL/Druid
- Redis
- Dubbo/ZK

Interpretation:
- identity/session capability needs fast state access and contract-level reuse

### Order module
Usually carries:
- rpc/common/sso
- MyBatis/MySQL/Druid
- Redis
- Dubbo/ZK
- payment SDK in later stages

Interpretation:
- order becomes the transaction-truth boundary, with payment attached later as an external integration

## Config-shape lessons

### Redis config lesson
If Redis appears in several business-facing modules, treat it as shared support capability with per-module usage contexts, not as one isolated technical trick.

### Search config lesson
ES belongs where retrieval/search experience matters, usually near portal-facing product retrieval flows.

### Payment config lesson
Payment config should be attached to modules that map external settlement back into internal order state, not sprinkled everywhere.

### SMS/captcha config lesson
Verification-related config belongs near identity/trust-sensitive user flows, not necessarily in every module.

## How to answer with this reference

Use this when the user asks:
- how should a modular shopping platform manage config and dependencies?
- what does Dubbo + ZooKeeper mean in this kind of project?
- why do portal/order/sso modules have different support dependencies?
- how do support SDKs enter module-level configs over time?

A strong answer should:
1. explain parent-level dependency governance
2. explain module-level capability adoption
3. explain RPC/contract choice separately from business boundaries
4. avoid turning dependency lists into architecture explanation by themselves

## Source notes

Generalized from the user's 乐SHOP parent POM and module POM dependency patterns.
