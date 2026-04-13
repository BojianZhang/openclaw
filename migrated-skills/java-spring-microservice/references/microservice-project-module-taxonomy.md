# Microservice Project Module Taxonomy

Use this file when the user needs a reusable way to classify modules inside a multi-module Java microservice project.

This reference is inspired by the 乐Z家 project layout.

## Why taxonomy matters

When a project grows to many Maven modules, the first problem is often not code syntax but module meaning.
A clear taxonomy helps answer:
- which modules are platform/infrastructure?
- which are shared support modules?
- which are business capabilities?
- which are integration/data adapters?
- which are workflow/messaging nodes?

## Suggested taxonomy

### 1. Platform edge and discovery modules
Purpose:
- give the system an entry point and service-addressing baseline

Examples:
- registry center module
- gateway module

In the sample:
- `lzj-eureka`
- `lzj-gateway`

### 2. Shared support modules
Purpose:
- hold shared DTOs, common utilities, constants, helper logic, and cross-service support code

Examples:
- common utils
- shared pojos
- shared visual/banner/startup support

In the sample:
- `lzj-commons`
- `lzj-pojo`
- `lzj-banner`

### 3. Data/integration capability modules
Purpose:
- encapsulate access or conventions for a data technology or external infrastructure

Examples:
- MongoDB support module
- Redis support module
- RabbitMQ support module

In the sample:
- `lzj-mongodb`
- `lzj-redis`
- `lzj-rabbitmq`

### 4. Business capability modules
Purpose:
- own a user-visible or business-visible bounded capability

Examples in the sample:
- `lzj-hot-product`
- `lzj-recommendation`
- `lzj-product-details`
- `lzj-comment`
- `lzj-buytime`
- `lzj-login`
- `lzj-sendyzm`
- `lzj-order`

### 5. Message workflow modules
Purpose:
- isolate producer/consumer workflow around asynchronous business actions

Examples in the sample:
- `lzj-buyaction-message-producer`
- `lzj-buyaction-message-consumer`

## Reusable naming intuition

A practical naming model is:
- `xxx-gateway`, `xxx-eureka` -> platform role
- `xxx-commons`, `xxx-pojo` -> shared base role
- `xxx-redis`, `xxx-mongodb`, `xxx-rabbitmq` -> technology support role
- `xxx-order`, `xxx-login`, `xxx-comment` -> business capability role
- `xxx-*-producer`, `xxx-*-consumer` -> message workflow role

## Common mistakes this taxonomy prevents

### Mistake 1: putting business code into shared modules
Shared modules should not become a dumping ground for business logic.

### Mistake 2: naming technical support modules as if they were business services
A Redis helper module and an order service are not the same kind of module.

### Mistake 3: creating one gigantic “service-common” that owns everything
Split shared support from business capability.

### Mistake 4: introducing producer/consumer modules before the async business need exists
Workflow modules should solve a visible asynchronous problem.

## How to answer with this taxonomy

A strong answer usually does this:
1. classify modules into platform / shared / data / business / message
2. explain which category should grow slowly and which should grow with business features
3. identify any category currently overloaded or ambiguous
4. recommend the next module type only when the project actually needs it

## Source notes

Distilled from the user's 乐Z家 multi-module project structure across versions.
