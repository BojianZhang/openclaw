# Active Skills Candidates - 2026-04-13

## 目标

给 `migrated-skills/` 里的技能做一个更接近“后续是否值得转正”的简版决策单。

这里不是最终安装清单，而是长期保留与后续启用优先级建议。

## P0，最值得转正

### 1. `proxy-automation-stabilizer`
原因：
- 和当前长期主项目 `D:\playwright` 高度贴合
- 不是泛能力，而是围绕你真实问题沉淀出的专项技能
- 对后续 Dreamina / 代理 / 自动化稳定性问题最有直接价值

建议：
- 长期保留
- 后续如果要正式并入 active skills，这个优先级最高

### 2. `java-knowledge-corpus`
原因：
- 是 Java 技能树总入口
- 对后续 Java 方向的主题路由最有帮助
- 能避免每次直接掉进细分技能里

建议：
- 长期保留
- 若只转正一项 Java 技能，优先它

### 3. `java-troubleshooting-triage`
原因：
- 非常适合真实开发/排障第一跳
- 能快速决定先查 JVM、数据库、网络还是 Spring
- 对工程场景实用性很强

建议：
- 高优先级保留
- 适合作为 Java 体系第二个转正技能

## P1，建议成套保留

这些单独看都不错，但真正价值在于形成成体系 Java 能力树。

- `java-learning-planner`
- `java-interview-answering`
- `java-concurrency-jvm`
- `java-data-backend`
- `java-design-refactor`
- `java-jvm-performance`
- `java-network-microservices`
- `java-spring-microservice`

建议：
- 如果你后面还持续做 Java 学习、面试、后端、Spring、排障，就整套保留
- 不建议零散删除，容易把原来清晰的边界打碎

## P2，保留但不急着转正

### `frontend-template-corpus`
- 适合模板分类、旧站模板拆解、页面灵感抽取
- 有用，但不是当前最高频主线

### `html-template-refactor`
- 适合旧 HTML 模板现代化重构思路
- 有参考价值，但当前优先级次于 Java / 代理自动化

### `frontend-slides`
- 做 HTML 演示稿时有用
- 明显偏低频

### `skill-vetter`
- 安全审查第三方 skill 有价值
- 低频但靠谱，建议留着

### `summarize`
- 取决于本地是否装了 `summarize` CLI
- 没装的话，它更像待命工具

## 不建议当前转正的

### `_archive/self-improving-agent`
原因：
- 带 hooks / scripts / learnings 结构
- 当前没有明确证据表明你现在这套 OpenClaw 工作流需要它
- 启用收益不确定，但维护成本和兼容性风险更现实

建议：
- 保持归档
- 未来如果你真想做“自动沉淀 learnings + hook 工作流”，再单独复审

## 实际建议顺序

如果后面你想把技能正式收口成 active 集合，我建议顺序是：

1. `proxy-automation-stabilizer`
2. `java-knowledge-corpus`
3. `java-troubleshooting-triage`
4. 剩余 Java 技能整套
5. `skill-vetter`
6. `frontend-template-corpus`
7. 其他低频参考技能

## 当前最稳的停点

目前最稳的状态其实是：
- `migrated-skills/` 作为已筛选候选区
- `_archive/` 作为已归档观察区
- 暂时不再移动目录

这样你后面真的要启用时，再做最后一步，不容易反复折腾。
