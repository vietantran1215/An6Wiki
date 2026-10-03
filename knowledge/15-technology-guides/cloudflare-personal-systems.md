# Cloudflare for Low-Cost Personal Systems

## Good fit

Cloudflare's edge/serverless ecosystem is attractive for lightweight personal systems where cost and operational simplicity matter.

Typical capabilities include:

- Workers for serverless logic;
- Pages/Workers for web delivery;
- D1 for lightweight relational persistence;
- KV/cache-oriented storage depending on access pattern;
- R2 for object storage when needed.

## Architecture principle

Do not add storage services without a real persistence/access-pattern requirement.

For a personal static knowledge or quiz system, local JSON/content files can remain simpler if write concurrency and multi-device mutation are not required.

## API example

```ts
export default {
  async fetch(request: Request): Promise<Response> {
    const url = new URL(request.url);

    if (url.pathname === "/health") {
      return Response.json({ status: "ok" });
    }

    return new Response("Not found", { status: 404 });
  },
};
```

## Decision dimensions

- persistence;
- query complexity;
- expected traffic;
- data size;
- write frequency;
- cost;
- vendor coupling.

## Rule

For personal projects, operational simplicity is often a more valuable optimization than theoretical scalability.
