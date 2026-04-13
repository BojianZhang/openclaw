# Spring Cloud Call-Path Bridges

Use this file when the user asks about Spring Cloud components, but the real problem is moving from component names into call-path reasoning.

## When this file matters

Read this when the user mentions one or more of:
- Feign / OpenFeign timeout behavior
- Ribbon instance choice and call failure
- Hystrix / Sentinel around downstream calls
- Zuul / Gateway forwarding behavior
- Sleuth trace chain during service invocation
- why a request failed somewhere across gateway -> consumer -> provider chain

This file is not for explaining component definitions in isolation. It is for linking them into one transport path.

## Mental model: one request path

A common Spring Cloud request path looks like:
1. client enters through gateway (or directly to a service)
2. gateway forwards to a downstream service
3. consumer side chooses a provider instance (historically Ribbon or equivalent)
4. call is made via HTTP client / Feign / OpenFeign
5. protection layer may apply timeout, isolation, fallback, flow control, or degradation
6. trace context may be propagated for observability
7. downstream service responds or times out / fails

When debugging, do not ask "which component is broken?" first.
Ask:
- where in the path did latency or failure first appear?
- which layer made a routing / timeout / retry / fallback decision?
- what evidence exists in logs, metrics, traces, and gateway behavior?

## Feign / OpenFeign path risks

Typical call-path risks:
- timeout mismatch between caller and downstream
- retries creating amplification
- hidden client defaults that are too optimistic or too aggressive
- assuming declarative clients remove transport cost

Good reminder:
- declarative call style changes code ergonomics, not network physics

## Ribbon path risks

Typical issues:
- stale or skewed instance view
- load-balancing rule not matching traffic pattern
- retries accidentally targeting unhealthy instances repeatedly
- confusion between client-side balancing and gateway / server-side balancing

## Hystrix / Sentinel path risks

These components often appear in conversations about "why the request failed fast".

Look for:
- was the failure a true downstream timeout, or a protection-layer timeout?
- was fallback triggered because of circuit state rather than immediate network failure?
- was traffic blocked by protection rules before the downstream was even attempted?

Do not confuse business failure, network failure, and protection decision.

## Gateway path risks

For Zuul / Gateway / edge layers, typical path issues are:
- route mismatch
- filter logic blocking or mutating requests
- header propagation issues
- auth / token propagation mistakes
- timeout mismatch between gateway and downstream services
- large response / streaming / long-connection behavior interacting badly with the gateway layer

## Sleuth / tracing value

Tracing helps answer:
- which hop consumed the latency budget?
- which hop returned an error first?
- whether retries or fan-out widened the call tree

Trace data should narrow the path, not just decorate dashboards.

## Practical troubleshooting pattern

1. Draw the path in one line: client -> gateway -> service A -> service B.
2. Mark timeouts configured at each layer.
3. Mark retries / fallback / degradation rules.
4. Identify whether balancing is client-side, gateway-side, or both.
5. Use tracing/logs to find the first slow or failing hop.
6. Only then discuss framework-specific fixes.

## Hand-off guidance

- If the user wants component definitions and architecture responsibilities, hand back to `java-spring-microservice`.
- If the user wants interview wording, hand to `java-interview-answering`.
- If the user wants path-level diagnosis, continue inside `java-network-microservices` with timeout/reset/proxy references.
