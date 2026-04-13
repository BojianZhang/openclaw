# Network Q&A

## Is `connection reset` always a network problem?

No. It is a transport symptom that may reflect peer close, proxy policy, stale keep-alive reuse, timeout mismatch, or overloaded downstream systems.

## Should I just increase timeouts?

Not by default. Longer timeouts can hide dependency slowness and worsen tail latency or retry pileups.

## Why does one slow downstream call hurt the whole request path?

Because synchronous call chains compound latency and increase failure surface, especially when retries or fan-out are involved.

## Is keep-alive always beneficial?

Usually yes for reuse and latency, but it must align with idle timeout and pool behavior across the path.

## What is the first question in network troubleshooting?

First ask which hop is failing and whether the dominant problem is transport, client config, downstream latency, or retry amplification.
