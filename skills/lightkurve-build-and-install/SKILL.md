---
name: lightkurve-build-and-install
description: This skill should be used when users ask about build and install in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: Build and Install

## High-Signal Playbook
### Route Conditions
- Use this skill for package install, contributor environment setup, dependency/tooling issues, and docs build/publish workflow (`docs/source/about/install.rst`, `docs/source/development/index.rst`, `docs/source/development/documentation.rst`).
- Route release-governance questions (version bumps, release order) to `lightkurve-developer-guide`.
- Route runtime data/API usage questions to `lightkurve-reference` or `lightkurve-analysis-and-output`.
- Route testing tactics (`--remote-data`, cache tuning, skipped tests) to `lightkurve-advanced-topics` (`docs/source/development/testing.rst`).

### Triage Questions
- Is the goal end-user install, contributor setup, or maintainer release prep?
- Are they using `pip` only or a `poetry` dev environment?
- Do they need editable behavior (`pip install --editable .`) or standard install?
- Is the failure during install, import, test run, or docs build?
- Are they blocked by permissions (`PermissionError`) or missing tools (`pandoc`)?
- Do they need offline docs build, or just hosted docs usage?

### Canonical Workflow
1. Pick install mode: user install (`python -m pip install lightkurve --upgrade`) or dev checkout (`git clone ...`, then env setup) (`docs/source/about/install.rst`).
2. For contributor work, create isolated env using `poetry install` (`docs/source/development/index.rst`).
3. Run commands via `poetry run ...` so code/tests execute against the dev env (`docs/source/development/index.rst`).
4. If not using poetry, use editable install (`python -m pip install --editable .`) for immediate source reflection (`docs/source/development/index.rst`, `docs/source/development/contributing.rst`).
5. Configure git remotes for sync (`git remote add upstream ...`) before branch work (`docs/source/development/index.rst`, `docs/source/development/contributing.rst`).
6. Build docs only when needed: `cd docs && make clean && make html` (`docs/source/development/documentation.rst`).
7. If docs fail with pandoc missing, install pandoc and re-run (`docs/source/development/documentation.rst`, `docs/README.rst`).
8. Verify install by importing and printing `lightkurve.__version__` (`docs/source/about/install.rst`).

### Minimal Working Example
```bash
# End-user install + smoke check
python -m pip install lightkurve --upgrade
python -c "import lightkurve; print(lightkurve.__version__)"
```

```bash
# Contributor setup
git clone https://github.com/lightkurve/lightkurve.git
cd lightkurve
python -m pip install poetry
poetry install
poetry run pytest
```

### Pitfalls and Fixes
- `PermissionError` on install: retry with a user-managed environment (or `--user`) (`docs/source/about/install.rst`).
- Source edits not reflected: use `poetry run ...` or editable install (`docs/source/development/index.rst`).
- Reinstalling on every edit: switch from `pip install .` to editable or poetry-managed workflow (`docs/source/development/index.rst`).
- Missing upstream remote causes stale branches: add `upstream` and pull before branch work (`docs/source/development/contributing.rst`).
- Docs build unexpectedly slow after `make clean`: notebook compilation can take >30 minutes (`docs/source/development/documentation.rst`).
- `Pandoc wasn't found`: install `pandoc` (brew/conda/official installer) and rebuild (`docs/source/development/documentation.rst`, `docs/README.rst`).
- Forgetting dependency floor checks: inspect `pyproject.toml` dependency table when version conflicts appear (`docs/source/about/install.rst`).

### Convergence / Validation Checks
- `python -c "import lightkurve; print(lightkurve.__version__)"` runs without import errors (`docs/source/about/install.rst`).
- `poetry run pytest` completes for local development baseline (`docs/source/development/index.rst`).
- Docs build reaches HTML output (`docs` `make html`) when docs edits are part of the change (`docs/source/development/documentation.rst`).
- Git remotes show both `origin` and `upstream` before syncing branches (`docs/source/development/index.rst`, `docs/source/development/contributing.rst`).

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/source/development/index.rst`
- `docs/README.rst`
- `docs/source/development/contributing.rst`
- `docs/source/about/install.rst`
- `docs/source/development/documentation.rst`
- `docs/source/about/citing.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/source/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/lightkurve/version.py`
- `src/lightkurve/__init__.py`
- `src/lightkurve/config/__init__.py`
- `src/lightkurve/io/read.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
