# Anti-Patterns

## Do not introduce patterns for style alone

A pattern is justified only when it removes real complexity, coupling, or branching pressure.

## Do not recommend big-bang rewrites by default

Prefer phased migration and behavior-preserving refactors unless the user explicitly asks for a rewrite plan.

## Do not hide tradeoffs

If an abstraction adds indirection, ceremony, or cognitive load, say so clearly.

## Do not confuse Spring structure with good domain design

Moving code across packages is not the same as improving responsibilities and boundaries.

## Do not over-abstract early

If the variation is small and unlikely to grow, simple code may be the better design.
