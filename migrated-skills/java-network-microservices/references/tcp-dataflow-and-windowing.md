# TCP Data Flow and Windowing

Use this file when a user needs to understand why throughput, latency, acknowledgements, and send/receive coordination affect Java service behavior.

## Core idea

TCP is a byte-stream protocol with flow-control and acknowledgement behavior. The sender and receiver coordinate how much data can be in flight without requiring an acknowledgement after every small piece of data.

## Practical concepts

### Sliding window
TCP allows multiple segments to be in flight before stopping for acknowledgement. This improves throughput compared with stop-and-wait behavior.

### Acknowledgements are cumulative
The receiver does not need to acknowledge every segment separately. Acknowledgements usually confirm receipt of a sequence of bytes up to a point.

### Throughput and latency interact
If acknowledgements, receive windows, downstream processing speed, or retransmissions behave poorly, Java services may observe:
- unstable throughput
- bursty latency
- head-of-line waiting effects
- inconsistent call completion times

## Why this matters for Java services

Even when application code appears simple, transport-level flow behavior influences:
- large payload uploads and downloads
- streaming responses
- long-lived service calls
- proxy and gateway buffering behavior

## Practical reminder

Do not treat a TCP connection as a fixed-speed pipe. Data flow behavior depends on both ends and on the path between them.
