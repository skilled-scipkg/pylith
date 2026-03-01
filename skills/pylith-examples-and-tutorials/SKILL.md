---
name: pylith-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Examples and Tutorials

## High-Signal Playbook
### Route Conditions
- Use this skill when the user asks for runnable examples, tutorial progression, minimal reproductions, or how docs tutorial pages map to example folders (`docs/user/examples/index.md`, `examples/README.md`).
- Route model-construction details to `pylith-inputs-and-modeling`.
- Route run/output utility details to `pylith-simulation-workflows`.
- Route hard runtime failures to `pylith-troubleshooting`.
- Route onboarding/install prerequisites to `pylith-getting-started`.

### Triage Questions
- What difficulty level is needed: novice, beginner, or intermediate (`docs/user/examples/index.md`)?
- 2D or 3D, and what physics/fault style is required?
- Need mesh generation steps (Gmsh/Cubit) or bundled meshes?
- Single-step reproduction or full-suite execution?
- Are there step dependencies on previous outputs (for example subduction inversion workflow)?
- Is the goal validation/training or debugging a failure?

### Canonical Workflow
1. Pick suite by difficulty and physics using `docs/user/examples/index.md`.
2. Open matching runnable instructions in `examples/<suite>/README.md`.
3. If meshing is optional, run mesh-generation scripts only when needed and keep overwrite warnings in mind.
4. Execute steps in documented order from simpler to more complex.
5. Use `pylith_cfgsearch` to find cfg files by features when selecting reproductions (`docs/user/run-pylith/utilities.md`).
6. For multi-step pipelines, complete prerequisite steps that provide required outputs.
7. If outputs/errors diverge from docs, pivot to troubleshooting examples before source inspection.

### Minimal Working Example
```bash
# Discover feature-tagged examples.
pylith_cfgsearch --path=examples/strikeslip-2d --display=description,keywords

# Novice baseline run.
cd examples/box-2d
pylith step01_axialdisp.cfg

# Beginner fault run.
cd ../strikeslip-2d
pylith step01a_slip.cfg
```

### Pitfalls And Fixes
- Mesh generation scripts can overwrite distributed mesh files; copy backups first (`examples/subduction-2d/README.md`, `examples/crustal-strikeslip-2d/README.md`).
- Some legacy steps are explicitly not updated for newer versions; prefer updated steps/suites (`examples/subduction-2d/README.md`, `examples/subduction-3d/README.md`).
- Multi-step suites may consume prior outputs; skipping prerequisites breaks later steps (for example Subduction 3D Step 7).
- Spatial DB format/name issues in copied inputs often mimic solver failures; use troubleshooting error walkthroughs (`docs/user/examples/troubleshooting-2d/step06-error04.md`, `step06-error05.md`).
- Fault geometry/termination mistakes can manifest as PETSc divergence; verify fault info output and buried edge labeling (`docs/user/examples/troubleshooting-2d/step06-error07.md`).

### Convergence And Validation Checks
- Confirm expected output files are produced per step before moving to the next step.
- Compare coarse/refined/higher-order variants where available in the suite README.
- For inversion tutorials, ensure data-generation scripts complete before inversion scripts (`examples/subduction-3d/README.md`).
- Use troubleshooting suite as a control for interpreting common PyLith error signatures.
- Keep docs and runnable folder alignment explicit: pair `docs/user/examples/<suite>/...` with `examples/<suite>/README.md`.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/README.md`
- `examples/reverse-2d/README.md`
- `examples/poroelastic-outerrise-2d/README.md`
- `examples/crustal-strikeslip-2d/README.md`
- `examples/subduction-3d/scratch/README.md`
- `docs/user/components/faults/FaultCohesiveImpulses.md`
- `docs/user/components/problems/GreensFns.md`
- `docs/user/examples/troubleshooting-2d/step06-error09.md`
- `docs/user/examples/troubleshooting-2d/step06-error08.md`
- `docs/user/examples/troubleshooting-2d/step06-error07.md`
- `docs/user/examples/troubleshooting-2d/step06-error05.md`
- `docs/user/examples/troubleshooting-2d/step06-error04.md`

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
- `pylith/apps/RunnerApp.py` and `pylith/utils/SimulationMetadata.py` (example cfg discovery and execution)
- `pylith/problems/GreensFns.py` / `modulesrc/problems/GreensFns.i` / `libsrc/pylith/problems/GreensFns.cc` (Green's function behavior used in tutorial workflows)
- `pylith/faults/FaultCohesiveImpulses.py` / `modulesrc/faults/FaultCohesiveImpulses.i` / `libsrc/pylith/faults/FaultCohesiveImpulses.cc` (fault impulse setup)
- `pylith/problems/ProblemDefaults.py` (simulation naming/output defaults used throughout examples)
- `examples/subduction-3d/make_synthetic_gnssdisp.py` and `examples/subduction-3d/slip_invert.py` (post-processing and inversion tutorial scripts)
- `pylith/problems/SubfieldDisplacement.py`, `pylith/problems/SubfieldVelocity.py`, and `pylith/problems/SubfieldPressure.py` (solution subfield wiring reflected in outputs)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
