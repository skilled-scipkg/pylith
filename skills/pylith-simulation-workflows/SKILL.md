---
name: pylith-simulation-workflows
description: This skill should be used when users ask about simulation workflows in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Simulation Workflows

## High-Signal Playbook
### Route Conditions
- Use this skill for run sequencing, utility usage, solver/output controls, progress monitoring, and workflow continuation across multi-step examples (`docs/user/run-pylith/index.md`, `docs/user/run-pylith/utilities.md`, `docs/user/problems/output.md`).
- Route initial setup questions to `pylith-getting-started`.
- Route model/physics wiring to `pylith-inputs-and-modeling`.
- Route concrete example selection and step scripts to `pylith-examples-and-tutorials`.
- Route persistent runtime errors and solver failures to `pylith-troubleshooting`.

### Triage Questions
- Single run, batch run, or suite run (`pylith` vs `pylith_runner`)?
- Serial or parallel run, and what launcher/scheduler settings are used?
- Time-dependent (`TimeDependent`) or Green's function (`GreensFns`) workflow?
- Are outputs required at domain, boundary, points, or faults/materials?
- What output cadence is needed (`OutputTriggerStep` vs `OutputTriggerTime`)?
- Is this a continuation from a prior step (for example, Step 6 outputs reused in Step 7 inversion)?
- Is failure happening during startup/configuration, solve, or post-processing?

### Canonical Workflow
1. Confirm run mode and command shape (`pylith ...cfg` or `pylith_runner --path=...`) (`docs/user/run-pylith/overview.md`, `docs/user/run-pylith/utilities.md`).
2. Validate metadata/help output before long runs (`--help-properties`, `pylith_dumpparameters`) (`docs/user/run-pylith/overview.md`, `docs/user/run-pylith/utilities.md`).
3. Run in serial first on coarse mesh, then scale to parallel with validated launcher/scheduler (`docs/user/run-pylith/overview.md`).
4. Set output writer/trigger strategy (HDF5 preferred; step/time decimation as needed) (`docs/user/problems/output.md`).
5. Track progress with progress monitor files and PETSc monitors (`docs/user/problems/output.md`, `docs/user/run-pylith/petsc-options.md`).
6. For continuation/restart-style workflows, follow documented step dependencies that reuse previous outputs (for example `subduction-3d` Step 6 to Step 7 inversion) (`docs/user/examples/subduction-3d/step07-greensfns.md`).
7. If Xdmf metadata is missing/corrupted after file moves, regenerate with `pylith_genxdmf` from the same relative working path (`docs/user/run-pylith/utilities.md`).

### Minimal Working Example
```bash
# 1) Baseline run.
pylith step01_axialdisp.cfg

# 2) Snapshot full resolved parameters for reproducibility.
pylith_dumpparameters --format=json --filename=output/step01-parameters.json

# 3) Batch-run a suite that has metadata.arguments in cfg files.
pylith_runner --path=examples/box-2d

# 4) Recover Xdmf sidecar metadata if needed.
pylith_genxdmf --files=output/*.h5
```

### Pitfalls And Fixes
- `pylith_runner` skips cfg files lacking simulation metadata arguments; add valid `[pylithapp.metadata]` (`docs/user/run-pylith/pylithapp.md`, `docs/user/run-pylith/utilities.md`).
- Unexpectedly sparse output with time trigger: use slightly smaller `elapsed_time` (for example `0.9999*year`) to avoid roundoff skips (`docs/user/components/meshio/OutputTriggerTime.md`).
- Parallel HDF5/Xdmf read issues after moving files: run `pylith_genxdmf` from original relative layout (`docs/user/run-pylith/utilities.md`, `docs/user/problems/output.md`).
- Solver failure due missing constraints (e.g., zero pivot): add/verify Dirichlet constraints or adjust preconditioner (`docs/user/run-pylith/troubleshooting.md`).
- Fault-split parallel divergence with some defaults: use documented fallback solver settings when needed (`docs/user/run-pylith/petsc-options.md`).
- VTK output at scale becomes cumbersome; prefer HDF5 output for large runs (`docs/user/problems/output.md`).

### Convergence And Validation Checks
- Progress monitor file updates should align with expected completion behavior (`docs/user/components/problems/ProgressMonitorTime.md`, `docs/user/components/problems/ProgressMonitorStep.md`).
- PETSc monitor output should show decreasing residuals and clear convergence reasons (`docs/user/run-pylith/petsc-options.md`).
- Output file set should include expected `info` and `data` artifacts for configured observers (`docs/user/problems/output.md`).
- For continuation workflows, verify downstream scripts consume outputs from expected prior steps (for example Step 6 to Step 7 inversion chain) (`docs/user/examples/subduction-3d/step07-greensfns.md`).
- For multi-step suites, compare key observables between coarse/refined variants before scaling up (`examples/reverse-2d/README.md`, `examples/subduction-3d/README.md`).

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/subduction-3d/README.md`
- `examples/crustal-strikeslip-3d/README.md`
- `examples/magma-2d/README.md`
- `examples/troubleshooting-2d/README.md`
- `tests/manual/powerlaw-3d/README.md`
- `tests/manual/powerlaw-2d/README.md`
- `docs/developer/git-workflow/index.md`
- `docs/user/run-pylith/index.md`
- `docs/user/problems/index.md`
- `docs/user/examples/troubleshooting-2d/index.md`
- `docs/user/benchmarks/savage-prescott.md`
- `docs/user/run-pylith/utilities.md`

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
- `pylith/apps/PyLithApp.py` (application run pipeline: meshing, setup, run, finalize)
- `pylith/apps/RunnerApp.py` (`pylith_runner` search/dispatch behavior)
- `pylith/problems/TimeDependent.py` and `libsrc/pylith/problems/TimeDependent.cc` (time-step solve loop)
- `pylith/problems/ProgressMonitorTime.py` and `pylith/problems/ProgressMonitorStep.py` (progress file behavior)
- `pylith/utils/DumpParametersJson.py` (capturing resolved run configuration)
- `pylith/meshio/OutputTriggerTime.py` and `pylith/meshio/OutputTriggerStep.py` (output decimation logic)
- `pylith/meshio/DataWriterHDF5.py` and `pylith/meshio/DataWriterHDF5Ext.py` (HDF5 writer modes)
- `pylith/problems/Physics.py` / `modulesrc/problems/Physics.i` / `libsrc/pylith/problems/Physics.cc` (problem-physics integration)
- `pylith/faults/KinSrcTimeHistory.py` and `pylith/faults/KinSrcStep.py` (time-dependent rupture source components)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
