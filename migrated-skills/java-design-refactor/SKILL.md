---
name: java-design-refactor
description: Design and refactor Java codebases with emphasis on object-oriented design, design pattern selection, layering, module boundaries, code smell remediation, and behavior-preserving restructuring. Use when reviewing or improving Java or Spring Boot architecture, class design, responsibilities, abstractions, legacy code structure, or refactoring plans.
---

# Java Design Refactor

Improve Java code structure without unnecessary rewrites. Focus on clearer responsibilities, better abstractions, maintainable module boundaries, and safe incremental refactoring.

## Workflow

1. Identify the concrete design problem before proposing solutions.
2. Classify the issue as one or more of: responsibility, coupling, abstraction, layering, duplication, extensibility, or framework leakage.
3. Prefer the smallest behavior-preserving improvement first.
4. Introduce a design pattern only when it reduces real complexity, branching, duplication, or coupling.
5. Separate domain logic, orchestration, and infrastructure concerns.
6. For larger changes, propose a staged migration plan instead of a big-bang rewrite.

## Core Heuristics

- Prefer removing accidental complexity before adding abstraction.
- Prefer composition over inheritance unless inheritance models a true is-a relationship and remains stable.
- Prefer explicit boundaries over clever generic frameworks.
- Keep business rules out of controllers, entity mappers, and infrastructure adapters.
- Keep Spring annotations and framework concerns from spreading deep into core domain code unless the project is intentionally framework-centric.
- Avoid god classes, deep call chains, and methods that mix validation, orchestration, persistence, and business rules.
- Preserve behavior first; optimize architecture second.

## Common Targets

- Long methods with mixed concerns
- God services or god managers
- Switch-heavy branching for business variants
- Duplicate validation or mapping logic
- Leaky service layers
- Transaction scripts pretending to be domain models
- Tight coupling to Spring, JPA, or external SDKs
- Package structures that group by technical type but hide business boundaries

## Refactor Strategy

### Small refactors

Use for local complexity with low migration risk.

- Extract method
- Rename for clarity
- Split conditionals
- Move method or field
- Remove duplication
- Replace magic values with named constants or value objects
- Encapsulate construction or validation

### Medium refactors

Use when responsibilities are mixed across a few classes.

- Extract service or domain collaborator
- Extract strategy for branching business rules
- Introduce interface at external or infrastructure boundaries
- Separate orchestration from domain logic
- Replace conditional logic with polymorphism where justified
- Split package or module by responsibility

### Large refactors

Use when the architecture itself causes recurring friction.

- Redesign module or aggregate boundaries
- Replace inheritance trees with composition
- Introduce ports-and-adapters boundaries around external systems
- Isolate legacy code behind anti-corruption layers
- Split monolithic services into cohesive components with explicit contracts

## How To Respond

When reviewing or proposing changes:

1. State the design problem clearly.
2. Explain why the current structure hurts maintainability, testability, or extensibility.
3. Give the smallest safe refactor first.
4. Mention tradeoffs and what not to change yet.
5. For large changes, provide a phased plan with safe checkpoints.
6. Use Java and Spring Boot idioms when they help, but do not force patterns for style alone.

## When To Read References

- Read `references/smells.md` when identifying code smells or mapping symptoms to likely refactors.
- Read `references/patterns.md` when deciding whether a design pattern is appropriate.
- Read `references/refactor-playbook.md` when planning phased refactors for legacy code.
- Read `references/spring-boot-structure.md` when the codebase uses Spring Boot or has layering and framework-boundary problems.
- Read `references/examples.md` when the user needs concrete review or refactor response patterns.
- Read `references/anti-patterns.md` when guarding against over-engineering, pattern cargo culting, or rewrite-heavy advice.
- Read `references/project-architecture-guidelines.md` when the problem involves module boundaries, package structure, layering, or system evolution.
- Read `references/design-patterns-qa.md` and `references/refactoring-qa.md` for reusable explanation patterns.
- Read `references/design-patterns-core.md`, `references/refactoring-core.md`, and `references/clean-code-core.md` for concept-level reinforcement from the migrated corpus materials.
- Read `references/head-first-design-patterns.md` when the user needs a broader pattern-oriented deep summary beyond the compact core cards.
- Read `references/refactoring.md` when the user needs a broader refactor-oriented deep summary beyond the compact core and playbook references.
- Read `references/module-package-template.md`, `references/facade-orchestration-template.md`, and `references/domain-error-template.md` when the user needs implementation-oriented structure guidance.

## Output Expectations

Prefer outputs in this order:

1. Diagnosis
2. Smallest safe improvement
3. Example restructuring or code sketch
4. Migration steps
5. Risks and tradeoffs

Keep advice practical. Do not recommend rewriting the whole codebase unless the user explicitly asks for a rewrite plan.
