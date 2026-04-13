# Skill Triage - 2026-04-13

Target folder reviewed: `migrated-skills/`

## 结论总览

### 建议优先保留并视为候选启用
这些和用户当前长期工作、历史上下文、排障模式最贴近，迁移价值最高。

- `proxy-automation-stabilizer`
  - 直接对应 `D:\playwright` / Dreamina / 代理自动化主战场
  - 高度贴合真实长期项目，不是泛技能
  - 建议保留，后续可考虑正式纳入 active skills

- `java-knowledge-corpus`
  - 作为 Java 总入口，结构完整
  - 适合做主题路由，不需要每次都深挖单项技能
  - 建议保留

- `java-learning-planner`
- `java-interview-answering`
- `java-troubleshooting-triage`
- `java-concurrency-jvm`
- `java-data-backend`
- `java-design-refactor`
- `java-jvm-performance`
- `java-network-microservices`
- `java-spring-microservice`
  - 这是一整套成体系的 Java 技能树
  - 和旧长期记忆里提到的“五层结构”一致
  - 如果你后续还会继续做 Java 面试、后端、Spring、排障，这套值得完整保留
  - 建议保留整套，不建议拆散删除

## 建议保留为参考库，不急着启用
这些有价值，但和你当前主线关联没上面那么强，或者更像辅助型资产。

- `frontend-template-corpus`
  - 对模板筛选、页面灵感、旧站点模板拆解有价值
  - 适合作为参考资料库
  - 建议保留，但不用优先启用

- `html-template-refactor`
  - 适合处理旧 HTML 模板重构思路
  - 有用，但当前不是你的长期主战方向
  - 建议保留为参考

- `frontend-slides`
  - 做演示稿/HTML slides 时会有用
  - 不属于高频核心技能
  - 建议保留为低频工具型技能

- `summarize`
  - 是工具型 skill，前提是本地真的装了 `summarize` CLI
  - 若未安装，对当前帮助有限
  - 建议保留，但标记为“依赖外部 CLI”

- `skill-vetter`
  - 对以后装第三方 skill 有用
  - 低频，但有安全价值
  - 建议保留

## 建议归档观察，不建议主动启用
这些不是完全没用，但当前有重复、维护成本或潜在不匹配问题。

- `self-improving-agent`
  - 思路不错，但它带 hooks / scripts / learnings 资产
  - 如果当前 OpenClaw 版本、hooks 机制、你的工作流没专门接它，贸然启用可能带来额外维护负担
  - 更适合作为“参考实现”归档，不建议先启用

## 当前不建议删除的原因
虽然有些技能不是高频，但它们的总体体量不算夸张，而且大多是文档型资产，误删收益很低。
当前阶段更合理的是：
- 保留核心技能
- 把辅助技能留作参考
- 把高风险/高维护的技能归档观察
而不是直接删掉

## 推荐落地分组

### A. 建议未来转正到 active skills
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

### B. 建议保留在 `migrated-skills/` 当参考库
- `frontend-template-corpus`
- `html-template-refactor`
- `frontend-slides`
- `summarize`
- `skill-vetter`

### C. 建议单独归档观察
- `self-improving-agent`

## 我给你的实际建议

如果你想继续收口，我建议下一步做的是：

1. 把 A 组正式移到一个你认可的长期技能目录
2. 把 C 组移到 `migrated-skills/_archive/`
3. B 组先不动，按需再用

这样最稳，也最符合你现在的主线工作。
