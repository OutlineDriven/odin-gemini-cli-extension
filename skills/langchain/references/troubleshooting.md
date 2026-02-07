# LangChain Troubleshooting

## Common Symptoms and Actions

- Tool calls not firing:
Confirm tools are bound to the model/agent and schema names match prompt/tool registration.
- Infinite or long loops:
Add loop caps, tool-call limits, and explicit stop criteria.
- Invalid structured output:
Log raw response, validate schema, and tighten prompt contract.
- Middleware not applied:
Confirm middleware registration path and execution order.
- Non-deterministic behavior:
Set temperature to 0 for tests and isolate random/external dependencies.

## Debug Flow

1. Reproduce with smallest prompt/tool set.
2. Capture raw model output and tool call payload.
3. Verify schema and middleware order.
4. Add regression test reproducing the failure.
5. Patch and re-run integration test.

## Official Pointers

- https://docs.langchain.com/oss/python/langchain/how_to/debugging
- https://docs.langchain.com/langsmith/observability-quickstart
