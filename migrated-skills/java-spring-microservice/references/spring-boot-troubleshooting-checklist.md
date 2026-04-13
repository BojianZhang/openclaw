# Spring Boot Troubleshooting Checklist

Use this checklist when a Spring Boot service fails to start, behaves unexpectedly, or shows unstable runtime behavior.

## 1. Classify the failure

Typical categories:
- startup failure
- config binding issue
- bean wiring issue
- missing dependency or classpath mismatch
- environment-specific failure
- runtime exception after startup

## 2. Confirm evidence

Collect:
- startup logs
- stack trace root cause
- active profiles
- environment variables and external config sources
- dependency version changes
- recent deployment or config changes

## 3. Narrow the layer

Ask whether the issue sits in:
- configuration
- bean creation
- external dependency access
- web layer
- persistence layer
- thread pool or async path

## 4. Check common causes

- wrong property name or binding prefix
- missing bean or duplicate bean
- profile mismatch
- incompatible starter or version set
- invalid endpoint, datasource, or credential config
- port conflict
- environment variable or secret missing
- startup mode mismatch between main method, build tool, and external container

## 5. Practical triage reminders

- Read the first meaningful root cause instead of the outer `Application run failed` wrapper.
- If external Tomcat fails first, validate with embedded-container startup before chasing container-specific noise.

## 5. Fix smallest clear cause first

Prefer:
- config correction
- dependency alignment
- bean scope or qualifier correction
- startup sequence clarification

## 6. Recheck operational impact

After fixing startup, confirm health checks, logs, thread pools, downstream connectivity, and config visibility.
