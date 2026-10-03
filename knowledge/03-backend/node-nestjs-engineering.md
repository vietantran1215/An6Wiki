# Node.js & NestJS Engineering

## 1. Runtime model

Node.js is strong for I/O-heavy services because the event loop can coordinate many concurrent network operations efficiently.

Do not confuse this with unlimited throughput. CPU-heavy synchronous work blocks progress.

## 2. Service layering

A practical NestJS structure:

```text
controller
  ↓
application/service
  ↓
domain rules
  ↓
repository / external adapters
```

Controllers should translate transport concerns. Business rules should not depend on HTTP objects.

## 3. Example

```ts
@Injectable()
export class ClaimService {
  constructor(private readonly repo: ClaimRepository) {}

  async approve(claimId: string, actorId: string) {
    const claim = await this.repo.getById(claimId);

    if (!claim) {
      throw new NotFoundException();
    }

    // Domain rule: only submitted claims can be approved.
    if (claim.status !== "submitted") {
      throw new ConflictException("Claim is not approvable");
    }

    claim.approve(actorId);
    await this.repo.save(claim);

    return claim;
  }
}
```

## 4. Important production concerns

- request validation;
- dependency injection boundaries;
- database transactions;
- idempotency;
- async errors;
- graceful shutdown;
- connection pooling;
- tracing;
- queue consumers;
- memory usage.

## 5. NestJS trap

Decorators and modules make structure convenient, but they do not automatically create good boundaries. Avoid circular module dependencies and application services that grow into god classes.

## 6. Decision rule

Use NestJS when strong conventions, DI, modularity, and a larger team justify the framework. Use a lighter Node framework when explicit minimalism is more valuable.
