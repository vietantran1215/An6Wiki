# Cloud, DevOps & SRE

## 1. Objective

The objective is to deliver changes safely and operate systems predictably.

Recurring environments and tools include AWS, Azure, Docker, ECS/Fargate, Kubernetes, Terraform, GitHub Actions, GitLab CI, CloudWatch, OpenTelemetry, Prometheus/Grafana, and Argo CD.

## 2. Delivery pipeline

```text
push
 → test
 → build
 → create immutable artifact/image
 → scan
 → publish
 → deploy
 → verify
 → rollback if needed
```

Use commit-SHA image tags for production artifacts. Avoid relying on mutable `latest`.

## 3. Infrastructure and GitOps

Terraform describes infrastructure state. Configuration tools configure machines/software. GitOps makes Git the desired state and uses reconciliation to correct drift.

## 4. SRE model

- SLI — measured reliability signal.
- SLO — reliability target.
- Error budget — allowed unreliability.
- Burn-rate alert — how fast the budget is consumed.

## 5. Observability

Logs explain events. Metrics show trends. Traces show causality across components.

## 6. Deployment safety

Prefer health/readiness checks, progressive rollout, rollback automation, feature flags, backwards-compatible DB migrations, capacity limits, and cost limits.

## 7. Security

Use least-privilege IAM, managed identities where appropriate, encryption, secret managers, network segmentation, audit logs, dependency scanning, and image scanning.
