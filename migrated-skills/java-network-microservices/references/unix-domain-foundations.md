# Unix Domain Foundations

Use this file when a user needs to understand local inter-process communication that looks socket-like but does not behave like ordinary cross-network TCP/IP traffic.

## Core idea

Unix domain communication uses socket-style APIs for local process communication on the same host. It is related to networking concepts, but it is not the same as ordinary TCP/IP over a network path.

## Practical concepts

### Local IPC instead of routed networking
Unix domain communication stays on the local machine. It avoids many network-path issues, but still has connection, buffering, and ownership behavior that can fail.

### Why it matters to service systems
Modern systems may use Unix domain sockets for:
- local proxies
- sidecars
- service mesh agents
- container-local communication
- local daemon interaction

### Failure thinking
When a call uses a Unix domain socket, problems may resemble connection failure, timeout, or permission issues, but the path is different from ordinary remote network traffic.

## Practical reminder

Do not explain every socket-like failure as a TCP/IP path problem. First ask whether the communication is local Unix domain IPC or remote network transport.
