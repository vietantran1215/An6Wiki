# Model Runtime Parameter Compatibility

Last reviewed: 2026-10-03.

## Why this matters

LLM runtime parameters are not universally portable across model families, API families, providers, or reasoning modes.

A configuration that works for one model may be rejected by another even when both expose a superficially similar chat interface.

Common examples include:

- `temperature`
- `top_p`
- `top_logprobs`
- `logprobs`
- reasoning effort or reasoning budget
- tool/function-calling support
- structured output support
- streaming behavior

The correct rule is:

> Treat model configuration as a compatibility matrix, not as a bag of generic defaults.

## Compatibility dimensions

Before configuring a model, identify these dimensions:

1. **Model family** — different families may expose different runtime controls.
2. **API family** — Responses, Chat Completions, provider-specific APIs, and compatibility APIs may expose different capabilities.
3. **Reasoning mode** — reasoning models may disable or restrict traditional sampling controls.
4. **Tool usage** — some model/API combinations restrict function calling under particular reasoning modes.
5. **Structured output mode** — schema-constrained output can change which features are available.
6. **Streaming mode** — token streaming, reasoning streaming, and tool-progress streaming can have different rules.
7. **Provider implementation** — protocol compatibility does not imply identical semantics.

## Do not blindly reuse sampling defaults

A common historical pattern is:

```python
model = ChatOpenAI(
    model=MODEL_NAME,
    temperature=0,
)
```

The intent is usually deterministic output.

That is no longer a safe universal default.

For some reasoning models, `temperature` is unsupported unless reasoning is disabled or moved to a compatible mode.

Think this way:

```text
Old assumption

temperature=0
→ deterministic
→ safe everywhere

Better model

model family
+ API family
+ reasoning mode
+ tool requirements
→ supported parameter set
→ runtime configuration
```

## Reasoning models change the configuration model

Reasoning-capable models often introduce controls such as:

```text
reasoning_effort
reasoning mode
reasoning budget
reasoning summary
```

These controls may interact with traditional sampling parameters.

A production configuration layer should validate combinations rather than forwarding arbitrary values directly to the provider.

Example:

```python
def validate_runtime_config(
    *,
    reasoning_enabled: bool,
    temperature: float | None,
    temperature_supported_with_reasoning: bool,
) -> None:
    if (
        reasoning_enabled
        and temperature is not None
        and not temperature_supported_with_reasoning
    ):
        raise ValueError(
            "temperature is not supported for this model "
            "while reasoning is enabled"
        )
```

## Tool-calling compatibility

Tool support is not independent from runtime mode.

A provider can support all of these individually:

- reasoning
- tool calling
- chat completions

while not supporting a particular combination of them.

Therefore do not ask only:

```text
Does this model support tools?
```

Ask:

```text
Does this model support tools
with this API family
and this reasoning mode?
```

This distinction is critical in agent systems.

## API-family decisions

Do not assume API families are interchangeable.

A useful decision sequence is:

```text
required capability
      ↓
reasoning?
tools?
structured output?
streaming?
      ↓
select API family
      ↓
select compatible model
      ↓
validate runtime parameters
```

Avoid doing it backwards:

```text
pick familiar SDK defaults
↓
pick a model
↓
hope the parameters work
```

## OpenAI-compatible gateways

An OpenAI-compatible endpoint normally means some level of protocol compatibility, not full behavioral compatibility.

A gateway may differ in:

- supported model names
- reasoning controls
- sampling parameters
- streaming chunk behavior
- structured output
- tool calling
- error format
- token accounting

Therefore:

```python
ChatOpenAI(
    base_url=CUSTOM_GATEWAY,
    model=MODEL_NAME,
)
```

does not guarantee that every parameter accepted by OpenAI is accepted by that gateway.

The gateway's own compatibility matrix remains authoritative.

## Current case study: GPT-6 Luna

GPT-6 Luna is a concrete example of why this compatibility problem matters.

At the time of review:

- the default reasoning effort is `medium`;
- when reasoning effort is not `none`, sampling parameters such as `temperature`, `top_p`, and `top_logprobs` are unsupported;
- Chat Completions has additional restrictions around `logprobs`;
- Chat Completions function calling requires `reasoning_effort="none"`;
- when reasoning and tools are both required, the Responses API is the preferred API family.

Therefore this is not a safe generic default for that model:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
    temperature=0,
)
```

A safer reasoning-enabled configuration is:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
)
```

If reasoning is explicitly disabled:

```python
model = ChatOpenAI(
    model="gpt-6-luna",
    reasoning_effort="none",
    temperature=0,
)
```

The important lesson is model-agnostic:

> Model capabilities must be checked as combinations, not as isolated feature flags.

## Production configuration pattern

Centralize model runtime configuration.

Do not scatter parameters across application code.

A runtime policy should make at least these decisions explicit:

```text
provider
model
API family
reasoning mode / effort
sampling parameters
tool requirements
structured output mode
streaming mode
fallback policy
```

Then validate the combination before constructing or invoking the SDK client.

Example conceptual configuration:

```python
MODEL_RUNTIME = {
    "provider": "openai",
    "model": "gpt-6-luna",
    "api_family": "responses",
    "reasoning_effort": "medium",
    "temperature": None,
    "tools_enabled": True,
    "streaming": True,
}
```

## Failure modes

### Unsupported parameter

Symptoms:

- HTTP 400
- provider validation error
- SDK exception before generation begins

Cause:

A parameter is invalid for the selected model/runtime mode.

### API capability mismatch

Symptoms:

- model works without tools but fails with tools
- reasoning works but function calling does not
- structured output behaves differently across endpoints

Cause:

The capability exists, but not in the selected API/model/mode combination.

### Gateway compatibility mismatch

Symptoms:

- provider-native examples work but the same configuration fails through a compatibility gateway
- streaming becomes buffered
- parameter validation differs from provider documentation

Cause:

The gateway implements only part of the upstream protocol or semantics.

## Decision rules

1. Never assume `temperature=0` is a universal safe default.
2. Check parameter support for the exact model family.
3. Check parameter support for the exact API family.
4. Check how reasoning mode changes supported parameters.
5. Validate tool support together with reasoning mode and API family.
6. Treat OpenAI-compatible gateways as separate compatibility targets.
7. Centralize and validate model runtime policy.
8. Re-check official documentation whenever changing model family, API family, SDK version, or provider.

## Current references

OpenAI documentation used for the current case study:

- https://developers.openai.com/api/docs/models/gpt-6-luna
- https://developers.openai.com/api/docs/guides/latest-model
- https://developers.openai.com/api/docs/guides/reasoning

These references document one current provider example. The engineering rules in this chapter are intentionally model-agnostic.
