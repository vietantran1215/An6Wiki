# AI Supply Chain & Dependency Risk

## AI systems have a large supply chain

Components may include:

- model provider;
- embedding model;
- reranker;
- vector database;
- parser/OCR;
- agent framework;
- MCP server;
- external tool;
- container image;
- Python/npm dependency.

## Risks

- malicious dependency;
- compromised model/artifact;
- changed provider behavior;
- vulnerable library;
- poisoned data;
- untrusted MCP server;
- leaked secret;
- unsigned artifact.

## Controls

- dependency pinning;
- SBOM;
- image scanning;
- signature/provenance verification;
- allowlisted model/tool providers;
- secret scanning;
- isolated execution;
- version tracking;
- evaluation after upgrades.

## Change management

A model upgrade is an application change.

Run regression evaluation before production promotion.

## Rule

AI supply-chain security extends normal software supply-chain security with models, prompts, datasets, embeddings, tools, and retrieval corpora.
