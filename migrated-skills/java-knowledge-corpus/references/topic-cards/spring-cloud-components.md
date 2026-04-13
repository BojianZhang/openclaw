# 专题卡：Spring Cloud 组件层

如果问题是在问具体组件分别做什么，或者多个组件怎么按职责分层理解，优先用这张卡。
如果问题是在问 Spring Cloud 整体定义和演进，先看 `spring-cloud-foundations.md`。
如果问题是在问超时、重试、调用链不稳定这类路径问题，转 `http-network-and-troubleshooting.md` 或 specialist skill。

## 适用问题
- Eureka / Consul / Ribbon / Feign / Hystrix / Sentinel / Gateway / Config 这些组件分别做什么？
- 服务注册、调用、容错、网关、链路追踪、配置中心之间是什么关系？
- 这些组件怎么按职责分组理解？

## 核心知识点
1. 注册与发现：Eureka / Consul / Nacos
2. 客户端调用与负载：Ribbon / Feign / OpenFeign
3. 稳定性保护：Hystrix / Sentinel
4. 网关：Zuul / Gateway
5. 观测：Sleuth / Zipkin
6. 消息驱动：Stream
7. 配置管理：Config / Bus / Consul Config / Apollo
8. 要把这些组件放到同一条调用链里理解，而不是孤立背名词

## 默认路由
- 架构解释、选型理解 -> `java-spring-microservice`
- 面试表达、对比题 -> `java-interview-answering`
- 调用链超时、重试、连接细节 -> `java-network-microservices`

## 常见提醒
- 不要把所有组件混成一个层次
- 不要只背组件名，不讲职责和协作关系
- 不要把老组件维护状态变化直接说成“不能用”
