# Start Here (from `skills/`)

## 1. Move to repo root
```bash
cd ..
```

## 2. Sanity-check environment
```bash
python -c "import lightkurve as lk; print(lk.__version__)"
```

If import fails, install the package and dependencies first:
```bash
python -m pip install -e .
# or: poetry install
```

## 3. Run a local simulation smoke test
```bash
pytest -q tests/test_synthetic_data.py -k "sine_sff"
```

## 4. Choose the right topic skill
- Routing index: `skills/lightkurve-index/SKILL.md`
- Data/search/config/seismology: `skills/lightkurve-reference/SKILL.md`
- Analysis/folding/export: `skills/lightkurve-analysis-and-output/SKILL.md`
- Correctors/periodograms/testing internals: `skills/lightkurve-advanced-topics/SKILL.md`
- API scripting and deterministic fixtures: `skills/lightkurve-api-and-scripting/SKILL.md`
- Install/build/docs environment: `skills/lightkurve-build-and-install/SKILL.md`
- Contribution/release workflow: `skills/lightkurve-developer-guide/SKILL.md`
- Package orientation/changelog/citation: `skills/lightkurve-about/SKILL.md`
