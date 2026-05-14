# AZ-204 - Developing Solutions for Microsoft Azure

> Visual study guide. Concept-only. Exam retires **July 31, 2026** - prep accordingly.

## How to use this guide

1. Skim this index to map the five exam domains.
2. Open each domain page and study the Mermaid concept map.
3. Run through the **Exam Decision Reference** (cheatsheet) and **Flashcards**.
4. Practice with the **AI Copilot Quiz** launcher.
5. Verify on the official **Practice Assessment** before booking.

## Exam at a glance

| Item | Value |
|---|---|
| Code | AZ-204 |
| Title | Developing Solutions for Microsoft Azure |
| Role | Azure Developer Associate (Intermediate) |
| Duration | 100 minutes |
| Pass | 700 / 1000 |
| Cost | $165 USD |
| Languages | EN, JP, ZH-CN/TW, KO, FR, DE, ES, PT-BR, IT |
| Last updated | 14 Jan 2026 |
| Retirement | **31 Jul 2026** |

## The 5 Exam Domains - Mind Map

```mermaid
mindmap
  root((AZ-204))
    Compute Solutions
      Containers
        ACR Registry
        ACR Tasks Build
        ACI Container Instances
        Container Apps
        Dapr sidecars
        KEDA scale rules
        Revisions Ingress
      App Service
        Web Apps
        App Service Plans
        Deployment Slots
        Autoscale rules
        TLS Custom Domain
        Networking VNet Integration
        Hybrid Connections
      Azure Functions
        Triggers HTTP Timer
        Triggers Blob Queue
        Triggers Service Bus
        Triggers Event Grid Hub Cosmos
        Input Output Bindings
        Durable Functions
        Orchestrator Activity Entity
        Consumption Premium Dedicated
        host.json local.settings.json
    Storage Solutions
      Cosmos DB
        APIs SQL Mongo Cassandra
        Consistency Levels
        Partition Keys
        Change Feed
        RU Provisioning
        Indexing Policies
        Server-side TTL
      Blob Storage
        Block Append Page blobs
        Access Tiers Hot Cool Cold Archive
        Lifecycle Management
        SAS User Delegation Account Service
        Stored Access Policies
        AzCopy SDK REST
        Static Website Hosting
        Soft Delete Versioning
        CORS Settings
    Azure Security
      Microsoft Identity
        Entra ID Tenants
        App Registrations
        MSAL Library
        OAuth2 OpenID Connect
        Auth Code Client Credential
        On-behalf-of Flow
        Microsoft Graph SDK
        Scopes Permissions
      Managed Identity
        System Assigned
        User Assigned
        Federated Credentials
      Key Vault
        Secrets Keys Certificates
        Soft Delete Purge Protection
        Access Policies vs RBAC
        Key Vault References
        Rotation
      Application Security
        Encryption at rest
        Encryption in transit
        Cosmos always encrypted
        Storage CMK
    Monitor Troubleshoot
      Application Insights
        SDK Auto-instrumentation
        Sampling Strategies
        Live Metrics
        Availability Tests
        Application Map
        KQL Queries
        Workspace-based
      Azure Monitor
        Log Analytics
        Alerts Action Groups
        Metrics Diagnostic Settings
      Caching
        Azure Cache for Redis
        Tiers Basic Standard Premium Enterprise
        CDN Front Door
        Cache-aside Pattern
    Connect Services
      API Management
        Products APIs Operations
        Policies Inbound Backend Outbound On-error
        JWT Validation
        Rate Limit Quota
        Caching policies
        Subscriptions Keys
        Versions Revisions
      Event Driven
        Event Grid Topics Subscriptions
        Event Grid System Custom Partner
        Event Hubs Throughput Units
        Event Hubs Capture
        Consumer Groups
      Service Bus
        Queues vs Topics
        Sessions FIFO
        Dead Letter Queue
        Message Lock Duplicate Detect
        Filters Subscriptions
      Storage Queues
        AES 64KB messages
        Visibility Timeout
        Poison Queue
```

## Official Skills Weighting

```mermaid
pie title AZ-204 Skills Measured Midpoints
  "Compute Solutions" : 27.5
  "Storage Solutions" : 17.5
  "Azure Security" : 17.5
  "Monitor and Troubleshoot" : 7.5
  "Connect to Services" : 22.5
```

## Pages

| # | Page | Purpose |
|---|---|---|
| 01 | [Develop Azure compute solutions](01-compute.md) | Containers, App Service, Functions |
| 02 | [Develop for Azure storage](02-storage.md) | Cosmos DB, Blob Storage |
| 03 | [Implement Azure security](03-security.md) | Auth, Key Vault, Managed Identities |
| 04 | [Monitor, troubleshoot, optimize](04-monitor.md) | Application Insights |
| 05 | [Connect to services](05-connect.md) | APIM, Event Grid/Hubs, Service Bus, Queue |
| 05 | [Exam Decision Reference](05-exam-cheatsheet.md) | Pick-the-right-service tables |
| 06 | [Concept & Reference Index](06-references.md) | Cross-domain index |
| 07 | [Extra Concepts](07-extra-az204-concepts.md) | Edge cases & lesser-known knobs |
| 08 | [Microsoft Learn Summaries](08-learn-summaries.md) | Curated learning paths |
| 09 | [Architectures](09-arch-az204.md) | End-to-end developer patterns |
| 11 | [Microsoft Reference Library](11-microsoft-resources.md) | Official docs by service |
| 12 | [Glossary & Acronyms](12-glossary.md) | Terms and abbreviations |
| 13 | [Flashcards](13-flashcards.md) | Self-test prompts |
| 14 | [Common Pitfalls](14-pitfalls.md) | Trap patterns to avoid |
| 15 | [Hands-On Labs](15-hands-on-labs.md) | Build-it-yourself exercises |
| 16 | [Azure Architecture Center](16-architecture-center.md) | Reference architectures |
| 17 | [AI Copilot Quiz](17-copilot-quiz.md) | Free practice via Copilot/ChatGPT/Gemini/Claude |
| 99 | [Practice Assessment](99-practice-assessment.md) | Microsoft official |
| 99 | [Video Tutorials](99-video-tutorials.md) | Curated video list |

## Top study targets

- App Service deployment slots, autoscaling, TLS / app settings
- Functions triggers + bindings (input vs output) - Timer, Service Bus, HTTP, Blob, Cosmos
- Container Apps revisions, ingress, scale rules (KEDA)
- Cosmos DB consistency levels (Strong ' Eventual) - choose by use case
- Blob lifecycle policies, access tiers, SAS types (user delegation vs account vs service)
- Microsoft Identity Platform: confidential vs public client, MSAL flows, on-behalf-of
- Key Vault references in App Service / Functions, Managed Identity types (system vs user)
- Application Insights: SDK vs auto-instrumentation, sampling, KQL queries
- API Management policies (inbound, backend, outbound, on-error) - caching, JWT validation, rate-limit
- Event Grid vs Event Hubs vs Service Bus - when to use which