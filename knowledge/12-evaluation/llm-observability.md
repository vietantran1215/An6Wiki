# LLM Observability

## Trace the complete execution

```text
request
 → router
 → retriever
 → reranker
 → prompt builder
 → model
 → tool
 → verifier
 → response
```

## Capture

- model/provider/version;
- prompt version;
- token usage;
- latency;
- cost;
- retrieval IDs;
- reranker scores;
- tool calls;
- policy decisions;
- errors;
- retries.

## Sensitive data

Telemetry itself is a security surface.

Use:

- redaction;
- sampling;
- access control;
- retention policy;
- hashed identifiers where appropriate.

## Example span

```python
with tracer.start_as_current_span("llm.generate") as span:
    span.set_attribute("model", model_name)
    span.set_attribute("prompt.version", prompt_version)

    result = model.invoke(messages)

    span.set_attribute("tokens.output", result.usage.output_tokens)
```

## Business telemetry

Technical metrics are not enough.

Measure:

- resolution rate;
- human override;
- task completion;
- adoption;
- time saved;
- defect rate.

## Rule

Observability should let you reconstruct why an AI decision occurred without indiscriminately storing sensitive prompt content.
