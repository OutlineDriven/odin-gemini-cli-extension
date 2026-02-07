# LangGraph Runtime

## Install packages

```bash
npm install @assistant-ui/react @assistant-ui/react-langgraph
```

## Implement provider with thread lifecycle

Use `useLangGraphRuntime` and define all lifecycle functions:

- `stream`: send messages to backend, call `initialize()` first
- `create`: create new backend thread and return `externalId`
- `load`: fetch existing state by `externalId`

```tsx
import { AssistantRuntimeProvider } from "@assistant-ui/react";
import { useLangGraphRuntime } from "@assistant-ui/react-langgraph";

const runtime = useLangGraphRuntime({
  stream: async (messages, { initialize, config }) => {
    const { externalId } = await initialize();
    if (!externalId) throw new Error("Thread not found");
    return sendMessage({ threadId: externalId, messages, config });
  },
  create: async () => {
    const { thread_id } = await createThread();
    return { externalId: thread_id };
  },
  load: async (externalId) => {
    const state = await getThreadState(externalId);
    return {
      messages: state.values.messages,
      interrupts: state.tasks?.[0]?.interrupts,
    };
  },
});

return (
  <AssistantRuntimeProvider runtime={runtime}>
    <Thread />
  </AssistantRuntimeProvider>
);
```

## Thread ID rules

- Treat `externalId` as your backend thread identifier.
- Always call `initialize()` in `stream` before sending.
- Keep `load` implementation resilient to missing interrupts/tasks.

## Common failure modes

- "Thread not found": `create`/`load` mismatch or missing backend record.
- Empty history after reload: `load` returns wrong message field.
- Lost HITL UI: interrupts not returned from backend state in `load`.

## Optional cloud composition

Add `cloud` to runtime options when persistence and cloud-managed thread metadata are required.

## Source pointers

- `docs/libaries/assistant-ui-docs.md`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/runtimes/langgraph/index.mdx`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/cloud/persistence/langgraph.mdx`
