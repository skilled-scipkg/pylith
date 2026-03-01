# pylith source map: Parallel and HPC

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `2d`
- `developer`
- `error06`
- `error10`
- `gpu`
- `hpc`
- `logging`
- `mpi`
- `openmp`
- `parallel`
- `performance`
- `scaling`
- `slurm`
- `step06`
- `troubleshooting`
- `user`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `pylith/apps/PyLithApp.py` | score: 13 | behavior check: `--nodes`, launcher, and scheduler option wiring
- `pylith/apps/RunnerApp.py` | score: 12 | behavior check: multi-run job dispatch for batch and queue workflows
- `pylith/mpi/Communicator.py` | score: 12 | behavior check: MPI communicator lifecycle and rank/world-size access
- `pylith/topology/Distributor.py` | score: 11 | behavior check: mesh distribution decisions across ranks
- `pylith/utils/PetscDefaults.py` | score: 11 | behavior check: default solver/parallel option categories
- `pylith/utils/PetscManager.py` | score: 11 | behavior check: PETSc option injection and initialization order
- `modulesrc/mpi/mpi.i` | score: 10 | behavior check: SWIG module surface for MPI helpers
- `modulesrc/mpi/mpi_comm.i` | score: 10 | behavior check: communicator binding API
- `modulesrc/mpi/mpi_error.i` | score: 10 | behavior check: MPI error translation layer
- `modulesrc/mpi/mpi_reduce.i` | score: 10 | behavior check: reduction helper bindings
- `modulesrc/topology/Distributor.i` | score: 9 | behavior check: SWIG boundary for distribution controls
- `libsrc/pylith/utils/mpi.hh` | score: 9 | behavior check: C++ MPI utility wrappers used by distributed code paths
- `libsrc/pylith/topology/Distributor.hh` | score: 9 | behavior check: distributed topology API contract
- `libsrc/pylith/topology/Distributor.cc` | score: 9 | behavior check: partition/distribution implementation
- `libsrc/pylith/problems/TimeDependent.cc` | score: 8 | behavior check: distributed solve-loop synchronization behavior
- `libsrc/pylith/problems/ProgressMonitorTime.cc` | score: 8 | behavior check: progress reporting behavior in MPI runs
