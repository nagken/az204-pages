# Common Pitfalls

> Trap patterns that show up in exam questions and real projects.

## Compute

- **Slot settings sticky** - a setting marked Deployment slot setting stays with the slot during swap. Use it for connection strings that differ between staging and production.
- **`WEBSITE_RUN_FROM_PACKAGE=1` makes wwwroot read-only** - kudu console writes are silently lost.
- **Functions cold start** on Consumption plan - picking Consumption for a chatty health endpoint is wrong; pick Premium or Flex Consumption.
- **Durable orchestrator non-determinism** - `DateTime.Now`, `Guid.NewGuid()`, random - must use `context.CurrentUtcDateTime` and `context.NewGuid()`.
- **Mixing in-process and isolated worker** Functions models in C# - different DI and package set.
- **App Service plan tier mismatch** - Free/Shared cannot use slots, scale-out, or VNet. Standard or above for production.

## Storage

- **Wrong partition key** in Cosmos - caps throughput at 10k RU/s per logical partition; expensive to fix later.
- **Strong consistency on multi-region writes** - fails to provision; use Bounded staleness.
- **Cosmos change feed missing deletes** - only inserts and updates; soft-delete with TTL on a `deletedAt` flag if you need them.
- **Archive tier is one-way** - rehydration takes 1-15 hours.
- **Blob lifecycle on access time** requires `lastAccessTimeTracking` enabled on the account.
- **Account SAS with long expiry** - leaked URL is full account access until expiry; use User Delegation SAS.
- **Forgetting to refresh session token** in Cosmos - apps reading from a different replica see stale data.

## Security

- **Client secret in source control** - use federated credentials + managed identity, or Key Vault.
- **Delegated vs application** permissions confusion - daemons need application scope.
- **Forgot RBAC on Key Vault** - managed identity has access policies but the vault is in RBAC mode (or vice versa).
- **v1.0 vs v2.0 endpoint** mismatch - `aud` claim does not match expected.
- **`User.Read.All` requires admin consent** - `User.Read` is enough to read the signed-in user.
- **MSAL public client storing a secret** - public clients cannot keep secrets; use PKCE.

## Monitor

- **`APPINSIGHTS_INSTRUMENTATIONKEY`** is deprecated - set `APPLICATIONINSIGHTS_CONNECTION_STRING`.
- **Both SDK and auto-instrumentation** enabled - telemetry duplicated and confused.
- **No `cloud_RoleName`** - application map merges all services.
- **Sampling disabled with no daily cap** - runaway ingestion cost.
- **Metric alert on a custom log signal** - must be a log alert with KQL.

## Connect

- **APIM secrets in policy XML** - use named values with Key Vault references.
- **`validate-jwt` without `required-claims`** - accepts any valid issuer token.
- **Storage Queue for over 64 KB** - switch to Service Bus.
- **Event Grid for ordering** - use Event Hubs (per-partition order) or Service Bus sessions.
- **Service Bus message lock** - forgetting to call `Complete` causes redelivery; abandon on transient errors increments delivery count.
- **APIM tier without VNet** - only Premium or v2 SKUs support VNet integration for private backends.
- **Event Hubs partition count immutable on Standard** - only Premium / Dedicated allow later changes.

---

[ Master Index](00-MASTER-INDEX.md)