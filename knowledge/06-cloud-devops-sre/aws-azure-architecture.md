# Cloud Architecture: AWS & Azure

## Cloud learning should be capability-based

Do not memorize service names in isolation.

Map services to capabilities:

- compute;
- storage;
- database;
- networking;
- identity;
- messaging;
- observability;
- AI/ML;
- security.

## AWS examples

- compute: EC2, ECS/Fargate, Lambda;
- storage: S3;
- relational DB: RDS/Aurora;
- messaging: SQS/SNS/EventBridge;
- search: OpenSearch;
- AI: Bedrock;
- observability: CloudWatch/X-Ray;
- identity: IAM.

## Azure examples

- compute: App Service, Functions, Container Apps, AKS;
- storage: Blob Storage;
- relational DB: Azure Database services;
- messaging: Service Bus/Event Grid;
- AI: Azure AI Foundry/Azure OpenAI;
- identity: Microsoft Entra ID/managed identity;
- observability: Azure Monitor/Application Insights.

## Managed identity principle

Prefer workload identity/managed identity over embedding long-lived credentials.

## Architecture questions

- private vs public networking;
- identity flow;
- data residency;
- encryption;
- backup/DR;
- service quotas;
- cost model;
- observability;
- IaC;
- failure region/zone.

## Rule

Choose cloud services by required capability, operational responsibility, security boundary, and cost—not by certification memorization.
