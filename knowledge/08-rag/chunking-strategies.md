# Chunking Strategies

## Why chunking matters

Chunking defines the atomic units that retrieval can rank.

It affects:

- retrieval recall;
- precision;
- context coherence;
- citations;
- token usage;
- index size.

## Fixed-size

Simple token/character windows.

Good baseline; poor structural awareness.

## Recursive

Split through a hierarchy such as:

```text
heading → paragraph → sentence → token window
```

Good general-purpose default.

## Semantic

Split when semantic similarity between adjacent regions changes.

Useful for irregular prose, but preprocessing is more expensive.

## Sentence-window

Retrieve a precise sentence but return neighboring sentences.

Good when retrieval needs precision and generation needs local context.

## Parent-child

Index small child chunks; return the larger parent.

```text
Section parent
 ├─ child chunk A  ← searchable
 ├─ child chunk B  ← searchable
 └─ child chunk C
```

## Structure-aware

Use:

- headings;
- tables;
- lists;
- pages;
- sections.

Strong for policies, manuals, reports, and documentation.

## Code-aware

Preserve logical code units such as:

- function;
- class;
- module;
- comment/docstring.

## AST-based

Use parser nodes as boundaries.

```python
import ast

tree = ast.parse(source)

for node in tree.body:
    # Top-level classes/functions can become retrievable units.
    if isinstance(node, (ast.FunctionDef, ast.AsyncFunctionDef, ast.ClassDef)):
        print(node.name, node.lineno, node.end_lineno)
```

AST-based is a subset of code-aware chunking.

## Multimodal

Preserve relationships between:

- text;
- image;
- table;
- chart;
- caption;
- page position.

## How to choose

Ask:

1. What unit is independently meaningful?
2. What unit do users ask about?
3. What unit can be cited?
4. How much neighboring context is required?
5. Is reliable structure available?
6. Is content code/table/image heavy?

## Rule

Evaluate chunking empirically against a golden query set. There is no universal best chunk size.
