---
name: pylith-user
description: This skill should be used when users ask about user in pylith; it prioritizes documentation references and then source inspection only for unresolved details.
---

# pylith: User

## High-Signal Playbook
### Route Conditions
- Use this skill for broad User Guide navigation requests spanning multiple user-doc sections (`docs/user/index.md`, `docs/user/components/index.md`, `docs/user/physics/index.md`).
- Route concrete onboarding/run tasks to `pylith-getting-started` and `pylith-simulation-workflows`.
- Route modeling details to `pylith-inputs-and-modeling`.
- Route example-specific execution to `pylith-examples-and-tutorials`.
- Use this skill as the map-quality gate during compile/audit passes (core playbook presence, doc/source maps, routing coherence).

### Triage Questions
- Is the request broad navigation or a specific simulation/build/debug task?
- Which user-guide section is primary: `run-pylith`, `problems`, `physics`, `components`, `examples`, or `file-formats`?
- Is the user asking for conceptual orientation, runnable commands, or component/property lookup?
- Which version context is relevant when interpreting user docs and examples?
- For skill-quality audits: do core skills include `## High-Signal Playbook`, `references/doc_map.md`, and `references/source_map.md`?
- For consolidation checks: how many topic skills have `Total docs grouped in this topic: 1`?

### Canonical Workflow
1. Classify the request and route to the narrowest topic skill first.
2. Use `docs/user/index.md` plus `docs/user/components/index.md` as the top-level routing map.
3. Pull only minimal section-specific docs from `references/doc_map.md` for the chosen route.
4. If docs are insufficient, escalate to source files listed in this skill (or routed skill) `references/source_map.md`.
5. For compile/audit mode, verify core skill completeness:
   - each core skill has `## High-Signal Playbook`,
   - doc/source maps remain present,
   - index routing still points to available topic skills.
6. Run one-doc-topic noise check before consolidation decisions.

### Minimal Working Example
```bash
# Quality-gate checks for skills folder audits.
rg -n "^## High-Signal Playbook" skills/pylith-*/SKILL.md
for f in skills/*/references/doc_map.md; do
  s=$(basename "$(dirname "$(dirname "$f")")")
  n=$(rg -n "Total docs grouped in this topic:" "$f" | sed -E 's/.*: ([0-9]+).*/\1/')
  printf "%s %s\n" "$s" "$n"
done | sort
```

### Pitfalls And Fixes
- Over-answering from the broad user map without routing to focused skills; always route first.
- Mixing developer docs into user-only questions too early; stay docs-first under `docs/user/*` unless escalation is required.
- Ignoring required simulation metadata when reproducing user runs; verify metadata section expectations (`docs/user/run-pylith/pylithapp.md`).
- Troubleshooting without full context; request version, parameters JSON, and full error output (`docs/user/intro/getting-help.md`).
- Consolidating one-doc skills too aggressively; only collapse when the count is truly noisy across many topics.

### Convergence And Validation Checks
- Routed skill should cover the request without opening many unrelated docs.
- User-answer path should cite concrete file paths under `docs/user/*` first.
- For compile audits, all core skills should have playbooks and preserved source entry links.
- Topic count should stay below cap and index routing should not reference missing folders.
- One-doc-topic consolidation decision should be explicit and evidence-backed.

## Scope
- Handle questions about documentation grouped under the 'user' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user/glossary/index.md`
- `docs/user/components/index.md`
- `docs/user/index.md`
- `docs/user/components/utils/index.md`
- `docs/user/components/topology/index.md`
- `docs/user/components/testing/index.md`
- `docs/user/components/problems/index.md`
- `docs/user/components/meshio/index.md`
- `docs/user/components/faults/index.md`
- `docs/user/components/bc/index.md`
- `docs/user/components/apps/index.md`
- `docs/user/physics/index.md`

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
- `skills/pylith-index/SKILL.md` (global route map for topic-skill dispatch)
- `pylith/problems/Physics.py`
- `pylith/meshio/gmsh_utils.py`
- `modulesrc/problems/Physics.i`
- `libsrc/pylith/problems/Physics.hh`
- `libsrc/pylith/problems/Physics.cc`
- `pylith/apps/PyLithApp.py` (top-level app composition seen by users in docs/help)
- `pylith/utils/SimulationMetadata.py` (metadata requirements for user cfg workflows)
- `pylith/utils/PetscDefaults.py`
- `pylith/problems/ProblemDefaults.py`
- `pylith/meshio/OutputPhysics.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`).
