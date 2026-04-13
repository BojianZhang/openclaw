# Java Network Foundations

Use this file for foundational Java networking explanations before diving into deeper protocol troubleshooting or multi-hop microservice failure analysis.

## What this file is for

This file covers the basic mental model behind Java-side networking:
- what happens when one service calls another
- where HTTP sits relative to TCP/IP
- why connections, pools, and timeouts matter
- how to explain network problems from a Java backend perspective

## Core foundations

### 1. A remote call is not a local method call

A service-to-service call adds:
- network delay
- connection setup or reuse behavior
- timeout and retry decisions
- dependency on another system's capacity and stability

### 2. HTTP semantics ride on transport behavior

At the application level, you may see HTTP methods, status codes, headers, and keep-alive behavior. Under that, TCP connection behavior still affects latency, resets, and reuse patterns.

### 3. Timeout is a design decision, not just a config number

Timeouts define how long one layer is willing to wait for another. Bad timeout alignment creates cascaded slowness and hard-to-debug failures.

### 4. Connection reuse helps, but misalignment hurts

Keep-alive and connection pooling often reduce latency and connection setup cost. But stale connections, idle timeout mismatch, and pool exhaustion can create intermittent failures.

## Practical explanation path

When a user asks a network question, start with:
1. which service calls which service?
2. which hop appears slow or unstable?
3. is the issue protocol-level, transport-level, timeout-level, or dependency-level?
4. are retries, fan-out, or pooling making the issue worse?

## Good beginner-level reminders

- a timeout often points to a slower dependency path, not just a bad client setting
- `connection reset` is a transport symptom, not a full diagnosis
- retries can multiply downstream pressure
- connection pools need to match keep-alive and timeout assumptions

## When to prefer this file

Use this file when:
- the user needs Java networking basics
- the question is about call-path understanding rather than deep packet-level analysis
- the answer should stay simpler than the heavier network checklist and timeout/reset materials
