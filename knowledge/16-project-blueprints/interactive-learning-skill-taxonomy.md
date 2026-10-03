# Interactive Learning & Skill Taxonomy Platform

## Problem

A quiz score such as 80% says little about which capability is weak or improving.

## Goal

Model learning around a hierarchical skill taxonomy and longitudinal evidence.

## Domain model

```text
Domain
 → Competency
 → Skill
 → Learning Objective
 → Question / Lab / Project Evidence
```

A question can map many-to-many to skills.

## Attempt evidence

Store:

- timestamp;
- question;
- selected options;
- correctness;
- explanation;
- skill mappings;
- difficulty;
- response time.

## Progression

Track skill-level trends such as:

```text
RAG Retrieval accuracy:
45% → 72% → 86%
```

Do not collapse all performance into one aggregate score.

## Persistence options

For a simple personal system:

- local JSON can be acceptable for low-concurrency single-user persistence;
- a database becomes useful when concurrent writes, querying, multiple users, or sync requirements increase.

## Analytics

Useful views:

- mastery by competency;
- weakest skills;
- strongest skills;
- learning velocity;
- repeated misconception;
- accuracy by difficulty;
- recent regression.

## Adaptive selection

A future adaptive engine can choose questions based on:

- low mastery;
- recency;
- prerequisite gaps;
- uncertainty;
- spaced repetition.

## Rule

The skill graph is the product model; the quiz UI is only one interaction surface.
