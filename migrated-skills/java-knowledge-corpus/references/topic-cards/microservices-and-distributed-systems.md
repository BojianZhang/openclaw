# 专题卡：微服务与分布式系统

如果问题是在问“该不该拆微服务、边界怎么定、RPC/注册中心/一致性怎么理解”，优先用这张卡。
如果问题还停留在微服务概念和演进认知，先看 `microservice-foundations.md`。
如果问题已经进入 Spring Cloud 平台与组件，转 `spring-cloud-foundations.md` 或 `spring-cloud-components.md`。

## 适用问题
- 该不该拆微服务？
- 服务边界怎么定？
- Dubbo / RPC / 注册中心怎么理解？
- 分布式一致性难点是什么？

## 核心知识来源
- 从 Paxos 到 Zookeeper
- Dubbo 的过去、现在以及未来
- Kafka / Distributed Stateful System 资料
- Microservice 在 Cloud Foundry 的应用
- Microservices Practice 参考

## 核心结论
1. 不要为了“像高级架构”而拆微服务
2. 先划清业务边界，再谈通信方式和中间件
3. 分布式系统的真正复杂度在一致性、网络不可靠、治理和运维
4. RPC 只是调用手段，不会抹平远程调用的代价
5. 注册中心、配置中心、链路追踪、限流熔断都是微服务复杂度的一部分

## 常见误区
- 服务拆得过早
- 服务边界按技术层而不是业务能力划分
- 把远程调用当成本地方法
- 忽视幂等、超时、重试风暴

