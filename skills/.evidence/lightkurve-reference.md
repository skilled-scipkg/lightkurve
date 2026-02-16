# Evidence: lightkurve-reference

## Primary docs
- `docs/source/reference/search.rst`
- `docs/source/reference/seismology.rst`
- `docs/source/reference/io.rst`
- `docs/source/reference/config.rst`
- `docs/source/reference/targetpixelfile.rst`
- `docs/source/reference/misc.rst`

## Primary source entry points
- `skills/lightkurve-reference/references/doc_map.md`
- `src/lightkurve/seismology/__init__.py`
- `src/lightkurve/config/__init__.py`
- `src/lightkurve/seismology/core.py`
- `src/lightkurve/targetpixelfile.py`
- `src/lightkurve/search.py`
- `src/lightkurve/seismology/utils.py`
- `src/lightkurve/seismology/stellar_estimators.py`
- `src/lightkurve/seismology/numax_estimators.py`
- `src/lightkurve/seismology/deltanu_estimators.py`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- A warning is issued if the legacy ``~/.lightkurve-cache`` directory still exists.
- #. The warning will no long appear once a custom ```cache_dir``` is specified.
- * To suppress the warning for any reason, you can set ``warn_legacy_cache_dir`` in the user's ``lightkurve.cfg``.
