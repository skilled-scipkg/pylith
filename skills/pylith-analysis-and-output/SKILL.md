---
name: pylith-analysis-and-output
description: This skill should be used when users ask about analysis and output in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Analysis and Output

## High-Signal Playbook
### Route Conditions
- Use this skill for output observer wiring, trigger cadence, writer format, Xdmf regeneration, and post-processing handoff.
- Route run orchestration and restart flow to `pylith-simulation-workflows`.
- Route mesh/material/BC setup issues to `pylith-inputs-and-modeling`.
- Route hard runtime failures to `pylith-troubleshooting`.

### Triage Questions
- What output scope is needed: domain, boundary, fault, material, or points?
- Which writer format is configured (`DataWriterHDF5`, `DataWriterHDF5Ext`, or `DataWriterVTK`)?
- What trigger policy is required (`OutputTriggerStep` vs `OutputTriggerTime`)?
- Are point locations supplied via a points-list file, and does it match mesh coordinates?
- Are `.h5` data files present but `.xmf` metadata missing?

### Canonical Workflow
1. Confirm observer list and output component names in cfg files (`docs/user/problems/output.md`).
2. Choose trigger strategy and cadence before long runs (`docs/user/components/meshio/OutputTrigger.md`).
3. Prefer HDF5 output for large simulations and keep filename prefixes deterministic.
4. Run one short baseline step and verify output artifacts before scaling up.
5. Regenerate Xdmf sidecars with `pylith_genxdmf` after file moves or copy operations.
6. Escalate to `references/source_map.md` only when docs and cfg inspection are insufficient.

### Minimal Working Example
```bash
cd examples/box-2d
pylith step01_axialdisp.cfg

# Regenerate Xdmf metadata if missing/corrupted.
pylith_genxdmf --files=output/*.h5
```

### Validation Checkpoints
- Output directory contains expected `*.h5` and `*.xmf` files for configured observers.
- Progress monitor and output timestamps advance consistently with trigger settings.
- Point-output files reflect requested coordinates and field names.
- Output field sets match configured subfields (for example displacement, pressure, velocity).

## Scope
- Handle questions about output formats, analysis, and post-processing.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/problems/output.md`
- `docs/user/run-pylith/utilities.md`
- `docs/developer/debugging/fields.md`
- `docs/user/physics/faults/slip-impulses.md`
- `docs/user/components/meshio/OutputSoln.md`
- `docs/user/components/meshio/OutputObserver.md`
- `docs/user/components/meshio/OutputTriggerTime.md`
- `docs/user/components/meshio/OutputTriggerStep.md`
- `docs/user/components/meshio/DataWriterHDF5.md`
- `tests/fullscale/linearelasticity/nofaults-3d/output_points.txt`
- `tests/fullscale/linearelasticity/nofaults-2d/output_points.txt`
- `tests/fullscale/linearelasticity/faults-3d/output_points.txt`
- `tests/fullscale/linearelasticity/faults-2d/output_points.txt`
- `tests/fullscale/incompressibleelasticity/nofaults-3d/output_points.txt`
- `tests/fullscale/incompressibleelasticity/nofaults-2d/output_points.txt`
- `docs/user/components/meshio/OutputTrigger.md`

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
- `pylith/meshio/OutputObserver.py` (observer lifecycle and component registration)
- `pylith/meshio/OutputSoln.py` (solution-field output orchestration)
- `pylith/meshio/OutputSolnPoints.py` (point-sampling path)
- `pylith/meshio/OutputTrigger.py` (shared trigger API contract)
- `pylith/meshio/OutputTriggerStep.py` and `pylith/meshio/OutputTriggerTime.py` (decimation behavior)
- `pylith/meshio/DataWriterHDF5.py` and `pylith/meshio/DataWriterHDF5Ext.py` (writer mode behavior)
- `modulesrc/meshio/OutputObserver.i`, `modulesrc/meshio/OutputSoln.i`, `modulesrc/meshio/OutputTriggerTime.i`, `modulesrc/meshio/DataWriterHDF5.i` (SWIG boundaries)
- `libsrc/pylith/meshio/OutputObserver.cc`, `libsrc/pylith/meshio/OutputSoln.cc`, `libsrc/pylith/meshio/OutputTriggerTime.cc`, `libsrc/pylith/meshio/DataWriterHDF5.cc` (C++ implementation checks)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
