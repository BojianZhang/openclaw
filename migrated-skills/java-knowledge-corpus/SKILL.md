---
name: java-knowledge-corpus
description: Java 总入口知识技能。用于 Java 后端问题的主题定位、结构化解释、学习路径推荐与跨主题知识整合。适用于回答 Java 基础、并发、JVM、性能、设计模式、重构、MySQL、Redis、网络协议、Spring Boot、微服务与面试准备等问题；优先将问题路由到合适主题，而不是一次加载整个资料库。
---

# Java Knowledge Corpus

## 目标

把这个 skill 当成 **Java 知识总入口**，不是总包办技能，也不是整座书库的全文代理。

它的职责只有四个：
- 做主题定位
- 做问题分流
- 给结构化解释
- 给学习路径与延伸阅读建议

它不负责长期承接所有深度工程实现。遇到专项问题时，应优先把用户带到合适的主题卡、问答模板、checklist，或交给更窄的专项技能。

## 使用原则

1. 先判断问题属于哪个主题，不要一上来遍历所有资料。
2. 先给主题级解释，再决定是否下钻。
3. 优先读取最短路径文件，不要默认加载大量 references。
4. 回答时优先输出：
   - 这是什么
   - 为什么会这样
   - 在 Java / Spring / 后端工程里怎么体现
   - 常见误区
   - 下一步该看什么
5. 当问题已经明显进入专项实施层，转向对应专项技能或专项参考资料，不要让总入口承担全部细节。
6. 当问题是“面试怎么答”“八股怎么组织”“一分钟/三分钟答案怎么说”时，优先转 `java-interview-answering`。
7. 当问题是“Java 应该怎么学”“先学什么”“怎么补短板”“怎么做 2 周/4 周/8 周计划”时，优先转 `java-learning-planner`。
8. 当问题是“面试流程怎么走”“不同轮次怎么看”“面经怎么复盘”“offer/职级/薪资预期怎么理解”时，优先转 `tech-interview-strategy`。
9. 当问题是“MyBatis、Dubbo、ZooKeeper、MQ、ES、Linux 这些后端生态栈面试题怎么分组或怎么准备”时，优先转 `backend-interview-corpus`。
10. 当问题是“系统出故障先怎么分层排查”“先看 JVM / 数据库 / 网络 / Spring 哪层”时，优先转 `java-troubleshooting-triage`。

## 首选导航文件

优先只读这些文件：
- `references/TABLE-OF-CONTENTS.md`
- `references/problem-routing.md`
- `references/learning-paths.md`
- `references/topic-cards/README.md`

只有在确实需要继续下钻时，才读取更细的 references。

## 主题入口

微服务 / Spring Cloud 相关问题，优先按这条导航链理解：
**微服务概念认知 -> 微服务拆分与分布式复杂度 -> Spring Cloud 总览与演进 -> Spring Cloud 组件职责与调用链**

优先按主题卡分流：
- `references/topic-cards/java-language-and-design.md`
- `references/topic-cards/java-concurrency.md`
- `references/topic-cards/jvm-and-performance.md`
- `references/topic-cards/mysql-and-innodb.md`
- `references/topic-cards/redis-and-caching.md`
- `references/topic-cards/http-network-and-troubleshooting.md`
- `references/topic-cards/spring-boot-engineering.md`
- `references/topic-cards/microservice-foundations.md` （微服务概念/演进认知）
- `references/topic-cards/microservices-and-distributed-systems.md` （拆分/边界/分布式复杂度）
- `references/topic-cards/spring-cloud-foundations.md` （Spring Cloud 总览/演进）
- `references/topic-cards/spring-cloud-components.md` （Spring Cloud 组件职责）
- `references/topic-cards/java-project-sample-library.md` （项目样本库总览：乐Z家 / Spring Cloud 全家桶 / 双11秒杀 / 乐SHOP / 易购商城）
- `references/topic-cards/java-project-sample-evaluation.md` （项目样本统一评价维度与角色定位）
- `references/topic-cards/java-project-sample-misuse-warnings.md` （项目样本误用警告与反例提醒）
- `references/topic-cards/java-basic-vs-complex-project-selection.md` （基础项目 vs 复杂项目 的样本选择原则）
- `references/topic-cards/java-role-based-sample-combos.md` （按岗位选择项目样本组合）
- `references/topic-cards/java-role-sample-middleware-matrix.md` （按岗位 + 项目样本 + 中间件的三维选择矩阵）
- `references/topic-cards/java-question-to-sample-middleware-mapping.md` （按高频问题反推项目样本与中间件）
- `references/topic-cards/backend-system-sample-selection.md` （后台系统样本如何在进销存 / CRM / 云E办之间选择）
- `references/topic-cards/ecommerce-sample-selection.md` （电商样本如何在 Ebuy / 乐SHOP / 易购商城 / 秒杀之间选择）
- `references/topic-cards/microservice-sample-selection.md` （微服务样本如何在 Spring Cloud 全家桶 / 乐Z家之间选择）
- `references/topic-cards/project-direction-comparison.md` （后台系统 / 电商 / 微服务 三大项目方向的总对照）
- `references/topic-cards/java-interview-prep.md`

## 下钻规则

### 主题解释阶段
默认使用：
- `topic-cards/`
- `learning-paths.md`

### 经典知识补充阶段
只有在需要更完整背景时，再读：
- `deep-summaries/`
- `chapter-cards/`

### 高频问答阶段
当问题属于经典题型、面试题型或标准问答题型时，读：
- `qa-templates/`

### 专项下钻阶段
当问题已经进入排障、调优、结构落地、微服务治理、数据后端、JVM 或 Spring 实施层时，优先转到对应专项技能，而不是继续在总入口下钻执行层材料。

## 主题范围

这个 skill 负责这些主题的总入口导航：
- Java 基础与语言设计
- 并发与多线程
- JVM 与性能
- 设计模式与重构
- MySQL 与 InnoDB
- Redis 与缓存
- HTTP / TCP/IP / 网络排障
- Spring Boot 工程实践
- 微服务与分布式系统
- Java 面试知识整理
- Java 学习路线与阶段规划
- Java 后端故障总分诊

## 回答方式

默认按这个顺序回答：
1. 问题归类
2. 核心原理
3. Java / Spring / 后端场景体现
4. 常见误区
5. 下一步建议
6. 需要时再给延伸阅读

不要默认堆书名，不要默认堆资料层级，不要把目录系统本身讲得比问题还复杂。

## 学习路径使用方式

当用户问“怎么学”时：
- 先判断目标：基础、后端、并发、JVM、数据库、微服务、面试、补短板
- 优先转 `java-learning-planner`
- 只有当仍需总入口导航时，再读取 `references/learning-paths.md`

## 与专项技能的关系

这个 skill 是总入口，不是所有专项能力的最终承接者。

当问题已经进入下列场景时，应优先转向更窄技能或更窄资料：
- 设计模式选型、职责拆分、结构重构 -> `java-design-refactor`
- JVM 参数调优与性能瓶颈定位 -> `java-jvm-performance`
- Spring Boot 工程结构治理 -> `java-spring-microservice`
- 微服务拆分与分布式治理 -> `java-spring-microservice`
- MySQL / Redis 深度调优与问题定位 -> `java-data-backend`
- 并发机制、线程池、JMM 细节 -> `java-concurrency-jvm`
- 网络调用链、超时、连接与代理问题 -> `java-network-microservices`
- 面试回答组织、模拟问答、项目表达 -> `java-interview-answering`
- 学习路线、补短板、阶段计划 -> `java-learning-planner`
- 故障总分诊、分层排查路径 -> `java-troubleshooting-triage`

总原则：
- 这个 skill 负责“先看清是什么问题”
- 专项 skill 负责“把问题做深、做细、做落地”

## 回答边界

- 不把自己当成 PDF 全文复述工具。
- 不默认展开全部层级。
- 不在一个回答里同时塞满语言、并发、JVM、数据库、网络、微服务全部内容。
- 当问题需要最新框架版本、源码实现或项目上下文时，应结合当前代码与版本信息判断。

## 本地书库位置

主目录：
`D:\BaiduNetdiskDownload\200本Java程序员必看书籍\Java必读电子书\Java必读电子书`
