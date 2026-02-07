# Cloud Persistence

## Use cloud only when needed

Enable Assistant Cloud when thread persistence, history continuity, or authenticated resume behavior is required.

## Required environment variables

```bash
NEXT_PUBLIC_ASSISTANT_BASE_URL=https://proj-[YOUR-ID].assistant-api.com
ASSISTANT_API_KEY=your-api-key-here
```

## Basic integration shape

Create `AssistantCloud`, then pass it into runtime options.

```tsx
import { AssistantCloud, AssistantRuntimeProvider } from "@assistant-ui/react";
import { useLangGraphRuntime } from "@assistant-ui/react-langgraph";

const cloud = new AssistantCloud({
  baseUrl: process.env.NEXT_PUBLIC_ASSISTANT_BASE_URL!,
  anonymous: true,
});

const runtime = useLangGraphRuntime({
  cloud,
  stream: async (messages, { initialize }) => {
    const { externalId } = await initialize();
    return sendMessage({ threadId: externalId!, messages });
  },
  create: async () => ({ externalId: (await createThread()).thread_id }),
  load: async (externalId) => ({ messages: (await getThreadState(externalId)).values.messages }),
});
```

## Authenticated mode

Use `authToken` callback when cloud sessions must map to authenticated users.

```tsx
new AssistantCloud({
  baseUrl: process.env.NEXT_PUBLIC_ASSISTANT_BASE_URL!,
  authToken: async () => getToken({ template: "assistant-ui" }),
});
```

## Guardrails

- Keep API key on server-side boundaries only.
- Avoid mixing anonymous and authenticated modes in the same user journey.
- Validate cloud base URL before runtime creation.

## Source pointers

- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/cloud/persistence/langgraph.mdx`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/cloud/overview.mdx`
