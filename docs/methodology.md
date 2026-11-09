# Pactmill delivery methodology

## Principles

1. **Contracts as source of truth** — ODCS/ODPS (and OpenAPI/MCP for ports), not wiki pages.  
2. **Compile into existing tools** — dbt, GX/Soda, Schema Registry, CI; do not rip-replace.  
3. **Autonomy is earned** — Data Product Agent Readiness gates what agents may do.  
4. **AI-assisted, human-owned** — agents draft; gates and humans decide.  
5. **A rule without verification is not a gate.**

## Engagement loop

```text
Discover → Assess readiness → Encode contracts → Compile & CI →
Optional MCP ports → Monitor → New contract tests from incidents
```

## Working with coding agents

| Allowed | Not allowed without gates |
|---------|---------------------------|
| Draft ODCS/ODPS from examples | Silent breaking schema changes |
| Generate expectations / stubs | Production write MCP tools |
| Open PRs with checklists | Skip readiness for “just a demo” |

Use starter skills in this repo on every PR that touches contracts or agent ports.

## Artifacts we leave behind

- Versioned contracts in git  
- CI workflows  
- Readiness scorecard  
- Skills installed in the client’s agent environment  
- Short ADR for major architecture choices  

## Privacy

Client names, data, and private runbooks stay out of public repos. Public labs use synthetic fixtures only.
