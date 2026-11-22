# OGRL Standard Library

The authoritative public repository for the shared **OGRL** (Open GRC Language) standard library as specified in [RFC 0001](https://ogrl.adversity.dev/rfcs/0001-object-model/) and [RFC 0002](https://ogrl.adversity.dev/rfcs/0002-tooling/).

Browse the published catalog at **[ogrl.adversity.dev/library](https://ogrl.adversity.dev/library/)**.

## Layout

All library objects live under `library/` so OGRL deployments can pull pinned revisions directly via Git tags (`library-v{version}`) or commit hashes:

- `library/bundle.yaml` — Library manifest (`bundle--ogrl-library`)
- `library/framework/` — External framework metadata:
  - **Public-domain (`reproduction: permitted`)**: NIST SP 800-53 Rev 5, NIST SP 800-171 Rev 3
  - **Citation-only (`reproduction: citation-only`)**: AICPA SOC 2 Trust Services Criteria (2017/2022), ISO/IEC 27001:2022 (identifiers and external citations only; no copyrighted standard prose per RFC 0001 §10)
- `library/requirement/` — Normalized obligations including statement `parts`, `parameters`, and NIST assessment `objectives` / `methods`
- `library/control/` — Standard OGRL operational controls (`origin: standard`) with configurable parameters, statements, objectives, and guidance
- `library/test/` — Standard library test specifications (`required: true`) linked to controls and NIST assessment objectives
- `library/mapping/` — Reviewed `control → requirement` crosswalks (with `#part` fragment targets and `parameter_map` bindings) alongside imported NIST `requirement → requirement` draft links
- `library/baseline/` — Library baselines (`ogrl-core`, `ogrl-soc2`, `ogrl-iso27001`, `ogrl-nist-800-171-r3`). `ogrl-soc2` selects 113 standard controls covering all 61 SOC 2 Trust Services Criteria (Security, Availability, Confidentiality, Processing Integrity, and Privacy).

## AI-Derived Content Disclaimer

Most standard controls and their crosswalks were drafted with AI assistance (Anthropic Claude). That includes the `ogrl-soc2` control set and its `control → requirement` mappings to NIST SP 800-53 Rev 5 and the SOC 2 Trust Services Criteria. The library maintainers published these mappings as `review_status: reviewed`. A qualified assessor has not validated each one individually.

Treat the controls and mappings as a starting point, not as audit or legal advice. Before you rely on them, check the control statements, mapping relationships, and coverage claims against the official AICPA and NIST publications and with your auditor. Corrections are welcome as pull requests.

## Regenerating & Validating

Generated NIST files under `library/requirement/nist-*` and `library/mapping/nist-*` should not be hand-edited. Regenerate and validate using the [`ogrl`](https://github.com/adversitydotdev/ogrl-rs) CLI:

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
