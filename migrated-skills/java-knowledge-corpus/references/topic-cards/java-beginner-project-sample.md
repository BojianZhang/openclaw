# 专题卡：Java 入门级项目样本

## 适用问题
- 有没有适合讲 Java 入门项目的样本？
- 如果我的项目不是微服务/电商/高并发，只是传统 Web 单体项目，该拿什么讲？
- 怎么介绍一个 Servlet/JSP/DAO 分层的入门项目？

## 样本：云日记
关键词：JSP、Servlet、MySQL、Tomcat、Maven、BaseDao、用户模块、类型模块、云记模块、主页模块、统计报表

## 这套样本更适合讲什么
- 传统 Java Web 单体项目从 0 到 1 的开发流程
- JSP/Servlet + DAO + Service + Web 层的基本分层
- 登录、免登录、用户、分类、记事、主页、统计报表这些基础模块怎么长出来
- 为什么入门项目更重要的是功能分析、前后端交互和数据库建模，而不是中间件堆砌

## 这套样本不适合讲什么
- Spring Cloud 组件治理
- Dubbo/ZooKeeper 服务协作
- 模块化电商平台能力演进
- 高并发秒杀链路

## 快速定位
如果问题是：
- “我做过一个 JSP/Servlet 项目，怎么讲？”
- “BaseDao/Servlet/Session/Cookie 这种传统项目要怎么介绍？”
- “入门级单体项目适合讲哪些价值点？”

优先用这套样本，而不是硬套微服务或电商平台项目。

## 默认路由
- 需要项目表达 -> `java-interview-answering`
- 需要样本总览/对照 -> `java-project-sample-library.md`
- 需要误用提醒 -> `java-project-sample-misuse-warnings.md`

## 常见提醒
- 不要因为项目“简单”就讲得像没有架构
- 不要用高级中间件话术硬包装入门项目
- 入门项目更该强调：功能拆分、MVC 思维、数据库设计、前后端交互、报表/统计能力
