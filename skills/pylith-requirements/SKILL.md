---
name: pylith-requirements
description: This skill should be used when users ask about requirements in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Requirements

## High-Signal Playbook
### Route Conditions
- Use this skill for dependency requirements, version compatibility checks, and environment prerequisite verification.
- Route install/build mechanics to `pylith-build-and-install`.
- Route run-time HPC tuning to `pylith-parallel-hpc`.
- Route domain simulation questions to workflow/modeling skills after requirements are confirmed.

### Triage Questions
- Is the request about Python requirements, compiled dependencies, or runtime version compatibility?
- Is this for docs tooling, development, or production simulation runtime?
- Does `pylith --version` run in the target environment?
- Are PETSc/MPI/dependency versions known and consistent with the requested workflow?

### Canonical Workflow
1. Start with `docs/requirements.txt` for declared requirement context.
2. Verify runtime version/dependency info from PyLith utilities.
3. Confirm environment can run a baseline simulation before deep troubleshooting.
4. Escalate to build/install skill if dependency reconciliation requires rebuild/reinstall.

### Minimal Working Example
```bash
python -m pip install -r docs/requirements.txt
pylith --version

cd examples/box-2d
pylith step01_axialdisp.cfg
```

### Validation Checkpoints
- Requirement versions are explicit and reproducible.
- Runtime reports dependency versions without import/link errors.
- Baseline simulation runs after requirement changes.
- Requirement guidance distinguishes docs/dev/runtime needs.

## Scope
- Handle questions about documentation grouped under the 'requirements' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/requirements.txt`

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
- `setup.py` and `configure.ac` (declared dependency surfaces for Python and compiled stacks)
- `pylith/utils/CollectVersionInfo.py` (runtime dependency report generation)
- `pylith/utils/PetscManager.py` (PETSc-dependent initialization path)
- `pylith/utils/SimulationMetadata.py` (version constraints in workflow metadata)
- `modulesrc/utils/PylithVersion.i` (compiled version metadata bridge)
- `libsrc/pylith/utils/PylithVersion.cc`, `libsrc/pylith/utils/DependenciesVersion.cc`, and `libsrc/pylith/utils/PetscVersion.cc` (dependency/version implementation checks)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
