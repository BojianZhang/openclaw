# JVM Troubleshooting Checklist

Use this checklist when a Java service shows GC pressure, OOM risk, latency spikes, high CPU, or unexplained throughput drops.

## 1. Identify the symptom first

Classify the main symptom:
- frequent Young GC
- frequent Full GC
- OOM
- high CPU
- long response times
- startup memory failure
- thread blockage or pool exhaustion

Also separate the likely problem domain early:
- heap pressure
- metaspace pressure
- thread or stack pressure
- direct or native memory pressure

Do not tune JVM flags before naming the dominant symptom.

## 2. Confirm evidence sources

Collect what is available:
- GC logs
- heap usage charts
- CPU and memory metrics
- thread dumps
- heap dump if OOM occurred
- container limits or host memory limits
- request latency and throughput metrics

If evidence is missing, say so explicitly and avoid false certainty.

## 3. Check memory pressure

Review:
- heap used vs max heap
- old generation growth trend
- metaspace growth
- allocation rate spikes
- off-heap or direct buffer usage if relevant

Typical questions:
- Is memory growing steadily or in bursts?
- Is old gen filling faster than expected?
- Are objects surviving too long?

## 4. Check GC behavior

Review:
- GC frequency
- pause duration
- pause distribution, not just averages
- whether Full GC is rare, periodic, or continuous
- collector in use and whether it fits the workload

Do not assume the collector is the root problem. Allocation behavior often matters more.

## 5. Check thread and CPU signals

Review:
- runnable thread count
- blocked or waiting thread patterns
- thread pool saturation
- lock contention
- CPU hotspots in profiling or stack traces

High CPU is not always GC. It may be serialization, regex, logging, locking, or busy retry logic.

## 6. Check environment constraints

Review:
- JVM version
- container memory limits
- cgroup awareness
- host swap pressure
- startup flags inherited from old deployments

A tuning guide without environment context is incomplete.

## 7. Prioritize likely causes

Order possible causes by evidence:
1. leak or retention issue
2. allocation rate too high
3. collector mismatch
4. wrong heap sizing
5. thread contention causing indirect latency
6. container or host memory mismatch

## 8. Change one thing at a time

Prefer:
- one flag change
- one memory sizing change
- one allocation reduction change
- one thread-pool change

Measure before and after. Avoid multi-flag tuning bursts.
