---
name: pylith-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Parallel and HPC

## High-Signal Playbook
### Route Conditions
- Use this skill for MPI execution, launcher/scheduler options, rank distribution, and scaling diagnostics.
- Route install/environment failures to `pylith-build-and-install`.
- Route modeling/input issues to `pylith-inputs-and-modeling`.
- Route generic runtime errors not tied to parallelism to `pylith-troubleshooting`.

### Triage Questions
- Desktop/laptop or cluster scheduler workflow?
- Serial run succeeds before enabling parallel execution?
- Which launcher/scheduler options are active (`--launcher`, `--scheduler`, `--nodes`)?
- Is failure in startup (MPI init), mesh distribution, solve, or output I/O?
- Is offline networking requiring `IF_PROVIDER=sockets`?

### Canonical Workflow
1. Validate simulation in serial mode first.
2. Scale to small MPI count (`--nodes=2` or `--nodes=4`) and compare behavior.
3. Use `--launcher.dry` / `--scheduler.dry` to verify generated execution commands.
4. Prefer HDF5 output for larger runs and monitor parallel I/O behavior.
5. Escalate to MPI/distributor source entry points when option-level fixes fail.

### Minimal Working Example
```bash
cd examples/box-2d
pylith step01_axialdisp.cfg --nodes=4

# Inspect launcher/scheduler command construction.
pylith step01_axialdisp.cfg --nodes=4 --launcher.dry
pylith step01_axialdisp.cfg --nodes=32 --scheduler=slurm --scheduler.dry
```

### Validation Checkpoints
- Parallel run reproduces serial results within expected tolerances.
- Dry-run launcher/scheduler command matches target HPC environment.
- No MPI init/network errors across ranks.
- Progress/output files are produced consistently for multi-rank runs.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/developer/performance/index.md`
- `docs/user/run-pylith/overview.md`
- `docs/user/run-pylith/petsc-options.md`
- `docs/user/examples/troubleshooting-2d/step06-error10.md`
- `docs/user/examples/troubleshooting-2d/step06-error06.md`
- `docs/developer/performance/logging.md`

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
- `pylith/apps/PyLithApp.py` and `pylith/apps/RunnerApp.py` (parallel launch option plumbing)
- `pylith/mpi/Communicator.py` (communicator/rank behavior)
- `pylith/topology/Distributor.py` (partition/distribution setup)
- `pylith/utils/PetscDefaults.py` and `pylith/utils/PetscManager.py` (parallel solver option defaults)
- `modulesrc/mpi/mpi.i`, `modulesrc/mpi/mpi_comm.i`, `modulesrc/mpi/mpi_error.i`, and `modulesrc/mpi/mpi_reduce.i` (MPI SWIG boundary)
- `modulesrc/topology/Distributor.i` (distribution SWIG boundary)
- `libsrc/pylith/utils/mpi.hh` (C++ MPI helper interfaces)
- `libsrc/pylith/topology/Distributor.cc` and `libsrc/pylith/problems/TimeDependent.cc` (distributed runtime behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
