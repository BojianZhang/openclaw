# Spring Cloud 项目连接句

Use this file when the user knows the theory but needs short project-oriented bridge lines to make answers sound more like real project experience.

## 通用连接句
- “如果放到项目里，我会先把它放回调用链位置，而不是单独背组件定义。”
- “这个组件我会从它解决的问题、落在调用链的哪一层、以及带来的代价三个角度去讲。”
- “如果项目里没完整用过这一套，我会明确说明自己掌握的是选型逻辑和实现模式，而不是硬说线上深度实践过。”

## 注册中心
- “项目里通常会把注册中心单独作为基础设施节点，业务服务启动后注册进去，消费者再按服务名发现实例。”

## Feign / 调用
- “在项目里 Feign 一般是以接口方式落在消费者服务里，方便把远程调用和业务逻辑分开，同时也更容易挂 fallbackFactory。”

## Hystrix / Sentinel
- “如果结合项目，我会重点讲 fallback 放在哪一层、是怎么避免把容错逻辑散落到 controller 里的。”

## Gateway
- “项目里网关通常是独立应用，不是每个服务都混着写路由和过滤逻辑，这样边界会更清晰。”

## Sleuth
- “链路追踪真正的价值不是多写几个注解，而是保住真实调用链，出问题时能知道第一跳慢在哪。”

## Stream
- “消息驱动这块我会强调生产者、消费者、绑定关系是分开建模的，不是把 MQ 细节直接揉进业务代码里。”

## Config / Bus / Apollo
- “如果结合项目，我会讲配置中心是怎么和客户端刷新、集群传播、环境隔离这些问题绑在一起的，而不是只背哪个组件名。”
