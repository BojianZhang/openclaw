---
name: java-network-microservices
description: Explain and troubleshoot Java service networking with focus on HTTP, TCP/IP, sockets, keep-alive, connection pools, timeout chains, reset errors, retries, proxies, gateways, and transport-level failure patterns in service-to-service calls. Use when diagnosing Java backend network issues, RPC timeout chains, connection instability, retry amplification, intermediary effects, or service-call behavior where the primary question is protocol, transport, or call-path mechanics. Prefer `java-spring-microservice` when the primary question is Spring Boot configuration, service structure, bean wiring, or microservice boundary/governance decisions.
---

# Java Network Microservices

## Goal

Explain and troubleshoot Java service networking with practical focus on HTTP behavior, TCP/IP concepts, service-to-service call paths, timeout alignment, connection handling, and network-related failure patterns in microservice systems.

## Scope

In scope:
- HTTP and TCP/IP reasoning for Java backends
- connection reuse, keep-alive, and connection-pool behavior
- timeout chains, reset errors, retry amplification, and fallback side effects
- proxy, gateway, cache, and load-balancer effects on service calls
- service-to-service transport behavior in microservices
- network-layer diagnosis for Java services and RPC-style interactions
- call-chain behavior that amplifies latency or failure

Out of scope unless directly relevant:
- pure Spring Boot structure questions
- Spring configuration, bean wiring, or startup failures as the main topic
- microservice boundary design or governance without transport/path symptoms
- JVM GC tuning without network symptoms
- deep database tuning without service-call impact

## Workflow

1. Clarify whether the issue is protocol understanding, timeout behavior, connection handling, retry amplification, intermediary behavior, or distributed call instability.
2. Separate application logic problems from transport and dependency-path problems.
3. Identify the dominant layer first: HTTP semantics, TCP connection behavior, client configuration, proxy/gateway effects, downstream latency, or service topology.
4. Prefer bounded troubleshooting paths over broad network speculation.
5. Explain timeout, retry, and fallback tradeoffs before suggesting client-side changes.
6. If the core problem is Spring configuration, startup, bean injection, service boundaries, or microservice governance, hand off to `java-spring-microservice`.

## When To Read References

Read `references/java-network-foundations.md` when the user needs simpler Java-side networking explanations before deeper protocol or call-chain analysis.
Read `references/tcpip-layering-foundations.md` when the problem needs a clearer layered model from HTTP down to transport and path behavior.
Read `references/http-message-and-headers.md` when request/response structure, header semantics, or status meaning are central.
Read `references/http-connection-behavior.md` when client behavior, connection reuse, redirect handling, or intermediary effects matter.
Read `references/http-core.md`, `references/tcpip-core.md`, and `references/unix-network-core.md` for chapter-level protocol and networking fundamentals.
Read `references/computer-network-foundations.md` and `references/tcp-ip-illustrated.md` when the user needs broader networking intuition or a deeper transport/path mental model beyond the core cards.
Read `references/unix-network-programming.md` and `references/wireshark-analysis.md` when the user needs extra packet/path intuition beyond the lighter troubleshooting and foundation references.
Read `references/unix-domain-foundations.md` when the communication may be local IPC through Unix domain sockets rather than ordinary network transport.
Read `references/tcp-dataflow-and-windowing.md` when throughput, acknowledgements, payload flow, or streaming behavior matter.
Read `references/routing-and-path-behavior.md` when failures look intermittent, path-sensitive, or environment-sensitive.
Read `references/timeout-and-reset.md` when diagnosing connection resets, idle timeout mismatch, or timeout-chain problems.
Read `references/network-troubleshooting-checklist.md` for structured network and call-path troubleshooting.
Read `references/network-intuition.md` when the user needs a simpler mental model before protocol-level or packet-level detail.
Read `references/proxy-cache-and-intermediaries.md` when gateways, proxies, caches, or load balancers may be changing the observed behavior.
Read `references/packet-capture-foundations.md` when logs and metrics are not enough and packet-level evidence may clarify the symptom.
Read `references/wireshark-troubleshooting.md` when timeout, reset, retransmission, handshake, or path-behavior evidence is needed.
Read `references/microservice-call-patterns.md` when the issue involves fan-out, retries, synchronous call depth, or service-call design.
Read `references/spring-cloud-call-path-bridges.md` when the user mentions Feign, Ribbon, Hystrix, Sentinel, Zuul, Gateway, or Sleuth but the real need is path-level reasoning across those layers.
Read `references/network-qa.md` for reusable concise answers to common networking questions.
Read `references/examples.md` for concrete troubleshooting and explanation response patterns.
Read `references/anti-patterns.md` when guarding against blind retries, timeout folklore, or transport-layer overguessing.

## Output Expectations

When answering:
1. Classify the network or call-chain problem.
2. Explain the relevant protocol or transport mechanism.
3. Narrow the likely failure point.
4. Recommend a stepwise troubleshooting path.
5. Mention retry, timeout, intermediary, and cascading-failure risks when relevant.
