---
name: lightkurve-developer-guide
description: This skill should be used when users ask about developer guide in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: Developer Guide

## High-Signal Playbook
### Route Conditions
- Use this skill for contribution policy, project-scope decisions, and maintainer release workflow (`docs/source/development/vision.rst`, `docs/source/development/release-procedure.rst`).
- Route environment/bootstrap/doc-build commands to `lightkurve-build-and-install`.
- Route runtime API and scientific analysis usage to `lightkurve-reference` / `lightkurve-analysis-and-output`.
- Route test execution specifics (`--remote-data`, cache for tests) to `lightkurve-advanced-topics`.

### Triage Questions
- Is this a feature-scope decision, contribution workflow question, or release action?
- Does the proposal align with reusable-building-block goals versus full pipeline behavior?
- Is the requester a contributor or maintainer with publish permissions?
- Are version files/changelog updates part of the current step?
- Have remote-data tests and docs build been completed?
- Is there a post-release `.dev` bump plan?

### Canonical Workflow
1. Check proposal fit against project vision: reusable, broadly applicable, tested, and documented (`docs/source/development/vision.rst`).
2. Develop on branch/PR with review and CI, not direct unreviewed main-branch edits (`docs/source/development/vision.rst`).
3. For release prep, sync to latest `main` and run tests including remote-data checks (`docs/source/development/release-procedure.rst`).
4. Build/upload docs and tutorials before tagging release (`docs/source/development/release-procedure.rst`).
5. Remove `.dev` suffix in version files before release artifact generation (`docs/source/development/release-procedure.rst`).
6. Finalize changelog date/content and commit changelog update (`docs/source/development/release-procedure.rst`).
7. Build and publish package artifacts (`poetry build`, `poetry publish`) (`docs/source/development/release-procedure.rst`).
8. Update conda feedstock and then bump to next `.dev` version (`docs/source/development/release-procedure.rst`).

### Minimal Working Example
```bash
# Release preflight
git checkout main
git pull
pytest --remote-data
cd docs
make html
```

```bash
# Release artifact publish
poetry build
poetry publish
```

### Pitfalls and Fixes
- Accepting features outside scope (full pipelines, niche/novel methods): push scope discussion first (`docs/source/development/vision.rst`).
- Releasing with `.dev` still present: synchronize release version in `pyproject.toml` and `src/lightkurve/version.py` (`docs/source/development/release-procedure.rst`).
- Skipping remote-data tests: run `pytest --remote-data` in release prep (`docs/source/development/release-procedure.rst`).
- Skipping docs compile/upload: run docs pipeline before release (`docs/source/development/release-procedure.rst`).
- Incomplete changelog date/content: finalize `CHANGES.rst` before release branch (`docs/source/development/release-procedure.rst`).
- Forgetting post-release bump to next `.dev`: complete step 9 after publish (`docs/source/development/release-procedure.rst`).

### Convergence / Validation Checks
- Proposed feature clearly satisfies vision criteria and avoids out-of-scope categories (`docs/source/development/vision.rst`).
- Release commit includes synchronized version metadata and changelog update (`docs/source/development/release-procedure.rst`).
- Tests (including remote-data) and docs build complete without blockers (`docs/source/development/release-procedure.rst`).
- PyPI publish and conda-feedstock update steps are both tracked to closure (`docs/source/development/release-procedure.rst`).

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/source/development/vision.rst`
- `docs/source/development/release-procedure.rst`

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
- `src/lightkurve/search.py`
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/io/detect.py`
- `src/lightkurve/correctors/corrector.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
