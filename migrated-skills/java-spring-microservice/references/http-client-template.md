# HTTP Client Template

Use this template when defining outbound HTTP integration structure.

## Practical rules

- Make timeout, retry, and fallback behavior explicit.
- Avoid hidden retry amplification.
- Keep client contracts narrow and observable.
- Separate transport concerns from business decision logic.
