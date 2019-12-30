<!---
# Copyright (c) 2017-2019 Michael C. Heiber
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
If you would like to contribute to the development of this project, please see the [contributing instructions](CONTRIBUTING.md).

Major releases and other significant developments will be announced on the Excimontec: General News mailing list. If you are interested in keeping up to date with the latest developments, please subscribe at the following link:
[Subscribe Here](http://eepurl.com/dis9AT)

#### Major Features:
- Adjustable periodic boundary conditions in all three directions allow users to perform 1D, 2D, or 3D simulations.
- Choose between several film architectures, including a neat film, bilayer film, or random blend film.
- Import bulk heterojunction morphologies generated by [Ising_OPV](https://github.com/MikeHeiber/Ising_OPV) v3.2 and v4.
- Donor and acceptor materials can take on an uncorrelated Gaussian density of states, a correlated Gaussian density of states with different correlation functions, or an uncorrelated exponential density of states model.
- Site energies at the donor-acceptor interface or in mixed regions can be modified using an interfacial energy shift model to generate an energy cascade.
- Custom site energies can also be imported from a text file to allow more exotic DOS distributions or implement the electrostatic potential due to fixed ionic dopants.
- Dynamics test simulations can be performed to generate exciton and charge carrier density transients that can be used to model exciton dissociation, charge carrier separation, and charge carrier recombination kinetics.
- Time-of-flight charge transport simulations of electrons or holes can be performed on neat, random blend, or bulk heterojunction blend films.
- Steady state charge transport simulations of holes can be performed on neat, random blend, or bulk heterojunction blends films with 3D periodic boundaries to estimate quasi-equilibrium properties including the steady state mobility, transport energy, and equilibration energy under different test conditions. Output of density of states and density of occupied states data can also be used to calculate the Fermi energy.  The Fermi energy and transport energy can then be used to calculate the Seebeck coefficient to investigate thermoelectric properties.
- Exciton diffusion simulations can be performed on any film architecture.
- Internal quantum efficiency simulations can be performed on bilayer, random blend, or bulk heterojunction blend films.
- Simulate complex exciton dynamics with events for intersystem crossing between singlet and triplet states as well as exciton-exciton and exciton-polaron annihilation events.
- Choose between Miller-Abrahams or Marcus models for polaron hopping.
- Charge carrier delocalization can be modeled with a spherical Gaussian delocalization model.
- Choose between several KMC algorithms (first reaction method, selective recalculation method, or full recalculation method).

For more details and examples of each type of simulation test, please see the [User Manual](https://mikeheiber.github.io/Excimontec/User_Manual.pdf)

## How to try Excimontec?

#### Building and Testing the Executable

This software tool uses [Message Passing Interface (MPI)](https://computing.llnl.gov/tutorials/mpi/) to utilize parallel computing power. 
As a result, using Excimontec requires that an MPI library is pre-installed on your system, and the final Excimontec executable must be built on your specific system. 
We cannot provide pre-built binaries for your system. 
Contact your HPC admin to determine the protocols for building MPI applications on your HPC system. 
In many cases, the HPC system will already be configured for you, and Excimontec comes with a default makefile that can be used with the [GCC compiler](https://gcc.gnu.org/) or the [PGI compiler](https://www.pgroup.com/).
If your system uses another compiler, you will need to edit the makefile and define your own compiler options.

If you wish, you can also install MPI on your own personal workstation and then build Excimontec there as well. 
For development and preliminary simulation tests, sometimes it is more efficient to run on your own workstation instead of an HPC system. 

For detailed installation instructions, please see the [User Manual](https://mikeheiber.github.io/Excimontec/User_Manual.pdf#page=13).

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
- DOS_data.txt - When performing a steady state charge transport test, the density of states distribution is calculated and output to this file.
- DOS_Coulomb_data.txt - When performing a steady state charge transport test, the density of states distribution, where the site energies include the Coulomb potential from the polarons, is calculated and output to this file.
- DOOS_data.txt - When performing a steady state charge transport test, the density of occupied states distribution is calculated and output to this file.
- DOOS_Coulomb_data.txt - When performing a steady state charge transport test, the density of occupied states distribution, where the site energies include the Coulomb potential from the polarons, is calculated and output to this file.

#### Data Analysis

For [Igor Pro](https://www.wavemetrics.com/) users, I am developing an open-source procedures package for loading, analyzing, and plotting data from Excimontec simulations called [Excimontec_Analysis](https://github.com/MikeHeiber/Excimontec_Analysis). 
This is a good starting point for managing the data generated by Excimontec, and the Igor Pro scripting environment provides a nice playground where users can perform more advanced data analysis as needed.

## Contact

If you would like some help in using or customizing the tool for your research, please contact me (heiber@mailaps.org) to discuss a collaboration. 
You can check out my research using this tool and other work on [Researchgate](https://www.researchgate.net/profile/Michael_Heiber).

Have a quick question or want to chat about Excimontec?  Join the discussion on Gitter: [![Gitter](https://img.shields.io/gitter/room/nwjs/nw.js.svg?style=for-the-badge)
](https://gitter.im/Excimontec)

## Citing This Work

This work will soon be submitted to the Journal of Open Source Software, and the citation will be provided here once published.
<!-- [M. C. Heiber, J. Open Source Software **X**, XXXX (2019).](https://doi.org/) [[ResearchGate]](https://www.researchgate.net/) -->

In addition, please also cite the DOI for the specific version that you used from [Zenodo.org](https://zenodo.org/search?page=1&size=20&q=conceptrecid:%22595806%22&sort=-version&all_versions=True).

## Recommended Reading

Below are some recommended resources for starting to learn about KMC modeling of organic electronic devices:

[M. C. Heiber, A. Wagenpfahl, and C. Deibel, "Advances in Modeling the Physics of Disordered Organic Electronic Devices" In *Handbook of Organic Materials for Electronic and Photonic Devices*, Woodhead Publishing Series in Electronic and Optical Materials, edited by O. Ostroverkhova (Woodhead Publishing, 2019) 2nd Ed., Chap. 10.](https://doi.org/10.1016/B978-0-08-102284-9.00010-3) [[ResearchGate]](https://www.researchgate.net/publication/329625990_Advances_in_Modeling_the_Physics_of_Disordered_Organic_Electronic_Devices)

[C. Groves, "Simulating Charge Transport in Organic Semiconductors and Devices: A Review" Rep. Prog. Phys. **80**, 026502 (2017).](http://dx.doi.org/10.1088/1361-6633/80/2/026502)[[ResearchGate]](https://www.researchgate.net/publication/311743859_Simulating_charge_transport_in_organic_semiconductors_and_devices_A_review)

[S. D. Baranovskii, "Theoretical description of charge transport in disordered organic semiconductors" Phys. Status Solidi B. **3** 487 (2014).](https://doi.org/10.1002/pssb.201350339)

[C. Groves, "Developing Understanding of Organic Photovoltaic Devices: Kinetic Monte Carlo Models of Geminate and Non-geminate Recombination, Charge Transport and Charge Extraction" Energy Environ. Sci. **6**, 32020 (2013).](https://doi.org/10.1039/c3ee41621f)[[ResearchGate]](https://www.researchgate.net/publication/260303139_Developing_Understanding_of_Organic_Photovoltaic_Devices_Kinetic_Monte_Carlo_Models_of_Charge_Recombination_Transport_and_Extraction)

## Development Status

The current release, [Excimontec v1.0.0-rc.4](https://github.com/MikeHeiber/Excimontec/releases), is built with [KMC_Lattice v2.1](https://github.com/MikeHeiber/KMC_Lattice/releases) and allows the user to perform several simulation tests relevant for OPV and OLED devices. 
All features that are to be included in v1.0 are now implemented and have undergone significant testing. 
However, there may still be bugs that need to be fixed, so please report any bugs or submit feature requests in the [Issues](https://github.com/MikeHeiber/Excimontec/issues) section. 
Please see the [Changelog](CHANGELOG.md) for a detailed listing of previous and upcoming changes. 

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

## For Software Developers

Public API documentation for the Excimontec package can be viewed [here](https://mikeheiber.github.io/Excimontec/).

## Acknowledgments
Thank you to Dr. Dean M. DeLongchamp at NIST for providing access to computing resources that have supported the development of v1.0. 
Development of v1.0 has been primarily supported by financial assistance award 70NANB14H012 from U.S. Department of Commerce, National Institute of Standards and Technology as part of the Center for Hierarchical Materials Design (CHiMaD).
