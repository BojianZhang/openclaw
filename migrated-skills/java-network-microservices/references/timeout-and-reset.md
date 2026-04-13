# Timeout and Reset Guidance

Use this file when Java services show timeouts, connection resets, or unstable downstream calls.

## Core ideas

- A timeout is often a call-path symptom, not the root cause.
- A reset is a transport symptom and may come from peer close, proxy behavior, idle timeout mismatch, or overload.
- Retry behavior can amplify both timeout frequency and downstream pressure.

## Practical reasoning

When diagnosing timeout or reset problems, ask:
- which hop timed out?
- do client timeout and server timeout budgets align?
- is connection reuse colliding with keep-alive or idle timeout mismatch?
- are retries multiplying load during partial failure?

## Warning

Do not solve transport symptoms only by increasing timeout values. That often hides deeper capacity or dependency-path problems.
