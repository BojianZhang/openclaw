# Service Discovery and Load Balancing

Use this file when the question is about registry centers, Eureka/Consul basics, service discovery flow, or Ribbon-style client-side load balancing.

If the user only needs a high-level picture of Spring Cloud and its generation shift, read `spring-cloud-foundations.md` first.

## Registry center role

A registry center is the service-directory layer of a microservice system.
Its core jobs are:
- service registration
- service discovery
- health-based instance availability
- addressing support for elastic scaling
- helping routing and failover happen without hardcoding provider addresses

A clean explanation:
- providers register themselves
- consumers discover available providers
- the registry plus client/load-balancer logic helps choose reachable instances

## Why a registry center is needed

Without a registry center, distributed calls degrade into hardcoded addresses or manual endpoint management.
In real systems you also need:
- timely registration and discovery
- unhealthy instance removal
- service scaling visibility
- dynamic routing support
- high availability of the registry itself

## Eureka essentials

Use when the question is about classic Netflix-style discovery.

Practical points:
- Eureka is a REST-based service discovery component from Netflix
- in Spring Cloud Netflix it acts as a classic registry/discovery center
- typical roles:
  - **Eureka Server**: registry center
  - **Service Provider**: registers itself
  - **Service Consumer**: fetches service list and invokes providers

Good interview wording:
- Eureka is best understood as an AP-style discovery system optimized for service availability and registration/discovery convenience in Spring Cloud Netflix ecosystems.

## Consul essentials

Use when the question is about a more integrated alternative.

Practical points:
- Consul is a HashiCorp tool for service discovery and configuration
- built-in strengths include service discovery, health checks, KV storage, multi-datacenter support, and HTTP/DNS interfaces
- common role model:
  - **server** nodes hold cluster state and coordinate
  - **client** nodes forward HTTP/DNS requests and interact with the local server cluster
- compared with Eureka, Consul is often framed as more "one-stop" because discovery and config can both live in the same system

## Registry comparison intuition

From the course materials, a practical compare path is:
- **Eureka**: classic Spring Cloud Netflix choice, service-discovery friendly, often remembered as AP-leaning
- **Consul**: one-stop discovery + health check + KV config + multi-DC support
- **Nacos**: strong domestic ecosystem fit, both registration and config are common
- **ZooKeeper**: older CP-oriented coordination choice with stronger coordination flavor than "simple registry" flavor

Do not turn comparison into CAP slogan recitation only. Explain operational style and ecosystem fit.

## Client-side vs server-side load balancing

Two common models:
- **server-side / centralized**: a separate facility like Nginx or F5 chooses the provider instance
- **client-side / in-process**: the consumer gets provider addresses from the registry and chooses an instance inside the client process

Ribbon belongs to the second model.

## Ribbon essentials

Use when the question is about classic client-side balancing in Spring Cloud Netflix.

Key points:
- Ribbon is a client-side load balancing library
- it usually works inside the consumer process
- it selects a provider instance from the discovered instance list
- Feign historically uses Ribbon underneath in classic stacks

Useful explanation:
- Ribbon does not replace the registry center; it consumes registry information and then chooses a target instance according to a rule.

## Ribbon common strategies

High-frequency strategy explanations:
- **RoundRobinRule**: sequential polling; the classic default explanation
- **RandomRule**: randomly choose an instance
- **WeightedResponseTimeRule**: lower-latency instances tend to receive more traffic
- **BestAvailableRule**: prefer instances with the fewest active requests, while avoiding tripped ones
- **RetryRule**: retry with rule-based selection when appropriate

Do not oversell strategy switching. The real question is whether the traffic pattern, instance heterogeneity, and failure mode justify a change.

## Practical answer pattern

When explaining discovery + balancing:
1. define registry center role
2. explain registration and discovery flow
3. explain how the consumer chooses an instance
4. separate registry responsibility from load-balancer responsibility
5. mention health checks, failover, and scaling implications

## Source notes

Distilled from the user's course materials covering:
- 注册中心基础 / 为什么需要注册中心
- Eureka / Eureka roles
- 常见注册中心对比
- Consul introduction / roles / working principles
- Ribbon definition / client-side load balancing / strategy choices
