# Frontend Engineering

## 1. What is the frontend responsible for?

A production frontend is responsible for more than rendering UI. It owns interaction, client state, server-state synchronization, accessibility, performance, routing, validation, error handling, authentication UX, and deployment behavior.

## 2. Core stack knowledge

Recurring technologies include JavaScript, TypeScript, React, Next.js, Angular, Vue, React Router, Vite/Rspack/Rsbuild, CSS/SCSS/LESS, Ant Design, and Material Design. They are tools, not architecture categories.

## 3. State categories

Separate state by responsibility:

- local UI state;
- form state;
- URL state;
- server state;
- global cross-cutting state.

Do not put all state into one global store.

## 4. Micro-frontends

Useful when different teams require independent delivery, ownership, or technology boundaries.

Common patterns:

- Module Federation;
- route-level composition;
- Next.js multi-zone;
- independently deployed frontend applications.

Evaluate shared dependencies, design-system consistency, routing ownership, auth/session propagation, observability, and deployment compatibility.

## 5. Production checklist

- Runtime validation for untrusted API responses.
- Error boundaries and fallback states.
- Loading, empty, error, and partial states.
- Accessibility checks.
- Bundle and Core Web Vitals monitoring.
- Stable API contracts.
- Feature flags for risky releases.
- E2E tests for critical user journeys.

## 6. Runtime validation example

```ts
import { z } from "zod";

// TypeScript types disappear at runtime.
// Validate data received from an external API.
const UserSchema = z.object({
  id: z.string(),
  email: z.string().email(),
  role: z.enum(["admin", "member"]),
});

export type User = z.infer<typeof UserSchema>;

export function parseUser(payload: unknown): User {
  return UserSchema.parse(payload);
}
```
