# Spring Boot Practice

Use this file when the question is about Spring Boot engineering, project structure, configuration, startup, exception handling, or operational conventions.

## Core principles

- Keep project structure understandable before making it clever.
- Keep configuration explicit and environment-aware.
- Keep business rules out of controllers and framework glue.
- Keep operational behavior observable through logs, metrics, and health signals.

## Common problem areas

- startup failure from config or bean wiring
- too much logic in controllers
- unclear service boundaries
- configuration sprawl across profiles and env vars
- exception handling that leaks internal detail or hides root cause

## Practical guidance

- First distinguish whether the system is a demo app, internal tool, or production service. The structure and operational discipline should match that reality.
- Keep transport, orchestration, domain, and infrastructure concerns separated where complexity justifies it.
- Keep configuration ownership clear.
- Be explicit about timeouts, retries, thread pools, and transaction boundaries.
- Prefer simple Spring Boot defaults unless there is a concrete reason to customize.

## Useful structural reminders

- Controllers should receive requests, validate basics, call service or facade layers, and return stable responses.
- Controllers should not absorb large business condition trees, direct HTTP integration logic, or raw persistence concerns.
- Facade or application layers help when one action spans multiple services or integrations.
