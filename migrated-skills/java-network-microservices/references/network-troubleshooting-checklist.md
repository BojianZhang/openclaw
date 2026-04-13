# Network Troubleshooting Checklist

Use this checklist when Java backend calls show timeout, reset, slow responses, or unstable cross-service behavior.

## 1. Identify the dominant symptom

Classify first:
- timeout
- connection reset
- intermittent latency
- pool exhaustion
- retry storm
- downstream saturation

## 2. Confirm evidence

Collect:
- client timeout and retry settings
- server-side latency evidence
- proxy or gateway behavior if present
- HTTP status distribution
- connection-pool metrics
- trace or request-id path if available

## 3. Narrow the layer

Ask whether the dominant issue is:
- client config
- downstream service latency
- transport connection behavior
- proxy or load balancer policy
- retry amplification
- service topology or fan-out depth

## 4. Check alignment

Review:
- timeout budgets across the call chain
- keep-alive and idle timeout settings
- connection reuse behavior
- retry count and backoff policy
- fallback and circuit-breaking behavior

## 5. Fix smallest useful cause first

Prefer:
- timeout alignment
- retry reduction
- clearer fallback policy
- pool or connection setting correction
- reducing synchronous call depth where justified
