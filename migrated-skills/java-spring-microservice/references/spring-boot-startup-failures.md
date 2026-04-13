# Spring Boot Startup Failures

Use this guide when a Spring Boot application fails during startup or immediately after initialization.

## Common root causes

- property binding errors
- bean definition conflicts
- missing dependency or wrong starter set
- datasource or external service configuration failure
- profile mismatch
- classpath incompatibility

## Triage order

1. Find the first meaningful root-cause exception.
2. Confirm active profile and external config source.
3. Check recent dependency, config, or environment changes.
4. Verify bean creation path and conditional configuration.
5. Re-run after the smallest correction.

## Warning

Do not chase every stack frame. Follow the first root cause that explains startup termination.

## Quick triage shortcuts

- `Port already in use`: change port or stop the conflicting process
- `Failed to bind properties`: inspect config names, prefixes, and types
- `NoSuchBeanDefinition` or `UnsatisfiedDependency`: inspect scanning, annotations, constructor wiring, and conditional configuration
- datasource or Redis init failure: inspect URL, credentials, driver, and network reachability
- only external Tomcat fails: validate embedded-container startup first and confirm WAR deployment is truly required
