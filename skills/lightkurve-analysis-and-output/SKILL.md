---
name: lightkurve-analysis-and-output
description: This skill should be used when users ask about analysis and output in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: Analysis and Output

## High-Signal Playbook
### Route Conditions
- Use this skill for `LightCurve`/`FoldedLightCurve` manipulation, plotting, post-processing, and export decisions (`docs/source/reference/lightcurve.rst`, `docs/source/reference/foldedlightcurve.rst`).
- Route archive search, download, reader, and config issues to `lightkurve-reference`.
- Route method-selection questions about systematic correctors/periodograms to `lightkurve-advanced-topics`.
- Route installation/toolchain problems to `lightkurve-build-and-install`.

### Triage Questions
- Are they working with `LightCurve` or already with a `FoldedLightCurve`?
- Is the goal cleaning, detrending, phase folding, visualization, or file export?
- Do they need robust handling of NaNs/outliers before analysis?
- Is the period known for folding, or still being estimated upstream?
- Which output format is required (`csv`, `fits`, `pandas`, table)?
- Do they need interoperability with other astronomy software tools?

### Canonical Workflow
1. Confirm object type and required columns (`time`, `flux`, `flux_err`) (`docs/source/reference/lightcurve.rst`).
2. Clean the series with `remove_nans()` and optionally `remove_outliers()` (`docs/source/reference/lightcurve.rst`).
3. Normalize/flatten depending on trend-removal needs (`docs/source/reference/lightcurve.rst`).
4. Fold on known period when phase-domain analysis is required (`docs/source/reference/lightcurve.rst`, `docs/source/reference/foldedlightcurve.rst`).
5. Use `plot`/`scatter`/`errorbar`/`plot_river` based on signal density and uncertainty needs (`docs/source/reference/lightcurve.rst`, `docs/source/reference/foldedlightcurve.rst`).
6. Persist results using `to_fits`, `to_csv`, `to_table`, or `to_pandas` (`docs/source/reference/lightcurve.rst`).
7. For external workflows, cross-check fit-for-purpose tools from community list (`docs/source/about/other_software.rst`).

### Minimal Working Example
```python
import lightkurve as lk

lc = lk.search_lightcurve("TIC 307210830", mission="TESS").download()
lc_clean = lc.remove_nans().remove_outliers().normalize().flatten()
flc = lc_clean.fold(period=5.0)

flc.scatter()
lc_clean.to_fits("clean-lightcurve.fits", overwrite=True)
```

```python
lc_clean.to_csv("clean-lightcurve.csv")
```

### Pitfalls and Fixes
- Assuming in-place edits: most light-curve manipulation methods return new objects (`docs/source/reference/lightcurve.rst`).
- Forgetting NaN cleanup before downstream operations: call `remove_nans()` early (`docs/source/reference/lightcurve.rst`).
- Misreading folded output: `FoldedLightCurve.time` represents phase values (`docs/source/reference/foldedlightcurve.rst`).
- Losing uncertainty context: inspect/use `flux_err` through the workflow (`docs/source/reference/lightcurve.rst`).
- Treating community software list as complete replacement guidance: use it as complement/interop pointers only (`docs/source/about/other_software.rst`).
- Exporting before confirming normalization/flattening choices can lock in avoidable artifacts (`docs/source/reference/lightcurve.rst`).

### Convergence / Validation Checks
- Pre/post-clean statistics (scatter/CDPP proxies) improve without erasing target variability (`docs/source/reference/lightcurve.rst`).
- Folded view shows stable phase structure; odd/even masks can be inspected for transit sanity checks (`docs/source/reference/foldedlightcurve.rst`).
- Output files reopen cleanly via Lightkurve/pandas tooling according to chosen export path (`docs/source/reference/lightcurve.rst`).
- Metadata needed downstream remains available in `meta`/attribute shorthand (`docs/source/reference/lightcurve.rst`).

## Scope
- Handle questions about output formats, analysis, and post-processing.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/source/reference/lightcurve.rst`
- `docs/source/about/other_software.rst`
- `docs/source/reference/foldedlightcurve.rst`

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
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/lightcurvefile.py`
- `src/lightkurve/collections.py`
- `src/lightkurve/convenience.py`
- `src/lightkurve/targetpixelfile.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
