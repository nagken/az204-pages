# Flashcards

> Self-test prompts. Hover or scroll to reveal the answer.

<section class="fc-section" data-fc-title="All">
<div class="flashcard-grid">
  <div class="flashcard"><div class="fc-q">Q1. Which Functions hosting plan supports VNet integration AND scale-to-zero?</div><div class="fc-a">Flex Consumption (newer) supports VNet and scale-to-zero. Classic Consumption does not support VNet; Premium has VNet but pre-warmed (no scale-to-zero).</div></div>
  <div class="flashcard"><div class="fc-q">Q2. What is the Cosmos DB default consistency level?</div><div class="fc-a">Session - read your own writes within a session token; cheaper than Strong.</div></div>
  <div class="flashcard"><div class="fc-q">Q3. How do you revoke a service SAS that is already in use?</div><div class="fc-a">Reference a stored access policy when generating the SAS; deleting or modifying the policy revokes all SAS tokens that reference it.</div></div>
  <div class="flashcard"><div class="fc-q">Q4. What format does an App Service Key Vault reference take?</div><div class="fc-a"><code>@Microsoft.KeyVault(SecretUri=https://VAULT.vault.azure.net/secrets/NAME/VER)</code> or <code>@Microsoft.KeyVault(VaultName=...;SecretName=...)</code>. Resolved via the resource managed identity.</div></div>
  <div class="flashcard"><div class="fc-q">Q5. Which Cosmos change feed mode automatically scales across multiple consumers?</div><div class="fc-a">Push model via the Change Feed Processor library or the Azure Functions Cosmos DB trigger - it uses a lease container to coordinate.</div></div>
  <div class="flashcard"><div class="fc-q">Q6. Which OAuth flow does a daemon use to call an Azure REST API with no signed-in user?</div><div class="fc-a">Client Credentials. Token has app-only permissions (application scopes).</div></div>
  <div class="flashcard"><div class="fc-q">Q7. What is the maximum Storage Queue message size?</div><div class="fc-a">64 KB. For larger payloads use Service Bus (256 KB Standard, 100 MB Premium) or store the body in Blob and queue a pointer.</div></div>
  <div class="flashcard"><div class="fc-q">Q8. Name the four APIM policy sections.</div><div class="fc-a">inbound, backend, outbound, on-error.</div></div>
  <div class="flashcard"><div class="fc-q">Q9. Which APIM policy validates an Entra ID JWT signature and claims?</div><div class="fc-a"><code>validate-jwt</code> with <code>openid-config</code> URL and <code>required-claims</code>.</div></div>
  <div class="flashcard"><div class="fc-q">Q10. Which Event Grid schema is recommended for portability across clouds?</div><div class="fc-a">CloudEvents v1.0.</div></div>
  <div class="flashcard"><div class="fc-q">Q11. What is the difference between Event Grid and Event Hubs?</div><div class="fc-a">Event Grid is push-based reactive eventing for discrete events (millions per day). Event Hubs is pull-based streaming for telemetry (millions per second), Kafka-compatible, with offsets and consumer groups.</div></div>
  <div class="flashcard"><div class="fc-q">Q12. How does Service Bus PeekLock work?</div><div class="fc-a">Receive locks the message for LockDuration. The receiver must call Complete (delete), Abandon (release for retry), DeadLetter, or Defer before the lock expires.</div></div>
  <div class="flashcard"><div class="fc-q">Q13. What does Adaptive Sampling do in Application Insights?</div><div class="fc-a">Auto-adjusts the sampling rate to keep telemetry near a target items-per-second budget while preserving correlation between requests, dependencies, and exceptions.</div></div>
  <div class="flashcard"><div class="fc-q">Q14. What environment variable holds the Application Insights connection string?</div><div class="fc-a"><code>APPLICATIONINSIGHTS_CONNECTION_STRING</code>.</div></div>
  <div class="flashcard"><div class="fc-q">Q15. What is the difference between system-assigned and user-assigned managed identity?</div><div class="fc-a">System-assigned is created and deleted with the resource (1 per resource). User-assigned is a standalone resource that can be attached to many resources and survives resource deletion.</div></div>
  <div class="flashcard"><div class="fc-q">Q16. What flow is used by a web API to call a downstream API as the original user?</div><div class="fc-a">On-Behalf-Of (OBO).</div></div>
  <div class="flashcard"><div class="fc-q">Q17. How is a Cosmos partition key chosen safely?</div><div class="fc-a">High cardinality, even access distribution, used as a filter in most queries. Avoid attributes that grow unbounded per partition.</div></div>
  <div class="flashcard"><div class="fc-q">Q18. What APIM tier is needed for VNet integration with private backends?</div><div class="fc-a">Premium, or v2 SKUs (Standard v2 / Premium v2).</div></div>
  <div class="flashcard"><div class="fc-q">Q19. How does a deployment slot swap stay zero-downtime?</div><div class="fc-a">Target slot is warmed (apps started, requests sent to local URL) before the routing swap; configuration that is marked slot-specific stays put.</div></div>
  <div class="flashcard"><div class="fc-q">Q20. What is the purpose of a Container Apps revision?</div><div class="fc-a">Immutable snapshot of a container app version. Multiple revisions can run simultaneously for blue/green or canary releases via traffic weights.</div></div>
</div>
</section>

---

[ Master Index](00-MASTER-INDEX.md)