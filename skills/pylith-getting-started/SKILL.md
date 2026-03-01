---
name: pylith-getting-started
description: This skill should be used when users ask about getting started in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Getting Started

## High-Signal Playbook
### Route Conditions
- Use this skill when the user needs first-run setup, install sanity checks, or a "what should I run first?" path (`docs/intro/quickstart.md`, `docs/user/install/index.md`).
- Route source-build and dependency breakages to `pylith-build-and-install`.
- Route model configuration questions to `pylith-inputs-and-modeling`.
- Route runtime/output/debugging issues to `pylith-simulation-workflows` or `pylith-troubleshooting`.
- Route example selection/depth progression to `pylith-examples-and-tutorials`.

### Triage Questions
- Which install mode is in use: binary package, Docker, or source build (`docs/user/install/index.md`)?
- What platform and shell are being used (Linux/macOS/WSL, bash-compatible shell for `setup.sh`)?
- Does `pylith --version` run successfully?
- Is the failure at import/startup, mesh read, configuration verification, or solve stage?
- Which example suite and step are they trying to run (`docs/user/examples/index.md`)?
- Serial or parallel run (`--nodes`), and are they offline (`IF_PROVIDER=sockets`) (`docs/user/run-pylith/overview.md`)?

### Canonical Workflow
1. Choose install path from `docs/user/install/index.md`; for binaries, unpack and `source setup.sh`.
2. Verify executable resolution and version before simulations (`docs/user/install/index.md`, `docs/user/run-pylith/overview.md`).
3. Start with a novice example (`box-2d` or `box-3d`) from `docs/user/examples/index.md`.
4. Run one baseline step, then inspect generated output files (`docs/user/run-pylith/overview.md`).
5. Use Pyre help switches to inspect component properties before changing parameters (`docs/user/run-pylith/overview.md`).
6. If running parallel, prefer HDF5 PETSc mesh format and validate launcher/scheduler with dry-run options (`docs/user/run-pylith/overview.md`, `docs/user/run-pylith/utilities.md`).
7. If errors persist, dump parameters and move to troubleshooting examples (`docs/user/run-pylith/troubleshooting.md`, `docs/user/examples/troubleshooting-2d/index.md`).

### Minimal Working Example
```bash
cd examples/box-2d
pylith step01_axialdisp.cfg

# Inspect available Pyre knobs before editing cfg files.
pylith step01_axialdisp.cfg --problem.help-properties
pylith step01_axialdisp.cfg --problem.help-components

# Dump resolved parameters to confirm what PyLith actually used.
pylith_dumpparameters --format=json --filename=output/step01-parameters.json
```

### Pitfalls And Fixes
- `ImportError: liblapack...`: environment not initialized; run `source setup.sh` in unpacked distribution (`docs/user/run-pylith/troubleshooting.md`).
- Running `pylith` with no simulation metadata/input: expected configuration error; run an example cfg first (`docs/user/install/index.md`).
- Wrong `mpirun` first on `PATH`: can cause unknown Pyre/launcher options (`docs/user/run-pylith/troubleshooting.md`).
- Offline desktop/laptop MPI failures: set `IF_PROVIDER=sockets` (`docs/user/run-pylith/overview.md`).
- Gmsh/HDF5 mesh not recognized: enforce `.msh` or `.h5` extension (`docs/user/run-pylith/mesh.md`).
- Conflicting system Python/libs with binary package: start from clean environment and prepend PyLith paths (`docs/user/install/index.md`).

### Convergence And Validation Checks
- Confirm a progress monitor file and final "Finalizing problem" messages appear (`docs/user/components/problems/ProgressMonitorTime.md`, `docs/user/install/index.md`).
- Confirm expected `output/*.h5` and `output/*.xmf` files are created (`docs/user/run-pylith/overview.md`).
- Run coarse first, then refine mesh/order and compare displacement/stress trends (`docs/user/examples/index.md`).
- Enable solver monitors when behavior is unclear (`docs/user/run-pylith/petsc-options.md`).
- For parallel startup, compare `--scheduler.dry` / `--launcher.dry` output against expected cluster command (`docs/user/run-pylith/overview.md`).

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/run-pylith/overview.md`
- `docs/developer/building/index.md`
- `docs/user/examples/index.md`
- `docs/intro/index.md`
- `docs/user/meshing/overview.md`
- `docs/intro/quickstart.md`
- `docs/user/benchmarks/index.md`
- `docs/developer/design/overview.md`
- `docs/user/examples/subduction-3d/index.md`
- `docs/user/examples/subduction-2d/index.md`
- `docs/user/examples/strikeslip-2d/index.md`
- `docs/user/examples/reverse-2d/index.md`

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
- `pylith/apps/PyLithApp.py` (top-level run sequence, setup/run/finalize stages)
- `pylith/apps/RunnerApp.py` (`pylith_runner` behavior and metadata-driven batch runs)
- `pylith/utils/SimulationMetadata.py` (required metadata fields, version constraints)
- `pylith/utils/DumpParametersJson.py` (parameter snapshots for reproducibility/debugging)
- `pylith/topology/MeshImporter.py` (mesh loading/reordering entry point)
- `pylith/meshio/MeshIOPetsc.py` (Gmsh/HDF5 mesh reader path)
- `pylith/problems/TimeDependent.py` (time-dependent problem execution)
- `pylith/problems/ProblemDefaults.py` (output directory/name/quadrature defaults)
- `pylith/utils/PetscDefaults.py` (default PETSc option categories)
- `libsrc/pylith/problems/TimeDependent.cc` (C++ solve call path when Python logs are insufficient)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
