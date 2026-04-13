# HTTP Message and Headers

Use this file when a user needs to understand HTTP as a text-oriented request/response protocol instead of treating it as a black-box library call.

## Core idea

HTTP is not only "an API call." It is a protocol with:
- request lines and response lines
- headers that carry semantics
- status codes that express server-side meaning
- connection behavior that affects how requests and responses are exchanged

## Practical concepts

### Request and response structure
A client sends method, target, headers, and optional body. A server responds with status line, headers, and optional body.

### Headers matter
Headers shape behavior such as:
- caching
- authentication
- content type
- connection reuse
- redirection handling
- intermediary behavior

### Status codes are semantics, not just numbers
A status code is part of the protocol contract. Misreading status meaning often leads to bad retry logic or poor failure handling.

## Why this matters in Java systems

Java clients often hide protocol details behind libraries, but debugging still requires understanding:
- what the client actually sent
- what the server actually returned
- which header or status semantics changed behavior

## Practical reminder

Do not debug HTTP-only problems as if they were pure business exceptions. The message shape and headers often explain the behavior.
