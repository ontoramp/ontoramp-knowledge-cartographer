# Usage examples — OntoRamp Knowledge Cartographer

Once connected (see [`../llms-install.md`](../llms-install.md)), an agent can call these tools. Inputs are realistic; outputs are described conceptually (your organization's real knowledge graph determines the response).

## `get_coverage_map` *(Free)*

See, domain by domain, how much organizational knowledge is actually captured.

```jsonc
{ "name": "get_coverage_map", "arguments": {}}
```

Returns a coverage map across governance/architecture domains — where knowledge is well-covered and where it's thin.

## `get_knowledge_health_score` *(Free)*

Get a single health score for the current knowledge state.

```jsonc
{ "name": "get_knowledge_health_score", "arguments": {}}
```

Returns an overall health score. Below ~50 (or coverage gap > 40%) the server surfaces an Agentic Readiness Assessment CTA.

## `detect_knowledge_gaps` *(Developer)*

Pinpoint where coverage is missing so ingestion can be targeted.

```jsonc
{ "name": "detect_knowledge_gaps", "arguments": {
  "domain": "SECURITY"
}}
```

Returns the specific gaps in that domain — what's undocumented or under-covered.

## `ingest_document` *(Developer — write, auth required)*

Add a document to the governed knowledge graph.

```jsonc
{ "name": "ingest_document", "arguments": {
  "title": "Data Retention Policy v3",
  "content": "...document text..."
}}
```

Returns an ingestion confirmation; the document is chunked, embedded, and attached to your graph with provenance.

## `request_assessment` *(all tiers, rate-limit exempt)*

```jsonc
{ "name": "request_assessment", "arguments": {
  "context": "Knowledge readiness review ahead of an agent rollout"
}}
```

Returns a confirmation; the OntoRamp team follows up.

---

**Tiers at a glance:** Free → `get_coverage_map`, `get_knowledge_health_score` (reads) + `request_assessment`, unlimited reads. Developer → `ingest_document` + `detect_knowledge_gaps`. Get a free key at [ontoramp.com/mcp](https://ontoramp.com/mcp).
