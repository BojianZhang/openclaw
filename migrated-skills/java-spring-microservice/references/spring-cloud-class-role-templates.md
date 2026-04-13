# Spring Cloud Class Role Templates

Use this file when the user needs code-structure guidance about what different Spring Cloud classes are supposed to do.

## 1. Startup application class

Typical responsibility:
- define the module role
- enable module-level framework capability
- bootstrap the Spring Boot app

Common shapes from the samples:
- registry server: `@EnableEurekaServer`
- Feign consumer: `@EnableFeignClients`
- circuit-breaker consumer: `@EnableCircuitBreaker`
- config server: `@EnableConfigServer`
- Apollo client: `@EnableApolloConfig`
- gateway app: usually plain `@SpringBootApplication`, with extra route/rule config classes nearby

Template guidance:
- keep startup classes thin
- do not push business logic into them
- let them answer only one question: what kind of node is this module?

## 2. Configuration class

Typical responsibility:
- define infrastructure beans
- define route/rule/filter/serializer/key-resolver beans
- centralize integration-specific plumbing

Seen in samples:
- `RestTemplate` bean + `@LoadBalanced`
- Sentinel-adapted `RestTemplate` with block/fallback handlers
- Gateway route builder configuration
- gateway key resolver config
- Zuul Sentinel rule registration config
- Redis config / cache serialization config

Template guidance:
- configuration classes should own framework plumbing, not business use cases
- if a bean exists to wire integration behavior, it belongs here first

## 3. Feign client interface

Typical responsibility:
- declare remote contract at consumer side
- bind service name to method signature

Seen in samples:
- `@FeignClient("service-provider")`
- `@FeignClient(value = "product-service", fallbackFactory = ...)`

Template guidance:
- keep transport mapping here
- keep business orchestration in service classes
- attach fallback/fallbackFactory at the client boundary instead of hiding it deeper in controllers

## 4. Fallback / FallbackFactory class

Typical responsibility:
- provide degraded return values when downstream calls fail
- optionally log/inspect the triggering exception

Seen in samples:
- simple fallback class implementing the same Feign interface
- `FallbackFactory<T>` that logs the throwable and returns an anonymous implementation
- gateway fallback providers returning standard error payloads
- Sentinel block/fallback helper utilities for RestTemplate/gateway

Template guidance:
- prefer dedicated fallback classes over burying fallback data in controller methods
- when cause visibility matters, prefer `FallbackFactory`
- keep fallback payloads explicit and easy to recognize as degraded data

## 5. Controller class

Typical responsibility:
- expose HTTP endpoints
- delegate to service/config holder
- present demo-visible behavior

Seen in samples:
- order/product query endpoints
- config inspection endpoints like `/name` and `/mysql`
- very thin endpoint layers delegating to service classes

Template guidance:
- controllers should expose behavior, not own remote-call plumbing or fallback policy
- for config demos, controllers often exist mainly to prove refresh/consumption works

## 6. Property holder / config holder class

Typical responsibility:
- bind config into typed fields
- provide one place to represent externalized config inside the app

Seen in samples:
- `@ConfigurationProperties(prefix = "mysql")`
- Apollo client `ConfigProperties` with grouped fields

Template guidance:
- when multiple related config fields exist, prefer a typed holder over many scattered `@Value`s
- use controller only to display/verify the values, not as the storage model

## 7. Exception / block handler utility class

Typical responsibility:
- centralize block-handling or fallback response building for framework-level protection

Seen in samples:
- Sentinel `ExceptionUtil` for `@SentinelRestTemplate`
- gateway block response handlers

Template guidance:
- keep protection-framework response shaping out of business controllers
- make handler naming explicit: block, fallback, degrade, gateway, etc.

## 8. Gateway fallback / gateway rule class

Typical responsibility:
- define route-specific fallback behavior
- define flow rules, API groups, filter beans, block handlers

Seen in samples:
- Zuul `FallbackProvider`
- Sentinel gateway rule config classes
- custom block-response classes

Template guidance:
- gateway-specific resilience should live in gateway modules, not downstream business services
- route name / API group naming should be explicit and stable

## Quick role map

- `*Application.java` -> module identity and startup
- `*Configuration.java` / `*Config.java` -> framework wiring and integration beans
- `*Service.java` / Feign interface -> remote contract or business orchestration
- `*Fallback*.java` -> degraded path and error-aware fallback behavior
- `*Controller.java` -> endpoint exposure and minimal delegation
- `*Properties.java` -> typed external config binding
- `*ExceptionUtil.java` / block handler -> framework-level protection response shaping

## Source notes

Distilled from the user's sample projects for Hystrix, Sentinel, Zuul, Gateway, Config, Consul Config, and Apollo.
