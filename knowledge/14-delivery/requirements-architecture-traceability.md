# Requirements to Architecture Traceability

## Why traceability matters

Large projects lose intent when business needs, architecture, backlog, and tests become disconnected.

A traceable chain:

```text
Business objective
 → requirement
 → architecture decision
 → user story
 → acceptance criteria
 → implementation
 → test
 → evidence
```

## Example

```text
Requirement:
Only project members may query project knowledge.

Architecture:
OIDC identity + permission-aware retrieval.

Acceptance criterion:
A user from Project A receives zero chunks from Project B.

Test:
Automated cross-project leakage test.

Evidence:
Evaluation report shows unauthorized retrieval count = 0.
```

## Requirements types

Separate:

- functional;
- quality/non-functional;
- security;
- operational;
- compliance.

## Change impact

When a requirement changes, traceability identifies affected:

- architecture;
- APIs;
- data;
- tests;
- training;
- rollout.

## Rule

Traceability should support change and audit—not produce documents that nobody uses.
