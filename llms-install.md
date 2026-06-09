# Install — OntoRamp Knowledge Cartographer (for AI agents)

You are an AI agent (e.g. Cline) setting up the **OntoRamp Knowledge Cartographer** MCP server. It is a **hosted, remote** server (Streamable HTTP). There is **nothing to clone, build, install, or run locally** — add one config entry pointing at the hosted endpoint with the user's API key.

## Step 1 — Ensure the user has a free API key

Ask the user for their OntoRamp API key (`or_free_…`). If they don't have one, tell them to get a free key — no credit card — at **https://ontoramp.com/mcp** (emailed). Do **not** invent a key.

## Step 2 — Add the server to the MCP config

In Cline that is `~/.cline/mcp.json` (CLI) or the Cline UI → MCP Servers → Configure. Merge into any existing `mcpServers`:

```json
{
  "mcpServers": {
    "ontoramp-knowledge-cartographer": {
      "url": "https://ontoramp-knowledge-cartographer.fly.dev/mcp",
      "headers": { "Authorization": "Bearer <USER_API_KEY>" },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Replace `<USER_API_KEY>` with the user's key. Transport is **Streamable HTTP**; do not set `command`/`args` (not a stdio server).

## Step 3 — Confirm reachability

```bash
curl https://ontoramp-knowledge-cartographer.fly.dev/health
```

Expect `{"status":"ok",...}`.

## Step 4 — Available tools

- `get_coverage_map` — domain knowledge coverage map (Free tier, read-only)
- `get_knowledge_health_score` — overall knowledge health score (Free tier, read-only)
- `detect_knowledge_gaps` — where coverage is thin/missing (Developer tier)
- `ingest_document` — add a document to the governed knowledge graph (Developer tier, **write — auth required**)
- `request_assessment` — request an Agentic Readiness Assessment (all tiers)

On the **free tier** the two read tools (`get_coverage_map`, `get_knowledge_health_score`) and `request_assessment` work; `ingest_document` and `detect_knowledge_gaps` return an upgrade message — that is expected, not an error. `ingest_document` never accepts unauthenticated writes by design.

## Notes

- No environment variables, dependencies, or local process.
- Bearer API key in the `Authorization` header (or `?api_key=` query param if headers are unavailable).
