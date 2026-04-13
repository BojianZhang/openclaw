# Spring Cloud Config Patterns

Use this file when the user needs realistic config-key patterns from classic Spring Cloud sample projects rather than only conceptual descriptions.

## Parent POM / version-management pattern

A repeated parent-POM pattern appears across the samples:
- parent: `spring-boot-starter-parent`
- property: `spring-cloud.version=Hoxton.SR1`
- optional property: `spring-cloud-alibaba.version=2.1.0.RELEASE`
- import BOMs through `dependencyManagement`
- split infra and business modules under one aggregator `pom`

Practical lesson:
- many course/demo projects teach Spring Cloud first through multi-module version alignment, not through one isolated service

## Eureka registry config pattern

Typical keys:
```yml
spring:
  application:
    name: eureka-server
server:
  port: 8761

eureka:
  instance:
    hostname: eureka01
    prefer-ip-address: true
    instance-id: ${spring.cloud.client.ip-address}:${server.port}
  client:
    service-url:
      defaultZone: http://localhost:8762/eureka/
```

What to preserve conceptually:
- app name identifies the registry app
- server port separates nodes
- `prefer-ip-address` + `instance-id` help instance identity clarity
- `defaultZone` often points to peer nodes in HA demos

## Config Client bootstrap pattern

Typical classic Config Client bootstrap file:
```yml
spring:
  cloud:
    config:
      name: config-client
      uri: http://localhost:8888
      label: master
      profile: dev
```

Meaning:
- `name`: remote config file prefix / app identity
- `uri`: config server address
- `label`: branch
- `profile`: environment profile

Practical lesson:
- in classic Spring Cloud Config, these bootstrap-stage keys matter because config resolution must happen early

## Config Server pattern

Typical Config Server keys:
```yml
server:
  port: 8888
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/.../config-repo
          # username/password/default-label/search-paths optional
```

Optional bus-enabled extension:
```yml
spring:
  rabbitmq:
    host: 192.168.10.101
    port: 5672
    username: guest
    password: guest
    virtual-host: /
```

And actuator exposure pattern:
```yml
management:
  endpoints:
    web:
      base-path: /actuator
      exposure:
        include: bus-refresh
```

Practical lesson:
- Config + Bus demos usually combine config-server, message broker, and actuator exposure in one place

## Consul Config client pattern

The samples show a lighter client-side dependency pattern:
- `spring-cloud-starter-consul-discovery`
- `spring-cloud-starter-consul-config`
- `spring-boot-starter-actuator`

Typical mental model:
- discovery + config can live in one ecosystem
- refresh still tends to be demonstrated through `@RefreshScope` and property-binding classes

## Apollo client pattern

The samples emphasize client consumption rather than custom server implementation.
Typical signs:
- dependency: `apollo-client`
- startup annotation: `@EnableApolloConfig`
- properties injected through `@Value` or configuration holder classes

Practical lesson:
- Apollo demos are often about client-side central config consumption and typed property exposure, not about building config-server logic yourself

## Gateway config patterns

Even when Java config classes define routes/rules, the config story still usually includes:
- registry participation for service discovery
- route IDs mapping to service names
- rate-limit key resolution or gateway flow rules
- optional Sentinel gateway integration

Good engineering reminder:
- route/rule definition may live in Java config, but the environment and registry-related keys still shape behavior outside those classes

## Common config-shape heuristics

1. `spring.application.name` is almost always the first identity anchor.
2. Infra modules usually expose `server.port` explicitly.
3. Registry-aware apps usually carry `eureka.client.service-url.defaultZone` or equivalent discovery config.
4. Dynamic-config demos usually separate bootstrap-stage config from ordinary application config.
5. Refresh demos usually combine config source + refresh annotation + exposed endpoint/controller.
6. Bus demos add message-broker config and actuator exposure.
7. Consul/Apollo demos often emphasize typed property holders, not just raw `@Value` scattered everywhere.

## Source notes

Distilled from the user's sample projects for Eureka, Config, Bus, Consul Config, Apollo, and related Spring Cloud demos.
