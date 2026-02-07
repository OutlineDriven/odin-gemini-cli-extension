# HITL Interrupts

## Use This File For

- Designing human approval and resume flows.

## Interrupt Design Rules

- Interrupt only at semantically meaningful checkpoints.
- Include enough context for a human decision without dumping full internal state.
- Normalize resume payloads into typed action categories.

## Resume Contract

- Define accepted actions (for example: approve, retry, skip).
- Map each action to a deterministic next edge.
- Preserve audit fields for user decisions and feedback.

## Validation Checklist

- Approve path advances correctly.
- Retry path re-enters intended node.
- Skip path terminates or routes next item safely.
- Invalid resume payload is rejected with explicit error.

## Official Pointers

- https://langchain-ai.github.io/langgraph/how-tos/human_in_the_loop/add-human-in-the-loop/
