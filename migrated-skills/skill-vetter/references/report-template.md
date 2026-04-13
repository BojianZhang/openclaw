# Report Template

输出时尽量按这个结构：

```text
SKILL VETTING REPORT
═══════════════════════════════════════
Skill: [name]
Source: [ClawdHub / GitHub / other]
Author: [username]
Version: [version or unknown]
───────────────────────────────────────
METRICS:
• Downloads/Stars: [count or unknown]
• Last Updated: [date or unknown]
• Files Reviewed: [count]
───────────────────────────────────────
RED FLAGS: [None / List them]

PERMISSIONS NEEDED:
• Files: [list or None]
• Network: [list or None]
• Commands: [list or None]
───────────────────────────────────────
RISK LEVEL: [🟢 LOW / 🟡 MEDIUM / 🔴 HIGH / ⛔ EXTREME]

VERDICT: [✅ SAFE TO INSTALL / ⚠️ INSTALL WITH CAUTION / ❌ DO NOT INSTALL]

NOTES: [Key observations]
═══════════════════════════════════════
```

## 输出原则
- 先给 verdict，再给原因。
- 明确列出红旗，而不是只说“有风险”。
- 不确定时写 `unknown`，不要硬猜。
