# Microservices Checklist

Use this checklist when reviewing service decomposition, RPC behavior, or distributed runtime risks.

## 1. Clarify service boundary

Ask:
- what business capability does this service own?
- what data does it own?
- what upstream and downstream calls are mandatory?

## 2. Check dependency shape

Review:
- fan-out count
- synchronous call depth
- timeout alignment
- retry amplification
- fallback behavior

## 3. Check governance basics

Review:
- service registration and discovery assumptions
- config source ownership
- health checks and readiness behavior
- observability coverage

## 4. Check failure handling

Review:
- what happens when a dependency is slow?
- what happens when config is wrong?
- what happens when one service scales differently from another?

## 5. Avoid common traps

- shared database without ownership clarity
- chatty service interfaces
- retries without budget control
- distributed complexity without observability
- splitting before business boundaries are stable
- treating remote calls like local method calls

## Decision reminder

Check whether the monolith can be clarified first. Splitting is not the default fix for unclear boundaries.
