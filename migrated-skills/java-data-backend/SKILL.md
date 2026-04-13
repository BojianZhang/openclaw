---
name: java-data-backend
description: Design, troubleshoot, and optimize Java backend data access with focus on MySQL, InnoDB, Redis, caching, indexing, transactions, consistency, and persistence patterns. Use when diagnosing slow queries, cache failures, index issues, transaction behavior, or Java service data-access design.
---

# Java Data Backend

## Goal

Improve Java backend data access decisions and troubleshooting for MySQL, InnoDB, Redis, caching, transactions, and persistence-layer integration.

## Scope

In scope:
- MySQL indexing, slow queries, transactions, locks, and InnoDB behavior
- Redis data structures, cache design, consistency, and failure patterns
- Cache penetration, breakdown, avalanche, and double-write concerns
- Repository and persistence access structure in Java services
- Data-path bottlenecks that affect backend behavior

Out of scope unless directly relevant:
- JVM tuning unrelated to data access
- Spring Boot project structure as a whole
- Broad architecture refactoring unrelated to persistence or cache boundaries

## Workflow

1. Identify whether the problem is database-side, cache-side, consistency-side, or Java integration-side.
2. Ask what evidence exists: slow logs, execution plan, hit ratio, latency metrics, lock waits, error logs, or traffic patterns.
3. Explain the underlying storage or caching mechanism before proposing fixes.
4. Prefer the smallest fix that removes the bottleneck or inconsistency risk.
5. Distinguish schema, query, cache strategy, and application-layer causes.

## When To Read References

- Read `references/mysql-checklist.md` for MySQL troubleshooting.
- Read `references/redis-checklist.md` for Redis troubleshooting.
- Read `references/mysql-slow-query.md` for slow-query diagnosis.
- Read `references/redis-cache-decisions.md` for cache strategy tradeoffs.
- Read `references/mysql-index-qa.md` for indexing Q&A.
- Read `references/redis-consistency-qa.md` for consistency and invalidation Q&A.
- Read `references/mysql-high-performance-core.md`, `references/innodb-core.md`, and `references/redis-core.md` for mechanism-level guidance.
- Read `references/mysql-high-performance.md` and `references/redis-in-action.md` when the user needs additional deep-summary background beyond the core mechanism cards.
- Read `references/innodb-internals.md` when the problem needs a deeper InnoDB internals view than the lighter core card provides.
- Read `references/mysql-repository-template.md` and `references/redis-cache-template.md` when code structure or implementation patterns are needed.
- Read `references/seckill-architecture-patterns.md` when the user is asking about flash-sale / seckill architecture, stock deduction pressure, Redis hot-path checks, MQ async order handling, anti-oversell logic, or high-concurrency e-commerce purchase flows.
- Read `references/seckill-write-path-patterns.md` when the user needs a deeper write-path explanation for seckill systems, including request admission, duplicate-order prevention, MQ-based async handling, idempotency, and final order persistence.
- Read `references/seckill-cache-and-protection-patterns.md` when the user needs read-side optimization and protection-layer reasoning for seckill systems, such as shared session, page caching, hidden paths, captcha, and access limiting.
- Read `references/ecommerce-platform-data-capabilities.md` when the user is discussing Redis, Elasticsearch, SSO/session, order persistence, payment integration, SMS verification, or cloud storage as staged data/support capabilities inside a Java shopping platform.
- Read `references/ecommerce-order-payment-identity-patterns.md` when the user needs a focused explanation of how identity/SSO, order, payment, Redis, and support capabilities relate inside an e-commerce platform.
- Read `references/ecommerce-redis-es-order-payment-patterns.md` when the user needs a more implementation-facing explanation of how Redis, Elasticsearch, order persistence, payment integration, SSO/session, SMS, and cloud storage fit together in a modular shopping platform.
- Read `references/ecommerce-rpc-search-cart-order-patterns.md` when the user is asking about Dubbo+ZooKeeper RPC collaboration, Solr search, cart state, order flow, payment adjacency, and MQ-assisted workflows in a traditional Java shopping platform.
- Read `references/examples.md` when the user needs concrete diagnosis or design response patterns.
- Read `references/anti-patterns.md` when guarding against blind indexing, cache hand-waving, or evidence-free SQL advice.

## Output Expectations

When answering:
1. Classify the issue.
2. State the key mechanism involved.
3. Point out the likely bottleneck or risk.
4. Give a practical diagnosis path.
5. Recommend the smallest effective change.
6. Note consistency, rollback, or traffic risk where relevant.
