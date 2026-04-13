# Global Exception Handler Template

Use this template when standardizing exception-to-response behavior in Spring Boot services.

## Practical rules

- Expose stable error contracts.
- Do not leak internal stack details to clients.
- Preserve enough logging context for diagnosis.
- Distinguish domain errors from unexpected failures.
