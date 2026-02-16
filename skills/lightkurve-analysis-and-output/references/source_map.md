# lightkurve source map: Analysis and Output

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "remove_nans\(|remove_outliers\(|flatten\(|fold\(|to_csv\(|to_fits\(" src/lightkurve/lightcurve.py`
- `rg -n "plot\(|scatter\(|errorbar\(|plot_river\(" src/lightkurve/lightcurve.py`

## Function-level entry points
- `src/lightkurve/lightcurve.py` | symbols: `remove_nans()`, `remove_outliers()`, `flatten()`, `fold()`, `to_csv()`, `to_fits()` | core analysis and export behavior.
- `src/lightkurve/lightcurvefile.py` | symbols: file-backed light-curve wrappers | ingestion/output compatibility behaviors.
- `src/lightkurve/collections.py` | symbol: `LightCurveCollection.stitch()` | combining multi-sector/campaign curves.
- `src/lightkurve/convenience.py` | symbol: `estimate_cdpp()` | quick noise-quality metric support.
- `src/lightkurve/targetpixelfile.py` | symbols: `to_lightcurve()`, `create_threshold_mask()` | upstream extraction choices that affect downstream analysis.

## Behavior checks
```bash
pytest -q tests/test_lightcurve.py -k "remove_nans or remove_outliers or flatten or fold"
pytest -q tests/test_lightcurve.py -k "to_csv or to_fits or river"
```

## Validation checkpoints
- Cleaning/flattening steps return expected `LightCurve` or `FoldedLightCurve` objects.
- Export tests produce readable outputs without metadata loss.
- Folded plots and river plots execute without shape/phase errors.
