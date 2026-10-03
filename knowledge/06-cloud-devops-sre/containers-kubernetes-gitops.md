# Containers, Kubernetes & GitOps

## Containers

Containers package the application and runtime dependencies into a reproducible image.

A good image is:

- minimal;
- non-root where possible;
- immutable;
- vulnerability-scanned;
- versioned.

## Docker example

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# Run as a non-root user in production.
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8080"]
```

## Kubernetes

Kubernetes manages desired workload state.

Key concepts:

- Pod;
- Deployment;
- Service;
- ConfigMap;
- Secret;
- readiness/liveness probes;
- HPA;
- requests/limits.

## GitOps

GitOps uses Git as desired-state source and a reconciler such as Argo CD or Flux to converge the cluster.

Benefits:

- auditability;
- declarative change;
- drift correction;
- rollback via Git history.

## Production concerns

- resource limits;
- pod disruption;
- graceful shutdown;
- network policy;
- secret management;
- image provenance;
- cluster upgrades.

## Rule

Do not adopt Kubernetes because it is "standard." Adopt it when workload scale, platform standardization, multi-service operations, and organizational maturity justify the operational layer.
