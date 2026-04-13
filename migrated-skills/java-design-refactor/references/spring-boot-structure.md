# Spring Boot Structure Guidance

Use this file when the Java codebase is built on Spring Boot.

## Common Structural Problems

### Fat Controller

Symptoms:
- Controller validates business rules
- Controller orchestrates too many collaborators
- HTTP layer leaks into domain decisions

Preferred direction:
- Keep controllers focused on transport concerns
- Move business decisions into application or domain services
- Keep request and response mapping near the edge

### God Service

Symptoms:
- One service owns many unrelated use cases
- Transaction boundaries, validation, orchestration, and persistence are tangled

Preferred direction:
- Split by use case or domain capability
- Separate command-style orchestration from reusable domain behavior

### Repository Abuse

Symptoms:
- Repositories contain business logic
- Query shape dictates domain behavior
- Service layer is just pass-through glue

Preferred direction:
- Keep repositories focused on persistence access
- Move business decisions upward into domain or application layer

### Annotation Spread

Symptoms:
- Spring stereotypes and framework annotations everywhere
- Core logic hard to test without full context startup

Preferred direction:
- Limit framework annotations to entry points, config, and adapters where practical
- Keep pure logic in plain Java classes when possible

## Suggested Layer Intent

This is guidance, not a mandatory template.

- `controller` or `api`: HTTP transport, auth-adjacent checks, request/response mapping
- `application` or `service`: use-case orchestration, transactions, coordination
- `domain`: business rules, policies, value objects, entities, domain services
- `infrastructure`: persistence, messaging, SDK clients, framework integration

Group by business capability when the project is large enough. Avoid a package tree that is technically clean but business-opaque.

## Practical Rules

- Keep DTOs out of domain logic
- Keep entities from becoming giant bags of getters and setters
- Avoid returning JPA entities directly from controllers
- Avoid stuffing all logic into `ServiceImpl`
- Do not use mapper layers as dumping grounds for business decisions
- Be explicit about transaction boundaries

## When To Stay Simple

Do not over-engineer small CRUD modules. If the use case is straightforward and unlikely to grow, a simple service plus repository may be enough. Add heavier boundaries only when change pressure justifies them.
