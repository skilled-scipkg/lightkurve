---
name: lightkurve-index
description: This skill should be used when users ask how to use lightkurve and the correct generated documentation skill must be selected before going deeper into source code.
---

# lightkurve Skills Index

## Start from `skills/`
- Move to repo root first so all `docs/`, `src/`, and `tests/` paths resolve: `cd ..`
- If dependencies are missing, install the project environment first: `python -m pip install -e .` (or `poetry install`)
- Quick import sanity check: `python -c "import lightkurve as lk; print(lk.__version__)"`
- Optional local simulation smoke test: `pytest -q tests/test_synthetic_data.py -k "sine_sff"`

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `lightkurve-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `lightkurve-analysis-and-output`: Analysis and Output (output formats, analysis, and post-processing)
- `lightkurve-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `lightkurve-developer-guide`: Developer Guide (developer architecture, extension points, and contribution workflow)
- `lightkurve-reference`: Reference (documentation grouped under the 'reference' theme)
- `lightkurve-about`: About (documentation grouped under the 'about' theme)
- `lightkurve-advanced-topics`: Advanced Topics (consolidated narrow docs: tutorials/getting-started/general entry points, correctors, periodograms, and testing workflows)

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `docs/source/tutorials`

## Test roots for behavior checks
- `tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open that skill's doc map (for example `skills/lightkurve-reference/references/doc_map.md`).
- If documentation still leaves ambiguity, open that skill's source map (for example `skills/lightkurve-reference/references/source_map.md`) and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" src`).

## Source directories for deeper inspection
- `src`
