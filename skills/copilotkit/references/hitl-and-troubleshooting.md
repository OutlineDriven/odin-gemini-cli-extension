# HITL and Troubleshooting

## Use This File For

- Interrupt workflows and production issue triage.

## HITL Rules

- Define interrupt points in backend graph with explicit intent.
- Map each interrupt type to a specific frontend handler.
- Resume with typed payloads only.

## Common Issues

- "Agent not found":
Verify agent name alignment across runtime registration and frontend hook usage.
- "Endpoint not found":
Verify runtime URL, endpoint type, and backend health.
- Tool calls not streamed:
Verify runtime/tool configuration path and async invocation behavior.
- Streamed messages disappear:
Verify message persistence strategy and filtering settings.

## Debug Sequence

1. Verify endpoint reachability.
2. Verify provider and hook scopes.
3. Verify interrupt/action payload schema.
4. Reproduce with smallest flow and add regression test.

## Official Pointers

- https://docs.copilotkit.ai/coagents/human-in-the-loop/interrupt-flow
- https://docs.copilotkit.ai/coagents/troubleshooting/common-issues
