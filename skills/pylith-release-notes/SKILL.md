---
name: pylith-release-notes
description: This skill should be used when users ask about release notes in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Release Notes

## High-Signal Playbook
### Route Conditions
- Use this skill for "what changed", migration, compatibility, or release-history questions.
- For modern release details (v3+), use `CHANGES.md` via `docs/intro/release-notes.md`.
- For legacy migration specifics (v1.x/v2.x), use `release-notes/announce_v*.txt`.
- Route build failures caused by dependency changes to `pylith-build-and-install`.
- Route runtime behavior changes to the corresponding topic skills (`pylith-simulation-workflows`, `pylith-inputs-and-modeling`, `pylith-troubleshooting`).

### Triage Questions
- What source and target versions are being compared?
- Is the user on a released build or a development snapshot (`__version__`, `pylith --version`)?
- Is the issue about parameter/API migration, solver defaults, mesh/output format, or packaging?
- Do they need actionable migration edits for old cfg files?
- Is the question tied to binary/container/source distribution behavior?
- Should we anchor the answer in `CHANGES.md` (v3+) or legacy announcement files?

### Canonical Workflow
1. Identify version window first; do not summarize changes without explicit version bounds.
2. For v3+ questions, pull changes from `CHANGES.md` (included by `docs/intro/release-notes.md`).
3. For v1/v2 migration issues, read the corresponding `release-notes/announce_v*.txt` migration blocks.
4. Extract only behavior-impacting items (parameter renames, defaults, solver/output changes).
5. Map each change to affected workflows (run, mesh, materials, output) and route to the matching skill.
6. Validate installed runtime version before proposing migration edits.

### Minimal Working Example
```bash
# Show modern release stream and semantic-versioned sections.
rg -n "^## Version " CHANGES.md

# Pull legacy migration blocks for old parameter-file upgrades.
rg -n "MIGRATING FROM VERSION|DataWriter|partitioner" release-notes/announce_v2.0.0.txt release-notes/announce_v2.0.3.txt

# Check current runtime package version marker.
rg -n "__version__" pylith/__init__.py
```

### Pitfalls And Fixes
- Mixing legacy announcement notes with modern semver changelog entries: split by version era (`CHANGES.md` vs `release-notes/announce_v*.txt`).
- Assuming "no migration needed" across major versions; verify migration sections explicitly.
- Applying old parameter names from v1/v2 docs to v3+ inputs (for example dash/underscore and writer naming shifts).
- Ignoring release checklist context when discussing packaging/release process (`release-notes/checklist.txt`).
- Reporting changes without mapping to affected workflows; always connect release notes to concrete run/model/output implications.

### Convergence And Validation Checks
- Version comparison must be explicit and bounded (from X to Y).
- Every claimed change should map to a cited release-notes file path.
- Migration guidance should produce a runnable example or verifiable config diff.
- Runtime version in the current environment should match the migration advice target.
- If uncertainty remains, escalate to version-source files and component implementation paths.

## Scope
- Handle questions about documentation grouped under the 'release-notes' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `release-notes/announce_v2.0.3.txt`
- `release-notes/announce_v2.1.3.txt`
- `release-notes/announce_v2.2.1.txt`
- `release-notes/announce_v2.2.0.txt`
- `release-notes/announce_v2.1.4.txt`
- `release-notes/announce_v2.1.2.txt`
- `release-notes/announce_v2.1.0.txt`
- `release-notes/announce_v2.0.1.txt`
- `release-notes/announce_v2.0.0.txt`
- `release-notes/checklist.txt`
- `release-notes/announce_v1.4.0.txt`
- `release-notes/announce_v1.9.0.txt`

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
- `pylith/__init__.py`
- `pylith/utils/CollectVersionInfo.py` (version/dependency reporting used by CLI)
- `pylith/apps/PyLithApp.py` (`--version` and citation output path)
- `modulesrc/utils/PylithVersion.i` (Python binding for C++ version object)
- `libsrc/pylith/utils/PylithVersion.hh`
- `libsrc/pylith/utils/PylithVersion.cc`
- `pylith/utils/SimulationMetadata.py` (cfg version-constraint validation)
- `pylith/Makefile.am`, `modulesrc/Makefile.am`, `libsrc/Makefile.am` (release/build packaging entry points)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
