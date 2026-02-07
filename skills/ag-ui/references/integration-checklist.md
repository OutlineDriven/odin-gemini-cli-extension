# AG-UI Integration Checklist

## Pre-Implementation

- Select integration mode (`HttpAgent`, custom agent, or bridge).
- Confirm event types required by the target client.
- Confirm tool schema and execution ownership (frontend vs backend).

## Implementation

- Implement lifecycle events first.
- Implement message streaming next.
- Implement tool lifecycle and result propagation.
- Implement state sync strategy.

## Verification

- Validate event ordering with sample traces.
- Verify state reconstruction from initial load and resumed session.
- Verify tool call roundtrip including failure branch.
- Verify interrupt/cancel behavior if applicable.

## Release Readiness

- Document supported event subset.
- Add integration tests for normal and failure runs.
- Add observability for run and tool timings.
