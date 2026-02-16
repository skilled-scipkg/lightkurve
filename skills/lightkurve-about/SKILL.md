---
name: lightkurve-about
description: This skill should be used when users ask about about in lightkurve; it prioritizes documentation references and then source inspection only for unresolved details.
---

# lightkurve: About

## High-Signal Playbook
### Route Conditions
- Use this skill for package orientation, changelog navigation, citation expectations, ecosystem context, and issue-report entry points (`docs/source/about/index.rst`, `docs/source/about/changelog.rst`).
- Route install mechanics to `lightkurve-build-and-install` (`docs/source/about/install.rst`).
- Route API usage and workflow mechanics to `lightkurve-reference` / `lightkurve-analysis-and-output`.
- Route contribution/release process details to `lightkurve-developer-guide`.

### Triage Questions
- Is the request about what Lightkurve is, how it changed, or how to cite it?
- Is the user asking for installed version vs project changelog history?
- Is the intent bug reporting, feature request, or documentation clarification?
- Do they need dependency citation guidance in addition to Lightkurve citation?
- Are they asking for alternative/complementary tools from the ecosystem list?

### Canonical Workflow
1. Start from `docs/source/about/index.rst` to classify request (install, citing, changelog, other software, development links).
2. For version-history questions, consult `docs/source/about/changelog.rst` (which includes `CHANGES.rst`) and separate that from local installed version.
3. For citation requests, include Lightkurve citation plus dependency citation guidance (from `docs/source/about/citing.rst`, linked via about index).
4. For bug/problem reports, direct users to GitHub issues with a minimal reproducible example (`docs/source/about/index.rst`).
5. For ecosystem comparisons, use `docs/source/about/other_software.rst` as complement list, not compatibility guarantee.
6. Route deeper operational questions to the specialized skills above.

### Minimal Working Example
```bash
# Confirm installed version before interpreting changelog guidance
python -c "import lightkurve; print(lightkurve.__version__)"
```

```text
Issue/report target: https://github.com/lightkurve/lightkurve/issues
```

### Pitfalls and Fixes
- Conflating changelog history with currently installed package: check local `__version__` first.
- Providing citation without dependency guidance for astronomy workflows: include dependency citations when applicable (`docs/source/about/citing.rst`).
- Treating ecosystem list as exhaustive or endorsed benchmarks: frame it as community-produced complementary software (`docs/source/about/other_software.rst`).
- Filing vague bug reports: require a minimal reproducible example and context (`docs/source/about/index.rst`).
- Answering development-policy questions here: route to developer guide once about-level context is done.

### Convergence / Validation Checks
- User receives exact route for their request class (install/citing/changelog/issues/ecosystem).
- Installed-version check is explicit before release-history advice.
- Citation responses include both core Lightkurve citation and dependency-citation pointer when relevant.
- Escalation links remain concrete (`docs/source/about/*.rst`, issue URL, and source entry points below).

## Scope
- Handle questions about documentation grouped under the 'about' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/source/about/index.rst`
- `docs/source/about/changelog.rst`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/source/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/lightkurve/version.py`
- `src/lightkurve/__init__.py`
- `src/lightkurve/config/__init__.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
