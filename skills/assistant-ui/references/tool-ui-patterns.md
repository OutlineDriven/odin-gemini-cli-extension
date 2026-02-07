# Tool UI Patterns

## Prefer modern registration API

Use `useAui` and `Tools({ toolkit })` as the default approach for tool registration and rendering.

```tsx
import { AssistantRuntimeProvider, Tools, type Toolkit, useAui } from "@assistant-ui/react";
import { z } from "zod";

const toolkit: Toolkit = {
  getWeather: {
    description: "Get weather by location",
    parameters: z.object({
      location: z.string(),
      unit: z.enum(["celsius", "fahrenheit"]).default("celsius"),
    }),
    execute: async ({ location, unit }) => fetchWeather(location, unit),
    render: ({ args, result, status }) => {
      if (status.type === "running") return <div>Loading {args.location}...</div>;
      return <div>{result?.temperature}</div>;
    },
  },
};

const aui = useAui({ tools: Tools({ toolkit }) });
```

## Use `makeAssistantToolUI` for UI-only binding

Use `makeAssistantToolUI` when tool execution is defined elsewhere (for example LangGraph or MCP backend) and frontend only needs a renderer.

```tsx
import { makeAssistantToolUI } from "@assistant-ui/react";

const WeatherToolUI = makeAssistantToolUI<
  { location: string; unit: "celsius" | "fahrenheit" },
  { temperature: number; description: string }
>({
  toolName: "getWeather",
  render: ({ args, result, status }) => {
    if (status.type === "running") return <div>Checking {args.location}...</div>;
    return <div>{result?.temperature}</div>;
  },
});
```

## Keep tool names consistent

- Keep `toolName` exactly aligned with backend tool name.
- Keep argument/result types aligned with backend schema.
- Return deterministic fallback UI when result shape is partially missing.

## Fallback rendering

Provide `ToolFallback` in assistant message components to avoid blank tool content when no explicit renderer exists.

## Guardrails

- Prefer toolkit registration for new code.
- Treat legacy APIs as migration paths only.
- Keep render functions pure and status-driven.

## Source pointers

- `docs/libaries/assistant-ui-docs.md`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/(docs)/guides/tools.mdx`
- `https://github.com/assistant-ui/assistant-ui/blob/main/apps/docs/content/docs/(docs)/guides/tool-ui.mdx`
