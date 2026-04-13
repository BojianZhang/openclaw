# Microservice Project Stage Upgrade Signals

Use this file when the user is not just asking "what stages exist", but needs concrete signals for when a project should upgrade to the next architectural stage.

This reference complements `spring-cloud-evolution-roadmap.md` by adding decision signals.

## Why signals matter

A roadmap gives order.
Signals answer a harder question:
**"How do I know I am ready for the next stage?"**

## From Stage 0 to Stage 1

### Upgrade when
- one codebase already contains clearly separable business capability boundaries
- one internal capability changes or scales differently from the rest
- team conversations already speak in terms of distinct service responsibilities

### Do not upgrade just because
- microservices feel more advanced
- the course has reached Eureka/Feign

## From Stage 1 to Stage 2

### Upgrade when
- downstream service failure has become a visible risk
- consumer code already needs an explicit degraded response path
- there is repeated ad hoc exception handling around remote calls

### Prefer this move
- add `FallbackFactory` first

### Do not upgrade just because
- you want to say the project has fault tolerance

## From Stage 2 to Stage 3

### Upgrade when
- external clients are beginning to hit multiple backend services separately
- route management at the edge is becoming messy
- auth/filtering/shared entry behavior is being duplicated across services or clients

### Do not upgrade just because
- gateway sounds like standard microservice architecture

## From Stage 3 to Stage 4

### Upgrade when
- runtime config is now spread across several services and environments
- changing config requires editing many local files manually
- the team can already feel the pain of environment drift

### Branch choice signals
- choose classic Config path when you want Spring Cloud-native config mechanics first
- choose Consul path when discovery + config one-stop simplicity matters
- choose Apollo path when config governance/namespace/environment management matters more

## From Stage 4 to Stage 5

### Upgrade when
- multiple running client instances need coordinated refresh
- manual per-node refresh is painful or error-prone
- config centralization is already in place, but propagation is now the bottleneck

### Do not upgrade just because
- Bus exists in the ecosystem

## From Stage 5 to Stage 6

### Upgrade when
- gateway-facing traffic pressure is measurable
- route-level throttling or API grouping has become necessary
- boundary-level failure shaping matters more than internal method-level fallback

### Do not confuse this with
- service-level resilience only
- downstream business fallback only

## From Stage 6 to Stage 7

### Upgrade when
- synchronous workflows are causing coupling, latency, or buffering pain
- some business actions clearly do not need immediate synchronous completion
- the team can accept eventual consistency and operational cost

### Do not upgrade just because
- MQ seems more scalable
- async sounds more advanced

## Signals from the 乐Z家 sample

The sample implies a healthy progression:
- recommendation/detail/search/comment appear before login/order/messaging complexity
- Redis enters when read/query behavior becomes richer
- login + verification appear when user-flow complexity increases
- RabbitMQ and order workflow appear later, when action decoupling becomes valuable

This is a strong reminder that middleware usually enters after business pressure appears, not before.

## Quick diagnostic prompts

Use these prompts when advising a user:
- Which problem is hurting today: split boundaries, call failure, edge entry, config sprawl, propagation, traffic pressure, or sync coupling?
- Is the pain already visible, or is this still architecture anticipation?
- Will the next stage solve a problem the team already feels?

## Output guidance

When answering with this reference:
1. identify the user's current stage
2. identify the concrete pain signal
3. recommend the smallest next-stage upgrade that addresses it
4. explicitly say what *not* to add yet

## Source notes

Distilled from the user's Spring Cloud roadmap work plus the 乐Z家 staged project evolution sample.
