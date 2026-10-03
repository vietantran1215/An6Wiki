# Prompt Injection & Trust Boundaries

## Core problem

LLMs treat instructions and data through the same language channel.

Untrusted content may contain text that attempts to influence model behavior.

Sources include:

- user input;
- retrieved documents;
- websites;
- email;
- tool output;
- uploaded files.

## Trust separation

```text
Trusted policy
  ≠
Untrusted content
```

The application must preserve this distinction even though both eventually become tokens.

## Defensive controls

- least-privilege tools;
- permission-aware retrieval;
- instruction/data separation;
- tool allowlist;
- schema validation;
- human approval;
- output validation;
- sandboxing;
- monitoring.

## Example tool gate

```python
ALLOWED_TOOLS = {"search_policy", "get_claim"}

def validate_tool_call(call):
    if call.name not in ALLOWED_TOOLS:
        raise PermissionError("Tool is not available in this workflow")
```

## Important limitation

A stronger system prompt does not solve prompt injection by itself.

## Rule

Assume untrusted data can attempt to manipulate the model. Design authorization and side-effect safety outside the model.
