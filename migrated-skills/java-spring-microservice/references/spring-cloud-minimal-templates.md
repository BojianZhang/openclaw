# Spring Cloud Minimal Templates

Use this file when the user wants the smallest reusable project patterns that can be copied into a real project and then evolved gradually.

The goal of these templates is not production completeness. The goal is a clean starting skeleton.

## 1. Eureka Server minimal template

### Module role
A dedicated registry module.

### Startup class
```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }
}
```

### application.yml
```yml
spring:
  application:
    name: eureka-server
server:
  port: 8761

eureka:
  instance:
    hostname: localhost
    prefer-ip-address: true
    instance-id: ${spring.cloud.client.ip-address}:${server.port}
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

### Dependency hint
- `spring-cloud-starter-netflix-eureka-server`
- `spring-boot-starter-web`

### Upgrade path
- later add peer node for HA
- later refine self-registration / fetch-registry behavior
- later externalize environment-specific addresses

## 2. Service Provider minimal template

### Module role
A normal business service that exposes HTTP endpoints and registers itself.

### Startup class
```java
@SpringBootApplication
public class ProductServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProductServiceApplication.class, args);
    }
}
```

### Controller
```java
@RestController
@RequestMapping("/product")
public class ProductController {
    @GetMapping("/{id}")
    public Product getById(@PathVariable Integer id) {
        return new Product(id, "demo-product");
    }
}
```

### application.yml
```yml
spring:
  application:
    name: product-service
server:
  port: 7070

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

### Upgrade path
- later add service layer
- later add persistence
- later add health/readiness separation

## 3. Feign Consumer minimal template

### Module role
A consumer service that calls another service by service name.

### Startup class
```java
@SpringBootApplication
@EnableFeignClients
public class OrderServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

### Feign client
```java
@FeignClient("product-service")
public interface ProductClient {
    @GetMapping("/product/{id}")
    Product getById(@PathVariable("id") Integer id);
}
```

### Controller
```java
@RestController
@RequestMapping("/order")
public class OrderController {
    private final ProductClient productClient;

    public OrderController(ProductClient productClient) {
        this.productClient = productClient;
    }

    @GetMapping("/{id}")
    public Product query(@PathVariable Integer id) {
        return productClient.getById(id);
    }
}
```

### application.yml
```yml
spring:
  application:
    name: order-service
server:
  port: 8081

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

### Upgrade path
- later add fallbackFactory
- later add timeout / retry governance
- later separate controller and orchestration service

## 4. Feign + FallbackFactory minimal template

### Why this version matters
This is a better growth path than teaching a bare fallback first, because exception visibility is preserved.

```java
@FeignClient(value = "product-service", fallbackFactory = ProductClientFallbackFactory.class)
public interface ProductClient {
    @GetMapping("/product/{id}")
    Product getById(@PathVariable("id") Integer id);
}

@Component
public class ProductClientFallbackFactory implements FallbackFactory<ProductClient> {
    @Override
    public ProductClient create(Throwable cause) {
        return id -> new Product(id, "fallback-product");
    }
}
```

### Upgrade path
- later add logging and error tags
- later distinguish timeout / business fallback / empty-result fallback

## 5. RestTemplate + LoadBalanced minimal template

Use only when the user explicitly wants classic RestTemplate-style teaching or legacy compatibility.

```java
@SpringBootApplication
public class OrderServiceRestApplication {
    @Bean
    @LoadBalanced
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

### Upgrade path
- prefer Feign/OpenFeign for cleaner consumer-side contracts in most newer teaching flows

## 6. Gateway minimal template

### Startup class
```java
@SpringBootApplication
public class GatewayServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayServerApplication.class, args);
    }
}
```

### Java route config
```java
@Configuration
public class GatewayRoutesConfiguration {
    @Bean
    public RouteLocator routeLocator(RouteLocatorBuilder builder) {
        return builder.routes()
                .route("product-service", r -> r.path("/product/**")
                        .uri("lb://product-service"))
                .build();
    }
}
```

### Upgrade path
- later add custom filter
- later add rate limiting / key resolver
- later add sentinel gateway protection

## 7. Config Server minimal template

### Startup class
```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

### application.yml
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
          uri: https://github.com/example/config-repo
```

### Upgrade path
- later register into registry center
- later add bus refresh
- later split environments and credentials handling

## 8. Config Client minimal template

### bootstrap.yml
```yml
spring:
  cloud:
    config:
      name: config-client
      uri: http://localhost:8888
      label: master
      profile: dev
```

### Controller
```java
@RestController
public class ConfigController {
    @Value("${name}")
    private String name;

    @GetMapping("/name")
    public String getName() {
        return name;
    }
}
```

### Better growth path
When config fields multiply, move from scattered `@Value` to a typed properties holder.

## 9. Typed config holder minimal template

```java
@Component
@ConfigurationProperties(prefix = "mysql")
public class MySQLProperties {
    private String host;
    private Integer port;
    private String username;
    private String password;
    // getters/setters
}
```

### Why this is the better evolution path
- cleaner than many scattered `@Value`
- easier to validate and test
- easier to expose/debug in config demos

## 10. Apollo client minimal template

### Startup class
```java
@EnableApolloConfig
@SpringBootApplication
public class OrderServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

### Config holder
```java
@Component
public class ConfigProperties {
    @Value("${name}")
    private String name;
    @Value("${mysql.host}")
    private String mysqlHost;
}
```

### Upgrade path
- later move to clearer grouping / validation
- later separate sensitive config display from public endpoints

## 11. Stream producer minimal template

```java
@EnableBinding(Source.class)
public class MessageProducer {
    private final MessageChannel output;

    public MessageProducer(Source source) {
        this.output = source.output();
    }
}
```

## 12. Stream consumer minimal template

```java
@EnableBinding(Sink.class)
public class MessageConsumer {
    @StreamListener(Sink.INPUT)
    public void receive(String message) {
        System.out.println(message);
    }
}
```

## Template selection advice

- want the smallest service-registry demo -> Eureka Server + Provider
- want service-to-service invocation -> add Feign Consumer
- want graceful evolution -> use FallbackFactory before overcomplicated resilience layers
- want unified entry -> add Gateway
- want externalized config -> add Config Server + Config Client
- want typed config growth -> add properties holder
- want centralized client-side config without building config server -> Apollo client path
- want async/event demo -> Stream producer + consumer

## Important boundary

These are teaching templates, not production blueprints. Use them to start small and upgrade intentionally.
