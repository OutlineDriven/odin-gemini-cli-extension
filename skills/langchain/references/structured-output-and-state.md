# Structured Output and State

## Use This File For

- Enforcing typed output contracts.
- Managing short-term state safely.

## Structured Output Rules

- Use schema-driven output (`pydantic`, `zod`, or equivalent).
- Fail fast on validation errors; do not silently coerce malformed payloads.
- Keep a clear boundary between model text and validated object payloads.

## State Rules

- Keep state minimal and intentional.
- Store only fields that are required for later decisions.
- Use deterministic merge/update strategy for repeated turns.

## Validation Checklist

- Schema checks run in tests and at runtime boundary.
- Invalid payload path has explicit fallback behavior.
- State mutation rules are documented in code comments or type definitions.

## Official Pointers

- https://docs.langchain.com/oss/python/langchain/structured-output
- https://docs.langchain.com/oss/javascript/langchain/structured-output
