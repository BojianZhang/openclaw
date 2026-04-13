---
name: java-interview-answering
description: 结构化回答 Java 面试题，并把零散知识整理成可讲的答案。Use when the user asks for Java interview preparation, mock answers, one-minute or three-minute response structures, interview question breakdowns, “八股”优化，project-plus-theory answer framing, or how to explain Java / 并发 / JVM / MySQL / Redis / Spring Boot / 微服务问题更像面试回答。
---

# Java Interview Answering

## Goal

把“知道一些点”整理成“能说出口的答案”。

重点不是扩写成教科书，而是把回答压成适合面试表达的结构：
- 先给结论
- 再给原理
- 再给工程体现
- 最后补项目经验或边界条件

## Workflow

1. 先判断题型：概念题、对比题、设计题、排障题、项目题。
2. 先给 **短答版**，默认控制在 3~6 句。
3. 再给 **展开版**，按“原理 -> 场景 -> 风险/误区 -> 实战例子”展开。
4. 如果用户是准备面试，再补：
   - 面试官追问点
   - 容易答崩的点
   - 可以接项目经历的切口
5. 如果问题已经进入工程落地或故障处理，转给对应专项技能，不要继续把面试回答写成排障手册。

## Default Answer Shapes

### 1. 概念题
按这个顺序：
1. 一句话定义
2. 为什么需要它
3. 核心机制
4. Java / Spring / 后端里的典型体现
5. 常见误区

### 2. 对比题
按这个顺序：
1. 先给结论和选择建议
2. 再按维度对比：语义、性能、适用场景、风险
3. 最后给一句工程建议

### 3. 设计题
按这个顺序：
1. 先说明目标和约束
2. 再讲方案与边界
3. 再讲为什么不用别的方案
4. 最后讲演进路径

### 4. 排障题
按这个顺序：
1. 先看现象
2. 再看证据
3. 再做分层定位
4. 最后给修复与预防

### 5. 项目题
按这个顺序：
1. 背景
2. 你的职责
3. 难点
4. 决策
5. 结果
6. 复盘

## Read Path

优先读取：
- `references/answer-structures.md`
- `references/high-frequency-java-topics.md`
- `references/project-answer-framing.md`
- `references/microservice-foundation-answers.md`（当问题是微服务基础概念、对比题、架构演进题时）
- `references/spring-cloud-foundation-answers.md`（当问题是 Spring Cloud 定义、总览、代际演进、Alibaba、版本命名时）
- `references/spring-cloud-components-answers.md`（当问题是 Eureka/Consul/Ribbon/Feign/Hystrix/Sentinel/Zuul/Gateway/Sleuth/Stream/Config/Apollo 这类组件单题时）
- `references/spring-cloud-call-chain-answers.md`（当问题是一次请求经过哪些层、多个组件如何协作、如何沿调用链解释故障时）
- `references/spring-cloud-project-connection-lines.md`（当用户需要把 Spring Cloud 理论题答得更像项目表达时）
- `references/seckill-project-answers.md`（当问题是秒杀系统设计、双11项目、Redis+MQ削峰、接口安全、超卖与项目表达时）
- `references/seckill-project-deep-answers.md`（当用户需要把秒杀项目讲成完整高并发请求链，或回答更深的追问时）
- `references/ecommerce-platform-project-answers.md`（当问题是模块化电商平台项目，涉及 portal/manager/SSO/order/Redis/搜索/支付/短信 等项目表达时）
- `references/ecommerce-platform-deep-answers.md`（当用户需要把电商平台项目讲成模块边界清晰、能力演进合理的完整项目回答时）
- `references/ecommerce-platform-followup-answers.md`（当用户需要接电商平台项目的追问，如为什么拆 portal/manager、为什么单独做 SSO、为什么先 order 后 payment 等）
- `references/ego-mall-project-answers.md`（当问题是传统 Java 多模块 易购商城项目，涉及 ego-rpc/ego-sso/ego-order、Dubbo、Solr、购物车、订单支付、RabbitMQ 等项目表达时）
- `references/ego-mall-followup-answers.md`（当用户需要接 易购商城项目的追问，如为什么用 Dubbo+ZooKeeper、为什么有 ego-rpc、为什么购物车不能只当成前端功能等）
- `references/ecommerce-platform-comparison-answers.md`（当用户需要对比 乐SHOP 与 易购商城 两类商城平台样本，并说明各自更适合讲什么时）
- `references/beginner-web-project-answers.md`（当问题是传统 JSP/Servlet/DAO 风格的 Java 入门级 Web 项目表达时）
- `references/beginner-web-project-followups.md`（当用户需要接 Java 入门级 Web 项目的追问，如为什么项目简单也值得讲、为什么 BaseDao 值得提等）
- `references/traditional-web-commerce-project-answers.md`（当问题是传统 Java Web 单体电商项目，涉及商品分类、搜索、详情、购物车、订单、后台管理等项目表达时）
- `references/traditional-web-commerce-followups.md`（当用户需要接传统 Java Web 电商项目的追问，如为什么单体项目也值得讲、为什么购物车值得单独提等）
- `references/inventory-management-project-answers.md`（当问题是进销存/后台管理型业务系统项目表达时）
- `references/crm-project-answers.md`（当问题是 CRM/客户管理/营销管理/权限报表类项目表达时）
- `references/office-platform-project-answers.md`（当问题是云E办这类前后端分离办公平台项目表达时）
- `references/office-platform-project-followups.md`（当前后端分离办公平台项目需要接权限、安全、消息、协同等追问时）
- `references/office-platform-vs-traditional-backend-answers.md`（当用户在比较前后端分离平台与传统后台项目时）
- `references/office-platform-10-drills.md`（当用户需要围绕云E办这类项目做 10 题实战演练时）
- `references/office-platform-security-answers.md`（当用户被追问 Spring Security、OAuth2、JWT、Redis token、SSO 等安全体系问题时）
- `references/middleware-project-placement-answers.md`（当用户问不同中间件在各项目样本里该怎么落位、怎么表达时）
- `references/backend-system-comparison-answers.md`（当用户在比较 CRM、进销存、云E办 这三类后台系统样本时）
- `references/backend-system-followup-tree.md`（当用户已经介绍后台系统项目，但需要继续接追问时）
- `references/backend-system-drill-pack.md`（当用户想集中刷后台系统项目题时）
- `references/backend-system-mock-answers.md`（当用户要围绕后台系统项目做模拟答法时）
- `references/ecommerce-project-drill-pack.md`（当用户想集中刷电商项目题时）
- `references/ecommerce-project-mock-answers.md`（当用户要围绕电商项目做模拟答法时）
- `references/ecommerce-project-followup-tree.md`（当用户已经介绍电商项目，但需要继续接追问时）
- `references/microservice-springcloud-drill-pack.md`（当用户想集中刷微服务 / Spring Cloud 项目题时）
- `references/microservice-springcloud-mock-answers.md`（当用户要围绕微服务 / Spring Cloud 项目做模拟答法时）
- `references/microservice-project-followup-tree.md`（当用户已经介绍微服务 / Spring Cloud 项目，但需要继续接追问时）
- `references/project-direction-speaking-strategy.md`（当用户不知道该先讲后台系统、电商还是微服务项目时）
- `references/java-project-high-frequency-20-questions.md`（当用户要围绕全部项目样本做统一刷题或 20 题总练习时）
- `references/beginner-vs-complex-project-answers.md`（当用户在纠结该讲基础项目还是复杂项目时）
- `references/java-project-sample-selection-answers.md`（当用户在问“这类问题该拿哪套项目样本来讲”时）
- `references/java-project-sample-playbacks.md`（当用户需要真实问题回放式的样本选择与最佳回答姿势时）
- `references/java-project-top-questions.md`（当用户要准备 Java 后端项目题/架构题的高频问题集时）
- `references/java-project-10-drills.md`（当用户要做 10 题实战演练式的项目题训练时）
- `references/java-project-self-mapping-guide.md`（当用户想把自己的真实项目映射到样本库并借用合适的话术时）
- `references/role-based-project-speaking-strategy.md`（当用户想按目标岗位决定主讲哪几套项目样本时）
- `references/role-sample-middleware-speaking-strategy.md`（当用户想按岗位决定主讲哪个项目，并补哪些中间件、避免哪些误挂时）

当问题明显属于知识导航或学习路线时，再回到：
- `../java-knowledge-corpus/SKILL.md`
- `../java-learning-planner/SKILL.md`

## Handoff Rules

遇到下面情况，转专项技能：
- 并发/JMM/线程池细节排障 -> `java-concurrency-jvm`
- GC/OOM/性能分析 -> `java-jvm-performance`
- MySQL/Redis/缓存一致性 -> `java-data-backend`
- Spring Boot 工程结构/微服务治理 -> `java-spring-microservice`
- HTTP/TCP/timeout/reset/调用链网络问题 -> `java-network-microservices`
- 设计模式/职责拆分/重构方案 -> `java-design-refactor`
- 学习路线、补短板、阶段规划 -> `java-learning-planner`
- 面试流程、面经复盘、轮次策略、offer认知 -> `tech-interview-strategy`

## Output Rules

默认输出：
- 短答版
- 展开版
- 面试官可能追问
- 一句项目化表达（如果适用）

优先使用统一颗粒度：
- **概念题**：短答版 -> 展开版 -> 常见追问 -> 易错点/易答崩点 -> 项目化补句
- **对比题**：结论 -> 分维度对比 -> 选择建议 -> 常见坑 -> 项目连接句
- **设计题**：目标与约束 -> 方案 -> 权衡 -> 演进路径 -> 风险点
- **排障题**：现象 -> 证据 -> 分层定位 -> 修复方案 -> 预防方案
- **项目题**：背景 -> 职责 -> 难点 -> 决策 -> 结果 -> 复盘

如果某道题不需要全部小节，可以缩写，但尽量保持这个输出骨架，避免不同题型风格漂移太大。

不要默认输出：
- 大段书本目录
- 过长源码
- 纯定义堆砌
- 没有场景的八股背诵
