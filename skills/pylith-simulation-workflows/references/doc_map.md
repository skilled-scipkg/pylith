# pylith documentation map: Simulation Workflows

Generated from documentation roots:
- `docs`
- `release-notes`
- `examples`
- `docs/user/examples`
- `tests`
- `pylith/testing`

Total docs grouped in this topic: 51

## File inventory
- `examples/subduction-3d/README.md` | title: Examples: 3-D Subduction Zone | headings: Examples: 3-D Subduction Zone; Mesh generation using Cubit (optional); Run the Python script to generate the Cubit journal file in the scratch directory.
- `examples/crustal-strikeslip-3d/README.md` | title: Examples: Crustal 3D strike-slip faults | headings: Examples: Crustal 3D strike-slip faults; Mesh generation using Gmsh (optional); Mesh generation using Cubit
- `examples/magma-2d/README.md` | title: Examples: 2D Magma Reservoir Using Poroelasticity | headings: Examples: 2D Magma Reservoir Using Poroelasticity; Meshing; Step 1: Inflation
- `examples/troubleshooting-2d/README.md` | title: Troubleshooting: 2D Reverse Fault | headings: Troubleshooting: 2D Reverse Fault; Step 1: Gravitational body forces and linear isotropic elasticity; Step 6: Earthquake rupture on two faults and linear isotropic linear elasticity
- `tests/manual/powerlaw-3d/README.md` | title: 3D Power Law Manual Tests | headings: 3D Power Law Manual Tests; Run all tests and check Jacobians; Run a single test (no Jacobian test)
- `tests/manual/powerlaw-2d/README.md` | title: 2D Power Law Manual Tests | headings: 2D Power Law Manual Tests; Run all tests and check Jacobians; Run a single test (no Jacobian test)
- `docs/developer/git-workflow/index.md` | title: Git Workflow | headings: Git Workflow; git-quickref.md
- `docs/user/run-pylith/index.md` | title: Running PyLith | headings: Running PyLith
- `docs/user/problems/index.md` | title: Defining Simulations | headings: Defining Simulations
- `docs/user/examples/troubleshooting-2d/index.md` | title: Troubleshooting (2D) | headings: Troubleshooting (2D); Example Workflow
- `docs/user/benchmarks/savage-prescott.md` | title: Savage and Prescott Benchmark | headings: Savage and Prescott Benchmark; Problem Description; Running the Benchmark
- `docs/user/run-pylith/utilities.md` | title: Utilities | headings: Utilities; pylith_viz; plot_mesh Subcommand
- `docs/user/run-pylith/troubleshooting.md` | title: Troubleshooting | headings: Troubleshooting; Tips and Hints For Running PyLith; Common Error Messages
- `docs/user/run-pylith/petsc-options.md` | title: PETSc Options | headings: PETSc Options; Default PETSc Options; Monitoring Options
- `docs/user/benchmarks/quasistatic-strikeslip.md` | title: Strike-Slip Benchmark | headings: Strike-Slip Benchmark; Problem Description; Running the Benchmark
- `docs/developer/testing/run-cxxtests.md` | title: Running C++ unit tests and MMS tests | headings: Running C++ unit tests and MMS tests; Running C++ unit tests; List tests
- `docs/developer/git-workflow/tasks.md` | title: Git tasks | headings: Git tasks; Setting up your fork; Set the upstream repository
- `docs/developer/testing/fullscale.md` | title: Full-scale tests | headings: Full-scale tests; Command line arguments; Using the debugger
- `docs/user/examples/strikeslip-2d/step06-inversion-leastsquares.md` | title: Step 6: Least Squares Fault Slip Inversion | headings: Step 6: Least Squares Fault Slip Inversion; Show command line options for the inversion code; Plotting the results
- `docs/user/physics/faults/prescribed-slip.md` | title: Prescribed Slip (`FaultCohesiveKin`) | headings: Prescribed Slip (`FaultCohesiveKin`); Prescribed Slip Parameters (`KinSrc`); Step-Function Slip Time Function (`KinSrcStep`)
- `docs/user/examples/subduction-3d/step08-gravity.md` | title: Step 8: Use of Gravitational Body Forces | headings: Step 8: Use of Gravitational Body Forces; Simulation parameters; The output should look something like the following. This is for Step 8b.
- `docs/user/examples/subduction-3d/step07-greensfns.md` | title: Step 7: Generation of Green's Functions and Slow Slip Inversion | headings: Step 7: Generation of Green's Functions and Slow Slip Inversion; Simulation parameters; The output should look something like the following.
- `docs/user/examples/subduction-3d/step06-slowslip.md` | title: Step 6: Prescribed Slow Slip Events | headings: Step 6: Prescribed Slow Slip Events; Simulation parameters; Generate fault_slabtop_slowslip.spatialdb and fault_slabtop_slowslip.timedb.
- `docs/user/examples/subduction-3d/step04-eqcycle.md` | title: Step 4: Earthquake Cycle with Prescribed Slip | headings: Step 4: Earthquake Cycle with Prescribed Slip; Simulation parameters; The output should look something like the following.
- `docs/user/examples/subduction-3d/step03-interseismic.md` | title: Step 3: Interseismic Deformation | headings: Step 3: Interseismic Deformation; Simulation parameters; The output should look something like the following.
- `docs/user/examples/subduction-3d/step02-coseismic.md` | title: Step 2: Earthquake Rupture and Postseismic Relaxation | headings: Step 2: Earthquake Rupture and Postseismic Relaxation; Simulation parameters; The output should look something like the following.
- `docs/user/examples/subduction-3d/step01-axialdisp.md` | title: Step 1: Axial Compression | headings: Step 1: Axial Compression; Simulation parameters; The output should look something like the following.
- `docs/user/examples/subduction-2d/step03-eqcycle.md` | title: Step 3: Quasistatic Earthquake Cycle | headings: Step 3: Quasistatic Earthquake Cycle; Simulation parameters; Creep
- `docs/user/examples/subduction-2d/step02-interseismic.md` | title: Step 2: Quasistatic Interseismic Deformation | headings: Step 2: Quasistatic Interseismic Deformation; Simulation parameters; Running the simulation
- `docs/user/examples/strikeslip-2d/step05-greensfns.md` | title: Step 5: Green's Functions | headings: Step 5: Green's Functions; Simulation parameters; Running the simulation
- `docs/user/examples/strikeslip-2d/step01-slip.md` | title: Step 1: Static Coseismic Slip | headings: Step 1: Static Coseismic Slip; Step 1a: Coarse Mesh; Simulation parameters
- `docs/user/examples/reverse-2d/step05-onefault.md` | title: Step 5: Static Coseismic Slip | headings: Step 5: Static Coseismic Slip; Step 5a: Coarse Mesh; Simulation parameters
- `docs/user/examples/reverse-2d/step04-surfload.md` | title: Step 4: Surface Tractions | headings: Step 4: Surface Tractions; Step 4a: Coarse Mesh; Simulation parameters
- `docs/user/examples/reverse-2d/step03-gravity-incompressible.md` | title: Step 3: Gravitational Body Forces with Incompressible Elasticity | headings: Step 3: Gravitational Body Forces with Incompressible Elasticity; Simulation parameters; Running the simulation
- `docs/user/examples/reverse-2d/step01-gravity.md` | title: Step 1: Gravitational Body Forces | headings: Step 1: Gravitational Body Forces; Step 1a: Coarse Mesh; Simulation parameters
- `docs/user/examples/poroelastic-outerrise-2d/step01-no-faults-no-flexure.md` | title: Step 1: No faults, no flexure | headings: Step 1: No faults, no flexure; Simulation parameters; Running the simulation
- `docs/user/examples/magma-2d/step01-inflation.md` | title: Step 1: Magma inflation | headings: Step 1: Magma inflation; Simulation parameters; Running the simulation
- `docs/user/examples/crustal-strikeslip-3d/step02-varslip.md` | title: Step 2: Static Spatially Variable Coseismic Slip | headings: Step 2: Static Spatially Variable Coseismic Slip; Simulation parameters; Running the simulation
- `docs/user/examples/crustal-strikeslip-3d/step01-slip.md` | title: Step 1: Static Coseismic Slip | headings: Step 1: Static Coseismic Slip; Simulation parameters; Running the simulation
- `docs/user/examples/crustal-strikeslip-2d/step02-varslip.md` | title: Step 2: Static Spatially Variable Coseismic Slip | headings: Step 2: Static Spatially Variable Coseismic Slip; Simulation parameters; Running the simulation
- `docs/user/examples/crustal-strikeslip-2d/step01-slip.md` | title: Step 1: Static Uniform Coseismic Slip | headings: Step 1: Static Uniform Coseismic Slip; Simulation parameters; Running the simulation
- `docs/user/examples/box-3d/step05-sheardisptractrate.md` | title: Step 5: Time-Dependent Shear Displacement and Tractions | headings: Step 5: Time-Dependent Shear Displacement and Tractions; Simulation parameters; Running the simulation
- `docs/user/examples/box-3d/step04-sheardispic.md` | title: Step 4: Shear Displacement and Initial Conditions | headings: Step 4: Shear Displacement and Initial Conditions; Simulation parameters; Running the simulation
- `docs/user/examples/box-2d/step05-sheardisptractrate.md` | title: Step 5: Time-Dependent Shear Displacement and Tractions | headings: Step 5: Time-Dependent Shear Displacement and Tractions; Simulation parameters; Degrees of freedom (dof) 0 and 1 correspond to the x and y displacements.
- `docs/user/examples/box-2d/step04-sheardispic.md` | title: Step 4: Shear Displacement and Initial Conditions | headings: Step 4: Shear Displacement and Initial Conditions; Simulation parameters; Running the simulation
- `docs/user/components/meshio/OutputSolnPoints.md` | title: OutputSolnPoints | headings: OutputSolnPoints; Pyre Facilities; Pyre Properties
- `docs/user/problems/problems.md` | title: Types of Simulations | headings: Types of Simulations; Time-Dependent Problem (`TimeDependent`); Initial Conditions
- `docs/user/components/faults/KinSrcBrune.md` | title: KinSrcBrune | headings: KinSrcBrune; Pyre Facilities; Pyre Properties
- `docs/user/run-pylith/pylithapp.md` | title: PyLith Application | headings: PyLith Application; Simulation Metadata
- `docs/user/components/utils/SimulationMetadata.md` | title: SimulationMetadata | headings: SimulationMetadata; Pyre Properties; Example
- `docs/developer/contributing/workflow.md` | title: Workflow | headings: Workflow
