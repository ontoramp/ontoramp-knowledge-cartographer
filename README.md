# OntoRamp Knowledge Cartographer — MCP Server

> Turns your organization's scattered documents and decisions into a searchable, governed knowledge graph — one MCP call at a time.

**Problem:** Organizational knowledge is trapped in documents. AI agents can retrieve from these stores but cannot understand the structure, authority, or governance implications of what they find.

**Solution:** Ingest your organization's documents into a governed knowledge graph accessible to any AI agent. Returns knowledge health scores, coverage maps, and domain-specific gap analysis.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.ontoramp%2Fknowledge--cartographer-blue)](https://registry.modelcontextprotocol.io)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

---

## Tools

| Tool | Description | Tier |
|------|-------------|------|
| `get_coverage_map` | Return a domain-by-domain knowledge coverage map for your organization | Free |
| `get_knowledge_health_score` | Return a health score for your organization's current knowledge state | Free |
| `ingest_document` | Ingest a document into your organization's governed knowledge graph | Developer+ |

## Tiers

| Tier | Price | Limits | Features |
|------|-------|--------|----------|
| **Free** | — (no credit card) | Unlimited reads | `get_coverage_map` + `get_knowledge_health_score` (read-only, no ingest) |
| **Developer** | $0.015 read / $0.05 ingest | Unlimited | `ingest_document` (auth required) + all read tools · Staging queue |
| **Org** | $249/mo flat | Unlimited reads, 500 ingest/mo | Full provenance chains · ARA pre-population from coverage map |

## Quickstart

```json
{
  "mcpServers": {
    "ontoramp-knowledge-cartographer": {
      "type": "http",
      "url": "https://ontoramp-knowledge-cartographer.fly.dev/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

Get your free API key at [ontoramp.com/mcp](https://ontoramp.com/mcp).

## Why Free Read Tools Matter

The free tier `get_coverage_map` and `get_knowledge_health_score` show organizations their current knowledge state — almost always worse than they expect. This creates a clear, evidence-grounded path to both ingestion (improve coverage) and an ARA (interpret what the gaps mean for your AI program).

## ARA Trigger

When `get_knowledge_health_score` returns below 50, or coverage gap exceeds 40%, the server prompts:

> Your knowledge coverage has gaps that a manual review won't surface. An Agentic Readiness Assessment will diagnose your current state and build a prioritized remediation plan. [Schedule at ontoramp.com/assessment](https://ontoramp.com/assessment).

## Security

- All responses are SO-24 audited — no scoring-formula internals, no substrate architecture details
- Write-path (`ingest_document`) requires Developer or Org tier authentication
- Your data is scoped to your tenant namespace and never shared across organizations
- `GET https://ontoramp-knowledge-cartographer.fly.dev/health` returns live status

## Support

- Docs: [ontoramp.com/mcp](https://ontoramp.com/mcp)
- Issues: [github.com/MatthewDavisAIArchitect/ontoramp-knowledge-cartographer/issues](https://github.com/MatthewDavisAIArchitect/ontoramp-knowledge-cartographer/issues)
- Contact: m@ontoramp.com

---

*Governed by the Davis Canon — SSOT. OntoRamp LLC · [ontoramp.com](https://ontoramp.com)*
