---
name: pylith-api-and-scripting
description: This skill should be used when users ask about api and scripting in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: API and Scripting

## High-Signal Playbook
### Route Conditions
- Use this skill for component APIs, programmatic parameter control, SWIG/Python binding behavior, and script-driven simulation workflows.
- Route pure modeling choices to `pylith-inputs-and-modeling`.
- Route run orchestration/output utilities to `pylith-simulation-workflows`.
- Route compiler/toolchain failures to `pylith-build-and-install`.

### Triage Questions
- Is the user asking about Python component APIs, SWIG layer behavior, or C++ implementation details?
- Are they scripting one simulation or batch-driving many cfg files?
- Which component class is involved (`FaultCohesiveKin`, `Poroelasticity`, `KinSrc*`, etc.)?
- Is the issue in property discovery/help output, configuration resolution, or runtime behavior?

### Canonical Workflow
1. Start from component docs and governing-equation pages listed below.
2. Inspect runtime component/property surfaces with Pyre help switches before source edits.
3. Capture resolved parameters (`pylith_dumpparameters`) to verify API-driven overrides.
4. If behavior differs from docs, inspect Python class, SWIG `.i`, then C++ implementation in that order.
5. Use focused symbol search for method/property names rather than broad repository scans.

### Minimal Working Example
```bash
cd examples/strikeslip-2d
pylith step01a_slip.cfg --problem.help-components
pylith step01a_slip.cfg --problem.interfaces.help-components
pylith_dumpparameters --format=json --filename=output/step01a-parameters.json
```

### Validation Checkpoints
- Help output shows expected components/properties for the targeted class.
- Dumped parameters reflect scripted overrides and intended defaults.
- Python/SWIG/C++ symbols align for the same component method/property.
- A small example run produces expected outputs after API-related changes.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/physics/faults/index.md`
- `docs/developer/implementation/petsc-fem.md`
- `docs/user/components/utils/SimulationMetadata.md`
- `docs/user/components/utils/DumpParametersJson.md`
- `docs/user/components/faults/FaultCohesiveKin.md`
- `docs/user/appendices/analytical-solns.md`
- `docs/developer/testing/libtests.md`
- `docs/user/meshing/cubit.md`
- `docs/user/governingeqns/elasticity/prescribed-slip-dynamic.md`
- `docs/user/governingeqns/elasticity/infinitesimal-strain-quasistatic.md`
- `docs/user/governingeqns/poroelasticity/infinitesimal-strain-quasistatic.md`
- `docs/user/governingeqns/incompressible-elasticity/infinitesimal-strain-quasistatic.md`
- `examples/strikeslip-2d/gnss_stations.txt`
- `docs/user/governingeqns/poroelasticity/prescribed-slip-quasistatic.md`

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
- `pylith/faults/FaultCohesiveKin.py` (prescribed-slip interface component API)
- `pylith/faults/KinSrcTimeHistory.py` and `pylith/faults/KinSrcStep.py` (rupture time-function APIs)
- `pylith/materials/Poroelasticity.py` and `pylith/materials/Elasticity.py` (material API surfaces)
- `pylith/utils/SimulationMetadata.py` (metadata schema and argument handling)
- `pylith/utils/DumpParametersJson.py` (resolved parameter export behavior)
- `modulesrc/faults/FaultCohesiveKin.i` and `modulesrc/materials/Poroelasticity.i` (SWIG boundaries)
- `modulesrc/problems/Physics.i` (problem-physics API bridge)
- `libsrc/pylith/faults/FaultCohesiveKin.cc` and `libsrc/pylith/materials/Poroelasticity.cc` (C++ behavior checks)
- `libsrc/pylith/problems/Physics.cc` (problem integration behavior)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
