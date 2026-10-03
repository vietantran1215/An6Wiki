# Azure AI Application Architecture

## Capability map

Azure AI application architecture commonly involves:

- Microsoft Entra identity;
- Azure OpenAI / AI Foundry model access;
- managed identities;
- Azure AI Search or another retrieval layer;
- Key Vault;
- Azure Monitor/Application Insights;
- storage and compute services.

## Identity

Prefer managed identity for workloads where supported.

Separate:

- user authentication;
- workload identity;
- authorization to application resources;
- authorization to Azure resources.

## RAG permissions

Do not confuse "user can call the application" with "user may access every document in the search index."

Permission-aware retrieval is still application architecture.

## Secrets

Use Key Vault or workload identity rather than embedding credentials in application configuration.

## Monitoring

Capture:

- request latency;
- model latency;
- token/cost usage;
- retrieval behavior;
- failures;
- content/security events where appropriate.

## Rule

Azure services provide managed capabilities. Enterprise correctness still depends on your identity, permission, data, evaluation, and lifecycle design.
