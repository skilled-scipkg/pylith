# pylith source map: Troubleshooting

Generated from source roots:
- `applications`
- `libsrc`
- `modulesrc`
- `pylith`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `announce`
- `debug`
- `error`
- `failure`
- `faq`
- `issue`
- `known`
- `notes`
- `problem`
- `release`
- `troubleshoot`
- `troubleshooting`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" applications libsrc modulesrc pylith`
- `rg -n "class|def|struct|namespace" applications libsrc modulesrc pylith`
- If a doc mentions a function/class, search that exact symbol first, then inspect nearby implementation files.

## Suggested source entry points
- `pylith/problems/Problem.py` | score: 5 | matched tokens: problem
- `modulesrc/problems/Problem.i` | score: 5 | matched tokens: problem
- `modulesrc/mpi/mpi_error.i` | score: 5 | matched tokens: error
- `libsrc/pylith/utils/error.hh` | score: 5 | matched tokens: error
- `libsrc/pylith/utils/error.h` | score: 5 | matched tokens: error
- `libsrc/pylith/problems/Problem.hh` | score: 5 | matched tokens: problem
- `libsrc/pylith/problems/Problem.cc` | score: 5 | matched tokens: problem
- `pylith/problems/__init__.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldVelocity.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldTraceStrainDot.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldTraceStrain.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldTemperature.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldPressureDot.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldPressure.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldLagrangeFault.py` | score: 2 | matched tokens: problem
- `pylith/problems/SubfieldDisplacement.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolutionSubfield.py` | score: 2 | matched tokens: problem
- `pylith/problems/InitialConditionDomain.py` | score: 2 | matched tokens: problem
- `modulesrc/problems/InitialConditionDomain.i` | score: 2 | matched tokens: problem
- `libsrc/pylith/problems/InitialConditionDomain.hh` | score: 2 | matched tokens: problem
- `libsrc/pylith/problems/InitialConditionDomain.cc` | score: 2 | matched tokens: problem
- `pylith/problems/TimeDependent.py` | score: 2 | matched tokens: problem
- `pylith/problems/Solution.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispVelLagrange.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispVel.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispPresVel.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispPresTracStrainVelPdotTdotLagrange.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispPresTracStrainVelPdotTdot.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispPresTracStrainLagrange.py` | score: 2 | matched tokens: problem
- `pylith/problems/SolnDispPresTracStrain.py` | score: 2 | matched tokens: problem
