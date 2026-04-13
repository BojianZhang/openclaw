# E-commerce Platform Class Patterns

Use this file when the user needs class-level responsibility patterns for a modular Java shopping platform with portal, manager, SSO, order, shared support, RPC contracts, and support capabilities like Redis, search, payment, and SMS.

This reference is inspired by the 乐SHOP project structure.

## 1. Portal module classes

### Typical responsibility
- user-facing controllers
- shopping-flow orchestration
- page rendering / portal-facing API exposure
- coordination with SSO and RPC-facing service contracts

### Good boundary
Portal classes should express user interaction flow.
They should not own all identity internals or order persistence details directly.

## 2. Manager module classes

### Typical responsibility
- admin-facing controllers/services
- product/content/order management workflows for operators
- operational configuration flows

### Good boundary
Manager classes serve operators, not consumers.
Do not let them absorb end-user portal logic just because both are web-facing.

## 3. SSO module classes

### Typical responsibility
- login/session/token handling
- identity validation
- shared auth/session capability for multiple surfaces

### Good boundary
SSO classes should centralize identity semantics.
They should not become the home of order or portal business flow logic.

## 4. Order module classes

### Typical responsibility
- order creation/query/state-transition logic
- transaction-intent handling inside the platform
- coordination with payment results and user identity context

### Good boundary
Order classes own the platform's transaction truth.
They should not be buried in portal controllers or collapsed into payment SDK wrappers.

## 5. Common module classes

### Typical responsibility
- DTO/VO/POJO definitions
- result wrappers
- constants/enums/utilities
- shared helper code reused across modules

### Good boundary
Common classes support business modules.
They should not quietly accumulate domain behavior from portal/order/sso/search.

## 6. RPC/service-contract classes

### Typical responsibility
- shared interfaces/contracts
- collaboration seams across modules/services
- contract definitions for remote or modular invocation

### Good boundary
RPC contracts should define interaction shape.
They should not absorb the full business implementation.

## 7. Redis-related configuration/service classes

### Typical responsibility
- RedisTemplate or cache-access configuration
- hot/state access helpers
- session/token or high-frequency lookup support

### Good boundary
These classes provide fast-access infrastructure.
They should not redefine domain ownership.

## 8. Search/Elasticsearch classes

### Typical responsibility
- search indexing/query adapters
- search-oriented DTO mapping
- portal-facing retrieval support

### Good boundary
Search classes optimize retrieval experience.
They do not replace transactional business truth.

## 9. Payment integration classes

### Typical responsibility
- external SDK request building
- callback/return handling
- mapping payment outcomes into internal order state transitions

### Good boundary
Payment integration classes sit at the external settlement boundary.
They should not become the primary owner of order lifecycle.

## 10. SMS/cloud integration classes

### Typical responsibility
- verification/notification integration
- media/upload integration
- supporting external service adapters

### Good boundary
Treat them as support capabilities attached to business flows, not as core commerce-domain owners.

## Quick role map

- `portal/*Controller` -> end-user flow entry
- `manager/*Controller` -> admin/operator flow entry
- `sso/*Service` -> identity/session logic
- `order/*Service` -> order-state and transaction truth
- `common/*` -> shared support objects/utilities
- `rpc/*` -> contracts and collaboration seams
- `*Config` -> Redis/search/payment/SMS/cloud integration wiring
- `*Service` or adapter classes around external SDKs -> integration boundary implementations

## Source notes

Generalized from the user's 乐SHOP module layout and dependency progression.
