# Hooks and Actions

## Use This File For

- Selecting and wiring CopilotKit hooks.

## Hook Roles

- `useCoAgent`:
Bind agent shared state to frontend logic.
- `useCopilotAction`:
Expose frontend actions/tools callable by agent.
- `useLangGraphInterrupt`:
Handle LangGraph interrupt flows in frontend.

## Action Design Rules

- Define explicit argument schema.
- Keep side effects bounded and reversible where possible.
- Return structured status/error payloads.

## Validation Checklist

- Actions appear to the agent when expected.
- Action handlers run only in correct UI scope.
- Errors return user-safe messages and machine-usable status.

## Official Pointers

- https://docs.copilotkit.ai/reference/hooks/useCopilotAction
- https://docs.copilotkit.ai/reference/hooks/useCoAgent
- https://docs.copilotkit.ai/reference/hooks/useLangGraphInterrupt
