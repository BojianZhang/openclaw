# Spring Cloud Code Patterns

Use this file when the user is no longer asking only for conceptual explanation and needs to understand how classic Spring Cloud sample projects are usually wired at code level.

## What the sample repos consistently show

Across the user's course codebases, a repeated module shape appears:
- registry server modules (`eureka-server`, `eureka-server02`)
- business provider modules (`service-provider`, `product-service`)
- business consumer modules (`service-consumer`, `order-service`, `order-service-rest`, `order-service-feign`)
- gateway modules (`zuul-server`, `gateway-server`)
- config server modules (`config-server`, `config-server02`)
- message producer / consumer modules (`stream-producer`, `stream-consumer`)

This is useful because it gives a predictable teaching skeleton:
1. infra nodes
2. producer/provider nodes
3. consumer/order nodes
4. optional gateway / tracing / config / messaging nodes

## Discovery patterns

### Eureka server
Typical startup pattern:
- dedicated server application class
- `@EnableEurekaServer`
- standalone registry module, often duplicated as `eureka-server02` for HA demos

### Discovery client / service registration
Typical client pattern:
- ordinary Spring Boot service app
- registration through dependencies + config
- some demos use `@EnableDiscoveryClient`
- many newer setups rely mostly on starter + config rather than heavy annotation use everywhere

Practical guidance:
- teach discovery as a module-role pattern, not just one annotation
- the module boundary matters as much as the annotation

## Feign patterns

Typical code shape:
- consumer app startup class with `@EnableFeignClients`
- interface like `ProductService.java`
- `@FeignClient("service-provider")` or `@FeignClient(value = "product-service", fallbackFactory = ...)`
- methods annotated with Spring MVC mapping metadata in OpenFeign style

Common teaching pattern:
1. define interface
2. bind it to service name
3. inject interface into consumer-side service/controller
4. optionally attach fallback or fallbackFactory

Important nuance:
- `fallbackFactory` appears repeatedly in the samples and is often more informative than a bare fallback because it can surface the cause

## Ribbon / consumer patterns

Typical classic demo shape:
- separate consumer module
- service name lookup through registry
- load-balancing rule configured globally or per service in config
- sometimes a RestTemplate-based consumer and a Feign-based consumer exist side by side to compare styles

Teaching advice:
- explain RestTemplate consumer and Feign consumer as two client styles over similar discovery/load-balancing foundations

## Hystrix / Sentinel patterns

### Hystrix style in samples
Patterns seen in demos:
- Feign client with `fallbackFactory`
- RestTemplate-style consumer with circuit-breaker enabling comment or annotation path
- dedicated monitoring modules / streams in monitoring demos

Implementation cues worth preserving:
- isolate fallback logic into explicit classes
- do not bury fallback logic in controller code
- monitoring endpoints are part of the demo story, not an afterthought

### Sentinel style in samples
Patterns seen in demos:
- `@SentinelResource`
- Sentinel-adapted RestTemplate imports
- exception / block handling utility classes
- gateway integration modules with Sentinel gateway flow-rule configuration

Implementation cues worth preserving:
- Sentinel often appears not just in service methods but also in gateway-level rule configuration
- block handling and fallback responsibilities are often separated into helper classes

## Gateway patterns

### Zuul demos
Patterns seen:
- dedicated gateway module
- `@EnableZuulProxy`
- optional Sentinel-enhanced gateway module
- separate fallback/provider/config classes for gateway-level handling

### Gateway demos
Patterns seen:
- dedicated gateway module
- route definition through `RouteLocatorBuilder`
- optional Sentinel-enhanced gateway module with gateway flow-rule configuration

Teaching advice:
- explain gateway as its own application, not as a library sprinkled into every service
- route definition and gateway protection config should be treated as first-class gateway concerns

## Tracing patterns

Sleuth demos usually show:
- gateway + order-service + product-service shape
- Feign client path retained
- tracing added through dependency/config rather than complex business-code changes

Important lesson:
- tracing value often comes from preserving a realistic call chain in the demo, not from writing a lot of tracing code manually

## Stream patterns

Patterns seen in samples:
- producer and consumer as separate modules
- classic binder interfaces like `Source`, `Sink`, or custom processor interfaces
- `@EnableBinding(...)`
- producer classes and consumer/listener classes separated by responsibility

Implementation cues worth preserving:
- keep producer and consumer responsibilities explicit in code structure
- custom bindings/processors are useful when the sample wants to show richer topologies than simple Source/Sink

## Config / Bus / Apollo patterns

### Config server demos
Patterns seen:
- dedicated `config-server` modules
- `@EnableConfigServer`
- separate client modules consuming config
- `@RefreshScope` used at the consumer/controller layer to demonstrate refresh effects

### Bus demos
Patterns seen:
- config-server cluster + multiple config clients
- `@RefreshScope` on client-facing config controller endpoints
- demo structure designed to show cluster-wide refresh propagation

### Consul config demos
Patterns seen:
- lightweight client modules
- `@RefreshScope` still central to showing dynamic config refresh behavior
- emphasis on simpler one-stop config usage when Consul is already present

### Apollo demos
Patterns seen:
- client apps with `@EnableApolloConfig`
- app modules focused on consuming centrally managed config rather than implementing a custom config server

## Reusable implementation heuristics

1. Separate infra modules from business-service modules.
2. Let startup annotations reveal module role.
3. Keep fallback / block / gateway rule logic in dedicated classes, not scattered through controllers.
4. Use paired modules (`server`/`server02`, `order-service`/`order-service02`) to demonstrate HA, clustering, or propagation behavior.
5. Use controllers primarily to expose behavior; keep integration logic in service/config/fallback classes.

## Source notes

Distilled from the user's code samples under the Spring Cloud course directories, including demos for Eureka, Consul, Feign, Hystrix, Sentinel, Zuul, Gateway, Sleuth, Stream, Config, Bus, Consul Config, and Apollo.
