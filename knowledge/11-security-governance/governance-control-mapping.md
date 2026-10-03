# Governance & Control Mapping

## Governance answers

- Who owns the AI system?
- What risks are accepted?
- Which data may be used?
- Which models/tools are approved?
- What evidence supports release?
- Who reviews incidents?
- How are changes audited?

## Engineering evidence

Governance should map to concrete artifacts:

```text
Risk policy
 → architecture control
 → implementation
 → automated test/eval
 → telemetry
 → audit evidence
```

## Examples

### Access control policy

Implementation:

- OIDC;
- RBAC/ABAC;
- permission-aware retrieval.

Evidence:

- authorization tests;
- denied-access traces;
- audit logs.

### Quality policy

Implementation:

- golden dataset;
- regression gate.

Evidence:

- versioned evaluation report.

## Frameworks

Useful references include:

- OWASP guidance for LLM/agent applications;
- NIST AI Risk Management Framework;
- ISO/IEC 42001 for AI management systems.

These frameworks do not replace system-specific engineering decisions.

## Rule

Governance becomes valuable when policy is traceable to technical controls and operational evidence.
