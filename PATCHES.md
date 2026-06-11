# Compass patch stack (branch `compass-patches`)

Base: upstream `v0.5.1` (57ebffd). Build tag = `v0.5.1+compass.N`.
Workflow: /opt/compass/docs/plans/ibx-integration.md §4.
Fork: https://github.com/positronic-penguin/ibx (pushes from compass via
deploy key `~/.ssh/ibx-fork_ed25519`, ssh alias `github-ibx-fork`;
account-level ops via `gh` on viki01 as positronic-penguin).

| # | Commit | What | Why | Upstream status |
|---|--------|------|-----|-----------------|
| 1 | e602575 | build: pyo3 0.24 → 0.26 | pyo3-ffi 0.24 rejects CPython 3.14 (compass venv). Compiles clean, no source changes. | **PR open:** [#200](https://github.com/deepentropy/ibx/pull/200) (issue [#198](https://github.com/deepentropy/ibx/issues/198)), branch `pr/pyo3-python314` |
| 2 | 9d9d1b2 | fix: GTD orders rejected (good_till_date dropped + wrong 126/432 wire encoding) | `Order::attrs()` hardcoded `good_till: 0`; engine emitted 126 with space-separated timestamp. Every TIF=GTD order came back Inactive. Verified fix on paper acct: ack + broker-side auto-cancel at requested time. | **PR open:** [#201](https://github.com/deepentropy/ibx/pull/201) (issue [#199](https://github.com/deepentropy/ibx/issues/199)), branch `pr/gtd-expire-encoding` |

Permanent-local patches: none. Release-stamp commits (`pyproject.toml`
version) are fork-only and never upstreamed.

On upstream merge of either PR: next sync rebase drops the corresponding
local commit automatically (see plan §4 sync procedure), then rebuild,
run `scripts/ibx_spike.py` on paper, and re-vendor.
