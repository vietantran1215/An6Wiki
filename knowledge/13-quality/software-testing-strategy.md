# Software Testing Strategy

## 1. Test behavior at the cheapest useful layer

A balanced strategy uses:

- unit tests;
- component/module tests;
- integration tests;
- API/contract tests;
- E2E tests;
- performance tests;
- security tests.

## 2. Testing pyramid is a cost model

Unit tests are cheap and fast.

E2E tests provide strong business confidence but are slower and more brittle.

Do not use E2E to prove every branch of business logic.

## 3. Contract testing

Contract tests verify that independently deployed components agree on schemas and semantics.

Important for:

- microservices;
- frontend/backend;
- event producers/consumers;
- MCP tools;
- external integrations.

## 4. Example unit test

```python
def test_submitted_claim_can_be_approved():
    claim = Claim(status="submitted")

    claim.approve(actor_id="manager-1")

    assert claim.status == "approved"

def test_draft_claim_cannot_be_approved():
    claim = Claim(status="draft")

    with pytest.raises(InvalidState):
        claim.approve(actor_id="manager-1")
```

## 5. Risk-based testing

Test depth should follow:

- impact;
- probability;
- change frequency;
- complexity;
- reversibility.

## 6. Production feedback

Escaped defects should update:

- regression tests;
- monitoring;
- architecture assumptions;
- training.

## 7. Rule

The purpose of testing is not maximizing test count. It is reducing uncertainty about important behavior.
