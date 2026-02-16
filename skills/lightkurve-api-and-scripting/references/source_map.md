# lightkurve source map: API and Scripting

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "search_lightcurve|search_targetpixelfile|read\(|to_periodogram\(|to_seismology\(" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/__init__.py src/lightkurve/search.py src/lightkurve/io/read.py src/lightkurve/lightcurve.py src/lightkurve/targetpixelfile.py src/lightkurve/periodogram.py src/lightkurve/seismology/core.py`

## Function-level entry points
- `src/lightkurve/__init__.py` | symbols: top-level imports and `Conf` | public API surfacing.
- `src/lightkurve/search.py` | symbols: `search_lightcurve()`, `search_targetpixelfile()`, `SearchResult.download()` | archive-query entry points.
- `src/lightkurve/io/read.py` | symbols: `read()`, `read_lc_collection()`, `read_tpf_collection()` | local file scripting entry points.
- `src/lightkurve/targetpixelfile.py` | symbol: `TargetPixelFile.to_lightcurve()` | key conversion for scripted pipelines.
- `src/lightkurve/lightcurve.py` | symbols: `to_periodogram()`, `normalize()`, `remove_nans()` | common script transformations.
- `src/lightkurve/periodogram.py` | symbol: `Periodogram.to_seismology()` | handoff from frequency analysis to seismology.
- `src/lightkurve/seismology/core.py` | symbols: `estimate_numax()`, `estimate_deltanu()` | final asteroseismic estimators.

## Behavior checks
```bash
python - <<'PY'
import lightkurve as lk

tpf = lk.read("tests/data/synthetic/synthetic-k2-sinusoid.targ.fits.gz")
lc = tpf.to_lightcurve().remove_nans().normalize()
pg = lc.to_periodogram(method="lombscargle", minimum_period=1, maximum_period=10)
print(round(pg.period_at_max_power.value, 1))
PY

pytest -q tests/io/test_read.py -k "read_lc or read_tpf_collection"
```

## Validation checkpoints
- Script runs without network access using bundled synthetic files.
- Public API calls resolve from top-level `lightkurve` import.
- Returned period is physically plausible for the input fixture.
