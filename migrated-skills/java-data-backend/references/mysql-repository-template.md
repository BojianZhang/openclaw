# MySQL Repository Template

Use this template pattern when data access needs a clean Java repository boundary.

## Intent

Keep SQL and persistence concerns localized while preventing business logic from leaking into repository code.

## Structure guidance

- Repository handles persistence access.
- Service or application layer handles business decisions.
- Avoid making the repository an all-purpose business utility.
- Return shapes that fit the use case, not the entire table by default.

## Practical rules

- Keep queries explicit.
- Avoid hidden N+1 access patterns.
- Keep transaction ownership clear.
- Do not let mapper or repository layers absorb domain policy.
- Do not spread SQL assembly across unrelated service methods.
