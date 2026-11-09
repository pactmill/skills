---
name: mcp-port-policy
description: Define policy for exposing a data product output port as an MCP tool (side effects, sensitivity, schemas).
---

# MCP port policy

## When to use

Publishing or reviewing an MCP tool backed by a curated data product (ODCS/ODPS).

## Primary references

- [MCP specification](https://modelcontextprotocol.io/)  
- [OWASP MCP Security Testing Guide](https://github.com/OWASP/MCP-Security-Testing-Guide)

## Required annotations (on port or tool descriptor)

| Field | Allowed values / notes |
|-------|------------------------|
| `sideEffectClass` | `read-only` \| `write` \| `destructive` |
| `dataSensitivityCeiling` | e.g. public / internal / confidential / restricted |
| `inputSchema` | JSON Schema; required fields explicit |
| `contractId` | ODCS id for the backing data |
| `productId` | ODPS id |
| `approvalTier` | none / human-before-write / human-before-destructive |
| `costOrQpsCeiling` | optional but recommended |

## Rules

1. Default **deny** write/destructive tools.  
2. Never expose PII columns in tool output unless purpose-limited and approved.  
3. Readiness level must allow the side-effect class (see readiness assessment skill).  
4. Golden-trace evals recommended before production agent use.

## Agent instructions

- Generate MCP `inputSchema` from ODCS properties listed as inputs only.  
- Set `readOnlyHint` true iff `sideEffectClass=read-only`.  
- Refuse to add write tools to products below readiness gate for writes.

## Verification

```bash
# Ensure tool JSON declares sideEffectClass and contractId
python3 -c "import json,sys; t=json.load(open(sys.argv[1])); assert t.get('annotations',{}).get('sideEffectClass'); assert t.get('annotations',{}).get('contractId')" path/to/mcp_tool.json
```

**Fail:** MCP tool without side-effect class; write tool on a product with readiness &lt; write threshold.
