# Service Calls, Fault Tolerance, and Gateways

Use this file when the user asks about Feign/OpenFeign, Hystrix, Sentinel, Zuul, Gateway, or how service invocation, protection, and gateway responsibilities fit together.

If the user only needs a high-level picture of Spring Cloud and its component map, read `spring-cloud-foundations.md` first.

## Feign and OpenFeign

### What Feign is
- a declarative HTTP client in Spring Cloud ecosystems
- designed to reduce boilerplate in service-to-service HTTP calls
- historically integrates Ribbon for client-side balancing in classic stacks

### What OpenFeign adds
- better support for Spring MVC annotations such as `@RequestMapping`
- a more natural Spring-style interface definition model
- dynamic proxy generation behind `@FeignClient`

Practical explanation:
- RestTemplate is more manual
- Feign/OpenFeign is more declarative
- but neither removes distributed-system concerns like timeout, retry, versioning, idempotency, or fallback design

## Hystrix essentials

Use when the issue is classic Netflix fault tolerance.

Hystrix exists to reduce cascading failures in distributed calls.
Typical mechanisms mentioned in the materials:
- service isolation
- circuit breaking
- fallback / degradation
- request caching
- request collapsing / merging

### Snowball / avalanche explanation
A service avalanche happens when one downstream delay or failure blocks upstream threads and the failure propagates through the dependency chain.
A strong answer always mentions thread/resource exhaustion, not just "one service broke".

### Hystrix monitoring
Classic monitoring path:
- metrics stream exposure via Actuator / `hystrix.stream`
- Hystrix Dashboard for node-level visualization
- Turbine for cluster aggregation in older stacks

## Sentinel essentials

Use when the discussion is about newer traffic-governance / stability protection in Alibaba-style ecosystems.

Key positioning:
- Sentinel protects service stability with traffic control, circuit breaking / degradation, and system load protection
- it also includes strong real-time dashboard/console support
- it is a common replacement direction when discussing Hystrix maintenance mode and newer ecosystem choices

### Sentinel vs Hystrix
A concise compare frame:
- **Hystrix** focuses strongly on isolation, timeout, circuit breaking, and fallback around remote calls
- **Sentinel** starts more from traffic governance, flow control, degradation, and system protection, plus strong dashboard management
- both protect stability, but the center of gravity differs

Do not answer as if Sentinel simply "replaces every Hystrix concept one-to-one". Explain their emphasis difference.

## Why gateways are used

A gateway sits at the system boundary as the unified external entry.
Typical reasons to introduce it:
- clients should not know every internal service address
- centralize auth-related cross-cutting logic
- centralize routing, filtering, metrics, rate limiting, and some gray-release behavior
- reduce client complexity and shield internal architecture changes

Important nuance:
- gateways are common and useful in larger systems, but they are not a mystical requirement for every tiny microservice project

## Gateway responsibilities

High-frequency responsibility list:
- routing
- filtering
- auth / security checks
- observability / logging / metrics
- rate limiting / traffic governance
- some caching and static-response handling
- simplifying external access

## Zuul vs Gateway

### Zuul
- classic Netflix gateway answer
- integrates with Eureka/Ribbon/Hystrix in older Spring Cloud stacks
- good for explaining historical Spring Cloud gateway architecture

### Spring Cloud Gateway
- newer Spring ecosystem gateway direction
- intended as the main replacement direction for Zuul in Spring Cloud
- built around Spring 5 / Boot 2 / Reactor / Netty era capabilities
- often discussed together with filter chains, reactive support, and modern Spring ecosystem evolution

### Nginx / Kong vs business gateway
Useful compare frame:
- Nginx/Kong can act as broader infrastructure or portal gateways
- Zuul/Gateway are more application/business-facing gateways inside the Spring microservice ecosystem
- do not collapse all gateway layers into one concept

## Practical answer pattern

When answering invocation/protection/gateway questions:
1. separate call abstraction, stability protection, and entry-layer responsibilities
2. explain what problem the component solves
3. explain where it sits in the call path
4. mention the classic stack vs newer replacement direction
5. mention one common misuse or boundary

## Source notes

Distilled from the user's course materials covering:
- Feign / OpenFeign
- Hystrix fault tolerance / avalanche / monitoring / dashboard / Turbine
- Sentinel / Sentinel vs Hystrix
- Zuul / API gateway / why gateway / gateway responsibilities / Nginx+Lua comparisons
- Spring Cloud Gateway and its role as Zuul replacement direction
