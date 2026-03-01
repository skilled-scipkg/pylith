---
name: pylith-theory-and-methods
description: This skill should be used when users ask about theory and methods in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: Theory and Methods

## High-Signal Playbook
### Route Conditions
- Use this skill for governing-equation interpretation, constitutive-method questions, and theory-to-implementation mapping.
- Route practical simulation setup questions to `pylith-inputs-and-modeling`.
- Route run execution/output issues to `pylith-simulation-workflows`.
- Route unresolved runtime failures to `pylith-troubleshooting`.

### Triage Questions
- Which formulation is targeted: elasticity, incompressible elasticity, or poroelasticity?
- Is the question conceptual derivation, discretization behavior, or implementation mapping?
- Is quasistatic or dynamic behavior in scope?
- Is the user validating equations against a runnable benchmark/example?

### Canonical Workflow
1. Start from governing-equation docs and derivation pages.
2. Map each theoretical object (residual/Jacobian/subfield) to named implementation classes.
3. Validate with a minimal simulation representing the formulation.
4. Inspect source kernels/material classes only for unresolved symbol-level behavior.

### Minimal Working Example
```bash
cd examples/box-2d
pylith step01_axialdisp.cfg
```

### Validation Checkpoints
- Equation terms cited in answers map directly to the referenced docs.
- Theory statements are linked to specific implementation files/classes.
- Minimal example behavior is consistent with stated assumptions (quasistatic/dynamic).
- Parameter names used in explanations match current component docs.

## Scope
- Handle questions about theoretical background and algorithmic methods.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/governingeqns/index.md`
- `docs/user/governingeqns/elasticity/derivation.md`
- `docs/user/governingeqns/elasticity/index.md`
- `docs/user/governingeqns/poroelasticity/index.md`
- `docs/user/governingeqns/incompressible-elasticity/index.md`

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
- `pylith/materials/Elasticity.py` and `pylith/materials/Poroelasticity.py` (theory-level material behavior classes)
- `pylith/materials/RheologyElasticity.py` and `pylith/materials/IsotropicLinearElasticity.py` (constitutive model wiring)
- `modulesrc/materials/Elasticity.i` and `modulesrc/materials/RheologyElasticity.i` (SWIG boundaries for constitutive APIs)
- `libsrc/pylith/materials/Elasticity.cc` and `libsrc/pylith/materials/RheologyElasticity.cc` (C++ constitutive behavior)
- `libsrc/pylith/fekernels/Elasticity.hh` (residual/Jacobian kernels tied to derivations)
- `pylith/problems/Physics.py` and `libsrc/pylith/problems/Physics.cc` (theory-to-problem integration surface)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
