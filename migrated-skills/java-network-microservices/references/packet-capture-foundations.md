# Packet Capture Foundations

Use this file when a user needs to understand when packet capture is appropriate and what kinds of networking questions it can answer.

## Core idea

Packet capture is useful when logs and metrics are not enough to explain what actually moved across the wire or socket boundary.

## What packet capture helps answer

- Did the request actually leave the client?
- Did the response actually come back?
- Did the connection reset, retransmit, or stall?
- Did a timeout happen before any useful response arrived?
- Did a proxy or intermediary change the visible behavior?

## When capture is worth it

Use capture when:
- timeout or reset symptoms remain ambiguous
- logs disagree across systems
- retransmission or handshake problems are suspected
- proxy or gateway behavior is unclear

## When capture is not the first tool

Do not jump to packet capture if:
- the root cause is obviously an application exception
- slow SQL or JVM pressure already explains the symptom
- a simpler log, metric, or trace can answer the question faster

## Practical reminder

Capture is an evidence tool, not a replacement for narrowing the problem first.
