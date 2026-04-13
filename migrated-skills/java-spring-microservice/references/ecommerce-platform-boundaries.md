# E-commerce Platform Boundaries

Use this file when the user needs help reasoning about module boundaries in a Java shopping platform with portal, manager, SSO, order, shared common code, and RPC contracts.

This reference is inspired by the 乐SHOP project structure.

## Core boundary model

### Portal boundary
`shop-portal`
- user-facing pages and shopping flows
- product browsing, cart, user interactions
- should not absorb admin workflows

### Manager/admin boundary
`shop-manager`
- admin/back-office operations
- content/product/order operations for operators
- should not become the place where user-facing business logic lives

### Identity boundary
`shop-sso`
- login/session/token/single-sign-on concerns
- should be treated as a capability used by portal and other modules, not duplicated everywhere

### Order boundary
`shop-order`
- order creation, order-state flow, order query, payment adjacency
- should be a domain module, not a helper package inside portal

### Shared support boundary
`shop-common`
- shared DTOs, utility code, result wrappers, cross-module helpers
- should not become a dumping ground for order/search/login business logic

### RPC/service-contract boundary
`shop-rpc`
- shared service interfaces/contracts for distributed or modular invocation
- should define collaboration seams, not absorb full business implementations

### Generator/support boundary
`shop-generator`
- scaffolding/codegen support
- should remain a tooling/support module rather than a runtime business module

## External capability attachments

From the topic progression, these are capability attachments rather than core top-level business domains:
- Qiniu storage
- Redis cache
- Elasticsearch search
- payment integration
- SMS verification

A useful rule:
- treat them as enablers of business flows
- do not let them redefine core domain boundaries by themselves

## Common mistakes this sample helps prevent

### Mistake 1: merging portal and manager because both are “web”
Their actors and workflows differ.

### Mistake 2: hiding SSO inside portal only
Identity capability usually serves more than one boundary.

### Mistake 3: putting order logic into portal controllers/services directly
Order deserves its own capability boundary once the platform grows.

### Mistake 4: letting `common` become a business junk drawer
Common modules should support business capabilities, not replace them.

### Mistake 5: treating Redis / ES / payment / SMS as top-level domain modules by default
They are often supporting capabilities for user/business flows.

## Output guidance

When answering:
1. identify user-facing, admin-facing, identity, order, shared, and contract boundaries
2. explain which capabilities are core domains vs supporting integrations
3. recommend the smallest split that preserves role clarity

## Source notes

Distilled from the user's 乐SHOP module layout and stage topics.
