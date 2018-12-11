<!---
# Copyright (c) 2017-2018 Michael C. Heiber
# This source file is part of the Excimontec project, which is subject to the MIT License.
# For more information, see the LICENSE file that accompanies this software.
# The Excimontec project can be found on Github at https://github.com/MikeHeiber/Excimontec
--->
# Excimontec

Kinetic Monte Carlo simulations are a powerful computational tool that have been used in concert with experiments and more detailed theoretical methods to understand and optimize organic semiconductor materials and devices. 
However, despite over 30 years of applying KMC tools to organic semiconductors, no widespread or standardized software tools have taken hold in the community. 
Instead, many research groups around the world have maintained private codebases of varying complexity, efficiency, and reliability. 
As a result, there have been large barriers to entry for new researchers and a lot of repeated effort throughout the community that would be much better off applied to pushing the capabilities of the technique and further refining the physical models. 

Excimontec represents an honest effort to bring the community together around a well-tested, optimized, reliable, and accessible open-source tool for performing KMC simulations of organic electronic devices. 
The software is being developed in modern C++ and is optimized for efficient execution on high performance computing clusters using MPI. 
This software package uses object-oriented design and extends the [KMC_Lattice](https://github.com/MikeHeiber/KMC_Lattice) framework. 
If you would like to contribute to the development of this project, please see the [contributing instructions](./CONTRIBUTING.md).

#### Major Features:
- Adjustable periodic boundary conditions in all three directions allow users to perform 1D, 2D, or 3D simulations.
- Choose between several film architectures, including a neat film, bilayer film, or random blend film.
- Import bulk heterojunction morphologies generated by [Ising_OPV](https://github.com/MikeHeiber/Ising_OPV) v3.2 and v4.
- Donor and acceptor materials can take on an uncorrelated Gaussian DOS, a correlated Gaussian DOS with different correlation functions, or an uncorrelated exponential DOS model.
- Site energies at the donor-acceptor interface or in mixed regions can be modified using an interfacial energy shift model to generate an energy cascade.
- Custom site energies can also be imported from a text file.
- Dynamics test simulations can be performed to generate exciton and charge carrier density transients that can be used to model exciton dissociation, charge carrier separation, and charge carrier recombination kinetics.
- Time-of-flight charge transport simulations of electrons or holes can be performed on neat, random blend, or bulk heterojunction blend films.
- Steady state charge transport simulations of electrons or holes can be performed on neat, random blend, or bulk heterojunction blends films with 3D periodic boundaries to estimate quasi-equilibrium properties including the steady state mobility, transport energy, and equilibration energy under different test conditions.
- Exciton diffusion simulations can be performed on any film architecture.
- Internal quantum efficiency simulations can be performed on bilayer, random blend, or bulk heterojunction blend films.
- Simulate complex exciton dynamics with events for intersystem crossing between singlet and triplet states as well as exciton-exciton and exciton-polaron annihilation events.
- Choose between Miller-Abrahams or Marcus models for polaron hopping.
- Charge carrier delocalization can be modeled with a spherical Gaussian delocalization model.
- Choose between several KMC algorithms (first reaction method, selective recalculation method, or full recalculation method).

## Current Status

The current release, Excimontec
[![GitHub (pre-)release](https://img.shields.io/github/release/MikeHeiber/Excimontec/all.svg?style=flat-square)](https://github.com/MikeHeiber/Excimontec/releases)
, is built with KMC_Lattice [![GitHub (pre-)release](https://img.shields.io/github/release/MikeHeiber/KMC_Lattice/all.svg?style=flat-square)](https://github.com/MikeHeiber/KMC_Lattice/releases) and allows the user to perform several simulation tests relevant for OPV and OLED devices. 
All features that are to be included in v1.0 are now implemented and have undergone significant testing. 
However, there may still be bugs that need to be fixed, so please report any bugs or submit feature requests in the [Issues](https://github.com/MikeHeiber/Excimontec/issues) section. 
Please see the [Changelog](CHANGELOG.md) for a detailed listing of previous and upcoming changes. 

Major releases and other significant developments will be announced on the Excimontec: General News mailing list. If you are interested in keeping up to date with the development and application of this tool, please subscribe at the following link:
[Subscribe Here](http://eepurl.com/dis9AT)

#### Continuous Integration and Testing Status:

Excimontec is currently being tested on [Ubuntu](https://www.ubuntu.com/) v14.04 with the [GCC compiler](https://gcc.gnu.org/) (versions 4.7, 4.8, 4.9, 5, 6, 7, and 8) and on both [Open MPI](http://www.open-mpi.org/) v1.6.5 and [MPICH](http://www.mpich.org/) v3.04 using [Travis CI](https://travis-ci.com/).

| Branch | Status |
| :------: | ------ |
| Master | [![Build Status](https://img.shields.io/travis/MikeHeiber/Excimontec/master.svg?style=for-the-badge)](https://travis-ci.org/MikeHeiber/Excimontec) |
| Development | [![Build Status](https://img.shields.io/travis/MikeHeiber/Excimontec/development.svg?style=for-the-badge)](https://travis-ci.org/MikeHeiber/Excimontec) |

Code is being tested using [googletest](https://github.com/google/googletest) with test coverage assessment by [Coveralls](https://coveralls.io/).

| Branch | Status |
| :------: | ------ |
| Master | [![Coveralls github branch](https://img.shields.io/coveralls/github/MikeHeiber/Excimontec/master.svg?style=for-the-badge)](https://coveralls.io/github/MikeHeiber/Excimontec?branch=master) |
| Development | [![Coveralls github branch](https://img.shields.io/coveralls/github/MikeHeiber/Excimontec/development.svg?style=for-the-badge)](https://coveralls.io/github/MikeHeiber/Excimontec?branch=development) |

## Contact

If you would like some help in using or customizing the tool for your research, please contact me (heiber@mailaps.org) to discuss a collaboration. 
You can check out my research using this tool and other work on [Researchgate](https://www.researchgate.net/profile/Michael_Heiber).

Have a quick question or want to chat about Excimontec?  Join the discussion on Gitter: [![Gitter](https://img.shields.io/gitter/room/nwjs/nw.js.svg?style=for-the-badge)
](https://gitter.im/Excimontec)

## How to try Excimontec?

#### Building and Testing the Executable

This software tool uses [Message Passing Interface (MPI)](https://computing.llnl.gov/tutorials/mpi/) to utilize parallel computing power. 
As a result, using Excimontec requires that an MPI library is pre-installed on your system, and the final Excimontec executable must be built on your specific system. 
We cannot provide pre-built binaries for your system. 
Contact your HPC admin to determine the protocols for building MPI applications on your HPC system. 
In many cases, the HPC system will already be configured for you, and the package comes with a default makefile that can be used with the [GCC compiler](https://gcc.gnu.org/) or the [PGI compiler](https://www.pgroup.com/). 

If you wish, you can also install MPI on your own personal workstation and then build Excimontec there as well. For development and preliminary simulation tests, sometimes it is more efficient to run on your own workstation instead of an HPC system. More information about common MPI packages can be found here:
- Open MPI, http://www.open-mpi.org/
- MPICH, http://www.mpich.org/
- MVAPICH, http://mvapich.cse.ohio-state.edu/

Once you have an MPI library installed, to build Excimontec, first copy the Excimontec directory to your machine.  On Linux this can be done using the command,

```git clone --recurse-submodules https://github.com/MikeHeiber/Excimontec```

Then set Excimontec as your working directory,

```cd Excimontec```

and finally build the software package with the default makefile.

```make```

In the default makefile, compilation flags have been set for the GCC and PGI compilers.  If you are using another compiler, you will need to edit the makefile and define your own compiler options.
Once the normal build is successful, you should test Excimontec on your own hardware using the unit and system tests provided before you use the tool. 
Build the testing executable by running

```make test```

Once the test build is complete, run the test suite.

```./test/Excimontec_tests.exe```

Please report any build or testing errors in the [Issues](https://github.com/MikeHeiber/Excimontec/issues) section. 

#### Usage

In most cases, your HPC system will use a job scheduler to manage the computing workload. 
For performing Excimontec simulations, it is recommended to submit batch jobs where you will request the resources needed to perform the simulation. 
An example batch script for the [SLURM](https://slurm.schedmd.com/) job scheduling system is provided with this package (slurm_script.sh). 
Similar batch scripts can also be written for other job schedulers.

Regardless of the job scheduler, the program execution command is essentially the same. 
Excimontec.exe takes one required input argument, which is the filename of the input parameter file. 
An example parameter file is provided with this package (parameters_default.txt).

For example, within the batch script, to create a simulation that runs on 10 processors, the execution command is

```mpiexec -n 10 Excimontec.exe parameters_default.txt```

In this example, the parameters_default.txt file that is located in the current working directory is loaded into the Excimontec program to determine which simulation to run.

#### Output

Excimontec will create a number of different output files depending which test is chosen in the parameter file:
- results#.txt -- This text file will contain the results for each processor where the # will be replaced by the processor ID.
- analysis_summary.txt -- When MPI is enabled, this text file will contain average final results from all of the processors.
- dynamics_average_transients.txt -- When performing a dynamics test, calculated exciton, electron, and hole transients will be output to this file.
- ToF_average_transients.txt -- When performing a time-of-flight charge transport test, calculated current transients, mobility relaxation transients, and energy relaxation transients will be output to this file.
- ToF_transit_time_hist.txt -- When performing a time-of-flight charge transport test, the resulting polaron transit time probability histogram will be output to this file.
- ToF_results.txt -- When performing a time-of-flight charge transport test, the resulting quantitative results are put into this parsable delimited results file.
- Charge_extraction_map#.txt -- When performing a time-of-flight or IQE test, the x-y locations where charges are extracted from the lattice are saving into this map file.
- DOS_correlation_data#.txt -- When a correlated density of states model is enabled, data showing the statistical correlation of site energies vs. distance is output into this file.

#### Data Analysis

For [Igor Pro](https://www.wavemetrics.com/) users, I am developing an open-source procedures package for loading, analyzing, and plotting data from Excimontec simulations called [Excimontec_Analysis](https://github.com/MikeHeiber/Excimontec_Analysis). 
This is a good starting point for managing the data generated by Excimontec, and the Igor Pro scripting environment provides a nice playground where users can perform more advanced data analysis as needed.

## For Software Developers

Public API documentation for the Excimontec package is still under development and can be viewed [here](https://mikeheiber.github.io/Excimontec/).
