# Spring Boot Layering Template

Use this template when a Spring Boot project needs clearer structural boundaries.

## Intent

Keep controllers focused on transport, services on orchestration, domain logic on business rules, and infrastructure on integrations.

## Practical rules

- Do not bury business decisions inside controllers.
- Do not let mapper or config classes become logic sinks.
- Keep external integrations near the edge.
