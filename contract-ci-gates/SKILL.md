---
name: contract-ci-gates
description: Add CI that fails on breaking ODCS schema changes and keeps compile artifacts in sync.
---

# Contract CI gates

## When to use

Wiring contracts into GitHub Actions / GitLab CI for a data product or the Pactmill compiler.

## Goals

- Reject **breaking** schema changes on protected branches.  
- Optionally recompile expectations / JSON Schema / MCP stubs on every contract change.  
- Prefer integrating [datacontract-cli](https://cli.datacontract.com/) over reinventing export.

## Minimum gate set

| Gate | Fail when |
|------|-----------|
| Lint / schema validate | Invalid ODCS |
| Breaking diff | Removed property or incompatible `logicalType` change |
| Artifact drift (optional) | Committed compile outputs out of date vs sources |

## Agent instructions

1. Diff `before` (main) vs `after` (PR) ODCS files.  
2. For each property in `before`: if missing in `after` → break; if `logicalType` changed → break.  
3. Exit non-zero on any break.  
4. Do not auto-bump major versions without human confirmation.

## Verification (lab / spike pattern)

```bash
# Example using Pactmill labs hello-contract:
PYTHONPATH=. python3 -m hello_contract check-breaking \
  --before fixtures/baseline.odcs.yaml \
  --after fixtures/candidate.odcs.yaml
# expect exit 1 on breaking changes
```

**Fail:** CI green while a column type changed without a major SemVer bump and changelog note.
