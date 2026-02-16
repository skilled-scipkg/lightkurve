---
name: lightkurve-reference
description: This skill should be used when users ask about reference in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: Reference

## High-Signal Playbook
### Route Conditions
- Use this skill for archive search/download flows, file readers, configuration/cache behavior, target-pixel interfaces, seismology entry points, and utility flags (`docs/source/reference/search.rst`, `docs/source/reference/io.rst`, `docs/source/reference/config.rst`, `docs/source/reference/targetpixelfile.rst`, `docs/source/reference/seismology.rst`, `docs/source/reference/misc.rst`).
- Route light-curve cleaning, folding, plotting, and export specifics to `lightkurve-analysis-and-output`.
- Route corrector internals, periodogram-only deep dives, and test-run guidance to `lightkurve-advanced-topics`.
- Route install/environment failures to `lightkurve-build-and-install`.

### Triage Questions
- Are they searching MAST remotely or opening a local FITS file?
- Is the product type light curve, target pixel file, tesscut cutout, or mixed collection?
- Which mission/author/exposure-time constraints matter?
- Do they need one product (`download`) or a collection (`download_all`)?
- Are they blocked by cache/config warnings (legacy cache path)?
- Do they need seismology estimators (`numax`, `deltanu`, etc.)?
- Are quality flags/metadata filtering part of the issue?

### Canonical Workflow
1. Start with a search API (`search_lightcurve`, `search_targetpixelfile`, or `search_tesscut`) (`docs/source/reference/search.rst`).
2. Filter `SearchResult` metadata (e.g., exposure time) before downloading (`docs/source/reference/search.rst`).
3. Download one product with `.download()` or many with `.download_all()` (`docs/source/reference/search.rst`).
4. If data is local/on disk, call `lightkurve.read()` and let it auto-detect product type (`docs/source/reference/io.rst`).
5. For collections, subset by mission fields (`sector`, `quarter`, `campaign`) before stitching/plotting (`docs/source/reference/search.rst`).
6. Check config paths using `lightkurve.conf` and `config.get_cache_dir()` when cache behavior is unexpected (`docs/source/reference/config.rst`).
7. For asteroseismic estimates, convert to seismology and use estimator methods (`docs/source/reference/seismology.rst`).
8. Escalate to `src/lightkurve/search.py`, `src/lightkurve/io/read.py`, `src/lightkurve/targetpixelfile.py`, or `src/lightkurve/seismology/core.py` only if docs leave ambiguity.

### Minimal Working Example
```python
import lightkurve as lk

result = lk.search_lightcurve("TIC 307210830", mission="TESS")
result = result[result.exptime.value < 1000]
lc = result.download().remove_nans().normalize()

all_lc = lk.search_lightcurve("TIC 307210830", mission="TESS").download_all()
subset = all_lc[(all_lc.sector >= 13) & (all_lc.sector <= 19)]
print(len(subset), lc.flux[:3])
```

```python
import lightkurve as lk

product = lk.read("my-product.fits")
print(lk.config.get_cache_dir())
```

### Pitfalls and Fixes
- Treating `SearchResult` like downloaded data: call `.download()` / `.download_all()` first (`docs/source/reference/search.rst`).
- Calling product-specific readers directly without need: prefer generic `lightkurve.read()` (`docs/source/reference/io.rst`).
- Downloading too much data: filter by metadata (`exptime`, mission fields) first (`docs/source/reference/search.rst`).
- Ignoring legacy cache warning: migrate `~/.lightkurve-cache` to `~/.lightkurve/cache` or set explicit config (`docs/source/reference/config.rst`).
- Confusing collection-level and item-level operations: subset collection, then call methods on members (`docs/source/reference/search.rst`).
- Skipping quality diagnostics: use quality-flag utilities before interpreting anomalies (`docs/source/reference/misc.rst`).

### Convergence / Validation Checks
- Downloaded set matches intended `mission`/`author`/`exptime` filters (`docs/source/reference/search.rst`).
- Returned object type (TPF vs LightCurve) matches downstream method usage (`docs/source/reference/io.rst`, `docs/source/reference/targetpixelfile.rst`).
- Cache directory is explicit and warning-free (`docs/source/reference/config.rst`).
- Seismology estimates run on a suitable periodogram-derived workflow without method errors (`docs/source/reference/seismology.rst`).

## Scope
- Handle questions about documentation grouped under the 'reference' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/source/reference/search.rst`
- `docs/source/reference/seismology.rst`
- `docs/source/reference/io.rst`
- `docs/source/reference/config.rst`
- `docs/source/reference/targetpixelfile.rst`
- `docs/source/reference/misc.rst`

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
- `src/lightkurve/search.py`
- `src/lightkurve/io/read.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/config/__init__.py`
- `src/lightkurve/periodogram.py`
- `src/lightkurve/seismology/core.py`
- `src/lightkurve/seismology/utils.py`
- `src/lightkurve/seismology/stellar_estimators.py`
- `src/lightkurve/seismology/numax_estimators.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
