# Multi-Agent Setup

## OpenClaw
优先使用工作区文件与会话工具：
- `AGENTS.md`
- `SOUL.md`
- `TOOLS.md`
- `MEMORY.md`
- `memory/YYYY-MM-DD.md`
- `sessions_*` 工具做跨会话传递

OpenClaw 细节见：
- `openclaw-integration.md`
- `hooks-setup.md`

## Generic Agents
其他代理使用 `.learnings/` 目录：
- `LEARNINGS.md`
- `ERRORS.md`
- `FEATURE_REQUESTS.md`

## Copilot / Claude Code / Codex
- 可以使用 hooks 或提示词提醒
- 不需要把平台细节塞在主 `SKILL.md`
- 平台差异放在本参考文件与 `hooks-setup.md`
