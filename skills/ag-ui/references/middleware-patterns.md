# Middleware Patterns

## Use This File For

- Event filtering, logging, auth, and transformation boundaries.

## Recommended Middleware Order

1. Authentication and authorization.
2. Event validation/normalization.
3. Tool-call filtering or policy checks.
4. Logging and metrics.

## Guardrails

- Do not remove required lifecycle events.
- Do not rename protocol fields in middleware.
- Keep middleware side effects observable and bounded.

## Debug Checklist

- Validate event stream before and after middleware chain.
- Confirm middleware does not break terminal event emission.
- Confirm blocked tool calls return explicit policy feedback.

## Official Pointers

- https://docs.ag-ui.com/concepts/middleware
