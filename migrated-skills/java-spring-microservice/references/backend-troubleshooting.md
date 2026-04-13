# Backend Troubleshooting

Use this file when a Java backend problem spans startup, runtime, downstream dependencies, data access, and service integration.

## Investigation order

1. Identify whether the symptom is startup failure, runtime latency, error spike, dependency timeout, or resource pressure.
2. Narrow whether the dominant factor is application logic, Spring wiring, JVM, database, cache, or downstream network call.
3. Gather the most relevant evidence for that layer first: app logs, GC logs, thread dumps, slow-query logs, Redis signals, or HTTP timeout traces.
4. Follow the smallest useful branch before expanding scope.

## Practical rule

Do not investigate all layers at once. Narrow the dominant failing path first.

## Common cross-layer branches

- startup failure: first real exception, config, port, bean wiring, datasource, external dependency reachability
- slow API: CPU, lock contention, SQL, cache, network timeout, thread-pool queueing
- unstable microservice calls: timeout alignment, retries, retry storms, downstream capacity, missing tracing
