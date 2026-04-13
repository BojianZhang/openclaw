# 问答模板：Spring Boot 工程实践

## Q: Spring Boot 项目怎么分层最合适？
### 短答版
小中型项目优先做清晰单体：controller 管边界、service 管规则、facade/application 管流程编排、integration/client 管外部依赖。

### 展开版
推荐把层次拆清：
1. **controller**：接请求、做基础校验、返回结果
2. **service**：放核心业务规则
3. **facade/application**：串多个 service 的完整流程
4. **integration/client**：访问第三方系统、HTTP、消息、外部平台
5. **common/config**：异常、日志、配置、工具

这样做的好处是：边界清晰、可测试性更好、后续扩展不容易糊成一团。

## Q: Spring Boot 应该用 main 方法跑，还是外部 Tomcat？
### 短答版
默认优先 main 方法 + 内嵌容器；只有明确 WAR 部署要求时，才考虑外部 Tomcat。

### 展开版
这本质是一个部署复杂度与历史约束的取舍问题。默认情况下，main 方法 + 内嵌容器更简单、更稳；如果涉及统一容器规范或历史系统兼容，再进入 `spring-boot-vs-external-tomcat.md` 做完整判断。
