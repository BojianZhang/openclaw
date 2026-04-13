# Network Intuition

Use this file when a user needs a simpler, more intuitive explanation of network behavior before diving into protocol details or packet analysis.

## Core idea

A backend request path is not just code calling code. It is a chain of communication steps with delay, buffering, reuse, dependency, and failure points.

## Practical intuition

### 1. Every hop adds uncertainty

A request that crosses more services gains more places where latency, timeout, retry, or overload can appear.

### 2. Faster in one layer does not guarantee faster overall

A well-tuned HTTP client cannot compensate for a slow downstream service, unstable path, overloaded proxy, or mismatched timeout chain.

### 3. Reuse helps until assumptions drift

Connection pools and keep-alive reduce setup cost, but stale connections, mismatched idle timeouts, and overloaded pools can create intermittent failures that look random.

### 4. Symptoms are often indirect

A timeout may actually mean downstream overload.
A reset may actually mean peer close or path mismatch.
A slow call may actually be queueing somewhere else.

## When to prefer this file

Use this file when:
- the user needs a simpler mental model
- the issue is easier to explain by call-path intuition than by raw protocol details
- the answer should stay understandable before going deeper
