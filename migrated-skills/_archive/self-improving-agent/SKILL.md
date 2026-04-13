---
name: self-improvement
description: Captures learnings, errors, corrections, and missing capabilities so the agent improves over time. Use when a command or operation fails unexpectedly, a user corrects the agent, an external API or tool fails, the agent discovers a knowledge gap, a recurring better approach is found, or a missing capability should be recorded. Also review recent learnings before major tasks.
---

# Self-Improvement Skill

Log learnings and errors into durable files so future work gets better instead of repeating the same mistakes.

## Core Workflow

1. Notice a correction, failure, knowledge gap, better recurring approach, or missing capability.
2. Decide what kind of record it is:
   - learning
   - error
   - feature request
3. Log it immediately into `.learnings/` or the workspace memory system.
4. Link related entries when the pattern is recurring.
5. Promote broadly applicable lessons into long-term instruction files when they stop being one-off incidents.
6. If the pattern is broadly reusable, consider extracting it into a dedicated skill.

## What To Record

Record when:
- a command or operation fails unexpectedly
- a tool or external API fails
- a user corrects the agent
- the agent realizes prior knowledge was incomplete or outdated
- a repeated better approach becomes clear
- the user asks for a capability that does not yet exist

Do not bloat the log with every trivial hiccup. Prefer non-obvious, reusable, or recurring learnings.

## Default Destinations

### Generic log files
- `.learnings/LEARNINGS.md`
- `.learnings/ERRORS.md`
- `.learnings/FEATURE_REQUESTS.md`

### OpenClaw workspace promotion targets
- `AGENTS.md`
- `SOUL.md`
- `TOOLS.md`
- `MEMORY.md`
- `memory/YYYY-MM-DD.md`

## Read Path

- Read `references/detection-triggers.md` when deciding whether something is worth logging.
- Read `references/logging-format.md` for entry formats and ID generation.
- Read `references/promotion-rules.md` when deciding whether to promote a learning into longer-lived memory or instruction files.
- Read `references/review-routine.md` for periodic review and recurring-pattern handling.
- Read `references/openclaw-integration.md` for OpenClaw-specific workspace behavior.
- Read `references/hooks-setup.md` for hook-based reminders.
- Read `references/multi-agent-setup.md` for Claude Code / Codex / Copilot / generic-agent setup guidance.
- Read `references/examples.md` for concrete examples.

## Decision Rules

### Log as learning
Use for:
- corrections
- knowledge gaps
- best practices
- recurring safer workflows

### Log as error
Use for:
- failed commands
- exceptions
- tool failures
- unexpected outputs
- timeouts or connection failures

### Log as feature request
Use for:
- user-requested capabilities the agent does not currently support
- missing workflow automation worth building later

### Promote to long-term memory
Promote when the lesson:
- applies beyond one task
- prevents recurring mistakes
- belongs in project or workspace conventions
- should be remembered by future sessions or other agents

## Output Expectations

When using this skill:
1. classify the event
2. write the smallest useful durable record
3. link related entries if recurring
4. promote only the distilled rule, not the whole incident report

Prefer durable, concise learning capture over verbose journaling.
