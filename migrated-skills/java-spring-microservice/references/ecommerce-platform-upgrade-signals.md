# E-commerce Platform Upgrade Signals

Use this file when the user is not just asking what modules/capabilities exist in a shopping platform, but needs concrete signals for when the platform should introduce the next capability.

This reference complements the 乐SHOP module evolution sample by turning stage topics into upgrade criteria.

## Why upgrade signals matter

Platform roadmaps are useful, but teams usually struggle with a harder question:
**"How do I know it's time to add Redis / search / SSO / order / payment / SMS?"**

A good answer should connect each capability to a visible business or operational pain.

## From basic platform to cloud storage capability

### Upgrade when
- product/media assets are becoming hard to manage locally
- image/file distribution and storage concerns are no longer trivial
- the platform needs a cleaner resource-hosting path for product content

### Do not upgrade just because
- object storage is common in modern architectures

## From basic platform to Redis capability

### Upgrade when
- hot reads are putting repeated pressure on the database
- session/token or temporary state lookups are frequent enough to matter
- portal or order-adjacent flows are starting to show repeated access bottlenecks

### Do not upgrade just because
- Redis is a common interview keyword

## From Redis to Elasticsearch capability

### Upgrade when
- search experience becomes a visible product requirement
- database-native search is no longer sufficient for product retrieval expectations
- filtering, fuzzy search, ranking, or richer search-facing query behavior becomes important

### Do not upgrade just because
- ES sounds more advanced than MySQL

## From platform login to dedicated SSO capability

### Upgrade when
- identity/session/token concerns are reused across multiple modules or surfaces
- portal-only login handling is becoming duplicated or hard to govern
- unified identity handling has become more valuable than keeping auth inside one web module

### Do not upgrade just because
- SSO sounds more enterprise-grade

## From shopping flows to dedicated order capability

### Upgrade when
- order creation/state/query behavior is becoming a clear bounded domain
- portal logic is getting bloated with transaction-adjacent concerns
- transaction lifecycle deserves its own ownership boundary

### Do not upgrade just because
- “order-service” sounds like the next standard module to add

## From order capability to payment integration

### Upgrade when
- the platform has a stable internal order truth that now needs external settlement
- order lifecycle is clear enough to map payment callbacks/results back into it
- business is ready to close the transaction loop instead of only simulating checkout

### Do not upgrade just because
- payment SDK integration looks like a visible milestone

## From identity/order flows to SMS verification support

### Upgrade when
- login, registration, or sensitive transaction flows need stronger verification
- user trust/risk control requirements have become visible
- synchronous inline verification is becoming part of identity or transaction safety design

### Do not upgrade just because
- SMS is common in many commerce products

## How to reason about support capability timing

A healthy rule is:
- add support capabilities when a concrete business flow has started to demand them
- not when the architecture diagram feels incomplete without them

Examples:
- Redis follows hot state/read pressure
- ES follows search-experience pressure
- payment follows real transaction closure needs
- SMS follows trust/verification pressure
- cloud storage follows media/resource management pressure

## Quick diagnostic prompts

Use these prompts when advising a user:
- What specific product flow is hurting today?
- Is the pain in hot reads, identity reuse, search experience, transaction closure, or trust verification?
- Does the next capability solve an existing pain, or just decorate the architecture?

## Output guidance

When answering:
1. identify the platform's current capability stage
2. identify the visible business/operational pain
3. recommend the smallest next capability that addresses it
4. explicitly say what not to introduce yet

## Source notes

Distilled from the user's 乐SHOP stage sequence: platform setup -> cloud storage -> Redis -> Elasticsearch -> SSO -> order -> payment -> SMS verification.
