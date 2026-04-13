# Spring Cloud Evolution Roadmap

Use this file when the user is building their own project gradually and needs a staged roadmap instead of a pile of components.

This roadmap is intentionally conservative. Each stage should solve a visible problem before the next one is introduced.

## Stage 0: Single service / pre-split baseline

### Goal
Keep one service simple while clarifying business boundaries and external dependencies.

### What exists
- one Spring Boot app
- no registry
- no gateway
- local config or very small config surface

### What to focus on
- clean module boundaries inside the single app
- clear controller/service/repository layering
- isolate external calls behind interfaces if possible

### Do not rush into
- registry center
- gateway
- MQ
- config center

### Exit condition
You can clearly name which capability should become the first extracted service.

## Stage 1: First microservice split

### Recommended combination
- **Combination A**: Registry + Provider + Feign Consumer

### Goal
Prove one real service-to-service call path.

### What to introduce
- registry center
- one provider service
- one consumer service
- Feign/OpenFeign remote contract

### What this stage teaches
- service registration/discovery
- service-name-based invocation
- provider/consumer boundary

### Keep intentionally simple
- no gateway yet unless really needed
- no config center yet unless config pain is already visible
- no MQ

### Exit condition
The project has at least one stable internal service call and the team understands the new call boundary.

## Stage 2: Safer remote-call boundary

### Recommended combination
- **Combination B**: add `FallbackFactory`

### Goal
Introduce a deliberate degraded path without pulling in a large governance stack.

### What to introduce
- Feign fallback factory
- explicit degraded return policy
- logging around fallback causes

### What this stage teaches
- remote-call failure is normal
- fallback should live at the integration boundary
- graceful degradation is part of interface design

### Do not overdo yet
- avoid turning every endpoint into a giant fallback matrix
- avoid introducing too many resilience frameworks at once

### Exit condition
The team can explain what happens when downstream calls fail, and degraded behavior is no longer implicit or ad hoc.

## Stage 3: Unified external entry

### Recommended combination
- **Combination C**: Registry + Gateway + Provider + Feign Consumer

### Goal
Separate external entry from internal service topology.

### What to introduce
- gateway module
- route definitions
- light shared boundary concerns such as routing/filtering

### What this stage teaches
- edge boundary vs internal service boundary
- unified ingress
- route-based thinking

### Keep intentionally simple
- do not dump business rules into the gateway
- do not introduce advanced traffic rules too early

### Exit condition
External clients no longer need to know every internal service address.

## Stage 4: Centralized configuration

### Recommended combination
- **Combination D**: Config Server + Config Client
- or **Combination F/G** if the project is intentionally choosing Consul/Apollo path

### Goal
Move from scattered runtime config to centrally managed config.

### What to introduce
- config server/client or chosen config ecosystem
- bootstrap-stage config loading
- minimal config inspection endpoint
- typed config holder when config fields begin to multiply

### What this stage teaches
- config is a runtime dependency, not just a local file
- environment separation needs discipline
- config consumption and config governance are real design topics

### Upgrade branch choice
- choose **D** if you want classic Spring Cloud Config first
- choose **F** if you already want Consul as a one-stop path
- choose **G** if Apollo is the strategic config platform

### Exit condition
Configuration changes can be reasoned about centrally instead of by editing local service files one by one.

## Stage 5: Multi-instance refresh / config propagation

### Recommended combination
- **Combination E**: Config Server + Bus + Multiple Clients

### Goal
Handle clustered config refresh coherently.

### What to introduce
- Bus integration
- actuator refresh exposure discipline
- multi-client refresh demonstration

### What this stage teaches
- central config is not the same as coordinated propagation
- operational triggers and security around refresh matter

### Introduce only if needed
If you do not yet have multiple client instances or real propagation pain, skip this stage for now.

### Exit condition
The team can refresh clustered config intentionally instead of manually touching every node.

## Stage 6: Boundary traffic governance

### Recommended combination
- **Combination H**: Gateway + Sentinel

### Goal
Add controlled traffic protection at the system boundary.

### What to introduce
- gateway flow rules
- key resolvers / API groups
- block response shaping
- gateway-level observability around throttling/limits

### What this stage teaches
- gateway is not just routing; it is also a protection seam
- traffic governance belongs at the boundary when the problem is boundary traffic

### Do not confuse with
- service-level business fallback
- deep internal failure diagnosis

### Exit condition
The system can explicitly protect gateway-facing traffic under pressure.

## Stage 7: Async decoupling / event flow

### Recommended combination
- **Combination I**: Stream Producer + Stream Consumer

### Goal
Introduce asynchronous messaging only when there is a real decoupling or buffering need.

### What to introduce
- producer/consumer split
- message contract
- binder/middleware dependency

### What this stage teaches
- async flow changes delivery semantics
- eventual consistency and observability cost are real
- producer/consumer boundaries need explicit ownership

### Introduce only if needed
Do not add this stage just because it appears in the course stack.

### Exit condition
There is a concrete business or operational reason for async/event-driven flow, and the team accepts the new semantics.

## Recommended default roadmap for a self-built project

A practical conservative path is:
1. Stage 0: single service baseline
2. Stage 1: first split with registry + provider + Feign consumer
3. Stage 2: add `FallbackFactory`
4. Stage 3: add gateway
5. Stage 4: add config center path (Config / Consul / Apollo)
6. Stage 5: add Bus only when clustered propagation matters
7. Stage 6: add gateway traffic governance when boundary pressure appears
8. Stage 7: add Stream only when async need is explicit

## Quick decision rules

- If your problem is only internal code complexity -> stay at Stage 0 longer
- If your problem is first service split -> go to Stage 1
- If your problem is downstream instability -> Stage 2
- If your problem is too many external entry points -> Stage 3
- If your problem is config sprawl -> Stage 4
- If your problem is cluster-wide config refresh -> Stage 5
- If your problem is gateway traffic pressure -> Stage 6
- If your problem is sync coupling / buffering / async workflow -> Stage 7

## Anti-pattern warning

Do not jump from Stage 0 straight to Stage 4/5/6/7 unless there is already a real production-shaped need. A staged project grows better when every added layer solves a pain the team can already feel.
