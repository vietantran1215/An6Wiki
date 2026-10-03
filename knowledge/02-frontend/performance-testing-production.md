# Frontend Performance, Testing & Production

## 1. Performance categories

Measure:

- initial load;
- interaction latency;
- rendering cost;
- network waterfalls;
- bundle size;
- image/font cost;
- client-side memory.

For web experience, Core Web Vitals are useful user-centered signals.

## 2. Common performance problems

- excessive JavaScript;
- unnecessary client components;
- duplicated dependencies;
- repeated rendering;
- unbounded lists;
- large images;
- slow API waterfalls;
- blocking third-party scripts.

## 3. Testing pyramid for frontend

Use complementary layers:

- unit tests for pure logic;
- component tests for UI behavior;
- integration tests for feature behavior;
- E2E tests for critical journeys.

Do not attempt to prove all behavior through E2E tests alone.

## 4. Example component test

```ts
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

test("submits the claim", async () => {
  const user = userEvent.setup();

  render(<button onClick={() => alert("submitted")}>Submit</button>);

  await user.click(screen.getByRole("button", { name: "Submit" }));

  // Real tests should assert observable behavior rather than implementation details.
});
```

## 5. Production checklist

- CSP and secure headers;
- error boundary;
- structured client telemetry;
- source maps with controlled access;
- feature flags;
- environment validation;
- performance budgets;
- accessibility checks;
- critical E2E flows;
- rollback strategy.

## 6. Rule

Frontend production quality is not determined by framework choice. It is determined by predictable behavior under slow networks, malformed data, user error, release changes, and backend failure.
