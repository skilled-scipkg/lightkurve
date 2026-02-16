# lightkurve source map: Developer Guide

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "__version__|__citation__|class Corrector|detect_filetype" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/__init__.py src/lightkurve/search.py src/lightkurve/lightcurve.py src/lightkurve/targetpixelfile.py src/lightkurve/io/detect.py src/lightkurve/correctors/corrector.py src/lightkurve/version.py`

## Function-level entry points
- `src/lightkurve/version.py` | symbol: `__version__` | release-state source for dev/release workflow checks.
- `src/lightkurve/__init__.py` | symbols: `__citation__`, `Conf`, import surface | package-level policy and export boundary.
- `src/lightkurve/correctors/corrector.py` | symbol: `Corrector` base class | extension contract for new correctors.
- `src/lightkurve/io/detect.py` | symbol: `detect_filetype()` | file-dispatch decision point for reader behavior.
- `src/lightkurve/search.py` | symbol: `SearchResult` | user-facing query result API and display behavior.
- `src/lightkurve/lightcurve.py` | symbol: `LightCurve` | core domain object architecture.
- `src/lightkurve/targetpixelfile.py` | symbol: `TargetPixelFile` | core pixel-domain object architecture.

## Behavior checks
```bash
python -c "import lightkurve as lk; print(lk.__version__)"
pytest -q tests/test_lightcurve.py -k "invalid_lightcurve or normalize"
pytest -q tests/io/test_read.py -k open
```

## Validation checkpoints
- Version metadata and public imports stay consistent after refactors.
- Core object tests pass for representative light-curve behavior.
- File dispatch/read path remains operational for contributor changes.
