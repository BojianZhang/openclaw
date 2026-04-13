# Project Architecture Guidelines

## 适用场景
当用户在做 Java / Spring Boot 项目，并问：
- 架构怎么设计
- 包结构怎么分
- controller/service/facade 怎么拆
- 单体还是微服务
- 项目怎么重构
优先加载本文件。

## 核心原则
1. 先做清晰的单体，再考虑拆微服务
2. 先理顺模块边界，再引入复杂中间件
3. 把“运行起来”和“可维护”分开设计
4. 配置、日志、异常、任务等横切能力统一收口

## 推荐项目分层
### 对单体项目
- controller：请求入口
- facade / application：流程编排
- service：核心业务规则
- repository / dao：数据访问
- integration / client：第三方依赖调用
- common：共享能力

## 什么时候引入 facade
当一个用例跨多个 service，并且流程会持续扩展时，引入 facade/application 层。

## 什么时候不该拆微服务
- 业务边界不稳定
- 团队小
- 发布流程还不成熟
- 当前主要痛点是代码混乱

## 什么时候要优先重构项目结构
- 一个 controller/service 巨大无比
- 包名混乱
- 模块间互相引用严重
- 很多功能改动会牵一大片代码

## 推荐回答方式
遇到架构问题时，不要只给“理想架构图”，而要给：
1. 当前问题是什么
2. 为什么当前结构扛不住
3. 最小重构路径
4. 未来演进方向
