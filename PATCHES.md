# Compass patch stack (branch `compass-patches`)

Base: upstream `v0.5.1` (57ebffd). Build tag = `v0.5.1+compass.N`.
Workflow: /opt/compass/docs/plans/ibx-integration.md §4.

| # | Commit | What | Why | Upstream status |
|---|--------|------|-----|-----------------|
| 1 | e602575 | build: pyo3 0.24 → 0.26 | pyo3-ffi 0.24 rejects CPython 3.14 (compass venv). Compiles clean, no source changes. | **pending-upstream** — TODO: file issue + PR |
| 2 | 9d9d1b2 | fix: GTD orders rejected (good_till_date dropped + wrong 126/432 wire encoding) | `Order::attrs()` hardcoded `good_till: 0`; engine emitted 126 with space-separated timestamp. Every TIF=GTD order came back Inactive. Verified fix on paper acct: ack + broker-side auto-cancel at requested time. | **pending-upstream** — TODO: file issue + PR (reference rejection strings: 'Message must contain field # 432', 'Invalid value in field # 126/432') |

Permanent-local patches: none. Release-stamp commits (`pyproject.toml`
version) are fork-only and never upstreamed.

Push + PR prerequisites (not yet done on this box): GitHub fork under
Ryan's account, `gh` CLI auth or SSH key. Until then patches live only
in this local clone — **do not delete ~/src/ibx**.
