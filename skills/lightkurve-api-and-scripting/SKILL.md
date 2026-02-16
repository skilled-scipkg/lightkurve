---
name: lightkurve-api-and-scripting
description: This skill should be used when users ask about api and scripting in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: API and Scripting

## High-Signal Playbook
### Route Conditions
- Use this skill for API-surface discovery, scripting entry points, and deterministic fixture-driven workflows (`docs/source/reference/index.rst`, `tests/data/synthetic/README.md`).
- Route archive search/download/config semantics to `lightkurve-reference`.
- Route light-curve processing/visual output questions to `lightkurve-analysis-and-output`.
- Route packaging/dev environment concerns to `lightkurve-build-and-install`.

### Triage Questions
- Is the user asking for public API usage or internal implementation behavior?
- Which object family is central (`LightCurve`, `TargetPixelFile`, `Periodogram`, `Seismology`, `Corrector`)?
- Is reproducible local test data required (no network)?
- Are they writing a quick script, notebook prototype, or regression test?
- Do they need API enumeration/navigation or concrete method-call recipes?
- Are they targeting synthetic sine/planet/flat fixtures specifically?

### Canonical Workflow
1. Start at API index to pick the correct object family and docs subsection (`docs/source/reference/index.rst`).
2. Prefer top-level `import lightkurve as lk` APIs before private-module imports (`docs/source/reference/index.rst`).
3. For deterministic script/test behavior, use synthetic fixtures under `tests/data/synthetic` (`tests/data/synthetic/README.md`).
4. Load fixture with `lk.read(...)` or standard search/download flow if remote data is acceptable.
5. Convert to desired object (`to_lightcurve`, `to_periodogram`, `to_seismology`) and apply methods.
6. Compare results against known synthetic injection facts (e.g., 5-day period fixtures) when validating scripts (`tests/data/synthetic/README.md`).
7. Escalate unresolved method-signature behavior to `src/lightkurve/__init__.py`, `src/lightkurve/lightcurve.py`, `src/lightkurve/targetpixelfile.py`, and related module entry points.

### Minimal Working Example
```python
import lightkurve as lk

tpf = lk.read("tests/data/synthetic/synthetic-k2-sinusoid.targ.fits.gz")
lc = tpf.to_lightcurve().remove_nans().normalize()
pg = lc.to_periodogram()

print(round(pg.period_at_max_power.value, 1))
```

```python
tpf_flat = lk.read("tests/data/synthetic/synthetic-k2-flat.targ.fits.gz")
print(tpf_flat.shape)
```

### Pitfalls and Fixes
- Jumping straight to internal modules: start from documented public API index (`docs/source/reference/index.rst`).
- Using network downloads in reproducibility-sensitive checks: prefer bundled synthetic fixtures (`tests/data/synthetic/README.md`).
- Ignoring fixture metadata: synthetic files include noiseless signals and injection parameters in dedicated HDUs/headers (`tests/data/synthetic/README.md`).
- Treating API index as full argument reference: drill into autosummary targets for parameter-level details (`docs/source/reference/index.rst`).
- Mixing object types in scripts (TPF vs LightCurve) without conversion: call explicit conversion methods first.

### Convergence / Validation Checks
- Script uses documented public objects/functions present in the API index (`docs/source/reference/index.rst`).
- Synthetic workflows recover expected qualitative behavior (e.g., strong ~5-day signal for sinusoid fixture) (`tests/data/synthetic/README.md`).
- File-based runs are deterministic and do not require network availability (`tests/data/synthetic/README.md`).
- Escalation path to source is explicit when docs do not fully specify behavior.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `tests/data/synthetic/README.md`
- `docs/source/reference/index.rst`

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
- `src/lightkurve/__init__.py`
- `src/lightkurve/io/read.py`
- `src/lightkurve/search.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/periodogram.py`
- `src/lightkurve/seismology/core.py`
- `src/lightkurve/config/__init__.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
