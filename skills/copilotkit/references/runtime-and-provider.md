# Runtime and Provider

## Use This File For

- Bootstrapping CopilotKit runtime and provider wiring.

## Runtime Decision Rules

- Use LangGraph endpoint when backend graph execution and thread management are already in LangGraph.
- Use remote backend runtime when actions are hosted in a custom backend service.

## Provider Checklist

- `<CopilotKit>` wraps all components that use Copilot hooks.
- Runtime URL and public key/env vars are configured for the target environment.
- Endpoint type matches runtime integration mode.

## Validation Checklist

- Chat initializes without endpoint errors.
- First message reaches backend runtime.
- Streaming responses render in UI.

## Official Pointers

- https://docs.copilotkit.ai/quickstart
- https://docs.copilotkit.ai/coagents/quickstart/langgraph
