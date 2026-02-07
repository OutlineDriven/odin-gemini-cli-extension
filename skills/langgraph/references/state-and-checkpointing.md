# State and Checkpointing

## Use This File For

- Checkpointer setup.
- Thread identity and resumability.

## State Contract Rules

- Define state shape as a typed contract.
- Keep mutable fields minimal and intentionally merged.
- Avoid storing duplicated derived values.

## Checkpoint Rules

- Treat checkpoints as super-step snapshots.
- Keep `thread_id` stable across resumed runs.
- Ensure state is serializable and backward compatible.

## Reliability Checklist

- Recovery from mid-run interruption is deterministic.
- Re-running same thread from same checkpoint yields equivalent routing.
- Large state fields are pruned or summarized.

## Official Pointers

- https://langchain-ai.github.io/langgraph/concepts/persistence/#checkpoints
- https://langchain-ai.github.io/langgraph/how-tos/persistence/
