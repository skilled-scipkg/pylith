---
name: pylith-references
description: This skill should be used when users ask about references in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: References

## High-Signal Playbook
### Route Conditions
- Use this skill for bibliography/citation lookup, canonical references, and provenance metadata requests.
- Route release-history comparisons to `pylith-release-notes`.
- Route simulation setup/run instructions to `pylith-getting-started` and `pylith-simulation-workflows`.
- Route requirements/build dependency questions to `pylith-requirements` or `pylith-build-and-install`.

### Triage Questions
- Does the user need scientific citations, software provenance, or runtime dependency versions?
- Is the request tied to a specific workflow/topic skill that should be routed first?
- Is the answer expected as references only, or with reproducible runtime metadata?

### Canonical Workflow
1. Start with `docs/references.md` for formal bibliography and citations.
2. Pair citation answers with runtime version/provenance context when needed.
3. Use version/dependency utilities before claiming environment provenance.
4. Route domain-specific technical questions to the matching topic skill.

### Minimal Working Example
```bash
rg -n "^#|^##|{bibliography}" docs/references.md
pylith --version
```

### Validation Checkpoints
- Every citation claim maps to `docs/references.md`.
- Version/provenance metadata is derived from runtime utilities, not guesses.
- Routed follow-up questions point to the narrowest relevant skill.

## Scope
- Handle questions about documentation grouped under the 'references' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/references.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`
- `docs/user/examples`

## Test references
- `tests`
- `pylith/testing`

## Optional deeper inspection
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

## Source entry points for unresolved issues
- `pylith/apps/PyLithApp.py` (runtime version/citation output path)
- `pylith/utils/CollectVersionInfo.py` (dependency provenance reporting)
- `pylith/utils/SimulationMetadata.py` (workflow metadata normalization)
- `pylith/utils/DumpParametersJson.py` (reproducible run metadata capture)
- `pylith/viz/PlotField.py` and `pylith/viz/core.py` (reference-linked post-processing APIs)
- `modulesrc/utils/PylithVersion.i` (SWIG version metadata boundary)
- `libsrc/pylith/utils/PylithVersion.cc` and `libsrc/pylith/utils/DependenciesVersion.cc` (C++ provenance behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
