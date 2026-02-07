# CoAgents and Shared State

## Use This File For

- Designing shared-state contracts and rendering behavior.

## Shared-State Rules

- Separate input, output, and internal state fields.
- Keep frontend-editable fields explicit.
- Keep state transitions deterministic and testable.

## Rendering Rules

- Render critical state both in-chat and out-of-chat when UX requires continuity.
- Use state render hooks/components for stable serialization boundaries.

## Validation Checklist

- State updates propagate to UI in real time.
- Rehydration works after page reload/resume.
- Agent can observe intended frontend state changes.

## Official Pointers

- https://docs.copilotkit.ai/coagents/shared-state
- https://docs.copilotkit.ai/coagents/generative-ui/agentic
