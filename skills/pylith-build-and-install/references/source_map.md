# pylith source map: Build and Install

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `3d`
- `build`
- `cmake`
- `compile`
- `contributing`
- `cubit`
- `debugging`
- `dependencies`
- `developer`
- `docker`
- `git`
- `gui`
- `install`
- `installation`
- `make`
- `meshing`
- `parameter`
- `quickref`
- `run`
- `subduction`
- `user`
- `workflow`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `configure.ac` | score: 14 | behavior check: build-system feature/probe toggles that alter compile outcomes
- `setup.py` | score: 13 | behavior check: Python package install metadata and entry-point wiring
- `pylith/apps/PyLithApp.py` | score: 13 | behavior check: runtime startup path after install
- `pylith/apps/PetscApplication.py` | score: 12 | behavior check: PETSc application initialization used by CLI tools
- `pylith/apps/RunnerApp.py` | score: 12 | behavior check: batch run launcher used in simulation suites
- `pylith/utils/CollectVersionInfo.py` | score: 11 | behavior check: dependency/version reporting for install verification
- `pylith/utils/SimulationMetadata.py` | score: 11 | behavior check: metadata schema validation used by cfg workflows
- `pylith/utils/DumpParametersJson.py` | score: 10 | behavior check: resolved parameter capture for post-install sanity checks
- `modulesrc/utils/PylithVersion.i` | score: 10 | behavior check: Python/C++ version binding interface
- `libsrc/pylith/utils/PylithVersion.hh` | score: 10 | behavior check: version API declarations
- `libsrc/pylith/utils/PylithVersion.cc` | score: 10 | behavior check: version data implementation
- `pylith/Makefile.am` | score: 9 | behavior check: package-level build target composition
- `modulesrc/Makefile.am` | score: 9 | behavior check: extension module build graph
- `libsrc/Makefile.am` | score: 9 | behavior check: core C++ library build graph
- `modulesrc/module.am` | score: 8 | behavior check: module source aggregation used by autotools
