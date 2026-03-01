---
name: pylith-index
description: This skill should be used when users ask how to use pylith and the correct generated documentation skill must be selected before going deeper into source code.
---

# pylith Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `pylith-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `pylith-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `pylith-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `pylith-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `pylith-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `pylith-developer-guide`: Developer Guide (developer architecture, extension points, and contribution workflow)
- `pylith-analysis-and-output`: Analysis and Output (output formats, analysis, and post-processing)
- `pylith-troubleshooting`: Troubleshooting (known issues, diagnostics, and debugging patterns)
- `pylith-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `pylith-parallel-hpc`: Parallel and HPC (MPI/OpenMP/GPU execution, scaling, and batch systems)
- `pylith-theory-and-methods`: Theory and Methods (theoretical background and algorithmic methods)
- `pylith-user`: User (documentation grouped under the 'user' theme)
- `pylith-release-notes`: Release Notes (documentation grouped under the 'release-notes' theme)
- `pylith-tests`: Tests (documentation grouped under the 'tests' theme)
- `pylith-references`: References (documentation grouped under the 'references' theme)
- `pylith-requirements`: Requirements (documentation grouped under the 'requirements' theme)

## Documentation-first inputs
- `docs`
- `release-notes`

## Tutorials and examples roots
- `examples`
- `docs/user/examples`

## Test roots for behavior checks
- `tests`
- `pylith/testing`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, search that skill's map file (for example `skills/pylith-simulation-workflows/references/doc_map.md`).
- If documentation still leaves ambiguity, open that skill's source map (for example `skills/pylith-simulation-workflows/references/source_map.md`) and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).

## Source directories for deeper inspection
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`
