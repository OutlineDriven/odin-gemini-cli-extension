# Tooling and Middleware

## Use This File For

- Tool schema design.
- Middleware ordering and policy enforcement.

## Tool Contract Rules

- Define schemas that match actual implementation fields exactly.
- Keep tool outputs machine-parseable for downstream logic.
- Treat side-effect tools as privileged operations with explicit checks.

## Middleware Ordering

1. Authentication and authorization checks.
2. Input validation and normalization.
3. Tool filtering/permission middleware.
4. Logging/metrics middleware.
5. Output redaction middleware.

## Quality Checklist

- Tool arguments validate before execution.
- Tool errors are surfaced to the model in a controlled format.
- Middleware cannot be bypassed by alternate code paths.

## Official Pointers

- https://docs.langchain.com/oss/python/langchain/tools
- https://docs.langchain.com/oss/python/langchain/middleware
- https://docs.langchain.com/oss/javascript/langchain/tools
