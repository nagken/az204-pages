# Exam Decision Reference

> Pick-the-right-service tables. Pair with **Concept & Reference Index** for cross-domain links.

## Compute: which service?

| Workload shape | Pick |
|---|---|
| HTTP web app, scheduled or always-on | **App Service** |
| Tiny event handler, scale-to-zero | **Functions (Consumption)** |
| Functions but need VNet, no cold start | **Functions (Premium / Flex)** |
| Long-running stateful workflow | **Durable Functions (orchestrator)** |
| Containerized microservices, KEDA + Dapr | **Container Apps** |
| Single ephemeral container, no orchestrator | **Container Instances** |
| Custom Linux + sidecars + GPU | **Azure Kubernetes Service (out of scope, but appears as a distractor)** |

## Functions triggers and bindings

| Need | Trigger or binding |
|---|---|
| Run on schedule | **Timer trigger** (NCRONTAB) |
| React to HTTP | **HTTP trigger** |
| Process queue | **Queue Storage trigger** or **Service Bus trigger** |
| React to telemetry stream | **Event Hubs trigger** |
| Reactive on Azure event | **Event Grid trigger** |
| React to Cosmos changes | **Cosmos DB trigger** (uses change feed + lease container) |
| Read a doc inline | **Cosmos / Blob input binding** |
| Write a queue message | **Queue / Service Bus output binding** |
| Send email / SMS | Output binding to **SendGrid** / **Twilio** |

## Cosmos consistency picker

| Need | Level |
|---|---|
| Linearizable reads, multi-region | **Strong** |
| Bound the staleness window | **Bounded staleness** |
| Default - read your own writes | **Session** |
| Order matters but staleness OK | **Consistent prefix** |
| Cheapest, no order guarantee | **Eventual** |

## Blob tier picker

| Pattern | Tier |
|---|---|
| Active reads | **Hot** |
| Cold backup, occasional read | **Cool** |
| Long retention, rare read | **Cold** |
| Compliance archive, hours to rehydrate | **Archive** |

## SAS picker

| Need | Pick |
|---|---|
| Long-lived, broad access | **Account SAS** (avoid if possible) |
| Revocable per-resource | **Service SAS** + **stored access policy** |
| User-scoped, Entra-signed, no shared key | **User delegation SAS** (preferred) |

## Auth flow picker

| Caller / context | Flow |
|---|---|
| Interactive web user | **Authorization Code + PKCE** |
| SPA | **Authorization Code + PKCE** (no secret) |
| Background daemon | **Client Credentials** |
| Mid-tier API calling another API as user | **On-Behalf-Of** |
| CLI on TV / IoT | **Device Code** |

## Messaging picker

| Need | Pick |
|---|---|
| Reactive event on resource change | **Event Grid** |
| Telemetry stream, Kafka clients | **Event Hubs** |
| Enterprise messaging, FIFO with sessions | **Service Bus queue** |
| Pub/sub with property filters | **Service Bus topic** |
| Cheap simple background jobs | **Storage Queue** |

## API Management policy quick map

| Goal | Policy |
|---|---|
| Validate Entra token | `validate-jwt` |
| Throttle by caller | `rate-limit-by-key` / `quota-by-key` |
| Cache GET response | `cache-lookup` + `cache-store` |
| Rewrite path / headers | `rewrite-uri` / `set-header` |
| Forward to backend with MI | `authentication-managed-identity` |
| Short-circuit response | `return-response` |
| Stitch a side-call | `send-request` |

## Application Insights instrumentation

| Stack | Best path |
|---|---|
| New .NET / Java / Node app | **OpenTelemetry distro** |
| App Service / Functions | **Auto-instrumentation** toggle |
| Existing classic .NET | **Application Insights SDK** |

---

[ Master Index](00-MASTER-INDEX.md)