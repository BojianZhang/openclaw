# Anti-Patterns

## Do not recommend microservice splitting by default

A large codebase alone is not enough reason to split services.

## Do not hide failure cost behind framework convenience

Timeouts, retries, startup behavior, and config ownership must stay explicit.

## Do not let Spring structure substitute for business boundaries

Package layers are useful, but real ownership and integration cost matter more.

## Do not over-template simple services

Use templates to clarify common structure, not to force unnecessary ceremony.

## Do not investigate every layer at once

For troubleshooting, narrow the dominant failing path first.

## Do not treat Eureka, Consul, Nacos, Config, and Apollo as interchangeable boxes

They may overlap in capability, but their operational model, governance depth, and ecosystem fit differ.

## Do not assume Feign or OpenFeign removes distributed-system complexity

It reduces call boilerplate, not timeout, retry, idempotency, versioning, or fallback risk.

## Do not switch Ribbon or load-balancing rules casually

A different rule is not automatically better; match the rule to traffic shape, instance behavior, and failure mode.

## Do not use Hystrix or Sentinel as a slogan for "system stability"

Always clarify whether the issue is isolation, circuit state, fallback behavior, traffic control, or system protection.

## Do not push every cross-cutting rule into the gateway

Gateways should centralize boundary concerns, but not become a dumping ground for business logic.

## Do not confuse tracing with root-cause diagnosis

Sleuth / traces narrow the path; they do not replace evidence-based reasoning.

## Do not introduce Stream or MQ abstraction without a real async or decoupling need

Message-driven design adds eventual-consistency and operability costs.

## Do not choose a config center only by familiarity

Compare Spring Cloud Config, Consul Config, and Apollo by governance needs, refresh model, operational footprint, and environment complexity.
