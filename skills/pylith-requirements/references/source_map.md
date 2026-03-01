# pylith source map: Requirements

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `requirements`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `setup.py` | score: 13 | behavior check: Python package dependency and install metadata
- `configure.ac` | score: 13 | behavior check: compile-time dependency probes and feature gates
- `pylith/utils/CollectVersionInfo.py` | score: 12 | behavior check: runtime dependency reporting used for requirement checks
- `pylith/apps/PyLithApp.py` | score: 11 | behavior check: requirement-sensitive startup behavior and version reporting
- `pylith/utils/SimulationMetadata.py` | score: 11 | behavior check: metadata validation tied to compatible runtime versions
- `pylith/utils/PetscManager.py` | score: 10 | behavior check: PETSc initialization affected by dependency builds
- `modulesrc/utils/PylithVersion.i` | score: 10 | behavior check: SWIG bridge for compiled dependency/version metadata
- `libsrc/pylith/utils/PylithVersion.hh` | score: 10 | behavior check: PyLith version interface contract
- `libsrc/pylith/utils/PylithVersion.cc` | score: 10 | behavior check: PyLith version implementation
- `libsrc/pylith/utils/DependenciesVersion.hh` | score: 10 | behavior check: dependency version interface contract
- `libsrc/pylith/utils/DependenciesVersion.cc` | score: 10 | behavior check: dependency version implementation
- `libsrc/pylith/utils/PetscVersion.hh` | score: 10 | behavior check: PETSc version interface contract
- `libsrc/pylith/utils/PetscVersion.cc` | score: 10 | behavior check: PETSc version implementation
