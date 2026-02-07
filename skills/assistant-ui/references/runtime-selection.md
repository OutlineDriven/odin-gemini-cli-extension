# Runtime Selection

## Decision matrix

| Need | Recommended runtime |
| --- | --- |
| Chat endpoint with standard streaming and minimal thread state | `@assistant-ui/react-ai-sdk` |
| LangGraph thread lifecycle, interrupts, and graph state loading | `@assistant-ui/react-langgraph` |
| Full external ownership of message/thread state | External store runtime |
| Persistent threads plus auth/user continuity | Add `AssistantCloud` to AI SDK or LangGraph runtime |

## Core provider shape

Every integration must include:

- A runtime hook (for example `useChatRuntime` or `useLangGraphRuntime`)
- `AssistantRuntimeProvider` wrapping the chat UI
- `Thread` and optional `ThreadList` components wired to runtime context

## AI SDK path (high level)

- Install the AI SDK runtime integration package.
- Configure transport to your backend endpoint.
- Mount runtime provider at page or layout boundary.

Use this path for rapid integration when graph-specific state operations are not required.

## LangGraph path (high level)

- Install `@assistant-ui/react-langgraph`.
- Implement `stream`, `create`, and `load` functions.
- Use `initialize()` inside `stream` to resolve or create thread context.

Use this path for graph-managed runs, interrupts, and explicit thread state recovery.

## External store path (high level)

- Keep application message/thread state in your own store.
- Bind assistant-ui primitives to external state adapters.
- Use only when global app architecture requires centralized non-assistant state ownership.

## Runtime selection checklist

- Confirm whether thread IDs are backend-owned and must be loaded later.
- Confirm whether human interrupts must round-trip through runtime state.
- Confirm whether cloud persistence is required now or later.
- Confirm whether migration risk is acceptable for legacy APIs in current code.

## Source pointers

- `docs/libaries/assistant-ui-docs.md`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/runtimes/pick-a-runtime.mdx`
- `https://deepwiki.com/assistant-ui/assistant-ui`
