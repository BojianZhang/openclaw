# HTTP Connection Behavior

Use this file when a user needs to understand how client behavior, connection reuse, redirection, and related HTTP-side behavior affect Java service calls.

## Core idea

HTTP behavior is shaped not only by message syntax, but also by how clients and servers manage connections, reuse them, redirect requests, and interact with intermediaries.

## Practical concepts

### Connection reuse
Reusing connections can reduce latency and setup cost, but it also creates failure modes around stale connections, idle timeout mismatch, and pool assumptions.

### Redirection
A redirect is part of protocol behavior, not just an application surprise. Clients need clear rules for whether to follow, transform, or reject redirected calls.

### Client-side caching and intermediaries
Caching and proxy behavior can change what the client observes. A response may look strange because the path includes more than one actor.

## Why this matters in Java systems

In Java backends and service clients, visible symptoms such as timeout, retry, stale response, or odd redirect chains may come from connection and protocol behavior rather than only server business logic.

## Practical reminder

Do not reason about HTTP only in terms of controller code or client methods. Include connection reuse, proxy behavior, and redirect semantics in the mental model.
