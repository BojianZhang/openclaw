# E-commerce Platform Module Evolution

Use this file when the user wants a realistic example of how a Java e-commerce platform grows module by module across capabilities such as portal, manager/admin, SSO, order, search, payment, SMS, and shared RPC/support layers.

This reference is distilled from the user's 乐SHOP project snapshots.

## Why this sample matters

This project is not centered on Spring Cloud component choreography.
It is a business-platform growth sample that shows how a commerce system gradually gains:
- portal frontend/backend capability
- admin/manager capability
- shared service contracts and common modules
- SSO/login capability
- order capability
- Redis caching
- Elasticsearch-based search
- payment integration
- SMS verification
- external cloud/storage integration

That makes it valuable as an application-evolution sample rather than a pure middleware sample.

## Stable module taxonomy

Across the later snapshots, the recurring modules are:
- `shop-common`
- `shop-generator`
- `shop-manager`
- `shop-portal`
- `shop-rpc`
- `shop-sso`
- `shop-order`

### Suggested interpretation
- `shop-common`: shared support and common code
- `shop-generator`: code generation / scaffolding support
- `shop-manager`: admin/backend management capability
- `shop-portal`: user-facing portal capability
- `shop-rpc`: shared service contracts / RPC-facing layer
- `shop-sso`: login / identity / single sign-on capability
- `shop-order`: order domain capability

## Capability growth by stage topic

Based on the stage folders, the project appears to grow through these capability themes:
1. mall/platform bootstrap
2. cloud object storage (Qiniu)
3. Redis cache
4. Elasticsearch search
5. single sign-on
6. order implementation
7. payment integration
8. SMS verification

This sequence is useful because it mirrors a realistic commerce product path:
- first get the platform up
- then add asset/storage support
- then add cache/search capability
- then add identity and order flows
- then payment and user-verification enhancements

## Architectural lessons

### 1. Shared support and service contracts come early
The presence of `shop-common` and `shop-rpc` indicates that common logic and service boundaries are treated as first-class modules before the business platform becomes feature-rich.

### 2. Portal and manager are separated
This is a useful commerce-system pattern:
- `shop-portal` serves end users
- `shop-manager` serves admin/operations workflows

Do not collapse these blindly when the use cases diverge.

### 3. SSO becomes its own capability
Identity is not hidden inside the portal. A dedicated `shop-sso` module indicates the system treats login/token/session concerns as a standalone capability.

### 4. Order is introduced as a separate domain module
This is a strong sign of business-domain decomposition. Order is not merely a utility feature inside portal code.

### 5. Middleware enters as business capability needs appear
The stage topics show Redis, Elasticsearch, payment, SMS, and cloud storage arriving as concrete feature enablers, not as day-one decoration.

## How to answer using this sample

Use this reference when the user asks:
- how should a Java e-commerce platform be modularized?
- what module types appear in a realistic shopping platform?
- when should portal, manager, SSO, order, and shared RPC layers be split?
- how do Redis / ES / payment / SMS fit into platform evolution?

A strong answer should:
1. classify the modules by role
2. explain the business capability growth order
3. show why middleware additions follow visible product needs
4. avoid claiming every system needs the exact same sequence

## Source notes

Distilled from the user's 乐SHOP project directories across stages 1 to 8, including module layout and topic progression (platform setup, Qiniu, Redis, Elasticsearch, SSO, order, payment, SMS).
