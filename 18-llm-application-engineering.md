# LLM Application Engineering

## A production LLM application is a system, not a prompt

A common architecture is:

```text
Input
 → validation / policy
 → context / retrieval
 → prompt construction
 → model gateway
 → structured output / tool use
 → output validation
 → telemetry / evaluation
```

## Core capabilities

- structured outputs;
- tool calling;
- streaming;
- prompt caching;
- batch processing;
- model routing;
- guardrails;
- context engineering;
- token/cost controls.

## Structured output

Prefer schema-constrained output whenever downstream code depends on the result.

```python
from pydantic import BaseModel

class TicketClassification(BaseModel):
    category: str
    priority: int
    requires_human: bool

# Bind this schema to the SDK's structured-output feature.
# Validate the result before using it in business logic.
```

## Prompt caching

Useful when a large stable prefix is reused:

- system instructions;
- long reference context;
- stable tool definitions;
- shared policy.

## Batch processing

Good for workloads that do not require immediate response:

- embeddings;
- large evaluation runs;
- classification;
- extraction;
- offline dataset processing.

## Model routing

Routing may consider:

- task complexity;
- latency;
- cost;
- privacy;
- modality;
- context length;
- reliability.

## Rule

The model may propose. Deterministic code validates before a consequential action is executed.
