# Troubleshooting

## CLI and setup issues

### Dependency conflicts during `init` or `add`

- Retry with a clean lockfile install.
- If package peer conflicts block setup, retry with package-manager compatibility flags.
- Use explicit overwrite only when regeneration is intended.

### Components added but imports fail

- Verify alias/path config in `components.json` or `assistant-ui.json`.
- Confirm generated component paths match app import conventions.

## Runtime issues

### "Thread not found" in LangGraph flow

- Confirm `create` returns valid `externalId`.
- Confirm `initialize()` is called in `stream`.
- Confirm backend thread lookup and `load(externalId)` are aligned.

### Message history not restored

- Confirm `load` returns the message array from the backend state shape.
- Confirm runtime provider wraps Thread/ThreadList tree at the correct boundary.

### Interrupt UI missing

- Confirm `load` returns `interrupts` when backend exposes them.
- Confirm frontend interrupt handling components are mounted.

## Tool UI issues

### Tool component never renders

- Confirm frontend `toolName` matches backend tool identifier exactly.
- Confirm tool payload schema matches argument typing.
- Add `ToolFallback` to validate that tool events are arriving.

### Tool result parsing failures

- Guard against partial result shapes.
- Render by `status.type` first, then optional result fields.

## Upgrade and migration issues

- Run `update --dry` before changing packages.
- Run `upgrade` before targeted codemods.
- Re-run app checks after codemods and tool render changes.

## Debug aids

- Use assistant-ui devtools package to inspect runtime state and events.
- Use isolated reproduction with a single Thread view before debugging app-wide composition.

## Source pointers

- `docs/libaries/assistant-ui-docs.md`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/devtools.mdx`
