---
name: data-product-readiness-assessment
description: Score Data Product Agent Readiness and map scores to allowed autonomy (observe → gate → agent tools → missions).
---

# Data Product Agent Readiness assessment

## When to use

Before enabling agents on a data product, or as Offer #1 (assessment engagement).

## Inspiration

Factory.com [Agent Readiness](https://docs.factory.com/agent-readiness/overview) scores **repos**. This skill scores **data products**.

## Scorecard (0–2 each; document evidence)

| Pillar | 0 | 1 | 2 |
|--------|---|---|---|
| Schema stability | Frequent breaks | Occasional; SemVer | ≥30d no breaking change |
| Quality + SLA | None | Partial monitors | Contracted + enforced |
| Ownership | Unclear | Named but slow | Owner + support channel |
| Lineage | None | Partial | Critical jobs emit OpenLineage |
| PII / policy | Unknown | Tagged | Purpose limits + access controls |
| Agent eval harness | None | Ad-hoc | Golden traces in CI |
| Side-effect inventory | Unknown | Documented | Enforced on MCP ports |

**Level unlock (provisional):** pass ≥80% of prior level’s pillars to unlock the next autonomy tier.

## Autonomy ceiling

| Level | Allowed |
|-------|---------|
| L0 Observe | Monitor only |
| L1 Warn | Alerts |
| L2 Gate | CI / promote blocks |
| L3 Auto-remediate | Quarantine / demote with policy |
| L4 Supervised agents | Read-only tools; write only with approval |
| L5 Missions | Multi-agent only if L4 green + human outcome owner |

## Agent instructions

- Store scorecard on ODPS `customProperties` or companion YAML — do not invent a parallel product identity.  
- Never enable write MCP tools below L4.  
- Output a 90-day backlog ranked by pillar gaps.

## Verification

Deliverable must include: scored table with evidence links, recommended autonomy level, and backlog. **Fail** if autonomy recommendation exceeds evidence.
