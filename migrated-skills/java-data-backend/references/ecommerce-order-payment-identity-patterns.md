# E-commerce Order, Payment, and Identity Patterns

Use this file when the user needs a focused reasoning model for the relationship between SSO, order, payment, Redis, and support integrations in a Java shopping platform.

This reference is inspired by the 乐SHOP module layout and dependency progression.

## Core relationship model

A practical commerce-platform relationship chain is:
1. user identity is established and reused (`shop-sso`)
2. portal/user actions produce shopping intent
3. order domain captures business transaction intent (`shop-order`)
4. payment integration closes the transaction externally (Alipay or similar)
5. surrounding support capabilities such as Redis, SMS, and cloud storage improve performance, verification, and resource handling

This sequence helps avoid mixing identity, order, and payment into one blob.

## Identity / SSO layer

### What it owns
- login/session/token handling
- shared identity capability for portal and possibly manager or other modules
- fast identity state access, often helped by Redis

### What it should not own
- order business logic
- payment closure logic

## Order layer

### What it owns
- order creation
- order query/state flow
- business transaction intent
- order persistence

### What it should not own
- generic login/session concerns
- all payment-SDK details as if payment were just a utility helper

## Payment adjacency

### What payment integration usually owns
- external SDK interaction
- payment request building
- callback/return handling
- mapping external payment result back into platform order state

### Why order and payment must be separated conceptually
Order is the platform's business truth.
Payment is an external settlement interaction tied to that truth.
The two are tightly related, but not the same boundary.

## Redis as support layer, not domain replacement

In this sample, Redis dependencies appear in several business-facing modules.
A good explanation is:
- Redis supports performance/state access around portal, SSO, and order-adjacent flows
- it should accelerate the system, not redefine business ownership

## SMS verification as support capability

SMS verification usually supports:
- account/login verification
- sensitive operation confirmation
- user-trust and anti-abuse steps

It should be explained as a support workflow attached to identity or transaction risk control, not as a core shopping domain by itself.

## Common mistakes in answers

### Mistake 1: treating SSO as just a login page
It is really an identity capability.

### Mistake 2: collapsing order and payment into one sentence
A stronger answer separates internal order state from external payment closure.

### Mistake 3: making Redis the center of the architecture story
Redis is support infrastructure for hot access/state, not the business domain itself.

### Mistake 4: treating SMS or cloud storage as core domains
They are supporting capabilities unless the product itself revolves around them.

## How to answer using this reference

A strong answer usually does this:
1. explain the identity -> order -> payment relationship
2. place Redis/SMS/storage as support capabilities
3. explain which modules should own which responsibilities
4. describe how these capabilities are introduced gradually in a growing platform

## Source notes

Distilled from the user's 乐SHOP modules (`shop-sso`, `shop-order`, `shop-portal`, `shop-manager`, `shop-common`, `shop-rpc`) and later-stage dependency additions such as Redis, Alipay, Tencent SMS, and cloud storage.
