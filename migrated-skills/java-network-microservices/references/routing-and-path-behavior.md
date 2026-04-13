# Routing and Path Behavior

Use this file when network symptoms look intermittent, path-dependent, or difficult to explain from application code alone.

## Core idea

IP forwarding is connectionless. Packets are moved according to current path knowledge rather than a single application-owned path contract. This helps explain why some failures look inconsistent or bursty.

## Practical concepts

### Path behavior can vary
Different packets or calls may be affected by changing path conditions, congestion points, or intermediary behavior.

### Routing is outside application control
Java code can configure timeouts, retries, and pools, but it does not control the network path directly.

### Dynamic routing exists to adapt
Real networks use routing behavior that changes as topology and availability change. This is one reason intermittent network symptoms may not map neatly to one code-level cause.

## Why this matters for microservices

A service may show:
- occasional timeouts
- inconsistent latency to the same downstream
- failures that appear only in some environments
- retry storms after partial path degradation

These symptoms can be amplified by the service design even when the root cause is not fully inside the service itself.

## Practical reminder

When failures look path-sensitive or environment-sensitive, do not blame only Java code, but also do not stop at saying “the network is flaky.” Narrow the failing hop and the call-path behavior.
