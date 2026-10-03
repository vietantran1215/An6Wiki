# GPT-6 Luna Runtime Parameters

Last verified: 2026-10-03 against official OpenAI API documentation.

## Why this matters

Do not assume sampling parameters that worked for older chat models are valid for reasoning models.

For GPT-6 Luna, parameter compatibility depends on the active reasoning effort. A common failure is to configure `temperature=0` while leaving Luna at its default reasoning effort. That combination is invalid because Luna defaults to `medium` reasoning effort, and sampling parameters such as `temperature` are unsupported whenever reasoning effort is not `none`.

## Core behavior

GPT-6 Luna supports these reasoning effort values:

- `none`
- `low`
- `medium`
- `high`
- `xhigh`
- `max`

The default is `medium`.

When reasoning effort is not `none`, remove:

- `temperature`
- `top_p`
- `top_logprobs`

For Chat Completions, also remove `logprobs`.

Therefore this configuration is unsafe for the default Luna behavior:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
    temperature=0,
)
```

Unless the integration explicitly sets `reasoning_effort="none"`, the model may reject the request.

## Safe configuration patterns

### Pattern 1 — keep reasoning enabled

Use Luna with its default reasoning behavior and omit unsupported sampling parameters:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
)
```

This is the preferred default when the application benefits from model reasoning and does not specifically require temperature-based sampling control.

### Pattern 2 — disable reasoning and use temperature

If the workload is simple and deterministic sampling control is more important than model reasoning:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
    reasoning_effort="none",
    temperature=0,
)
```

This pattern is valid because Luna supports `none` reasoning effort.

## Tool-calling consequence

For GPT-6 Luna with Chat Completions, function calling is supported only when `reasoning_effort="none"`.

If an application needs reasoning plus tools, prefer the Responses API.

This is an architectural decision, not a cosmetic parameter choice:

```text
Need reasoning + tools
        ↓
Prefer Responses API

Need Chat Completions + function calling
        ↓
Use reasoning_effort="none"
```

## Failure mode

Typical mistake:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
    temperature=0,
)
```

Expected developer assumption:

```text
temperature=0
→ more deterministic
→ safer default
```

Actual issue:

```text
GPT-6 Luna
→ default reasoning_effort=medium
→ temperature unsupported
→ request can fail
```

The lesson is broader than Luna:

> Never copy generation parameters across model families without checking current parameter compatibility.

## Production guidance

Treat model configuration as versioned runtime policy.

At minimum, keep these decisions explicit:

- model name
- API family: Responses vs Chat Completions
- reasoning effort
- reasoning mode where applicable
- tool/function-calling requirements
- sampling parameters
- streaming requirements
- fallback behavior

Do not hide these choices in scattered defaults.

A production configuration layer should validate incompatible combinations before requests reach the provider.

Example validation logic:

```python
def validate_luna_config(
    reasoning_effort: str,
    temperature: float | None,
) -> None:
    if reasoning_effort != "none" and temperature is not None:
        raise ValueError(
            "GPT-6 Luna does not support temperature "
            "when reasoning_effort is not 'none'."
        )
```

## Decision rules

Use this quick rule set:

1. If using GPT-6 Luna with default reasoning, omit `temperature`.
2. If `reasoning_effort != "none"`, omit sampling parameters that OpenAI marks unsupported.
3. If using Chat Completions function calling with Luna, set `reasoning_effort="none"`.
4. If reasoning and tools are both required, prefer Responses API.
5. Re-check official model documentation when changing model families or SDK versions.

## Sources

- OpenAI GPT-6 Luna model documentation: https://developers.openai.com/api/docs/models/gpt-6-luna
- OpenAI GPT-6 migration and parameter compatibility guide: https://developers.openai.com/api/docs/guides/latest-model
- OpenAI reasoning guide: https://developers.openai.com/api/docs/guides/reasoning
