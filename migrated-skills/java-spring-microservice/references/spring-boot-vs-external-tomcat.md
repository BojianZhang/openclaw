# Spring Boot vs External Tomcat

Use this file when deciding between embedded Spring Boot runtime and external container deployment.

## Prefer embedded Spring Boot when

- deployment simplicity matters
- the service is owned and operated as an independent application
- consistent packaging and startup behavior are desired

## Consider external Tomcat when

- an existing platform standard requires it
- operational constraints are already built around shared container deployment

## Tradeoff reminder

External container deployment can introduce version, classpath, and lifecycle complexity. Do not choose it for nostalgia alone.

## Practical default

For most ordinary Spring Boot services, prefer the main method, embedded container, and `java -jar` packaging unless an external Tomcat requirement is explicit.
