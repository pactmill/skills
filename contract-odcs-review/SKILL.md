---
name: contract-odcs-review
description: Review or author an Open Data Contract Standard (ODCS) YAML for a curated data product port.
---

# Contract ODCS review

## When to use

Authoring or reviewing an ODCS contract before merge, publish, or compile.

## Primary standard

- [ODCS](https://bitol-io.github.io/open-data-contract-standard/) (Bitol / LF AI & Data)

## Checklist (fail if any required item missing)

1. **Identity:** `apiVersion`, `id`, `name`, `version`, `status` present.  
2. **Schema:** At least one object with named properties; logical types set.  
3. **Keys:** Primary key / uniqueness called out for grain.  
4. **Quality:** ≥1 quality rule on critical columns (notNull, unique, or validValues).  
5. **SLA:** Freshness or completeness (or explicit “none — reason”).  
6. **Team:** Owner identifiable.  
7. **Servers / physical:** Physical name or server pointer if deployable.  
8. **Breaking change:** Version bump matches SemVer vs previous (major if incompatible type/removal).

## Agent instructions

- Prefer ODCS fields over inventing parallel YAML.  
- Use `customProperties` for feature parity / agent context — do not fork the standard casually.  
- Link the contract `id` from ODPS `outputPorts[].contractId` when a product descriptor exists.

## Verification

```bash
# Prefer official tooling when available:
# datacontract lint path/to/contract.odcs.yaml
# Or schema-validate against ODCS JSON Schema from Bitol.
test -f path/to/contract.odcs.yaml
```

**Fail:** lint/schema errors; missing owner; no quality on PK columns; silent type change without major version.
