---
name: pylith-build-and-install
description: This skill should be used when users ask about build and install in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Build and Install

## High-Signal Playbook
### Route Conditions
- Use this skill for dependency setup, binary/source installation, environment initialization, and compile/install verification.
- Route first simulation execution questions to `pylith-getting-started`.
- Route cluster launcher/runtime tuning to `pylith-parallel-hpc`.
- Route simulation-logic failures after successful install to `pylith-troubleshooting`.

### Triage Questions
- Is the user on a binary package, container, or source build?
- Which platform and shell are used for environment setup?
- Does `pylith --version` run after setup?
- Is failure during configure, compile, import/linking, or first simulation startup?
- Are Python and MPI executables coming from the intended environment?

### Canonical Workflow
1. Choose install path from `docs/user/install/index.md` and initialize the environment (`source setup.sh` for binary package).
2. Verify executable and dependency visibility with `pylith --version`.
3. For source builds, run configure/build/install with explicit prefixes and MPI/PETSc paths as needed.
4. Run a minimal example simulation to confirm runtime stack integrity.
5. Capture resolved parameters to confirm runtime is not using stale configs.
6. Escalate to source maps for version/binding/build-graph checks only when docs-based fixes fail.

### Minimal Working Example
```bash
# Binary package workflow
source setup.sh
pylith --version

cd examples/box-2d
pylith step01_axialdisp.cfg
```

```bash
# Source-build workflow (adjust prefixes/toolchain as needed)
./configure
make -j"$(nproc)"
make install
```

### Validation Checkpoints
- `pylith --version` succeeds in the same shell used for simulations.
- A novice example runs without import/linker failures.
- Output files appear under the simulation output directory with expected names.
- Parameter dump reflects current environment and cfg values.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/install/index.md`
- `docs/developer/building/index.md`
- `INSTALL`
- `docs/user/run-pylith/parameter-gui.md`
- `docs/developer/git-workflow/git-quickref.md`
- `docs/developer/debugging/ci-docker.md`
- `docs/user/examples/subduction-3d/meshing-cubit.md`
- `docs/developer/contributing/documentation/install.md`

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
- `configure.ac` (autotools feature detection and dependency probes)
- `setup.py` (Python packaging/install metadata)
- `pylith/apps/PyLithApp.py` (startup path used by installed CLI)
- `pylith/apps/PetscApplication.py` (PETSc initialization behavior)
- `pylith/utils/CollectVersionInfo.py` (runtime dependency/version verification)
- `modulesrc/utils/PylithVersion.i` and `libsrc/pylith/utils/PylithVersion.cc` (compiled version metadata path)
- `pylith/Makefile.am`, `modulesrc/Makefile.am`, and `libsrc/Makefile.am` (build graph wiring)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
