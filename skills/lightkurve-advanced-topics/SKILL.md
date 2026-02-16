---
name: lightkurve-advanced-topics
description: This skill should be used when users ask about narrow advanced topics in lightkurve (tutorial navigation, correctors, periodograms, testing workflows, or general docs entry points) that were consolidated from single-doc topic skills.
---

# lightkurve: Advanced Topics

## Scope
- Handle specialized topics consolidated from single-doc skills: tutorials navigation, correctors/modeling internals, periodograms, testing workflows, and general docs landing pages.
- Keep answers docs-first and route back to core skills when the request is primarily installation, reference/API lookup, or analysis/output workflow.

## High-Signal Playbook
### Canonical Workflow
1. Pick one advanced target first: correctors, periodograms, tutorials, or testing (`docs/source/reference/correctors.rst`, `docs/source/reference/periodogram.rst`, `docs/source/tutorials/index.rst`, `docs/source/development/testing.rst`).
2. Prefer local synthetic fixtures before remote products for deterministic behavior checks (`tests/data/synthetic/README.md`).
3. For detrending experiments, build from `TargetPixelFile -> to_lightcurve() -> corrector.correct(...)`.
4. Validate recovered signals with `to_periodogram(...)` and compare against known injections (e.g., ~5-day synthetic fixtures).
5. Escalate to function-level source files only when docs do not settle argument defaults, masks, or numerical assumptions.

### Minimal Working Example
```python
import lightkurve as lk

tpf = lk.read("tests/data/synthetic/synthetic-k2-sinusoid.targ.fits.gz")
lc = tpf.to_lightcurve().remove_nans()
cor_lc = tpf.to_corrector("pld").correct()
pg = cor_lc.to_periodogram(method="lombscargle", minimum_period=1, maximum_period=10)

print(round(pg.period_at_max_power.value, 1))
```

### Validation Checkpoints
- Derived period is near the injected signal scale (~5 days for the sinusoid fixture).
- Corrected light curve remains finite and preserves expected astrophysical structure.
- Targeted tests pass for the selected component (`correctors`, `periodogram`, or `synthetic_data`).

## Route the request
- Tutorial catalog, onboarding sequence, and notebook organization: `docs/source/index.rst`, `docs/source/tutorials/README.md`, `docs/source/tutorials/index.rst`.
- Systematics-correction model selection (`CBV`, `PLD`, `SFF`, regression/design-matrix plumbing): `docs/source/reference/correctors.rst`.
- Frequency-domain API and periodogram object operations: `docs/source/reference/periodogram.rst`.
- Local/remote test execution, skips, warning handling, and test caching: `docs/source/development/testing.rst`.
- If the question becomes broad install/dev setup, route to `lightkurve-build-and-install`.
- If the question becomes data search/read/config/seismology, route to `lightkurve-reference`.
- If the question becomes light-curve cleaning/folding/export, route to `lightkurve-analysis-and-output`.

## Primary documentation references
- `docs/source/index.rst`
- `docs/source/tutorials/README.md`
- `docs/source/tutorials/index.rst`
- `docs/source/reference/correctors.rst`
- `docs/source/reference/periodogram.rst`
- `docs/source/development/testing.rst`

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
- `src/lightkurve/periodogram.py`
- `src/lightkurve/correctors/cbvcorrector.py`
- `src/lightkurve/correctors/pldcorrector.py`
- `src/lightkurve/correctors/sffcorrector.py`
- `src/lightkurve/correctors/regressioncorrector.py`
- `src/lightkurve/correctors/designmatrix.py`
- `src/lightkurve/correctors/metrics.py`
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/targetpixelfile.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
