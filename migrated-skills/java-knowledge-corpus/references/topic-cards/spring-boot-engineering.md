# 专题卡：Spring Boot 工程实践

## 适用问题
- Spring Boot 项目怎么分层？
- Controller / Service / Facade 怎么拆？
- 配置、异常、日志、校验怎么做？
- 直接跑 main 方法还是外部 Tomcat？

## 核心知识来源
- Spring Boot Practice 参考
- Effective Java
- 重构
- 阿里巴巴 Java 开发手册
- Practical API Design

## 核心结论
1. 小中型项目优先做清晰单体。
2. Spring Boot 工程实践的关键在于边界清晰、配置集中、异常分层、日志可排障。
3. 分层是为了职责清晰，不是为了目录好看。
4. 普通 Spring Boot 项目优先内嵌容器 + main 方法启动；外部 Tomcat 只在明确 WAR 部署要求时考虑。

## 常见误区
- Controller 过胖
- 配置写死在代码里
- 把所有流程都塞到 service
- 还没必要就硬上外部 Tomcat 或微服务

