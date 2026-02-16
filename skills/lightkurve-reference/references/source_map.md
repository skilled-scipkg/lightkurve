# lightkurve source map: Reference

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "search_lightcurve|search_targetpixelfile|read\(|get_cache_dir|to_seismology|estimate_numax|estimate_deltanu" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/search.py src/lightkurve/io/read.py src/lightkurve/targetpixelfile.py src/lightkurve/config/__init__.py src/lightkurve/periodogram.py src/lightkurve/seismology/core.py`

## Function-level entry points
- `src/lightkurve/search.py` | symbols: `search_lightcurve()`, `search_targetpixelfile()`, `search_tesscut()`, `SearchResult.download_all()` | remote archive search/download behavior.
- `src/lightkurve/io/read.py` | symbols: `read()`, `_read_collection()` | local product loading and collection handling.
- `src/lightkurve/targetpixelfile.py` | symbols: `to_lightcurve()`, `create_threshold_mask()` | pixel-product operations tied to reference docs.
- `src/lightkurve/config/__init__.py` | symbols: `get_cache_dir()`, `warn_if_default_cache_dir_migration_needed()` | cache/config semantics.
- `src/lightkurve/periodogram.py` | symbol: `to_seismology()` | conversion path from periodograms to seismology.
- `src/lightkurve/seismology/core.py` | symbols: `estimate_numax()`, `estimate_deltanu()` | seismic estimator implementations.
- `src/lightkurve/seismology/utils.py` | symbols: seismic helper utilities | shared methods used by estimators.
- `src/lightkurve/seismology/stellar_estimators.py` | symbols: stellar scaling relations | estimator support code.

## Behavior checks
```bash
pytest -q tests/io/test_read.py -k "read_lc or read_tpf"
pytest -q tests/test_conf.py -k get_cache_dir
pytest -q tests/seismology/test_stellar_estimators.py
```

## Validation checkpoints
- Search/read flows return the expected object families.
- Cache config checks pass and migration warnings stay controlled.
- Seismology estimator tests pass without API regressions.
