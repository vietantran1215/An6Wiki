# React & Next.js Architecture

## 1. Component architecture

Components should have clear responsibilities.

Useful separation:

- presentational rendering;
- domain interaction;
- data fetching;
- state ownership;
- routing/layout;
- cross-cutting concerns.

Avoid components that fetch data, transform domain logic, mutate global state, handle permissions, and render UI all at once.

## 2. Server vs client execution

Modern Next.js architectures require explicit thinking about execution location.

Questions:

- Does this code require browser APIs?
- Does it contain secrets?
- Can it run during server rendering?
- Does the result need hydration?
- Can the data be cached?
- Is the page static, dynamic, or personalized?

## 3. TypeScript is not runtime validation

```ts
import { z } from "zod";

const ArticleSchema = z.object({
  id: z.string(),
  title: z.string(),
  publishedAt: z.string().datetime(),
});

type Article = z.infer<typeof ArticleSchema>;

export async function loadArticle(id: string): Promise<Article> {
  const response = await fetch(`/api/articles/${id}`);
  const payload: unknown = await response.json();

  // Runtime validation protects the UI from malformed external data.
  return ArticleSchema.parse(payload);
}
```

## 4. Boundary design

Prefer domain-oriented folders over purely technical folders once an application becomes large.

Example:

```text
src/
  features/
    claims/
      api/
      components/
      hooks/
      model/
      tests/
    auth/
    reports/
  shared/
    ui/
    lib/
    config/
```

## 5. Micro-frontends

Patterns include:

- Module Federation;
- route-level composition;
- Next.js multi-zone;
- separate apps behind a gateway.

Use only when independent team ownership/release is worth the complexity.

Costs include:

- duplicated dependencies;
- cross-app navigation;
- shared auth;
- design consistency;
- observability;
- version compatibility.

## 6. Decision rule

Prefer a well-modularized single frontend until organizational boundaries create a real need for independent deployment.
