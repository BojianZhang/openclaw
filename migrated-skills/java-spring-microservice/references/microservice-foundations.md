# Microservice Foundations

Use this file when the user is asking foundational microservice questions rather than concrete Spring Boot startup/debug details.

## What this reference covers
- architecture evolution from monolith to vertical split to distributed service to microservice
- what microservices are and what they are not
- SOA vs microservices
- Dubbo vs Spring Cloud tradeoffs at interview / architecture-intuition level
- AKF scaling dimensions
- front-end/back-end separation, stateless-service principle, and RESTful communication style

## Architecture evolution

A practical interview-friendly path is:
1. **single application**: all capabilities in one deployment; simple deployment and low early cost
2. **vertical application split**: split by coarse business modules when a single codebase grows too large
3. **distributed service architecture**: extract shared core capabilities into reusable services; RPC/service-governance pressure appears
4. **microservice architecture**: split around narrower business capabilities with stronger independent deployment, team ownership, and operational autonomy

Do not tell the story as "microservices replaced monoliths because monoliths are bad". The better framing is that scale, delivery speed, team autonomy, and operational needs changed.

## What a microservice is

Use a restrained definition:
- a small service built around a business capability
- runs as an independent process / deployable unit
- communicates through lightweight mechanisms such as HTTP APIs or messaging
- owns its own evolution and ideally its own data boundary
- can be deployed independently with minimal centralized control

Important nuance:
- "small" does **not** mean tiny for its own sake
- microservice is an **architecture style**, not a mandatory deployment religion
- RPC, REST, and MQ are communication choices, not the definition itself

## Why teams adopt microservices

Typical gains:
- stronger business-capability ownership
- independent deployment and scaling
- clearer team autonomy
- technology choice flexibility
- easier isolated iteration for the right kind of organization

Typical costs:
- higher ops and observability burden
- distributed-system complexity
- interface/version compatibility problems
- harder troubleshooting across service boundaries
- transactions, consistency, timeout, and retry complexity

Always mention both sides. Interview answers that only praise benefits sound shallow.

## SOA vs microservices

Useful contrast:
- microservices can be viewed as a finer-grained and more modern SOA-style implementation
- SOA often emphasizes broader enterprise integration, shared governance, and sometimes shared data/platform layers
- microservices emphasize bounded context, smaller independently deployable services, decentralized ownership, and lighter communication mechanisms
- SOA often tolerates larger shared databases or enterprise bus patterns; microservices push harder toward service-local data ownership

Do not oversimplify to "SOA is old, microservices are new". The real difference is granularity, ownership model, and data/governance style.

## Dubbo vs Spring Cloud

Use this file for high-level tradeoff explanation, not protocol trivia.

A practical comparison:
- **Dubbo**: RPC-centered, stronger interface-style service invocation, commonly seen in domestic Java stacks, usually lower serialization / bandwidth overhead in traditional RPC usage
- **Spring Cloud**: broader microservice ecosystem thinking around configuration, gateway, tracing, bus, tasking, and service integration; common communication style is HTTP/REST

Explain the tradeoff like this:
- Dubbo often feels more like "remote method call"
- Spring Cloud often feels more like "HTTP service ecosystem"
- Dubbo may have stronger performance characteristics in some RPC scenarios
- Spring Cloud often has lower conceptual entry cost for teams already deep in Spring and web APIs
- both still face the same distributed-system truths: latency, retries, partial failure, versioning, and governance

Do not let the user conclude that "RPC is advanced so it is always better".

## AKF scaling model

Use AKF to explain that service splitting is only one scaling axis.

- **X-axis**: horizontal cloning; replicate the same service behind load balancing
- **Y-axis**: functional decomposition; split by business capability (this is where microservice decomposition sits)
- **Z-axis**: data / user / geography partitioning; shard by region, tenant, or other partition key

Good reasoning pattern:
- if load is the main issue, first consider X-axis
- if business capability and ownership are the issue, consider Y-axis
- if scale is driven by data locality or user partitioning, consider Z-axis

This prevents the classic mistake of using service splitting to solve every problem.

## Front-end / back-end separation

Treat front-end/back-end separation as a delivery and interface-governance principle, not the definition of microservices.

Benefits:
- cleaner API contracts
- independent front-end and back-end iteration
- easier support for web, mobile, and multiple clients
- clearer backend responsibility around unified data/service APIs

Caution:
- front-end/back-end separation alone does not make a system microservices

## Stateless service principle

Use a precise explanation:
- stateless services avoid depending on in-memory conversational state inside one application node
- business/session/cache state should move to shared or dedicated stateful stores when elasticity and node replacement matter
- stateless compute nodes scale and replace more easily

Concrete examples:
- local session -> Redis / distributed session solution
- local cache that must survive node churn -> distributed cache / separately managed state service

Nuance:
- the architecture still contains state; the point is to avoid pinning request correctness to one compute node's private memory

## RESTful communication style

When explaining why REST is often chosen in microservice systems:
- HTTP is widely supported and operationally familiar
- JSON is easy for humans and machines to inspect
- language interoperability is strong
- security, proxying, and ecosystem tooling are mature

But do not oversell it:
- REST is not automatically superior to every RPC option
- internal high-throughput systems may still use RPC or messaging where appropriate
- communication style should follow boundary, performance, operability, and team context

## How to answer foundational questions

A strong answer usually follows this pattern:
1. define the concept precisely
2. explain why teams use it
3. state the tradeoffs or costs
4. give the boundary / misuse warning
5. if relevant, compare with adjacent concepts (SOA, monolith, Dubbo, REST)

## Source notes

Distilled from the user's Spring Cloud course documents in `006_document/`, including topics on:
- 微服务架构介绍 / 技术架构演变
- 什么是微服务
- SOA 与 MicroServices 的区别
- Dubbo 和 SpringCloud 的区别
- 微服务设计：AKF 拆分原则、前后端分离原则、无状态服务、Restful 通信风格
