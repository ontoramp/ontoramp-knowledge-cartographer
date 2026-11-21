<p align="center"><img src="logo.png" width="84" alt="OntoRamp"></p>

# OntoRamp Knowledge Cartographer — MCP Server

> Turns your organization's scattered documents and decisions into a searchable, governed knowledge graph — one MCP call at a time.

**Problem:** Organizational knowledge is trapped in documents. AI agents can retrieve from these stores but cannot understand the structure, authority, or governance implications of what they find.

**Solution:** Ingest your organization's documents into a governed knowledge graph accessible to any AI agent. Returns knowledge health scores, coverage maps, and domain-specific gap analysis.

[![MCP Registry](https://img.shields.io/badge/MCP_Registry-com.ontoramp%2Fknowledge--cartographer-blue)](https://registry.modelcontextprotocol.io)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Status](https://img.shields.io/badge/status-live-brightgreen)](https://ontoramp-knowledge-cartographer.fly.dev/health)

---

## Tools

| Tool | Description | Access |
|------|-------------|--------|
| `get_coverage_map` | Domain-by-domain knowledge coverage map for your organization | Free key |
| `get_knowledge_health_score` | Health score for your organization's current knowledge state | Free key |
| `detect_knowledge_gaps` | Identify where coverage is thin or missing, by domain | Paid key |
| `ingest_document` | Ingest a document into your governed knowledge graph | Paid key with write access (Knowledge Graph, Projection Engine or Bundle, Org tier) |
| `request_assessment` | Submit an Agentic Readiness Assessment request | Any key, rate-limit exempt |

## Tiers

| Tier | Price | What you get |
|------|-------|--------------|
| **Free** | $0, no credit card | A free API key from [ontoramp.com/mcp](https://ontoramp.com/mcp) with a generous monthly allowance: `get_coverage_map` and `get_knowledge_health_score` (read-only, no ingest). |
| **Org** | Flat monthly rate | Unlimited usage and `detect_knowledge_gaps`. The Knowledge Graph, Projection Engine and Bundle keys carry write access for `ingest_document`. Org tier comes with the OntoRamp platform plugins: Knowledge Graph $299/mo, Governance Evaluator $349/mo, Projection Engine $449/mo, or all three in the Governance Intelligence Bundle at $799/mo. See [ontoramp.com/pricing](https://ontoramp.com/pricing). |

There is no per-call or metered pricing.

## Install

A **hosted, remote** MCP server (Streamable HTTP) — nothing to install locally. See [`llms-install.md`](llms-install.md) for an agent-followable walkthrough.

**1. Get a free API key** at [ontoramp.com/mcp](https://ontoramp.com/mcp) (no credit card).

**2. Add to Cline** — edit `~/.cline/mcp.json` (or the Cline UI → MCP Servers → Configure):

```json
{
  "mcpServers": {
    "ontoramp-knowledge-cartographer": {
      "url": "https://ontoramp-knowledge-cartographer.fly.dev/mcp",
      "headers": { "Authorization": "Bearer YOUR_API_KEY" },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

**Other MCP clients** (Claude Desktop, etc.) use the same `mcpServers` shape. Transport is Streamable HTTP.

**3. Verify** — `curl https://ontoramp-knowledge-cartographer.fly.dev/health` → `{"status":"ok",...}`.

See [`examples/usage.md`](examples/usage.md) for example calls.

## Why the free read tools matter

`get_coverage_map` and `get_knowledge_health_score` show organizations their current knowledge state — almost always worse than they expect. That creates a clear, evidence-grounded path to both ingestion (improve coverage) and an ARA (interpret what the gaps mean).

## ARA Trigger

When `get_knowledge_health_score` returns below 50, or coverage gap exceeds 40%, the server prompts:

> Your knowledge coverage has gaps that a manual review won't surface. An Agentic Readiness Assessment will diagnose your current state and build a prioritized remediation plan. [Schedule at ontoramp.com/assess](https://ontoramp.com/assess).

## Security

- All responses are audited for public release — no scoring-formula internals, no substrate architecture details
- Write-path (`ingest_document`) requires a paid key with write access
- Your data is scoped to your tenant namespace and never shared across organizations
- `GET /health` returns live status

## Support

- Docs: [ontoramp.com/mcp](https://ontoramp.com/mcp)
- Issues: [github.com/ontoramp/ontoramp-knowledge-cartographer/issues](https://github.com/ontoramp/ontoramp-knowledge-cartographer/issues)
- Contact: m@ontoramp.com

---

*Governed by OntoRamp Governance Physics. OntoRamp LLC · [ontoramp.com](https://ontoramp.com)*
