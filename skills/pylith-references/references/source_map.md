# pylith source map: References

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `references`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `pylith/apps/PyLithApp.py` | score: 12 | behavior check: CLI flags for version/citation/reporting references
- `pylith/utils/CollectVersionInfo.py` | score: 12 | behavior check: formatted dependency metadata used in user-facing reports
- `pylith/utils/SimulationMetadata.py` | score: 11 | behavior check: metadata normalization used by run descriptors
- `pylith/utils/DumpParametersJson.py` | score: 10 | behavior check: captures machine-readable provenance of simulation inputs
- `pylith/viz/PlotField.py` | score: 10 | behavior check: post-processing entry point tied to referenced workflows
- `pylith/viz/core.py` | score: 10 | behavior check: plotting backend helpers
- `modulesrc/utils/PylithVersion.i` | score: 10 | behavior check: Python bridge for C++ version details
- `libsrc/pylith/utils/PylithVersion.hh` | score: 10 | behavior check: C++ version API declarations
- `libsrc/pylith/utils/PylithVersion.cc` | score: 10 | behavior check: C++ version API implementation
- `libsrc/pylith/utils/DependenciesVersion.hh` | score: 9 | behavior check: dependency version interface contract
- `libsrc/pylith/utils/DependenciesVersion.cc` | score: 9 | behavior check: dependency version resolution implementation
- `libsrc/pylith/utils/PetscVersion.hh` | score: 9 | behavior check: PETSc version API declarations
- `libsrc/pylith/utils/PetscVersion.cc` | score: 9 | behavior check: PETSc version resolution implementation
