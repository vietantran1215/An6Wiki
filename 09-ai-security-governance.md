# AI Security & Governance

## 1. Security model

Do not treat the LLM as a security boundary. The model should receive only data and tools already approved by prior controls.

## 2. Secure RAG architecture

```text
User
 ↓
Authentication
 ↓
Authorization / Policy
 ↓
Input security / DLP / sanitization
 ↓
Permission-aware retrieval
 ↓
Secure context builder
 ↓
Prompt builder
 ↓
LLM gateway / model
 ↓
Output validation / DLP
 ↓
Response
```

## 3. Key threats

Prompt injection, indirect prompt injection, sensitive information disclosure, over-permissioned tools, insecure output handling, retrieval poisoning, exfiltration, supply-chain risk, excessive agency, and unsafe autonomous actions.

## 4. Secure context builder

Enforce tenant/resource permissions, remove unnecessary sensitive fields, limit context size, attach source metadata, separate instructions from untrusted retrieved text, and preserve provenance.

## 5. Tool security

For each tool define allowlists, least-privilege credentials, input/output validation, timeouts, rate limits, retry semantics, approval level, and audit trail.

## 6. Governance

Production AI needs ownership, model/prompt/tool versioning, data provenance, evaluation evidence, access policy, incident response, audit logs, risk classification, human oversight, and lifecycle review.

ISO/IEC 42001 is relevant as an AI management-system standard, while engineering controls still need to be implemented concretely.

## 7. Principle

> The model proposes; the control plane disposes.
