# Extra AZ-204 Concepts

> Lesser-known knobs and edge cases that show up in exam questions.

## Compute edges

- **Always On** for App Service prevents idle unloads (off by default on Free/Shared).
- **`functionTimeout`** in `host.json` caps Functions execution. Default Consumption = 5 min, max 10 min. Premium / Dedicated allow up to 60 min and unbounded respectively.
- **Functions scale controller** uses **trigger-specific signals** (queue length, event hub backlog) rather than CPU.
- **Container Apps single revision mode** auto-deactivates the previous revision; **multiple revision mode** keeps all and routes by traffic weight.
- **App Service ZIP deploy** with `WEBSITE_RUN_FROM_PACKAGE` accepts a SAS URL - useful for large packages.
- **Deployment center** wires CI/CD to GitHub, Azure DevOps, or external repos. Uses managed identity for ACR pull from `AcrPull` role.

## Storage edges

- **Cosmos DB autoscale** lets you set max RU/s; min is 10% of max, can be raised but not lowered below the highest historical max.
- **Cosmos DB Time-To-Live (TTL)** on container or item - `_ts` based; TTL=-1 means disabled, TTL=0 means immediate expiry on write.
- **Cosmos request charge** is in the `x-ms-request-charge` response header; surface it during testing.
- **Blob immutability policies** - time-based or legal hold; protect WORM compliance scenarios.
- **Blob versioning + soft delete** - enabled on the account; soft-deleted versions can be undeleted within retention.
- **Blob index tags** allow query via `findBlobsByTags` and lifecycle filtering by `blobIndexMatch`.

## Security edges

- **Federated credentials** allow GitHub Actions / Kubernetes / other IdPs to impersonate an Entra app without a secret.
- **Workload identity federation** for managed identity in AKS / GitHub Actions.
- **Conditional access** does not run for client-credentials flow without **continuous access evaluation** support.
- **Key Vault soft delete** is on by default and cannot be disabled. Purge protection adds a non-purgeable retention window.
- **Key Vault firewall** with "Allow trusted Microsoft services" exposes a small set of services; managed identity from a separate subscription typically still needs Private Endpoint.

## Monitor edges

- **Workspace-based Application Insights** stores telemetry in Log Analytics - required for new resources.
- **`ITelemetryProcessor`** lets you scrub or drop telemetry before send.
- **`ITelemetryInitializer`** adds custom properties to every item (e.g. user id, build version).
- **Smart detection** uses ML to surface anomalies; sensitivity is tunable.

## Connect edges

- **APIM revisions** vs **versions** - revisions are non-breaking iterations of the same version; versions are breaking changes (path/header/query).
- **APIM `set-backend-service` with backend entity** - reusable backend with credentials reference.
- **Event Grid topic event TTL** - 24 hours, retry until either success or DLQ.
- **Event Hubs `epoch`** receiver fences out other receivers on the same partition; non-epoch allows up to 5.
- **Service Bus message size** - Standard tier 256 KB body; Premium up to 100 MB.
- **Service Bus auto-forward** chains queues/subscriptions inside the namespace.
- **Service Bus `transactionality`** spans only the same namespace and entity (or via `via` for cross-entity send).

---

[ Master Index](00-MASTER-INDEX.md)