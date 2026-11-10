# paper5-memory-architectures

[![CI](https://github.com/aidless/paper5-memory-architectures/actions/workflows/ci.yml/badge.svg)](https://github.com/aidless/paper5-memory-architectures/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)  [![Data](https://img.shields.io/badge/data-CC--BY--4.0-lightgrey.svg)](LICENSE-DATA)

## What this repository is (定位)

Reserved publication slot for **PAPER-E — "Memory-Architecture Bias Propagation under
Controlled Contamination"** (memory-architectures line). This repository currently holds the
**governance baseline and the pointer**, not the manuscript: it is a named, versioned address
that PAPER-E will be published into.

## Honest status (真实状态)

**PAPER-E materials are not produced inside this repository yet.** As of the 2026-11-09 audit
the tree contains only the governance files listed under *Repository layout* below — there is
no `main.tex`, no `evidence/`, and no analysis code. Searched: a single branch `main`, no
`docs/`, no `evidence/`, and no tracked `.py` sources.

The actual PAPER-E research artifact does exist — it lives in a **sibling** repository, which
is its real home today. This repository does not fork or duplicate it (duplicating a frozen
evidence snapshot would break its SHA-256 manifest); it stays a pointer until the manuscript
is consolidated here.

| Where | What it holds | Verified on 2026-11-09 |
|---|---|---|
| [`memory-architecture-bias`](https://github.com/aidless/memory-architecture-bias) | Public evidence snapshot: 18-cell grid harness, protocol runners, analysis scripts, `source/verify_p5.py`, and `evidence/` archives with a per-file SHA-256 manifest | `source/verify_p5.py` present at 1,157 lines; the sibling README records its self-audit status as 0 HIGH / 0 MEDIUM / 4 LOW |
| [`loop-engineering`](https://github.com/aidless/loop-engineering) | Cross-paper registry that tracks PAPER-E | repository present and reachable |

## Roadmap (后续计划)

- [x] Reserve the slot with a full governance baseline (LICENSE + LICENSE-DATA, SECURITY, CONTRIBUTING, SUPPORT, CODEOWNERS, dependabot, CI, issue/PR templates, `.editorconfig`).
- [x] Point the slot at the live evidence home (`memory-architecture-bias`).
- [ ] **Decide the consolidation target for the manuscript + evidence** — this repo vs. `memory-architecture-bias`. Not yet decided.
- [ ] If consolidated here: import `main.tex`, the `evidence/` tree with its SHA-256 manifest, and the analysis harness, then wire `verify_p5.py` into CI as a required job.
- [ ] Publish a citable release once the manuscript PDF is frozen.

## Quickstart (what you can run here today)

There is no research code in this repository, so the only runnable check is the same
governance gate CI runs. Both commands below are offline and dependency-free:

```bash
git clone https://github.com/aidless/paper5-memory-architectures.git && cd paper5-memory-architectures

# 1) Reproduce CI's relative-Markdown-link check locally (identical to .github/workflows/ci.yml)
python3 - <<'PY'
import pathlib, re, sys
bad = []
for md in pathlib.Path('.').rglob('*.md'):
    if '.git' in md.parts:
        continue
    text = md.read_text(encoding='utf-8', errors='replace')
    for m in re.finditer(r'\]\(([^)#][^)]*)\)', text):
        t = m.group(1).split('#')[0].strip()
        if not t or t.startswith(('http://', 'https://', 'mailto:')):
            continue
        if not (md.parent / t).exists():
            bad.append(f'{md}: {t}')
print('broken relative links:', bad) ; sys.exit(1 if bad else 0)
PY

# 2) Confirm the pointer targets are reachable
git ls-remote https://github.com/aidless/memory-architecture-bias.git HEAD
git ls-remote https://github.com/aidless/loop-engineering.git HEAD
```

## Repository layout (结构导览)

| Path | Contents |
|---|---|
| `README.md` | this page — positioning, honest status, roadmap |
| `STATUS.md` | one-line status (`reserved placeholder`) |
| `LICENSE` / `LICENSE-DATA` | MIT for code/governance; CC-BY-4.0 for any data that lands here |
| `CHANGELOG.md` | Keep-a-Changelog history |
| `SECURITY.md`, `CONTRIBUTING.md`, `SUPPORT.md`, `CODE_OF_CONDUCT.md` | community/governance docs |
| `.github/workflows/ci.yml` | the governance gate: byte-compile, relative-link check, a mutation control that proves the compile gate can fail, and a full-history gitleaks scan |
| `.github/` (CODEOWNERS, dependabot, ISSUE/PR templates) | repo maintenance scaffolding |

## Limits (不做什么)

- **No manuscript, no data, no code in this repository.** Nothing here can reproduce a PAPER-E number.
- PAPER-E numbers are reproducible only from `memory-architecture-bias`, checked against its `evidence/evidence_manifest.json`; this repository carries no data of its own.
- The "consolidate manuscript here" roadmap item is **undecided**; until it is done, treat this repo as a stable address only.
- CI here checks governance hygiene only. A green badge means the governance files are intact — it says nothing about the science.

## License

Code and governance files: MIT (see [LICENSE](LICENSE)). Any data, documents, pre-registration records, figures and tables that land here: CC-BY-4.0 (see [LICENSE-DATA](LICENSE-DATA)) — share and adapt with attribution to *aidless* and a link to the license.
