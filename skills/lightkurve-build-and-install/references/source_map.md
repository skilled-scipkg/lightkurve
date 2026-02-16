# lightkurve source map: Build and Install

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Fast source navigation
- `REPO_ROOT="$(git rev-parse --show-toplevel)" && cd "$REPO_ROOT"`
- `rg -n "__version__|ConfigNamespace|get_cache_dir|warn_if_default_cache_dir_migration_needed" src/lightkurve`
- `rg -n "^def |^class " src/lightkurve/__init__.py src/lightkurve/config/__init__.py src/lightkurve/io/read.py src/lightkurve/version.py`

## Function-level entry points
- `src/lightkurve/version.py` | symbol: `__version__` | canonical package version value.
- `src/lightkurve/__init__.py` | symbols: import surface + `conf` initialization | import-time wiring most install failures surface through.
- `src/lightkurve/config/__init__.py` | symbols: `get_config_dir()`, `get_cache_dir()` | environment and cache path setup behavior.
- `src/lightkurve/io/read.py` | symbols: `read()`, `open()` | smoke-test API for real file IO after install.

## Behavior checks
```bash
python -c "import lightkurve as lk; print(lk.__version__)"
pytest -q tests/test_conf.py -k get_cache_dir
pytest -q tests/io/test_read.py -k "filenotfound or basic_ascii_io"
```

## Validation checkpoints
- Import succeeds and version is reported.
- Cache/config directory logic works in current environment.
- Core IO API raises expected errors and handles simple reads.
