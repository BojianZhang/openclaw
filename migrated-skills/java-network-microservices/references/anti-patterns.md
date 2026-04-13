# Anti-Patterns

## Do not blame the network without narrowing the layer

Many timeout symptoms come from downstream slowness, retries, or connection mismanagement rather than mysterious network failure.

## Do not retry blindly

Retries can multiply load and create cascades if timeout budgets and fallback rules are unclear.

## Do not treat remote calls like local method calls

Transport cost, failure modes, and observability requirements change the design.

## Do not change timeout values without system reasoning

Timeout, pool size, keep-alive, and retry settings must align across the whole call path.
