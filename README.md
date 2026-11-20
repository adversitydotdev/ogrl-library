# OGRL Standard Library

The authoritative public repository for the shared **OGRL** (Open GRC Language) standard library as specified in [RFC 0001](https://ogrl.adversity.dev/rfcs/0001-object-model/) and [RFC 0002](https://ogrl.adversity.dev/rfcs/0002-tooling/).

Browse the published catalog at **[ogrl.adversity.dev/library](https://ogrl.adversity.dev/library/)**.

## Layout

All library objects live under `library/` so OGRL deployments can pull pinned revisions directly via Git tags (`library-v{version}` or `v{version}`) or commit hashes:

- `library/bundle.yaml` — Library manifest (`bundle--ogrl-library`)
- `library/framework/` — External framework metadata (`nist-sp-800-53-r5`, `nist-sp-800-171-r3`)
- `library/requirement/` — Normalized obligations including statement `parts`, `parameters`, and NIST assessment `objectives` / `methods`
- `library/mapping/` — Crosswalk mappings between controls and requirements (imported NIST links start as `review_status: draft`)
- `library/control/` — *(Upcoming)* Standard OGRL operational controls (`origin: standard`)
- `library/baseline/` — *(Upcoming)* Standard library baselines
- `library/test/` — *(Upcoming)* Standard library test specifications

## Regenerating & Validating

Generated NIST files should not be hand-edited. Regenerate and validate them using the [`ogrl`](https://github.com/adversitydotdev/ogrl-rs) CLI:

```bash
# Regenerate pinned NIST SP 800-53 Rev 5 and SP 800-171 Rev 3 catalogs (with assessment objectives)
ogrl import nist --out library

# Validate strict YAML 1.2 authoring rules, RFC 0001 schemas, and §7.20 graph constraints
ogrl lint library --profile library

# Verify deterministic canonical formatting
ogrl fmt library --check

# Print deterministic RFC 8785 SHA-256 projection digest
ogrl bundle digest library
```
