# Refactor Playbook

Use this playbook for medium and large refactors in legacy Java systems.

## 1. Frame the problem

Document:
- What is hard to change now
- Which bugs or delays repeat
- Which classes or modules are involved
- What must remain behaviorally stable

Prefer concrete pain over abstract cleanliness.

## 2. Define the seam

Find a safe boundary where change can start.
Examples:
- A service method entry point
- An external client wrapper
- A package boundary
- A branching rule block

Good seams let you improve one area without rewriting the whole flow.

## 3. Stabilize behavior

Before larger changes:
- Add characterization tests if tests exist
- Capture sample inputs and outputs
- Log or document edge-case behavior

If tests are missing, propose minimal safety checks before structural change.

## 4. Refactor in layers

Recommended order:
1. Naming and extraction
2. Responsibility split
3. Boundary introduction
4. Pattern introduction if still needed
5. Module or package reshaping

Do not jump to architecture diagrams before cleaning local confusion.

## 5. Isolate external dependencies

Wrap:
- remote APIs
- SDKs
- repositories with awkward contracts
- time, UUID, and environment access

This reduces blast radius and improves testability.

## 6. Separate orchestration from rules

A common Java service problem is one method doing all of this:
- input validation
- loading data
- business decisions
- persistence
- event publishing
- DTO mapping

Split these concerns so business rules can be understood and tested independently.

## 7. Migrate incrementally

For large shifts:
- Keep old interface stable
- Route new logic behind the same entry point
- Move one branch or use case at a time
- Remove dead code only after callers are migrated

## 8. Stop at the right point

A refactor is successful when change becomes easier and risk drops. Do not continue polishing if the main pain is already removed.

## Warning signs

Pause and reconsider when:
- The plan requires touching too many callers at once
- Naming is still unclear after extraction
- New abstractions are harder to explain than the old code
- Refactor scope grows faster than business value
