---
name: skill-vetter
description: Security-first vetting for AI agent skills before installation or execution. Use before installing any skill from ClawdHub, GitHub, direct file shares, or other unknown sources. Checks for red flags, permission scope, suspicious patterns, and whether the requested capability matches the access the skill wants.
---

# Skill Vetter

Security-first vetting protocol for AI agent skills. Never install an unknown skill without reviewing its code and effective permission scope.

## Core Workflow

1. Check the source and trust level first.
2. Read all relevant files in the skill, not just `SKILL.md`.
3. Look for clear red flags.
4. Evaluate file, command, network, and data-access scope.
5. Classify risk.
6. Produce a short verdict with reasons.

## Read Path

- Read `references/source-check.md` for source and trust-level review.
- Read `references/red-flags.md` for immediate reject conditions and suspicious patterns.
- Read `references/permission-scope-checklist.md` for scope review.
- Read `references/risk-classification.md` for final classification.
- Read `references/report-template.md` for the output structure.

## Decision Rules

### Safe enough to install
Only when all are true:
- source is at least understandable
- no critical red flags found
- permission scope matches stated purpose
- no hidden credential, browser, or system-level access is involved

### Install with caution
Use when:
- risk is medium
- functionality is plausible but code or scope is broader than ideal
- human should understand tradeoffs before install

### Do not install
Use when:
- any critical red flag appears
- permissions are far broader than stated purpose
- code is obfuscated, unclear, or requests sensitive access without strong justification
- network exfiltration risk is non-trivial

## Output Expectations

When answering:
1. name the source
2. state what was reviewed
3. list red flags or say none found
4. summarize required permissions
5. assign a risk level
6. give a clear verdict

Prefer concise, specific security reasoning over vague caution language.
