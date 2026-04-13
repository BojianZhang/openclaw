# Code Smells

Use this file to map symptoms to structural problems and likely refactor directions.

## Common Smells

### God Class

Symptoms:
- Very large class
- Many fields with unrelated meanings
- Too many public methods
- Knows persistence, validation, orchestration, and business rules

Typical fixes:
- Split by responsibility
- Extract domain service or collaborator
- Move behavior closer to the data it truly belongs to
- Separate orchestration from core business rules

### Long Method

Symptoms:
- Many nested branches
- Multiple conceptual steps in one method
- Hard to name what the method does in one sentence

Typical fixes:
- Extract methods by intent
- Separate validation, fetching, rule evaluation, persistence, and response mapping
- Introduce small value objects for repeated parameter groups

### Feature Envy

Symptoms:
- Method touches another object's data more than its own
- Repeated getter chains

Typical fixes:
- Move method to the object whose data it depends on
- Introduce richer domain behavior
- Reduce anemic models when appropriate

### Shotgun Surgery

Symptoms:
- One change requires edits in many files
- Business rule scattered across layers

Typical fixes:
- Consolidate rule ownership
- Extract policy or strategy object
- Centralize variant logic behind a stable interface

### Divergent Change

Symptoms:
- One class changes for many unrelated reasons
- Team touches the same file for unrelated features

Typical fixes:
- Split responsibilities
- Create clearer module boundaries

### Primitive Obsession

Symptoms:
- Strings, ints, and maps used for domain concepts everywhere
- Repeated validation or formatting logic

Typical fixes:
- Introduce value objects
- Encapsulate parsing and validation
- Replace generic maps with typed request or domain objects

### Switch Explosion

Symptoms:
- Repeated switch or if-else trees for type-specific behavior
- New variant requires edits in several places

Typical fixes:
- Introduce strategy, polymorphism, or registry
- Keep branching in one place if full polymorphism would be excessive

### Inappropriate Intimacy

Symptoms:
- Classes reach into each other's internals
- Heavy reliance on getters, setters, and internal state layout

Typical fixes:
- Hide internals behind behavior methods
- Reduce bidirectional knowledge
- Introduce boundary interfaces

### Data Clumps

Symptoms:
- Same group of parameters passed together repeatedly
- Constructor or method signatures keep growing

Typical fixes:
- Extract parameter object or value object
- Group related concepts into richer types

### Framework Leakage

Symptoms:
- Domain decisions depend on framework annotations or HTTP concerns
- Core logic unusable without Spring context

Typical fixes:
- Move framework code to adapters or orchestration layer
- Keep core domain API framework-light

## Prioritization Heuristic

Fix smells in this order when time is limited:

1. Mixed responsibilities causing bugs
2. Duplicated business rules
3. Hard-to-change branching logic
4. Tight coupling to external systems
5. Naming and local readability issues

Do not refactor cosmetic smells first when structural issues are driving change cost.
