# lightkurve source map: About

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "__version__|__citation__|warn_legacy_cache_dir|cache_dir" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/__init__.py src/lightkurve/config/__init__.py src/lightkurve/version.py`

## Function-level entry points
- `src/lightkurve/version.py` | symbols: `__version__` | installed-version truth source used when reconciling changelog guidance.
- `src/lightkurve/__init__.py` | symbols: `__citation__`, `Conf`, `conf` | citation metadata and import-time configuration wiring.
- `src/lightkurve/config/__init__.py` | symbols: `get_cache_dir()`, `warn_if_default_cache_dir_migration_needed()` | cache path migration behavior that frequently appears in support reports.

## Behavior checks
```bash
python -c "import lightkurve as lk; print(lk.__version__)"
python -c "import lightkurve as lk; print(lk.__citation__.splitlines()[0])"
python -c "import lightkurve as lk; print(lk.config.get_cache_dir())"
```

## Validation checkpoints
- Version string is available and can be mapped to changelog entries.
- Citation text is exposed and non-empty.
- Cache-directory resolution runs without raising errors.
