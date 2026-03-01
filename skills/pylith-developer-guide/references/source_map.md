# pylith source map: Developer Guide

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `application`
- `architecture`
- `code`
- `contributing`
- `contribution`
- `debugging`
- `design`
- `develop`
- `developer`
- `flow`
- `ides`
- `implementation`
- `internals`
- `plugin`
- `quickref`
- `testing`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `pylith/apps/PyLithApp.py` | score: 13 | behavior check: top-level Python orchestration from preinitialize to run
- `pylith/apps/PetscApplication.py` | score: 12 | behavior check: PETSc startup/teardown lifecycle
- `pylith/problems/TimeDependent.py` | score: 12 | behavior check: problem setup and time-stepping integration hooks
- `pylith/problems/Physics.py` | score: 12 | behavior check: observer/material/fault registration path
- `pylith/problems/Problem.py` | score: 11 | behavior check: shared problem-level configuration flow
- `pylith/topology/MeshImporter.py` | score: 11 | behavior check: mesh import/reorder/distribute lifecycle
- `pylith/testing/TestCases.py` | score: 10 | behavior check: Python unit test harness patterns for extensions
- `pylith/testing/FullTestApp.py` | score: 10 | behavior check: full-scale regression harness behavior
- `modulesrc/problems/TimeDependent.i` | score: 10 | behavior check: SWIG boundary for time-dependent problem APIs
- `modulesrc/problems/Physics.i` | score: 10 | behavior check: SWIG boundary for physics observer APIs
- `modulesrc/problems/ObserverPhysics.i` | score: 10 | behavior check: SWIG boundary for observer plumbing
- `libsrc/pylith/problems/TimeDependent.hh` | score: 10 | behavior check: C++ time-dependent API contract
- `libsrc/pylith/problems/TimeDependent.cc` | score: 10 | behavior check: C++ solve-loop implementation
- `libsrc/pylith/problems/ObserverPhysics.hh` | score: 9 | behavior check: observer interface contract in C++
- `libsrc/pylith/problems/ObserverPhysics.cc` | score: 9 | behavior check: observer callback implementation path
- `libsrc/pylith/feassemble/Integrator.hh` | score: 9 | behavior check: FE integration extension surface
- `libsrc/pylith/utils/EventLogger.hh` | score: 8 | behavior check: instrumentation hooks used during developer debugging
