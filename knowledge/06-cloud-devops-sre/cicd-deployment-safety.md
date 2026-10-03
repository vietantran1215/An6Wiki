# CI/CD & Deployment Safety

## Pipeline objective

CI/CD should reduce the risk and cost of change.

```text
commit
 → lint/test
 → build
 → scan
 → immutable artifact
 → deploy
 → verify
 → promote or rollback
```

## Immutable artifacts

Build once and promote the same artifact across environments.

Prefer image tags based on commit SHA.

## Database migrations

Deployment must account for old and new application versions coexisting.

Use backwards-compatible migrations.

## Progressive delivery

Useful patterns:

- rolling;
- blue/green;
- canary;
- feature flags.

## Example GitHub Actions fragment

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - run: pip install -r requirements.txt
      - run: pytest
```

## Release verification

After deployment verify:

- health/readiness;
- error rate;
- latency;
- critical business flow;
- dependency health.

## Rule

A pipeline is not complete when deployment succeeds. It is complete when the release is verified and rollback is possible.
