# Pattern Selection Guide

Use patterns to solve recurring structural problems, not to decorate code.

## Strategy

Use when:
- Business rules vary by type, channel, region, or mode
- Conditionals keep growing
- New variants should be added with minimal edits

Avoid when:
- There are only one or two trivial branches
- The variation is unlikely to grow

## Factory / Abstract Factory

Use when:
- Object creation is complex
- Construction depends on configuration or variant type
- You need to hide assembly details

Avoid when:
- Constructors are simple and obvious
- The factory would just mirror constructors without adding clarity

## Adapter

Use when:
- Wrapping external SDKs, legacy APIs, or incompatible interfaces
- Isolating third-party dependencies from core code

Avoid when:
- The wrapper adds no semantic value

## Decorator

Use when:
- You need composable behavior layering
- Cross-cutting enhancements should stack cleanly

Avoid when:
- A simple collaborator or method extraction is enough

## Template Method

Use when:
- Several flows share a stable sequence with small overridable steps

Avoid when:
- Inheritance is otherwise weak
- Composition with strategy is clearer

## Observer / Domain Events

Use when:
- Side effects should react to a completed business action
- Multiple downstream reactions exist

Avoid when:
- Synchronous direct calls are simpler and clearer
- Eventing would make causality hard to follow

## Chain of Responsibility

Use when:
- A request passes through ordered checks or handlers
- Validation or policy evaluation is sequential and composable

Avoid when:
- The sequence is short and fixed
- A simple list of functions is clearer

## Specification

Use when:
- Business predicates must be composed and reused
- Rules need readable combination logic

Avoid when:
- Rules are small and local
- The abstraction would exceed the complexity of the rule itself

## Ports and Adapters

Use when:
- Core business logic should stay independent from Spring, databases, or remote APIs
- The project suffers from framework leakage
- You need testable boundaries around external systems

Avoid when:
- The app is small, CRUD-heavy, and unlikely to grow
- The added indirection would outweigh its benefit

## Pattern Choice Heuristics

Before introducing a pattern, ask:

1. What concrete pain does it remove?
2. Does it reduce future change surface?
3. Will the team understand and maintain it easily?
4. Is a smaller refactor enough?

If you cannot answer these clearly, do not introduce the pattern.
