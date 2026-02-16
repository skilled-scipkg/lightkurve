# Evidence: lightkurve-developer-guide

## Primary docs
- `docs/source/development/vision.rst`
- `docs/source/development/release-procedure.rst`

## Primary source entry points
- `skills/lightkurve-developer-guide/references/doc_map.md`
- `src/lightkurve/__init__.py`
- `src/lightkurve/seismology/__init__.py`
- `src/lightkurve/prf/__init__.py`
- `src/lightkurve/io/__init__.py`
- `src/lightkurve/correctors/__init__.py`
- `src/lightkurve/config/__init__.py`
- `src/lightkurve/seismology/core.py`
- `src/lightkurve/prf/tpfmodel.py`
- `src/lightkurve/prf/prfmodel.py`
- `src/lightkurve/version.py`
- `src/lightkurve/utils.py`
- `src/lightkurve/units.py`
- `src/lightkurve/time.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/search.py`
- `src/lightkurve/periodogram.py`
- `src/lightkurve/lightcurvefile.py`
- `src/lightkurve/lightcurve.py`
- `src/lightkurve/interact_bls.py`

## Extracted headings
- (none extracted)

## Executable command hints
- $ git checkout main
- $ git pull
- $ pytest --remote-data
- $ cd docs
- $ make html
- $ make upload
- $ git add CHANGES.rst
- $ git commit -m "Finalizing changelog for v<version>"
- $ poetry build
- $ poetry publish

## Warnings and pitfalls
- (none extracted)
