# LangGraph Debugging Playbook

## Common Symptoms and Actions

- Wrong next node:
Inspect router predicate inputs and state mutation order.
- Non-reproducible runs:
Verify thread/checkpoint identity and external non-determinism.
- Interrupt/resume failures:
Verify resume payload schema and parser mapping.
- Stuck retry loop:
Check retry counter increment and terminal edge condition.

## Debug Sequence

1. Reproduce on minimal graph path.
2. Log state before and after each critical node.
3. Verify edge predicates with captured state snapshot.
4. Replay from checkpoint where divergence begins.
5. Add regression test for the failing path.

## Official Pointers

- https://langchain-ai.github.io/langgraph/tutorials/get-started/
- https://langchain-ai.github.io/langgraph/concepts/
