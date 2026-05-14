# Hands-on Labs

> Build-it-yourself exercises that map to the AZ-204 outline. Each lab uses Azure CLI, Bicep, or the SDK and is intended to fit in 30-60 minutes.

## Lab 1 - App Service web app with deployment slot

1. `az appservice plan create -g rg-az204 -n plan-az204 --sku S1`.
2. `az webapp create -g rg-az204 -p plan-az204 -n web-az204-<rand> --runtime "DOTNETCORE:8.0"`.
3. `az webapp deployment slot create -g rg-az204 -n web-az204-<rand> --slot staging`.
4. ZIP-deploy a Hello World to staging, verify the staging URL.
5. `az webapp deployment slot swap -g rg-az204 -n web-az204-<rand> --slot staging`.
6. Inspect HTTP response headers; rollback by swapping again.

## Lab 2 - Functions with HTTP + Cosmos output binding

1. `func init` then `func new` (HTTP trigger).
2. Add a Cosmos DB output binding in `function.json` (Python/JS) or attribute (.NET).
3. `func azure functionapp publish` to a Consumption-plan Function App.
4. POST a JSON body, verify item written to Cosmos.

## Lab 3 - Cosmos DB change feed processed by Functions

1. Create a Cosmos NoSQL container with a leases container.
2. `func new` and pick **Cosmos DB trigger**; bind to the source container with leases.
3. Insert items via Data Explorer; observe Function executions.
4. Add a second Function with the same lease container - see partition rebalancing in logs.

## Lab 4 - Blob lifecycle to Cool then Archive

1. `az storage account create` (StorageV2 + Hot default).
2. Upload sample blobs.
3. Apply a JSON lifecycle policy: tier to Cool after 30 days, Archive after 180, delete after 365.
4. Use **Last access time tracking** and rerun.

## Lab 5 - Managed identity to Key Vault from App Service

1. `az webapp identity assign -g rg-az204 -n <web>` (system-assigned).
2. `az role assignment create --role "Key Vault Secrets User" --assignee <principal-id> --scope <kv-id>`.
3. Add app setting: `MY_SECRET=@Microsoft.KeyVault(SecretUri=https://<kv>.vault.azure.net/secrets/<name>)`.
4. Restart; read the env var in code, log it (then remove the log!).

## Lab 6 - APIM with validate-jwt and rate-limit

1. `az apim create -g rg-az204 -n apim-az204-<rand> --sku-name Consumption --publisher-name "AZ-204" --publisher-email a@b.com`.
2. Import an OpenAPI spec.
3. Add inbound policy:
   ```xml
   <validate-jwt header-name="Authorization" failed-validation-httpcode="401">
     <openid-config url="https://login.microsoftonline.com/<tenant>/v2.0/.well-known/openid-configuration" />
     <required-claims>
       <claim name="aud"><value>api://your-app</value></claim>
     </required-claims>
   </validate-jwt>
   <rate-limit-by-key calls="60" renewal-period="60" counter-key="@(context.Subscription.Id)" />
   ```
4. Test with and without a valid token; observe 401 / 429.

## Lab 7 - Service Bus queue with dead-letter

1. `az servicebus namespace create -g rg-az204 -n sb-az204-<rand> --sku Standard`.
2. Create a queue with `max-delivery-count=3`.
3. Send a message; receive with PeekLock; abandon repeatedly; observe message in DLQ.

## Lab 8 - Application Insights with OpenTelemetry

1. Add the **Azure Monitor OpenTelemetry distro** package to your app.
2. Set `APPLICATIONINSIGHTS_CONNECTION_STRING`.
3. Generate traffic; open **Transaction Search**, **Application Map**, **Live Metrics**.
4. Add an `ITelemetryProcessor` that scrubs the `Authorization` header from request telemetry.

---

[ Master Index](00-MASTER-INDEX.md)