---
name: java-troubleshooting-triage
description: 对 Java 后端故障做总分诊与排障路径规划。Use when the user asks “系统出故障了先怎么查”, “这个报错先看哪里”, “该从 JVM / 数据库 / 网络 / Spring 哪层下手”, or needs a first-pass troubleshooting plan before committing to a narrower skill. Best for symptom triage across startup failure, timeout, high CPU, Full GC, OOM, slow query, cache failure, connection reset, thread blockage, or mixed backend symptoms.
---

# Java Troubleshooting Triage

## Goal

先把故障看清，再决定往哪条专项路径走。

这个 skill 不负责把所有问题一次性查到底，它负责：
- 识别症状类型
- 建立分层视角
- 先列最小证据清单
- 判断先查哪层
- 转到合适专项技能

## Workflow

1. 先问清症状，不先猜原因。
2. 把问题先分到一类：启动失败、性能下降、GC/OOM、数据库/缓存、网络调用、并发阻塞、结构性设计问题。
3. 先看证据，再看推断。优先要：
   - 错误日志
   - 时间点
   - 监控指标
   - 线程栈 / GC 日志 / 慢日志 / 调用链
4. 先做分层，不要把“慢”直接等同于数据库或 JVM：
   - 应用启动层
   - JVM/线程层
   - 数据层
   - 网络/调用链层
   - Spring/配置层
5. 给出最小排障路径：先看什么，再看什么，不要一次铺满所有方向。
6. 一旦主导故障层清晰，立刻转对应专项技能，不在本 skill 里继续深挖实现细节。

## Symptom Buckets

### 1. 启动失败
优先怀疑：
- Spring 配置
- Bean 装配
- 环境变量 / 配置缺失
- 依赖冲突

转：`java-spring-microservice`

### 2. CPU 高 / 响应慢 / Full GC / OOM
优先怀疑：
- GC 压力
- 分配过快
- 线程阻塞
- 锁竞争
- 堆外或堆内存问题

转：`java-jvm-performance`
如果更明显是线程模型或共享状态问题，再转：`java-concurrency-jvm`

### 3. SQL 慢 / 缓存失效 / 数据一致性异常
优先怀疑：
- 索引或执行计划
- 锁等待
- 缓存穿透 / 击穿 / 雪崩
- 双写一致性
- 应用层数据访问方式

转：`java-data-backend`

### 4. timeout / reset / keep-alive / 下游调用不稳定
优先怀疑：
- 连接复用
- 超时链不一致
- 重试放大
- 代理 / 网关 / 负载均衡层
- 下游服务本身慢

转：`java-network-microservices`

### 5. 线程卡死 / 死锁 / 线程池打满 / CompletableFuture 混乱
优先怀疑：
- 锁竞争
- 线程池配置
- 阻塞任务进入错误线程池
- 共享状态设计问题

转：`java-concurrency-jvm`

### 6. 结构混乱导致问题反复出现
优先怀疑：
- 职责边界不清
- 模块耦合
- 事务、缓存、调用编排混在一起

转：`java-design-refactor`

## Read Path

优先读取：
- `references/triage-checklist.md`
- `references/symptom-to-skill-map.md`
- `references/minimum-evidence.md`

如需总入口配合：
- `../java-knowledge-corpus/references/problem-routing.md`

## Output Shape

默认按这个顺序输出：
1. 症状归类
2. 最可能的主导层
3. 最小证据清单
4. 建议排查顺序
5. 应转向的专项技能
6. 当前不要急着做什么

## Anti-Patterns

不要：
- 一上来甩一大堆 JVM 参数
- 没证据就认定数据库慢
- 没分层就默认网络有问题
- 在总分诊阶段直接展开源码级修复
- 把所有专项问题混在一个回答里
