# Azure AI Engineering Competency Map

## Platform fundamentals

Understand:

- resource hierarchy;
- regions;
- networking;
- identity;
- RBAC;
- managed identities;
- Key Vault;
- monitoring.

## AI application capabilities

- model deployment/access;
- prompt/application orchestration;
- embeddings;
- retrieval;
- safety controls;
- evaluation;
- monitoring.

## Enterprise RAG

Core design questions:

- Where is source data?
- How is identity propagated?
- How are document permissions applied?
- Which search/retrieval engine is used?
- How is model access governed?
- How are prompts/models evaluated?
- How are secrets avoided?

## Managed identity

Prefer workload-managed identity when a service can authenticate to another Azure resource without a stored long-lived secret.

## Permission distinction

User authorization to the application does not automatically imply authorization to all indexed content.

## Rule

Treat exam objectives as capability categories. Build one end-to-end architecture that forces those categories to interact.
