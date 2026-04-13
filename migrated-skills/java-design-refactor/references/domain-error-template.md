# 代码案例：业务异常模板

## 目标
把“可预期业务错误”和“系统异常”分开，减少 controller/service 到处抛裸异常。

## 示例
```java
public class BizException extends RuntimeException {
    private final String code;

    public BizException(String code, String message) {
        super(message);
        this.code = code;
    }

    public String code() {
        return code;
    }
}
```

```java
@ExceptionHandler(BizException.class)
public ResponseEntity<ApiResponse<Void>> handleBiz(BizException ex) {
    return ResponseEntity.badRequest().body(ApiResponse.fail(ex.code(), ex.getMessage()));
}
```

## 使用建议
- 业务规则失败优先抛业务异常
- 系统级故障交给全局异常兜底
- code 要稳定、可读、可检索
