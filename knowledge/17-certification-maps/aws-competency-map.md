# AWS Architecture & AI Competency Map

## Architecture foundation

Key capabilities:

- VPC/networking;
- IAM;
- EC2;
- load balancing;
- autoscaling;
- S3;
- RDS/Aurora;
- DynamoDB;
- SQS/SNS/EventBridge;
- monitoring;
- backup/DR;
- cost optimization.

## Developer capability

- SDK usage;
- application identity;
- serverless;
- deployment;
- troubleshooting;
- observability;
- CI/CD.

## DevOps capability

- pipeline automation;
- IaC;
- release strategies;
- governance;
- incident response;
- monitoring;
- resilient operations.

## Generative AI capability

- foundation model selection;
- embeddings;
- chunking;
- vector retrieval;
- RAG;
- agents/tool use;
- prompt design;
- guardrails;
- evaluation;
- responsible AI;
- cost/security.

## Engineering synthesis

A production AWS AI system may combine:

```text
S3 corpus
 → ingestion compute
 → embeddings
 → OpenSearch/Aurora pgvector
 → Bedrock model
 → API/ECS/Lambda
 → CloudWatch telemetry
 → IAM/KMS security
 → Terraform delivery
```

## Rule

Use certification topics as a coverage checklist, then prove them through an architecture and working system.
