# AG-UI Event Contracts

## Use This File For

- Required event types and ordering constraints.

## Core Lifecycle Contract

- Emit `RUN_STARTED` before any stream content.
- Emit exactly one terminal run event: `RUN_FINISHED` or `RUN_ERROR`.
- Keep `threadId`/`runId` consistent across all events in a run.

## Text Stream Contract

- `TEXT_MESSAGE_START` -> `TEXT_MESSAGE_CONTENT` (one or more) -> `TEXT_MESSAGE_END`.
- Preserve stable `messageId` across message events.

## Tool Call Contract

- `TOOL_CALL_START` -> `TOOL_CALL_ARGS` -> `TOOL_CALL_END` -> `TOOL_CALL_RESULT`.
- Emit complete args payload before result handling.

## State Contract

- Use `STATE_SNAPSHOT` for full baseline.
- Use `STATE_DELTA` for incremental updates only when client can safely apply patches.

## Official Pointers

- https://docs.ag-ui.com/concepts/events
- https://docs.ag-ui.com/concepts/state
