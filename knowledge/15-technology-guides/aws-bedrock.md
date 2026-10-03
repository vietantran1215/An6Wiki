# AWS Bedrock Application Architecture

## Capabilities

Bedrock is commonly used for:

- foundation-model access;
- embeddings;
- guardrails;
- model routing/application integration;
- agent/RAG-related workloads depending on architecture.

## Typical enterprise architecture

```text
Client
 → API service
 → identity/policy
 → retrieval
 → Bedrock model
 → validation
 → telemetry
```

Supporting services may include:

- S3 for corpus;
- OpenSearch/Aurora pgvector for retrieval;
- SQS/EventBridge for async workflows;
- CloudWatch/X-Ray/OpenTelemetry for telemetry;
- ECS/Lambda for compute;
- IAM/KMS/Secrets Manager for security.

## Security

Prefer IAM role/workload identity over static credentials.

Apply:

- least privilege;
- private networking where required;
- encrypted storage;
- redacted logs;
- approved model policy.

## Cost

Track:

- input/output tokens;
- embedding volume;
- retrieval infrastructure;
- guardrail calls;
- batch vs interactive workloads.

## Rule

Bedrock is a model/platform capability inside a larger application architecture; it does not remove the need for data, authorization, evaluation, or operational design.
