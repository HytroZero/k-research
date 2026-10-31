# Minimal MCP Contract

The MCP server should expose reusable data capabilities, not encode every research workflow as a tool. Skills own the process and judgment; MCP owns retrieval and persistence.

Tool names below are illustrative. A host may expose equivalent capabilities under different names. Skills should inspect available tools and adapt rather than assume every name exists.

## Recommended tools

| Tool | Input | Output |
|---|---|---|
| `search_papers` | query, filters, date range, limit | ranked paper records with stable IDs and provenance |
| `fetch_paper` | paper ID, sections or full-text preference | metadata, abstract/full text, section locators, access status |
| `search_citation_context` | paper ID or claim, direction, depth | cited-by/cites/related-paper records with relationship type |
| `query_research_graph` | project ID, entity IDs, relation filters | connected papers, claims, evidence, hypotheses, decisions |
| `read_research_artifact` | project ID, artifact ID, version | canonical artifact |
| `write_research_artifact` | project ID, artifact payload, expected version | created or updated artifact ID and version |
| `append_research_event` | project ID, event payload | immutable event ID |
| `list_research_artifacts` | project ID, type, status, pagination | artifact summaries |

## Recommended Resources

- `research://projects/{project_id}`
- `research://projects/{project_id}/papers/{paper_id}`
- `research://projects/{project_id}/hypotheses/{hypothesis_id}`
- `research://projects/{project_id}/evidence/{evidence_id}`
- `research://projects/{project_id}/history`

Resources should be read-oriented snapshots. Mutations should use tools with explicit inputs and version checks.

## Design requirements

1. **Stable identifiers:** papers, claims, evidence, hypotheses, and decisions need durable IDs.
2. **Source provenance:** every retrieved paper and evidence record carries a canonical source and retrieval metadata.
3. **Version checks:** writes should support optimistic concurrency, for example `expected_version`.
4. **Decision traceability:** retain meaningful decisions and their reasons. Backend events may carry these changes when needed by a consumer; they do not require local event logs, snapshots, or historical file exports. Follow [Project Layout](PROJECT-LAYOUT.md) for local artifacts.
5. **Idempotency:** event writes should accept an idempotency key where retries are possible.
6. **Pagination:** paper and artifact listings must be paginated.
7. **Explicit access state:** distinguish full text, abstract only, metadata only, inaccessible, and unverified.
8. **No invented completeness:** a search result set must expose its query, filters, and any known coverage limitations.

## Deliberately out of scope

Do not add MCP tools for:
- running shell commands or SSH sessions;
- provisioning GPUs or managing compute budgets;
- editing code or launching experiments;
- writing full papers or formatting submissions.

An external execution agent can return structured experiment observations through `append_research_event` or `write_research_artifact`. The research skills then interpret those observations.
