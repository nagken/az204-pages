# AZ-204 Reference Architectures

> End-to-end developer-centric architectures stitched from AZ-204 services.

## 1. Web app + API + Cosmos with managed identity

```mermaid
flowchart LR
    User["Browser"] -->|HTTPS| Front["App Service<br/>Front-end"]
    Front -->|HTTPS + token| API["App Service<br/>REST API"]
    API -->|Cosmos SDK| Cosmos[(Cosmos DB<br/>Session consistency)]
    API -->|Key Vault refs| KV[(Key Vault)]
    Front -->|Connection string<br/>via KV ref| KV
    API -->|Managed Identity| KV
    Front -->|Auto-instrument| AI[(Application Insights)]
    API -->|Auto-instrument| AI
```

**Key choices** - Authorization Code + PKCE for the user flow, On-Behalf-Of from front-end App Service to API. Both apps use a system-assigned managed identity with `Key Vault Secrets User` role. Cosmos uses Session consistency. Application Insights via auto-instrumentation; OpenTelemetry distro could replace it.

## 2. Event-driven Functions pipeline

```mermaid
flowchart LR
    Source["Source system<br/>HTTP webhook"] -->|POST| EG["Event Grid<br/>custom topic"]
    EG -->|Push| Fn1["Function<br/>Event Grid trigger"]
    Fn1 -->|Output binding| SB["Service Bus<br/>queue"]
    SB --> Fn2["Function<br/>Service Bus trigger"]
    Fn2 -->|Cosmos output binding| Cosmos[(Cosmos DB)]
    Fn2 -.->|Failures| DLQ[(Service Bus DLQ)]
```

**Why two stages** - Event Grid for fan-out, Service Bus to buffer + provide DLQ + ordering. Functions Premium plan to keep latency low.

## 3. Container Apps microservices with Dapr

```mermaid
flowchart LR
    Ingress["External ingress<br/>HTTPS"] --> A["Container App A<br/>orders"]
    A -->|Dapr pubsub| B["Container App B<br/>shipping"]
    A -->|Dapr state| State[(State store<br/>Cosmos)]
    B -->|Dapr secrets| KV[(Key Vault)]
    A --> ACR[(Azure Container Registry)]
    B --> ACR
    A -->|Logs| LA[(Log Analytics)]
    B -->|Logs| LA
```

**Notes** - Container Apps environment shares the Log Analytics workspace + VNet. KEDA scales B from queue length; Dapr sidecar abstracts state and pub/sub.

## 4. APIM front door for backend APIs

```mermaid
flowchart LR
    Client["Client app"] -->|HTTPS<br/>subscription key + JWT| APIM["API Management"]
    APIM -->|"validate-jwt<br/>rate-limit-by-key<br/>cache-lookup"| APIM
    APIM -->|set-backend-service| Backend1["App Service<br/>API"]
    APIM -->|authentication-managed-identity| Backend2["Azure Functions"]
    APIM --> Cache[(Redis cache<br/>or internal)]
    APIM -->|Logs + metrics| LA[(Log Analytics)]
```

**Notes** - Inbound section validates JWT and applies rate-limit. Backend section sets the upstream service and authenticates with managed identity. Outbound section caches successful 200 responses.

## 5. Streaming telemetry into Event Hubs + Functions + Cosmos

```mermaid
flowchart LR
    Devices["IoT or App<br/>producers"] -->|AMQP / Kafka| EH["Event Hubs<br/>16 partitions"]
    EH -->|Capture| Blob[(Blob<br/>Avro archive)]
    EH --> Fn["Function<br/>Event Hubs trigger"]
    Fn --> Cosmos[(Cosmos DB<br/>analytics container)]
    Fn -->|Custom metric| AI[(Application Insights)]
```

**Notes** - Event Hubs Capture writes raw stream to Blob for replay. Function uses checkpoint container for at-least-once processing. Cosmos analytics container with autoscale RU.

---

[ Master Index](00-MASTER-INDEX.md)