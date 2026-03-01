---
name: pylith-tests
description: This skill should be used when users ask about tests in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Tests

## High-Signal Playbook
### Route Conditions
- Use this skill for pytest/manual test execution, regression triage, and behavior validation before/after code/config changes.
- Route simulation setup corrections to `pylith-getting-started` or `pylith-simulation-workflows`.
- Route deep architecture changes to `pylith-developer-guide`.
- Route solver/runtime failure interpretation to `pylith-troubleshooting`.

### Triage Questions
- Is the failure in pytests, manual tests, or full-scale runs?
- Which subsystem is affected (meshio, problems, materials, mpi, utils)?
- Is this a reproducible regression or an environment-dependent failure?
- Is Jacobian checking required for the manual powerlaw suites?

### Canonical Workflow
1. Reproduce with the narrowest pytest target first.
2. If needed, escalate to manual powerlaw suites for constitutive/Jacobian behavior.
3. Compare expected artifacts (output files, logs, residual behavior) against baseline.
4. Use source map entry points for failing subsystem only.

### Minimal Working Example
```bash
pytest tests/pytests/test_pylith.py
pytest tests/pytests/problems/TestProblem.py
pytest tests/pytests/meshio/TestOutputSoln.py

cd tests/manual/powerlaw-2d
./run_tests.py --sim axialtraction_powerlaw
```

### Validation Checkpoints
- Reproduction test fails pre-fix and passes post-fix.
- No new failures in neighboring subsystem tests.
- Manual test logs show expected convergence trends.
- Output/point files match expected format and field inventory.

## Scope
- Handle questions about documentation grouped under the 'tests' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/developer/testing/index.md`
- `docs/developer/testing/pytests.md`
- `docs/developer/testing/fullscale.md`
- `tests/manual/powerlaw-2d/TODO.md`
- `tests/manual/powerlaw-2d/README.md`
- `tests/manual/powerlaw-3d/README.md`
- `tests/pytests/meshio/data/points.txt`
- `tests/pytests/meshio/data/point.txt`
- `tests/pytests/meshio/data/twohex8.txt`
- `tests/pytests/meshio/data/mesh2Din3D.txt`
- `tests/pytests/meshio/data/cube2.txt`

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
- `pylith/meshio/PointsList.py` and `pylith/meshio/OutputSolnPoints.py` (point-output behavior)
- `pylith/meshio/DataWriterHDF5.py`, `pylith/meshio/DataWriterHDF5Ext.py`, and `pylith/meshio/DataWriterVTK.py` (writer behavior under tests)
- `modulesrc/meshio/OutputSolnPoints.i` and `modulesrc/meshio/DataWriterHDF5.i` (SWIG boundaries for test targets)
- `libsrc/pylith/meshio/OutputSolnPoints.cc` and `libsrc/pylith/meshio/DataWriterHDF5.cc` (C++ implementation checks)
- `pylith/problems/Problem.py` and `pylith/problems/TimeDependent.py` (common failure surfaces in regression suites)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
