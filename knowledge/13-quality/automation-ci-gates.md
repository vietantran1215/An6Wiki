# Test Automation & CI Quality Gates

## Automation objective

Automation should provide fast, repeatable evidence.

## CI stages

```text
lint
 → unit tests
 → integration tests
 → contract tests
 → security scan
 → build
 → selected E2E
 → AI eval where applicable
```

## Example pytest markers

```python
import pytest

@pytest.mark.unit
def test_discount_rule():
    assert calculate_discount(total=1000, tier="gold") == 100

@pytest.mark.integration
async def test_claim_persists(db_session):
    claim = await create_claim(db_session, amount=100)
    assert await load_claim(db_session, claim.id)
```

## Quality gate

A release gate may include:

- deterministic test pass;
- coverage on critical modules;
- no critical vulnerabilities;
- performance threshold;
- zero authorization leakage;
- AI regression thresholds.

## Coverage

Coverage is evidence of executed lines/branches, not evidence of good assertions.

100% coverage can still contain weak tests.

## Flaky tests

Treat flakiness as a defect.

Track:

- failure frequency;
- root cause;
- retries;
- quarantined tests;
- ownership.

## Rule

CI should block known unacceptable risk, not become a slow ritual with ignored red builds.
