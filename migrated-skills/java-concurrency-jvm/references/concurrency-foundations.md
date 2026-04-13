# Concurrency Foundations

Use this file for foundational Java concurrency explanations before diving into heavier concurrency frameworks or performance-specific analysis.

## What this file is for

This file covers the basic mental model behind Java multithreading:
- what a thread is
- why shared state becomes dangerous
- why correctness problems and performance problems are not the same thing
- how to explain common concurrency concepts in simple engineering language

## Core foundations

### 1. A thread is an execution path, not a free speed button

Adding threads only helps when work can proceed independently and the surrounding resources can support the concurrency level.

### 2. Shared mutable state is the real source of pain

Most concurrency bugs come from multiple threads reading and writing the same mutable data without clear coordination.

### 3. Correctness comes before throughput

A program that is fast but sometimes wrong is not correctly concurrent. Always separate:
- state correctness
- visibility of updates
- ordering guarantees
- throughput under load

### 4. Coordination has a cost

Locks, signaling, queues, pools, and async orchestration all trade simplicity for control. Use them only when they solve a concrete coordination problem.

## Practical explanation path

When a user asks a concurrency question, start with:
1. what is the shared state?
2. who reads and writes it?
3. does the issue need visibility, mutual exclusion, ordering, or task scheduling?
4. can the design reduce sharing instead of synchronizing more?

## Good beginner-level reminders

- `volatile` is not a magic thread-safety keyword
- `synchronized` is about both mutual exclusion and visibility
- thread pools manage capacity; they do not guarantee speed
- async code often improves structure only when ownership and failure flow stay clear

## When to prefer this file

Use this file when:
- the user needs concurrency basics
- the question sounds like a foundation or interview-level explanation
- the answer should stay simpler than the heavier checklist or tuning-oriented materials
