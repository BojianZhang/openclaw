# TCP/IP Layering Foundations

Use this file when a user needs a clearer mental model of how Java service networking sits across protocol layers.

## Core idea

A Java service call is not just “HTTP request code.” It crosses multiple layers:
- application semantics such as HTTP method, headers, and status handling
- transport behavior such as connection establishment, retransmission, and reset
- network forwarding and path selection underneath

## Practical layering model

### Link layer
Handles local network delivery details on the immediate medium.

### Network layer
Moves packets across networks. IP is connectionless and does not guarantee delivery, ordering, or reliability by itself.

### Transport layer
Provides end-to-end transport behavior. In practice, TCP is used when Java services need reliable byte-stream delivery. UDP is used when low overhead matters more than built-in reliability.

### Application layer
Defines service behavior such as HTTP, RPC request semantics, response format, authentication, and business-level error meaning.

## Why this matters in Java systems

When a user sees a timeout, reset, or slow response, the visible symptom often appears in Java client code, but the cause may sit in:
- application semantics
- transport behavior
- dependency path latency
- lower-level path instability

## Practical reminder

Do not explain network problems as if everything happens inside HTTP alone. HTTP behavior rides on transport and path behavior underneath.
