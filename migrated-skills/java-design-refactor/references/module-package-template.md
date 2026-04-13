# 代码案例：模块化包结构模板

## 目标
避免把所有 controller/service/client 全堆在一个包里，给中型 Spring Boot 项目一个可演进结构。

## 推荐结构
```text
com.example.project
├─ common/
│  ├─ config/
│  ├─ exception/
│  ├─ web/
│  └─ util/
├─ integration/
│  ├─ externalA/
│  └─ externalB/
└─ module/
   ├─ user/
   │  ├─ controller/
   │  ├─ facade/
   │  ├─ service/
   │  └─ dto/
   ├─ task/
   └─ configcenter/
```

## 使用建议
- 按业务域而不是按技术层平铺所有类
- integration 与业务模块分开
- common 只放真正横切能力
