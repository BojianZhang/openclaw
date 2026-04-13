# 代码案例：Facade / Application 编排模板

## 目标
把跨多个 service 的完整业务流程从单一 service 中拆出来。

## 示例
```java
@Service
public class SignupFacade {
    private final UserService userService;
    private final MailService mailService;
    private final AuditService auditService;

    public SignupFacade(UserService userService, MailService mailService, AuditService auditService) {
        this.userService = userService;
        this.mailService = mailService;
        this.auditService = auditService;
    }

    public SignupResult signup(SignupRequest request) {
        User user = userService.createUser(request);
        mailService.sendWelcomeMail(user.getEmail());
        auditService.record("signup", user.getId());
        return new SignupResult(user.getId(), user.getEmail());
    }
}
```

## 适用场景
- 注册 + 发邮件 + 审计
- 批量任务启动 + 状态初始化 + 投递执行器
- 登录 + 拉取外部信息 + 更新缓存

## 使用建议
- facade 负责编排，不抢 service 的规则职责
- service 负责业务规则，facade 负责流程拼装
