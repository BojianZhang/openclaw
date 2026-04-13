---
name: java-spring-microservice
description: Build, review, troubleshoot, and structure Java Spring Boot and microservice systems with focus on startup failures, configuration, bean wiring, project structure, service boundaries, integration patterns, and governance decisions. Use when working on Spring Boot project structure, startup/configuration issues, dependency injection problems, profile/environment handling, service decomposition, or microservice boundary and governance questions. Prefer `java-network-microservices` when the primary issue is HTTP/TCP timeout chains, connection reuse, reset errors, retries, proxy/gateway behavior, or transport-level call instability.
---

# Java Spring Microservice

## Goal

Guide Spring Boot engineering and microservice design with practical focus on project structure, startup behavior, configuration, integration boundaries, service decomposition, and operational troubleshooting.

## Scope

In scope:
- Spring Boot project practices and structure
- startup failures and configuration issues
- bean wiring, profile/environment handling, and dependency setup
- service decomposition and microservice split decisions
- integration patterns and service-governance decisions
- common backend engineering templates in Spring services
- practical patterns for exception handling, config, HTTP clients, and batch work

Out of scope unless directly relevant:
- JVM tuning as a primary topic
- MySQL and Redis deep optimization
- pure transport-layer HTTP/TCP diagnosis
- timeout/reset/retry issues where protocol or intermediary behavior is the main question
- pure design-pattern or refactor-first questions without Spring or service context

## Workflow

1. Identify whether the problem is project structure, startup/configuration, bean wiring, service boundary, integration pattern, or distributed-system concern.
2. Clarify whether the user needs explanation, troubleshooting, decision support, or implementation guidance.
3. Prefer simple Spring Boot solutions before introducing microservice complexity.
4. For service-splitting questions, explain the business and operational tradeoffs before recommending decomposition.
5. For troubleshooting, narrow the failure to startup, configuration, dependency, wiring, integration choice, or runtime path.
6. If the core issue is timeout chains, keep-alive, connection reuse, reset errors, retries, or proxy/gateway behavior, hand off to `java-network-microservices`.

## When To Read References

- Read `references/spring-boot-practice.md` for project structure and practical guidance.
- Read `references/microservices-practice.md` for service boundary and governance decisions.
- Read `references/microservice-foundations.md` when the user is asking foundational questions such as what microservices are, architecture evolution, SOA vs microservices, Dubbo vs Spring Cloud, AKF, stateless services, or RESTful style.
- Read `references/spring-cloud-foundations.md` when the question is specifically about what Spring Cloud is, its component map, Netflix-era vs newer generation evolution, Spring Cloud Alibaba, or Spring Cloud version/release-train understanding.
- Read `references/service-discovery-and-load-balancing.md` when the question is about Eureka, Consul, registry-center role, service discovery flow, or Ribbon-style client-side load balancing.
- Read `references/service-calls-fault-tolerance-and-gateways.md` when the question is about Feign/OpenFeign, Hystrix, Sentinel, Zuul, Gateway, or how invocation/fault-tolerance/gateway responsibilities fit together.
- Read `references/tracing-messaging-and-config-centers.md` when the question is about Sleuth, Stream, Config, Bus, Consul Config, Apollo, or broader tracing/messaging/config-center reasoning.
- Read `references/spring-cloud-code-patterns.md` when the user needs code-level module layout, startup annotation patterns, fallback placement, gateway route config shape, or classic sample-project wiring for Spring Cloud components.
- Read `references/spring-cloud-config-patterns.md` when the user needs realistic config-key patterns, bootstrap/application.yml shapes, registry/config-center key conventions, or classic Spring Cloud sample configuration layouts.
- Read `references/spring-cloud-class-role-templates.md` when the user needs class-level responsibility templates for startup classes, configuration classes, Feign clients, fallback/fallbackFactory classes, controllers, property holders, or gateway/block-handler classes.
- Read `references/spring-cloud-minimal-templates.md` when the user wants the smallest reusable starting skeletons for Eureka server, provider, Feign consumer, gateway, config server/client, typed config holder, Apollo client, or Stream producer/consumer, with a clear upgrade path for real projects.
- Read `references/spring-cloud-starter-combinations.md` when the user wants staged starter packs such as “registry + provider + Feign consumer”, “gateway + consumer + provider”, “config server + config client”, “Apollo client + typed config holder”, or other gradual build-up combinations for a self-built project.
- Read `references/spring-cloud-evolution-roadmap.md` when the user wants a phase-by-phase project evolution path, such as when to stay monolithic longer, when to split first services, when to add gateway/config center/Bus/Sentinel/Stream, or how to upgrade a self-built project gradually without overengineering.
- Read `references/microservice-project-evolution-sample.md` when the user wants a realistic multi-version project evolution example showing how a microservice project grows module by module over time.
- Read `references/microservice-project-module-taxonomy.md` when the user needs a way to classify modules in a multi-module microservice project into platform, shared support, data/integration, business capability, and message workflow roles.
- Read `references/microservice-project-frontend-backend-shape.md` when the user is reasoning about a Java microservice backend together with a separate frontend shell, gateway boundary, page-driven service decomposition, or frontend mock-vs-gateway evolution.
- Read `references/microservice-project-module-skeletons.md` when the user wants reusable whole-repo module skeletons for a multi-module Java microservice project, including parent aggregator, platform modules, shared support modules, data/integration modules, business capability modules, message workflow modules, and frontend shell pairing.
- Read `references/microservice-project-stage-upgrade-signals.md` when the user needs concrete decision signals for when to move from one project stage to the next, such as when to split first services, when to add fallback/gateway/config center/Bus/traffic governance/messaging, and what not to add yet.
- Read `references/ecommerce-platform-module-evolution.md` when the user wants a realistic Java shopping-platform evolution sample covering portal, manager, SSO, order, shared RPC/common modules, and the staged introduction of Redis, Elasticsearch, payment, SMS, and cloud storage.
- Read `references/ecommerce-platform-boundaries.md` when the user needs help reasoning about portal/admin/SSO/order/common/RPC module boundaries in a modular e-commerce platform.
- Read `references/ecommerce-platform-upgrade-signals.md` when the user needs concrete signals for when a shopping platform should introduce cloud storage, Redis, Elasticsearch, SSO, order, payment, or SMS capability, and what not to introduce yet.
- Read `references/ecommerce-platform-class-patterns.md` when the user needs class-level responsibility guidance for portal, manager, SSO, order, common, RPC, and support capability integration classes in a modular shopping platform.
- Read `references/ecommerce-platform-config-and-rpc-patterns.md` when the user needs parent-level dependency governance, module-level config/integration patterns, or Dubbo + ZooKeeper interpretation in a modular shopping platform.
- Read `references/ecommerce-platform-starter-combinations.md` when the user wants staged starter combinations for building a shopping platform gradually rather than adopting the full capability set at once.
- Read `references/ecommerce-platform-minimal-skeletons.md` when the user wants the smallest reusable repo/module skeletons for common, portal, manager, SSO, order, and RPC layers in a shopping platform.
- Read `references/ecommerce-platform-comparison-samples.md` when the user wants to compare 乐SHOP and 易购商城 as two different Java shopping-platform evolution styles, including shared boundaries, stack differences, and which sample better fits a given architecture question.
- Read `references/traditional-web-project-layering.md` when the user needs a clean explanation of classic JSP/Servlet/DAO-style project layering, BaseDao value, session/cookie login handling, or how a simple Java Web single-project system grows by modules.
- Read `references/dubbo-evolution.md` when the user needs more historical or conceptual background on RPC and service-governance evolution.
- Read `references/paxos-to-zookeeper.md` when the user needs more distributed-coordination background behind service governance and platform decisions.
- Read `references/spring-boot-troubleshooting-checklist.md` for structured debugging.
- Read `references/spring-boot-startup-failures.md` for startup diagnostics.
- Read `references/microservices-checklist.md` for system-level checks.
- Read `references/microservice-splitting-qa.md` for common split questions.
- Read `references/backend-troubleshooting.md` when the issue spans startup, runtime, dependencies, JVM, data access, or network symptoms.
- Read `references/examples.md` when the user needs concrete troubleshooting or architecture response patterns.
- Read `references/anti-patterns.md` when guarding against premature microservice splits or framework-heavy overengineering.
- Read the code templates when the user needs implementation structure.

## Output Expectations

When answering:
1. Classify the Spring or service-engineering problem.
2. Explain the key Spring, configuration, or boundary mechanism.
3. Give the smallest workable solution first.
4. State when not to split or over-engineer.
5. Provide phased implementation or troubleshooting steps.
6. Mention operational impact when relevant.
