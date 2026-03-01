---
name: pylith-troubleshooting
description: This skill should be used when users ask about troubleshooting in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Troubleshooting

## High-Signal Playbook
### Route Conditions
- Use this skill for runtime errors, solver divergence, missing-data failures, and diagnosis workflows.
- Route install/link/import failures to `pylith-build-and-install`.
- Route model wiring mistakes to `pylith-inputs-and-modeling`.
- Route scheduler/MPI-only failures to `pylith-parallel-hpc`.

### Triage Questions
- What exact command, cfg file, and error text were used?
- Does the issue happen at startup, mesh import, setup, solve, or post-processing?
- Is the run serial or parallel?
- Are parameter dumps/log files available for reproduction?
- Is this a known issue in recent release notes?

### Canonical Workflow
1. Reproduce with the smallest example/cfg that still fails.
2. Capture full stderr/stdout plus a parameter dump.
3. Match error signature against troubleshooting docs/examples and release notes.
4. Apply minimum viable fix, then rerun the same reproduction command.
5. Escalate to source-level checks for unresolved errors.

### Minimal Working Example
```bash
pylith step06_twofaults.cfg > run.log 2>&1
pylith_dumpparameters --format=json --filename=output/failed-parameters.json
rg -n "PETSC ERROR|Traceback|ERROR" run.log
```

### Validation Checkpoints
- Reproduction command is stable and deterministic.
- Error signature maps to a documented troubleshooting pattern.
- Fix removes the targeted error without introducing new failures.
- Parameter dump confirms corrected settings are active.

## Scope
- Handle questions about known issues, diagnostics, and debugging patterns.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/run-pylith/troubleshooting.md`
- `docs/user/examples/troubleshooting-2d/index.md`
- `docs/developer/debugging/index.md`
- `release-notes/announce_v4.1.3.md`
- `release-notes/announce_v4.0.0.md`
- `release-notes/announce_v4.1.2.md`
- `release-notes/announce_v3.0.0.md`
- `release-notes/announce_v4.1.1.md`
- `release-notes/announce_v3.0.3.md`
- `release-notes/announce_v3.0.2.md`
- `release-notes/announce_v3.0.1.md`
- `release-notes/announce_v4.2.0.md`
- `release-notes/announce_v4.1.0.md`

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
- `pylith/problems/Problem.py` and `pylith/problems/TimeDependent.py` (common runtime failure surfaces)
- `pylith/utils/DumpParametersJson.py` (configuration capture during triage)
- `modulesrc/problems/Problem.i` and `modulesrc/mpi/mpi_error.i` (Python/C++ error boundary)
- `libsrc/pylith/utils/error.h` and `libsrc/pylith/utils/error.hh` (error macros and diagnostics)
- `libsrc/pylith/problems/Problem.cc` and `libsrc/pylith/problems/TimeDependent.cc` (solve-path error context)
- `libsrc/pylith/problems/ProgressMonitorTime.cc` (progress diagnostics behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
