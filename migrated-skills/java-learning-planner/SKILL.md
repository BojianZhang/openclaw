---
name: java-learning-planner
description: 为 Java 学习者制定分阶段学习路线、补短板计划与书单裁剪方案。Use when the user asks how to learn Java backend, what order to study topics, how to switch from zero/foundation to backend, how to prepare for interviews in weeks or months, how to fill gaps in 并发/JVM/MySQL/Redis/Spring Boot/微服务, or how to turn a large Java book list into a practical study plan.
---

# Java Learning Planner

## Goal

把“大而散的 Java 书单和知识点”压成可执行的学习计划。

这个 skill 不负责深度排障，也不负责代替专项技术分析。
它的职责是：
- 判断学习起点
- 判断目标导向
- 规划阶段路线
- 裁剪书单与资料
- 给出周计划 / 月计划 / 面试冲刺计划

## Workflow

1. 先判断用户当前阶段：零基础、Java 基础、初级后端、在职提升、面试冲刺。
2. 先判断目标：后端入门、并发/JVM、数据库、Spring Boot、微服务、面试。
3. 不一次性摊开全部书单，只保留当前阶段最相关的 3~7 项。
4. 回答时优先给：
   - 目标阶段
   - 学习顺序
   - 每阶段核心资料
   - 常见误区
   - 2 周 / 4 周 / 8 周可执行计划
5. 如果用户已经进入某个专项深水区，再转对应专项技能，不要继续停留在学习规划层。

## Read Path

优先读取：
- `references/stage-models.md`
- `references/planning-templates.md`
- `references/gap-to-skill-map.md`

补充读取：
- `../java-knowledge-corpus/references/learning-paths.md`
- `../java-knowledge-corpus/references/faq.md`

## Output Shapes

### 1. 路线推荐
按这个顺序：
1. 当前阶段判断
2. 目标判断
3. 推荐顺序
4. 每阶段资料
5. 时间安排
6. 不该做什么

### 2. 补短板计划
按这个顺序：
1. 当前短板
2. 先补哪块
3. 为什么先补
4. 练习方式
5. 验收标准

### 3. 面试冲刺计划
按这个顺序：
1. 时间预算
2. 核心模块
3. 每周重点
4. 高频题型
5. 项目表达补位

## Handoff Rules

遇到下面情况，转专项技能：
- 并发/JMM/线程池细节 -> `java-concurrency-jvm`
- GC/OOM/性能定位 -> `java-jvm-performance`
- MySQL/Redis/缓存策略 -> `java-data-backend`
- Spring Boot 工程与微服务治理 -> `java-spring-microservice`
- HTTP/TCP/服务调用链 -> `java-network-microservices`
- 设计模式与重构策略 -> `java-design-refactor`
- 面试答案表达与模拟问答 -> `java-interview-answering`
- 面试流程、轮次策略、面经复盘 -> `tech-interview-strategy`

## Output Rules

默认输出要可执行，不要只给书单。
优先给：
- 顺序
- 阶段目标
- 时间盒
- 验收方式

不要默认输出：
- 一长串书名
- 模糊的“多练多看”
- 没有优先级的建议
