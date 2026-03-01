# pylith source map: Release Notes

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `announce`
- `checklist`
- `notes`
- `release`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `pylith/__init__.py` | score: 13 | behavior check: package version string used by migration/version answers
- `pylith/apps/PyLithApp.py` | score: 12 | behavior check: `--version`/citation reporting path used by users
- `pylith/utils/CollectVersionInfo.py` | score: 12 | behavior check: runtime dependency report generation
- `pylith/utils/SimulationMetadata.py` | score: 11 | behavior check: cfg version constraints and metadata compatibility checks
- `modulesrc/utils/PylithVersion.i` | score: 11 | behavior check: SWIG boundary for C++ version metadata
- `libsrc/pylith/utils/PylithVersion.hh` | score: 11 | behavior check: version API contract
- `libsrc/pylith/utils/PylithVersion.cc` | score: 11 | behavior check: version data implementation
- `libsrc/pylith/utils/DependenciesVersion.hh` | score: 10 | behavior check: dependency version API contract
- `libsrc/pylith/utils/DependenciesVersion.cc` | score: 10 | behavior check: dependency version data implementation
- `libsrc/pylith/utils/PetscVersion.hh` | score: 10 | behavior check: PETSc version API contract
- `libsrc/pylith/utils/PetscVersion.cc` | score: 10 | behavior check: PETSc version implementation
- `setup.py` | score: 9 | behavior check: packaging metadata revision points between releases
- `pylith/Makefile.am` | score: 8 | behavior check: package build/release wiring
- `modulesrc/Makefile.am` | score: 8 | behavior check: extension build/release wiring
- `libsrc/Makefile.am` | score: 8 | behavior check: core-library release build wiring
