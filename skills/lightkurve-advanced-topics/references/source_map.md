# lightkurve source map: Advanced Topics

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "correct\(|diagnose\(|create_spline_matrix|to_periodogram\(" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/correctors src/lightkurve/periodogram.py`

## Function-level entry points
- `src/lightkurve/correctors/cbvcorrector.py` | symbols: `CBVCorrector.correct()`, `CBVCorrector.diagnose()` | cotrending basis vector fitting behavior.
- `src/lightkurve/correctors/pldcorrector.py` | symbols: `PLDCorrector.correct()`, `PLDCorrector.diagnose()` | PLD detrending path used in synthetic recovery tests.
- `src/lightkurve/correctors/sffcorrector.py` | symbols: `SFFCorrector.correct()`, `_estimate_arclength()` | SFF motion-correction internals.
- `src/lightkurve/correctors/regressioncorrector.py` | symbols: `RegressionCorrector.correct()`, `RegressionCorrector.diagnose()` | shared regression engine used by multiple correctors.
- `src/lightkurve/correctors/designmatrix.py` | symbols: `DesignMatrix.standardize()`, `DesignMatrix.pca()`, `create_spline_matrix()` | matrix construction and conditioning utilities.
- `src/lightkurve/periodogram.py` | symbols: `LombScarglePeriodogram`, `BoxLeastSquaresPeriodogram` | frequency-domain and transit-search behavior.
- `src/lightkurve/lightcurve.py` | symbol: `LightCurve.to_periodogram()` | bridge from time-domain curves to periodograms.

## Behavior checks
```bash
pytest -q tests/correctors/test_designmatrix.py -k "standardize or pca"
pytest -q tests/test_periodogram.py -k "can_find_periods or bls_period_recovery"
pytest -q tests/test_synthetic_data.py -k "sine_sff or sine_pld"
```

## Validation checkpoints
- Corrector pipelines produce finite corrected flux values.
- Periodogram tests recover known synthetic periods.
- Design-matrix transforms pass rank/conditioning checks.
