---
name: pylith-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Inputs and Modeling

## High-Signal Playbook
### Route Conditions
- Use this skill for mesh labels/groups, materials, boundary conditions, faults, subfields, and spatial database wiring (`docs/user/run-pylith/mesh.md`, `docs/user/physics/materials/index.md`, `docs/user/physics/bc/index.md`).
- Route run orchestration, output cadence, and utility commands to `pylith-simulation-workflows`.
- Route first-install onboarding to `pylith-getting-started`.
- Route governing-equation derivations to `pylith-theory-and-methods`.
- Route hard runtime failures to `pylith-troubleshooting`.

### Triage Questions
- Domain type: 2D or 3D, and cell type (tri/quad/tet/hex)?
- Mesh source and format: ASCII, Cubit Exodus, Gmsh, or PETSc HDF5 (`docs/user/run-pylith/mesh.md`)?
- Are material IDs and boundary/fault groups correctly labeled in the mesh?
- Physics model: elasticity, incompressible elasticity, or poroelasticity (`docs/user/physics/materials/index.md`)?
- Boundary condition inventory and types (`DirichletTimeDependent`, `NeumannTimeDependent`, etc.)?
- Fault style: prescribed slip (`FaultCohesiveKin`) or Green's function impulses (`FaultCohesiveImpulses`)?
- Which spatial databases are used, and do `value-names` match expected field names?

### Canonical Workflow
1. Validate mesh label strategy first: `material-id` plus boundary/fault groups (`docs/user/run-pylith/mesh.md`).
2. Define material components and per-material spatial DBs (`docs/user/physics/materials/index.md`).
3. Define BC component array and bind component types per boundary (`docs/user/physics/bc/index.md`).
4. Configure faults/interfaces and buried edges where required (`docs/user/components/faults/FaultCohesiveImpulses.md`).
5. Set problem defaults (`name`, `output_directory`, `quadrature_order`, `output_basis_order`) before tuning individual components (`docs/user/components/problems/ProblemDefaults.md`).
6. Use help switches to inspect component properties before editing low-level parameters (`docs/user/run-pylith/overview.md`).
7. Run the simplest relevant example step (`examples/box-2d`, `examples/strikeslip-2d`, `examples/reverse-2d`) and compare expected output structure.
8. Escalate to source map only after docs and example parity checks fail.

### Minimal Working Example
```cfg
[pylithapp.problem]
materials = [rock]
bc = [x_neg, x_pos]

materials.rock = pylith.materials.Elasticity
bc.x_neg = pylith.bc.DirichletTimeDependent
bc.x_pos = pylith.bc.NeumannTimeDependent

[pylithapp.problem.materials.rock]
label_value = 1
db_auxiliary_field = spatialdata.spatialdb.UniformDB
db_auxiliary_field.values = [density, vs, vp]
```

```bash
# Use with a compatible mesh/material labeling setup.
pylith step03_sheardisptract.cfg
```

### Pitfalls And Fixes
- Missing or wrong `material-id` labels: material assignment fails or is silently wrong; verify mesh group labeling (`docs/user/run-pylith/mesh.md`).
- Boundary conditions attached to invalid/disconnected surfaces: ensure proper mesh marking and simply connected boundaries (`docs/user/physics/bc/index.md`).
- Deprecated vertex-marked BC/fault groups: prefer faces/sidesets/physical groups; vertex marking is deprecated (`docs/user/run-pylith/mesh.md`).
- Gmsh/HDF5 reader misses format: filename must end in `.msh` or `.h5` (`docs/user/run-pylith/mesh.md`).
- Spatial DB name mismatches (dash vs underscore): use current field naming with underscores (`docs/user/examples/troubleshooting-2d/step06-error05.md`).
- Spatial DB count mismatch (`num-locs` inconsistent with point count): fix metadata and point rows (`docs/user/examples/troubleshooting-2d/step06-error04.md`).
- Fault intersections/termination errors in multi-fault models: set `edge` / `edge_value` for buried fault edges (`docs/user/examples/troubleshooting-2d/step06-error07.md`).

### Convergence And Validation Checks
- Open `*_info.xmf` files and verify fault/boundary orientation fields look physically consistent (`docs/user/problems/output.md`).
- Inspect HDF5 structure quickly (`h5dump -n output/<file>.h5`) to confirm field groups and timestamps (`docs/user/problems/output.md`).
- Compare coarse/refined or basis-order variants to ensure trends are stable (`examples/reverse-2d/README.md`, `examples/box-2d/README.md`).
- Keep nondimensional scales and material magnitudes consistent enough for solver robustness (`docs/user/problems/nondimensionalization.md`, `docs/user/run-pylith/petsc-options.md`).
- For output decimation by time, avoid exact time-step multiples when roundoff causes skipped output (`docs/user/components/meshio/OutputTriggerTime.md`).

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/barwaves-2d/README.md`
- `examples/subduction-2d/README.md`
- `examples/strikeslip-2d/README.md`
- `examples/box-3d/README.md`
- `examples/box-2d/README.md`
- `docs/user/physics/bc/index.md`
- `examples/subduction-3d/input/README.md`
- `docs/user/physics/materials/index.md`
- `docs/user/components/materials/index.md`
- `docs/user/meshing/gmsh.md`
- `docs/user/run-pylith/mesh.md`
- `docs/user/governingeqns/petsc-formulation.md`

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
- `pylith/materials/Material.py` and `libsrc/pylith/materials/Material.cc` (material setup and kernel hooks)
- `pylith/bc/DirichletTimeDependent.py` and `pylith/bc/NeumannTimeDependent.py` (BC inventory behavior)
- `pylith/faults/FaultCohesiveImpulses.py` and `libsrc/pylith/faults/FaultCohesiveImpulses.cc` (fault impulse configuration/verification)
- `pylith/meshio/gmsh_utils.py` (Gmsh physical-group helpers and labeling behavior)
- `pylith/topology/MeshImporter.py` and `pylith/meshio/MeshIOPetsc.py` (mesh import path)
- `pylith/problems/Physics.py` / `modulesrc/problems/Physics.i` / `libsrc/pylith/problems/Physics.cc` (physics component plumbing)
- `pylith/problems/ProblemDefaults.py` (global defaults for quadrature/output naming)
- `pylith/meshio/OutputSolnDomain.py` and `pylith/meshio/OutputSolnBoundary.py` (output field projection points)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
