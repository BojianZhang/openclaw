# Microservice Project Module Skeletons

Use this file when the user wants reusable project-level module skeletons for a Java microservice project, rather than only single-service templates.

This reference is inspired by the 乐Z家 project layout and focuses on module categories that can be introduced gradually in a real project.

## Why these skeletons matter

Single-service templates are useful at the component level.
Project module skeletons help when the user needs to shape the whole repo structure:
- parent aggregator
- platform modules
- shared support modules
- data/integration modules
- business capability modules
- message workflow modules

## 1. Parent aggregator skeleton

### Role
Top-level Maven aggregator controlling module registration, version alignment, and common plugin/dependency management.

### Minimal shape
```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>demo-microservices</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>pom</packaging>

  <modules>
    <module>demo-eureka</module>
    <module>demo-gateway</module>
    <module>demo-commons</module>
    <module>demo-pojo</module>
    <module>demo-product</module>
  </modules>

  <properties>
    <spring-boot.version>2.3.0.RELEASE</spring-boot.version>
    <spring-cloud.version>Hoxton.SR3</spring-cloud.version>
  </properties>
</project>
```

### Upgrade path
- add dependencyManagement BOMs
- add pluginManagement
- later split environment/build conventions

## 2. Platform module skeleton

### Includes
- registry module
- gateway module

### Role
Provide service discovery baseline and unified external entry.

### Suggested names
- `xxx-eureka`
- `xxx-gateway`

### Keep inside platform modules
- discovery registration
- route config
- boundary filters
- traffic governance later

### Do not mix in
- core business rules
- shared utility dumping

## 3. Shared support module skeleton

### Includes
- `xxx-commons`
- `xxx-pojo`
- optional startup/banner or small support module

### Role
Carry shared DTOs, constants, utility code, response wrappers, and cross-service helper pieces.

### Good contents
- DTO/VO/POJO definitions
- response/result wrapper
- shared enums/constants
- basic utility classes

### Avoid
- business service logic
- data-source-specific heavy implementation that belongs in integration modules

## 4. Data / integration module skeleton

### Includes
- `xxx-mongodb`
- `xxx-redis`
- `xxx-rabbitmq`
- similar technology support modules

### Role
Encapsulate technology-specific support that multiple business services may reuse.

### Good contents
- configuration classes
- client factories/templates
- repository support helpers
- technology-specific constants / utility adapters

### Avoid
- turning the integration module into a business service
- leaking unrelated domain behavior into shared integration code

## 5. Business capability module skeleton

### Suggested examples
- `xxx-hot-product`
- `xxx-recommendation`
- `xxx-product-details`
- `xxx-comment`
- `xxx-login`
- `xxx-order`

### Role
Own a user-visible or domain-visible bounded capability.

### Minimal internal shape
```text
src/main/java/
  controller/
  service/
  mapper or repository/
  config/ (only if local to this capability)
```

### Dependency rule of thumb
A business capability module may depend on:
- shared support modules
- one or more data/integration modules
- discovery/client modules as needed

But it should not become a mega-module that absorbs neighboring domains casually.

## 6. Message workflow module skeleton

### Suggested examples
- `xxx-buyaction-message-producer`
- `xxx-buyaction-message-consumer`

### Role
Isolate asynchronous workflow behavior around a concrete business action.

### Why separate these modules
This makes it explicit that the project has moved from synchronous service composition into asynchronous workflow design.

### Minimal producer shape
- controller or service entry
- message publishing service
- MQ support dependency

### Minimal consumer shape
- listener/consumer handler
- downstream business integration
- idempotency/retry considerations later

## 7. Frontend shell pairing skeleton

### Suggested placement
Keep frontend as a separate sibling project rather than embedding it into the Java multi-module backend.

### Role
- page flow
- state management
- UI interactions
- client-side request orchestration

### Boundary guidance
Frontend should primarily face the gateway, not memorize every internal service address.

## Recommended initial repo shape

For a gradual self-built project, a strong starting layout is:
```text
demo-root/
  pom.xml
  demo-eureka/
  demo-gateway/
  demo-commons/
  demo-pojo/
  demo-product/
  demo-order/
  frontend-app/
```

Then grow into:
```text
demo-root/
  demo-eureka/
  demo-gateway/
  demo-commons/
  demo-pojo/
  demo-mongodb/
  demo-redis/
  demo-product/
  demo-recommendation/
  demo-login/
  demo-order/
  demo-rabbitmq/
  demo-order-message-producer/
  demo-order-message-consumer/
  frontend-app/
```

## How to use this reference

Use this when the user asks:
- how should my whole multi-module repo be shaped?
- what module categories should I create first?
- should Redis/RabbitMQ be business services or support modules?
- when should I split out producer/consumer modules?

## Source notes

Distilled from the user's 乐Z家 multi-version project structure and generalized into reusable project-level skeleton patterns.
