# Architecture-Significant Requirements

## 1. Start from the problem

Architecture should follow business constraints and quality attributes.

Typical architecture-significant requirements:

- availability;
- latency;
- throughput;
- scalability;
- security;
- consistency;
- recoverability;
- auditability;
- deployability;
- maintainability;
- cost.

## 2. Quantify them

"We need high availability" is weak.

Better:

- 99.9% monthly availability;
- p95 API latency < 300 ms;
- RTO < 30 minutes;
- RPO < 5 minutes;
- tenant data must never cross boundaries;
- 10k concurrent users;
- 1M documents indexed within 4 hours.

## 3. Trade-offs

Improving one quality may hurt another.

Examples:

- stronger consistency can increase latency;
- more redundancy improves availability but increases cost;
- aggressive caching lowers latency but complicates freshness;
- microservices improve independent deployment but increase operational complexity.

## 4. Architecture workflow

```text
Business goal
 → constraints
 → quality attributes
 → architecture options
 → trade-off analysis
 → decision
 → validation
 → production feedback
```

## 5. Validation

Architecture should be tested through:

- load tests;
- failure injection;
- threat modeling;
- recovery exercises;
- cost modeling;
- prototype/spike;
- operational review.

## 6. Rule

If a requirement is important enough to drive architecture, make it measurable.
