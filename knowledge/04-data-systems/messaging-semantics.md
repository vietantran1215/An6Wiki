# RabbitMQ, Kafka & Messaging Semantics

## 1. Why messaging?

Messaging decouples producers from consumers in time and execution.

Use it for:

- asynchronous work;
- event propagation;
- workload smoothing;
- integration;
- audit/event streams.

## 2. RabbitMQ

RabbitMQ is commonly strong for:

- task queues;
- routing;
- per-message acknowledgement;
- work distribution.

## 3. Kafka

Kafka is commonly strong for:

- durable ordered logs;
- replay;
- high throughput;
- event streaming;
- multiple independent consumer groups.

## 4. Delivery semantics

"At least once" means duplicates are possible.

Therefore consumers should be idempotent.

```ts
async function handleOrderPaid(event: OrderPaid) {
  const alreadyHandled = await inbox.exists(event.eventId);

  if (alreadyHandled) return;

  await db.transaction(async (tx) => {
    await createShipment(tx, event.orderId);
    await inbox.markHandled(tx, event.eventId);
  });
}
```

## 5. Ordering

Global ordering is expensive and often unnecessary.

Usually ordering only matters per key:

- order ID;
- account ID;
- tenant ID.

## 6. DLQ

A dead-letter queue isolates repeatedly failing messages.

A DLQ requires an operational process:

- inspect;
- classify;
- fix;
- replay;
- document.

## 7. Backpressure

Consumers need bounded concurrency and broker prefetch/batch settings.

Without backpressure, an outage can create a huge recovery spike.

## 8. Decision rule

Choose RabbitMQ for routed work/message delivery.

Choose Kafka when durable replayable event streams and independent consumers are first-class requirements.

Do not choose either merely because the architecture is "event driven."
