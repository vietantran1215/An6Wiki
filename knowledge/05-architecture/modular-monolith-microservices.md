# Modular Monolith vs Microservices

## 1. Modular monolith

A modular monolith is one deployable application with strong internal boundaries.

Benefits:

- simple deployment;
- easy local development;
- low network overhead;
- straightforward transactions;
- fewer operational moving parts.

The challenge is maintaining module discipline.

## 2. Microservices

Microservices split independently deployable services around business boundaries.

Benefits can include:

- independent scaling;
- independent release cadence;
- ownership isolation;
- fault containment;
- technology freedom.

Costs include:

- distributed transactions;
- network failures;
- observability complexity;
- duplicated infrastructure;
- deployment coordination;
- data consistency issues.

## 3. Decision questions

Ask:

- Are teams blocked by shared releases?
- Do domains scale differently?
- Do domains require different reliability or security boundaries?
- Is independent ownership important?
- Is the organization capable of operating distributed systems?
- Is the current monolith actually modular?

## 4. Anti-pattern

A distributed monolith has many services but still requires coordinated release and shared assumptions.

That is often worse than a modular monolith.

## 5. Extraction path

```text
identify stable boundary
 → enforce module interface
 → separate data ownership
 → introduce async/API contract
 → observe
 → extract only if justified
```

## 6. Rule

Start with the simplest topology that preserves clear boundaries. Distribution should solve a concrete problem.
