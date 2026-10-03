# Prompting, Context & Structured Output

## Prompt roles

A production prompt often combines:

- system policy;
- task instruction;
- approved context;
- user input;
- output constraints.

## Prompt builder is not a security boundary

Instructions such as "do not reveal secrets" are useful, but they cannot replace:

- authorization;
- permission-aware retrieval;
- data minimization;
- output validation.

## Context engineering

Context engineering asks:

> What information should be present for this model call, in what representation, and with what priority?

Context may include:

- retrieved evidence;
- conversation state;
- tool results;
- user profile;
- business rules;
- intermediate plans.

## Structured output

Prefer structured output when downstream software depends on model output.

```python
from pydantic import BaseModel, Field

class RiskAssessment(BaseModel):
    risk_level: str
    reasons: list[str]
    requires_human: bool = Field(
        description="Whether a human must approve the next action"
    )
```

Bind the schema through the model SDK when supported, then validate before use.

## Prompt versioning

Treat important prompts as versioned application artifacts.

Record:

- prompt version;
- model version;
- evaluation dataset;
- release date;
- regression result.

## Failure modes

- ambiguous instructions;
- contradictory context;
- excessive context;
- missing source boundaries;
- prompt injection;
- unstable free-form output.

## Rule

A good prompt reduces ambiguity. A good application does not depend on the prompt for security or correctness guarantees that deterministic code can enforce.
