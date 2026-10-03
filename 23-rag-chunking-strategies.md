# RAG Chunking Strategies

Chunking is not a preprocessing detail. It defines what a retriever is able to return and therefore affects recall, context quality, citation precision, latency, and cost.

## Fixed-size chunking

Split text by a fixed token/character window.

Use when:

- content is regular;
- structure is weak or unavailable;
- a cheap baseline is needed.

Risks:

- semantic boundaries are ignored;
- tables/code/sections may be split poorly.

## Recursive chunking

Split by increasingly smaller separators such as headings, paragraphs, sentences, and characters.

Useful as a strong general-purpose baseline.

## Semantic chunking

Group semantically related sentences using embeddings or similarity changes.

Useful when paragraphs are irregular but semantic cohesion matters.

Trade-off: more preprocessing cost and more tuning.

## Sentence-window retrieval

Index a narrow sentence-level unit but return surrounding sentences as context.

Useful when precise retrieval and broader generation context are both important.

## Parent-child chunking

Index small child chunks for retrieval but return the larger parent section.

Useful when:

- small chunks improve retrieval precision;
- larger context is required for understanding.

## Structure-aware chunking

Use document structure such as:

- title;
- section;
- subsection;
- table;
- list;
- page;
- heading hierarchy.

Strong choice for policies, manuals, technical documentation, and reports.

## Code-aware chunking

Use language-aware heuristics to keep logical code blocks together:

- functions;
- classes;
- modules;
- comments;
- declarations.

This is broader than AST-based chunking.

## AST-based chunking

Parse source code into an Abstract Syntax Tree and split by syntactic nodes.

Advantages:

- preserves language structure;
- can attach symbol metadata;
- supports symbol-aware retrieval.

Trade-offs:

- language-specific parser dependency;
- malformed/incomplete code can reduce reliability;
- syntax boundaries are not always semantic boundaries.

## Multimodal chunking

For PDFs and rich documents, chunking may need to preserve:

- text;
- image;
- table;
- chart;
- caption;
- page coordinates;
- cross-modal relationship.

## Decision rule

Choose a chunking strategy by asking:

1. What unit does the user usually ask about?
2. What unit is independently meaningful?
3. What unit can be cited precisely?
4. How much neighboring context is needed?
5. Does structure exist and can it be parsed reliably?
6. Does the source include code, tables, or images?

## Evaluation

Do not judge chunking by intuition alone.

Evaluate:

- Recall@K;
- Precision@K;
- answer faithfulness;
- citation correctness;
- context utilization;
- average tokens per answer;
- latency and storage cost.
