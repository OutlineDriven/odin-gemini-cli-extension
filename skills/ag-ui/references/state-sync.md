# State Synchronization

## Use This File For

- Choosing snapshot/delta synchronization strategy.

## Strategy Matrix

- Snapshot-only:
Use for simple clients and low event volume.
- Delta-only:
Use when payload size must be minimized and patch handling is robust.
- Hybrid:
Use periodic snapshots plus deltas for long-lived sessions.

## Safety Rules

- Version state payload shape.
- Apply deltas idempotently where possible.
- Recover from drift by forcing a fresh snapshot.

## Validation Checklist

- Client can reconstruct state after reconnect.
- Delta failures trigger snapshot fallback.
- State updates do not reorder causal events.

## Official Pointers

- https://docs.ag-ui.com/concepts/state
