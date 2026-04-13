# Anti-Patterns

## Do not tune without evidence

Do not recommend JVM flags first when there is no GC log, heap trend, latency signal, or thread evidence.

## Do not blame all latency on GC

Lock contention, downstream calls, serialization, and thread-pool saturation often look like JVM pain.

## Do not dump large flag lists casually

Prefer one meaningful change at a time with before-and-after measurement.

## Do not treat heap growth as automatic success

A larger heap can hide retention issues and worsen pause behavior.

## Do not separate JVM problems from workload shape

Allocation pattern, object lifetime, traffic burstiness, and thread behavior matter as much as flags.
