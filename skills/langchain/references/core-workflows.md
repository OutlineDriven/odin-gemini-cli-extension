# LangChain Core Workflows

## Use This File For

- Selecting between LCEL chain and agent loop.
- Bootstrapping new LangChain logic in Python or TypeScript.

## Decision Rules

- Use LCEL chain when there are no tool calls and execution is linear.
- Use `create_agent` when the model must call tools iteratively.
- Use explicit state payload objects when business state must persist between turns.

## Baseline Build Sequence

1. Define input and output contracts.
2. Define prompt template and model config.
3. Add tools only after base model invocation is deterministic.
4. Add middleware for policy/guardrails.
5. Add tracing and timeouts.
6. Add tests.

## Minimal Python Skeleton

```python
from langchain.agents import create_agent
from langchain_openai import ChatOpenAI

model = ChatOpenAI(model="gpt-4o-mini", temperature=0)
agent = create_agent(model=model, tools=[])
result = agent.invoke({"messages": [{"role": "user", "content": "ping"}]})
```

## Minimal TypeScript Skeleton

```ts
import { createAgent } from "langchain";
import { ChatOpenAI } from "@langchain/openai";

const model = new ChatOpenAI({ model: "gpt-4o-mini", temperature: 0 });
const agent = createAgent({ model, tools: [] });
const result = await agent.invoke({ messages: [{ role: "user", content: "ping" }] });
```

## Official Pointers

- https://docs.langchain.com/oss/python/langchain/overview
- https://docs.langchain.com/oss/javascript/langchain/overview
- https://python.langchain.com/docs/how_to/#agents
