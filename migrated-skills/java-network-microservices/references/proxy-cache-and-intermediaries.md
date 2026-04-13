# Proxy, Cache, and Intermediaries

Use this file when a user needs to understand how gateways, proxies, caches, or intermediate components affect Java service networking behavior.

## Core idea

A request path often includes more than client and server. Intermediaries can change latency, response shape, connection reuse, retry behavior, and what each side believes happened.

## Practical concepts

### Proxies and gateways
They may terminate connections, rewrite headers, enforce timeout policy, or shape traffic before the request reaches the target service.

### Caches and stored responses
A client may receive behavior influenced by cached data, cache headers, or stale intermediary state rather than the immediate server state.

### Observability distortion
Different hops may log different events. This is why one side may claim success while another side reports timeout or reset.

## Why this matters in Java systems

Java service clients often see only the library-level result. Without considering intermediaries, engineers may blame the wrong service or the wrong layer.

## Practical reminder

When response behavior looks inconsistent, ask whether a proxy, gateway, load balancer, or cache sits in the path before assuming direct client-to-server behavior.
