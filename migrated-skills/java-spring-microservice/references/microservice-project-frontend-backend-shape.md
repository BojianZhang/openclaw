# Microservice Project Frontend-Backend Shape

Use this file when the user is working with a backend microservice project that also has a separate frontend shell and wants guidance on how to think about the combined shape.

This reference is inspired by the 乐Z家 sample, which includes a Vue frontend (`livegoods-vue`) alongside the backend multi-module project.

## What the sample shows

Frontend shell traits:
- Vue 2
- vue-router
- vuex
- element-ui
- axios
- local mock support via Express + nodemon

Backend traits:
- Spring Boot + Spring Cloud multi-module Maven project
- gateway + registry + multiple business services
- data-support modules and later messaging modules

## Why this matters

Many teaching examples discuss backend microservices in isolation.
Real projects often need a simpler mental model:
- frontend is the user interaction shell
- gateway is the backend boundary entry
- business services sit behind the gateway
- recommendation/detail/login/order capabilities map to real pages and flows

## Practical mental model

### Frontend layer
Responsible for:
- routing/pages
- UI state
- user interaction flow
- API request orchestration at the client side
- local mock/demo support during early frontend work

### Gateway layer
Responsible for:
- unified backend entry
- request routing
- shared boundary logic
- shielding internal service topology from the frontend

### Business service layer
Responsible for:
- domain-specific APIs and business behavior
- recommendation/detail/comment/login/order logic

### Shared/data support layer
Responsible for:
- shared Java support code
- integration support for Mongo/Redis/RabbitMQ and similar technologies

## Useful project-design lesson

If the frontend exists early, it can help drive more realistic backend service decomposition:
- homepage -> hot/recommendation services
- detail page -> product-details service
- comment flow -> comment service
- login flow -> login + verification capability
- purchase flow -> buytime/order/message workflow

This is often healthier than splitting services only by technical enthusiasm.

## Vue sample takeaways

The sample frontend suggests a classic teaching-project stack:
- Vue CLI app
- axios-based API access
- local mock server for parallel development
- router/store separated from backend service implementation details

Good reminder:
- frontend mock support is useful early, but the long-term contract should converge on gateway-backed APIs

## How to answer with this reference

Use this when the user asks:
- how should frontend and backend microservice projects line up?
- should frontend call services directly or go through gateway?
- how do page flows influence service decomposition?
- how can a Vue shell coexist with a growing Java microservice backend?

A strong answer should:
1. separate frontend shell, gateway boundary, and internal services
2. tie services back to real user flows/pages
3. avoid overcoupling frontend to internal service topology
4. treat mock support as a development aid, not the architecture target

## Source notes

Distilled from the user's 乐Z家 backend multi-module project and accompanying Vue frontend shell (`livegoods-vue`).
