# Table of Contents

## 0. 总入口
- `../SKILL.md`

## 1. 默认导航层（总入口优先保留）
这些文件是 `java-knowledge-corpus` 的核心：
- `problem-routing.md`
- `learning-paths.md`
- `faq.md`
- `topic-cards/`

说明：
- 默认先读这一层
- 能在这一层完成导航，就不要继续下钻

## 2. 书库与主题索引（按需读）
- `books-index.md`
- `topic-to-books.md`
- `core-books-summaries.md`

用途：
- 当用户明确要书单、主题到书籍映射、补充阅读建议时再读

## 3. 主题卡层（主导航层）
目录：`topic-cards/`

核心主题：
- Java 语言与设计
- Java 并发
- JVM 与性能
- MySQL 与 InnoDB
- Redis 与缓存
- HTTP / 网络 / 排障
- Spring Boot 工程
- 微服务与分布式系统
- Java 面试准备

## 4. 章节级基础卡层（轻量补充）
目录：`chapter-cards/`

当前保留的是更适合总入口的 Java 基础卡：
- `effective-java-core.md`
- `java-core-tech-vol1-vol2-core.md`
- `java8-core.md`

用途：
- 只在总入口解释需要补基础背景时读取
- 不承担 specialist 深度实施职责

## 5. 问答模板层（宽口径补充）
目录：`qa-templates/`

当前保留的是宽口径模板：
- `java-design-qa.md`
- `mysql-redis-qa.md`
- `network-microservices-qa.md`
- `spring-boot-qa.md`

用途：
- 用于高频、宽口径、主题级 Q&A
- 不代替 specialist checklist / decision / implementation references

## 6. 深摘要层（降级为按需读）
目录：`deep-summaries/`

作用：
- 提供经典书目的背景知识
- 用于总入口阶段的补充解释
- 不再承担执行层排障职责
- 默认不主动展开，只有在 topic-card 与 FAQ 不够时才读

## 7. 专项技能分流
当问题进入执行层、排障层、实现层时，优先转到对应专项技能：
- `java-design-refactor`
- `java-jvm-performance`
- `java-data-backend`
- `java-spring-microservice`
- `java-concurrency-jvm`
- `java-network-microservices`
- `java-interview-answering`
- `java-learning-planner`
- `java-troubleshooting-triage`

## 推荐阅读顺序

### 快速理解这套 skill
1. `../SKILL.md`
2. `problem-routing.md`
3. `learning-paths.md`
4. 对应 `topic-cards/`

### 解决具体问题
1. `problem-routing.md`
2. 先进入对应 `topic-cards/`
3. 需要轻量补充时再进入 `chapter-cards/` 或宽口径 `qa-templates/`
4. 需要书目映射时再进入书库索引层
5. 只有在上述信息不够时，再进入 `deep-summaries/`
6. 如果问题进入专项实施层，转对应专项技能
7. 如果问题进入面试表达层，转 `java-interview-answering`
8. 如果问题进入学习规划层，转 `java-learning-planner`
9. 如果问题先需要故障分层与总分诊，转 `java-troubleshooting-triage`
