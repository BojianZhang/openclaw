# 专题卡：Spring Cloud 基础

如果问题是在问 Spring Cloud 是什么、和 Spring Boot 什么关系、组件总览、Netflix/Alibaba 演进、版本命名，优先用这张卡。
如果问题已经进入具体组件职责，转 `spring-cloud-components.md`。
如果问题还停留在微服务概念层，先看 `microservice-foundations.md`。

## 适用问题
- Spring Cloud 是什么？
- Spring Boot 和 Spring Cloud 有什么关系？
- Spring Cloud 常用组件有哪些？
- Netflix 体系和 Alibaba 体系怎么理解？
- 为什么会有 Hoxton 这种版本名？

## 核心知识点
1. Spring Boot 偏单服务开发效率，Spring Cloud 偏多服务治理协作
2. Spring Cloud 的核心价值是把注册发现、配置、调用、网关、容错、消息、追踪等能力纳入统一生态
3. Netflix 体系是经典第一代认知来源；新一代更偏 Gateway、LoadBalancer、Resilience4J / Sentinel、Nacos 等演进方向
4. Spring Cloud Alibaba 是国内常见的实践路线，和 Nacos / Sentinel / RocketMQ / Seata 等生态强相关
5. 版本名本质是 release train，用来管理整套子项目的兼容版本集合

## 默认路由
- 如果用户在问架构理解、组件职责、版本认知 -> `java-spring-microservice`
- 如果用户在问面试表达、口语化回答 -> `java-interview-answering`
- 如果用户在问具体调用链、超时、网关链路不稳定 -> `java-network-microservices`

## 常见提醒
- 不要把 Spring Cloud 说成单个组件
- 不要把组件名堆砌当成理解
- 不要把 Netflix 体系和 Spring Cloud 本身完全画等号
- 不要只背版本名，不讲 release train 的目的
