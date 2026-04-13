# Spring Cloud Starter Combinations

Use this file when the user does not just want one isolated minimal template, but wants a sensible starter combination that can grow into a real project gradually.

These are not production architectures. They are staged starter packs.

## Combination A: Registry + Provider + Feign Consumer

### Best for
- first service-to-service call demo
- learning service registration + discovery + consumer/provider split
- replacing hardcoded URL calls with service-name-based invocation

### Modules
- `eureka-server`
- `product-service`
- `order-service`

### Core pieces
- registry startup via `@EnableEurekaServer`
- provider exposes `/product/{id}`
- consumer uses `@EnableFeignClients`
- Feign client binds to `product-service`

### Why this is the best first combo
It teaches the minimum useful distributed shape:
- one infra node
- one provider
- one consumer
- one remote contract

### Upgrade path
1. add `FallbackFactory`
2. add second registry node for HA demo
3. add gateway in front
4. later add config center

## Combination B: Registry + Provider + Feign Consumer + FallbackFactory

### Best for
- when the user already understands basic Feign usage
- when the project should start with a cleaner resilience seam

### Modules
- `eureka-server`
- `product-service`
- `order-service`

### Extra compared with A
- `@FeignClient(..., fallbackFactory = ...)`
- dedicated fallback/factory class
- explicit degraded return values

### Why choose this over plain fallback
- preserves exception visibility
- easier to add logging and reason-specific degradation later
- cleaner growth path into real project behavior

### Upgrade path
1. classify failures
2. add timeout governance
3. add metrics/log tags around fallback paths

## Combination C: Registry + Gateway + Provider + Feign Consumer

### Best for
- when the project already needs one unified external entry
- when you want to separate external access from internal service-to-service calls early

### Modules
- `eureka-server`
- `gateway-server`
- `product-service`
- `order-service`

### Core pieces
- gateway route config points to `lb://product-service` or `lb://order-service`
- consumer still uses Feign for internal calls
- clients hit gateway instead of every service directly

### Why this is a strong next step
It introduces boundary layering without pulling in too much complexity.

### Upgrade path
1. add custom gateway filter
2. add simple rate limiting / key resolver
3. later add Sentinel gateway protection

## Combination D: Registry + Config Server + Config Client

### Best for
- when the project has begun to accumulate environment-specific config
- when you want to stop scattering runtime config in local files

### Modules
- `eureka-server` (optional but recommended in the course-style ecosystem)
- `config-server`
- `order-service` or `config-client`

### Core pieces
- Config Server with Git-backed config source
- client bootstrap via `bootstrap.yml`
- client endpoint proving config consumption

### Why this is the right config-center first step
It teaches central config without immediately adding cluster-wide refresh complexity.

### Upgrade path
1. add `@RefreshScope`
2. add second config client instance
3. later add Bus for propagation

## Combination E: Config Server + Bus + Multiple Clients

### Best for
- when the user already has classic Config in place
- when clustered refresh behavior matters

### Modules
- `config-server`
- `config-server02` (optional demo cluster)
- `order-service`
- `order-service02`
- message broker dependency/path

### Core pieces
- `spring-cloud-starter-bus-amqp`
- actuator `bus-refresh` exposure
- `@RefreshScope` on client-facing config endpoints

### Why this combo matters
It demonstrates the moment config goes from "centralized" to "broadcast and coordinated".

### Upgrade path
1. tighten actuator exposure
2. separate refresh endpoints and operational policy
3. audit who can trigger refresh in real environments

## Combination F: Consul Discovery + Consul Config Client

### Best for
- when the project wants a lighter one-stop path for discovery + config
- when the team does not want to stand up classic Config Server first

### Modules
- `order-service`
- `order-service02`
- external Consul

### Core pieces
- `spring-cloud-starter-consul-discovery`
- `spring-cloud-starter-consul-config`
- `@RefreshScope`
- optional typed config holder such as `MySQLProperties`

### Why this combo is attractive
It is operationally simpler for some teams than running separate registry + config-server stacks.

### Upgrade path
1. move from `@Value` to typed config holder
2. separate discovery concerns from config-reading concerns in code structure
3. tighten refresh and exposure endpoints

## Combination G: Apollo Client + Typed Config Holder

### Best for
- when the user wants centralized config consumption without teaching Config Server internals first
- when config governance matters more than Spring Cloud Config mechanics

### Modules
- `order-service`
- `order-service02`
- external Apollo platform

### Core pieces
- `@EnableApolloConfig`
- `apollo-client`
- typed config holder / grouped properties
- simple controller endpoint for verification

### Why this combo is useful
It starts from consumer-side config discipline and can fit real projects well when Apollo is already chosen.

### Upgrade path
1. reduce public config exposure endpoints
2. validate and group config fields
3. split sensitive and non-sensitive config representation

## Combination H: Gateway + Sentinel

### Best for
- when the project already has a gateway and needs traffic protection at the boundary
- when you want to teach gateway-level flow control separately from service-level degradation

### Modules
- `gateway-server` or `gateway-server-sentinel`
- downstream business services
- registry as needed

### Core pieces
- gateway-specific Sentinel rule config
- block handler / gateway filter configuration
- optional API group definitions

### Why this combo should come later
This is useful, but not a good first combo. It assumes boundary layering already exists.

### Upgrade path
1. start with simple route-level rules
2. then define API groups
3. then refine response shaping and observability

## Combination I: Stream Producer + Stream Consumer

### Best for
- when the project genuinely needs async/event-driven decoupling
- when the user wants to add messaging without redesigning the whole platform first

### Modules
- `stream-producer`
- `stream-consumer`
- optional second consumer instance
- binder/middleware infrastructure

### Core pieces
- `@EnableBinding(Source.class)` / `@EnableBinding(Sink.class)`
- producer-side send
- consumer-side listener

### Why this combo should not be introduced too early
Async messaging adds delivery semantics, retries, observability, and consistency cost. Use it when there is a real reason.

### Upgrade path
1. start with one producer + one consumer
2. then add grouped consumers / custom bindings
3. later evolve into richer event contracts

## Recommended adoption order for a self-built project

If the user is building their own project gradually, a sensible path is:
1. **A** Registry + Provider + Feign Consumer
2. **B** Add `FallbackFactory`
3. **C** Add Gateway
4. **D** Add Config Server + Config Client, or **F/G** if choosing Consul/Apollo path
5. **E** Add Bus only when clustered refresh actually matters
6. **H** Add Gateway + Sentinel when traffic governance becomes a real need
7. **I** Add Stream only when async/event-driven needs are explicit

## Anti-overengineering reminder

Do not start with C + D + E + H + I all at once.
A good starter combination is small enough that every added component solves a visible problem.

## How to choose fast

- Need first microservice split -> choose **A**
- Need safer remote calls -> choose **B**
- Need unified external entry -> choose **C**
- Need centralized config -> choose **D**
- Already on Consul -> choose **F**
- Already on Apollo -> choose **G**
- Need gateway traffic control -> choose **H**
- Need async/event flow -> choose **I**
