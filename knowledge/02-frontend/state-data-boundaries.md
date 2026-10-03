# State, Data & Boundaries

## 1. Not all state is the same

State categories:

- local UI state;
- form state;
- URL/navigation state;
- server state;
- cross-feature application state;
- persisted client state.

The storage mechanism should follow the state category.

## 2. Server state

Server state has properties different from local state:

- it can become stale;
- another actor may change it;
- requests can fail;
- caching matters;
- refetch policy matters.

Use a server-state library or framework data APIs rather than manually rebuilding caching logic in a global store.

## 3. URL state

Filters, sorting, tabs, and pagination often belong in the URL because the URL should be shareable and restorable.

## 4. Form state

Form state includes:

- raw input;
- validation;
- dirty state;
- submit state;
- server errors.

Keep business validation on the server even when the client validates for UX.

## 5. Authentication state

Never treat client-side role display logic as the security boundary.

The frontend can hide unavailable actions for UX, but the backend must enforce authorization.

## 6. Example query state

```ts
type SearchParams = {
  page?: string;
  status?: string;
};

export function normalizeSearch(params: SearchParams) {
  return {
    page: Math.max(1, Number(params.page ?? 1)),
    status: params.status ?? "all",
  };
}
```

## 7. Decision framework

Ask:

- Who owns the state?
- How long should it live?
- Can another actor change it?
- Should it survive refresh?
- Should it be shareable in a URL?
- Is it sensitive?
- Does it require synchronization with the server?

The answer determines where it belongs.
