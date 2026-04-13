# Migration Notes - 2026-04-13

Source: `D:\260413 OpenClaw\.openclaw`
Target: `C:\Users\Administrator\.openclaw\workspace`

## Migrated core files

Copied from old workspace root:
- `IDENTITY.md`
- `USER.md`
- `TOOLS.md`
- `MEMORY.md`

Copied from old workspace memory folder:
- `memory/*`

## Migrated selected skills

Copied into `migrated-skills/` for safe review-first import:
- `proxy-automation-stabilizer`
- `java-knowledge-corpus`
- `java-learning-planner`
- `java-interview-answering`
- `java-troubleshooting-triage`
- `java-concurrency-jvm`
- `java-data-backend`
- `java-design-refactor`
- `java-jvm-performance`
- `java-network-microservices`
- `java-spring-microservice`
- `frontend-template-corpus`
- `frontend-slides`
- `html-template-refactor`
- `self-improving-agent` (later archived to `migrated-skills/_archive/self-improving-agent`)
- `skill-vetter`
- `summarize`

## Not migrated directly

Left in old directory for now:
- `openclaw.json` (contains auth/token/version-coupled config)
- `identity/device*.json`
- `devices/`
- `logs/`
- `completions/`
- root-level runtime/state files
- sqlite memory DBs

## Why selected skills were staged into `migrated-skills/`

This avoids overwriting current built-in or installed skills blindly.
You can later decide whether to:
1. keep them as archive/reference,
2. merge specific ones into active skills,
3. delete unneeded ones.
