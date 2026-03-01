---
name: pylith-developer-guide
description: This skill should be used when users ask about developer guide in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Developer Guide

## High-Signal Playbook
### Route Conditions
- Use this skill for internal architecture, extension points, coding workflows, debugging, and contributor-facing implementation questions.
- Route end-user simulation setup/execution to `pylith-getting-started` or `pylith-simulation-workflows`.
- Route release history and migration questions to `pylith-release-notes`.
- Route isolated test failures with runtime symptoms to `pylith-troubleshooting`.

### Triage Questions
- Is the user extending a Python component, SWIG binding, or C++ implementation?
- Is the change in app orchestration, problem/physics plumbing, mesh topology, or output?
- Which test layer is failing: pytests, C++ unit tests, MMS/fullscale?
- Is behavior difference between docs and code, or between Python and C++ layers?

### Canonical Workflow
1. Anchor on developer docs (`docs/developer/*`) for architecture and workflow expectations.
2. Reproduce behavior with the smallest relevant test target.
3. Inspect Python component class first, then SWIG `.i`, then C++ implementation.
4. Verify logging/instrumentation output before making deep structural changes.
5. Add or adjust tests close to the modified behavior surface.

### Minimal Working Example
```bash
# Narrow Python regression checks.
pytest tests/pytests/problems/TestProblem.py
pytest tests/pytests/problems/TestTimeDependent.py
pytest tests/pytests/meshio/TestOutputSoln.py
```

### Validation Checkpoints
- Reproduction test fails before change and passes after fix.
- Python/SWIG/C++ class interfaces remain aligned.
- No unrelated regressions in nearby pytest modules.
- Developer docs referenced in the answer map to touched architecture areas.

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/index.md`
- `docs/developer/index.md`
- `docs/developer/contributing/documentation/index.md`
- `docs/developer/testing/index.md`
- `docs/developer/implementation/index.md`
- `docs/developer/ides/index.md`
- `docs/developer/design/index.md`
- `docs/developer/debugging/index.md`
- `docs/developer/contributing/index.md`
- `docs/developer/ides/vs-code.md`
- `docs/developer/contributing/documentation/quickref.md`
- `docs/developer/design/application-flow.md`

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
- `pylith/apps/PyLithApp.py` and `pylith/apps/PetscApplication.py` (application lifecycle)
- `pylith/problems/TimeDependent.py` and `pylith/problems/Physics.py` (problem/physics plumbing)
- `pylith/topology/MeshImporter.py` (mesh pipeline entry point)
- `pylith/testing/TestCases.py` and `pylith/testing/FullTestApp.py` (test harness behavior)
- `modulesrc/problems/TimeDependent.i` and `modulesrc/problems/Physics.i` (SWIG boundary)
- `libsrc/pylith/problems/TimeDependent.cc` and `libsrc/pylith/problems/ObserverPhysics.cc` (C++ behavior checks)
- `libsrc/pylith/feassemble/Integrator.hh` (integration extension surface)
- `libsrc/pylith/utils/EventLogger.hh` (instrumentation hooks)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
