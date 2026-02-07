# Graph Design Patterns

## Use This File For

- Selecting graph topology and routing model.

## Common Topologies

- Linear pipeline:
Use for fixed multi-step transforms.
- Validation loop:
Use for generation + review + retry cycles.
- Router/supervisor:
Use for selecting specialized subflows based on task class.
- Fan-out/fan-in:
Use when independent branches produce mergeable outputs.

## Node Design Rules

- One responsibility per node.
- Inputs/outputs map directly to state keys.
- No hidden side effects in routing nodes.

## Routing Rules

- Encode terminal states explicitly.
- Encode retry caps in state and guard edge predicates.
- Route by typed reason, not free-form text.

## Official Pointers

- https://github.com/langchain-ai/langgraph
- https://langchain-ai.github.io/langgraph/tutorials/
