# Molecular dynamics bulk benchmarks
We run molecular dynamics simulations of bulks using LAMMPS to benchmark the simulation times on various CPUs and GPUs. Also, the computational performance of different force-fields might be compared.

Below, we present the number of timesteps per seconds for the various simulations and for various devices. All simulations were run in the micro-canonical ensemble (NVE), but the number of particles in the simulations vary.


| CPU                   | Computer  | Cores | Freq.   | LJ       | SW       | TIP4P  | SiC | SiO2  |
|-----------------------|-----------|-------|---------|----------|----------|--------|-----|-------|
| Intel Core i7-4500U   | Maxwell   | 4     | 1.80GHz | 357.790  |  14.694  |  2.701 |     | 0.055 |
| Intel Xeon E5-2620    | Bigfacet  | 16    | 2.10GHz |          |          |        |     |       |
| Intel Xeon E5-2683    | Fram      | 16    | 2.10GHz |          |          |        |     |       |
| Intel Xeon E5-2670    | Egil      | 16    | 2.60GHz |          |          |        |     |       |
| Intel Xeon W-2295     | Rahman    | 18    | 3.00GHz | 3134.155 | 225.875  | 34.796 |     | 0.666 |
| AMD EPYC 7252         | Hugefacet | 8     | 3.10GHz | 2082.737 | 119.200  | 20.081 |     |       |

| GPU                   | Computer  | Cores | Freq.   | LJ       | SW       | TIP4P  | SiC | SiO2  |
|-----------------------|-----------|-------|---------|----------|----------|--------|-----|-------|
| Nvidia RTX 2070 Super | Rahman    | 2560  | 1.60GHz |          |          |        |     |       |
| Nvidia P100 Pascal    | Bigfacet  | 3584  | 1.20GHz | 1604.503 |  925.301 |   -    |     | 3.013 |
| Nvidia A100 Ampere    | Hugefacet | 8192  | 1.40GHz | 2180.423 | 2070.548 |   -    |     | 14.647|

## Simulations
The different bulk simulations were chosen to spawn out the force-field space. The Lennard-Jones potential is a two-body potential. The TIP4P is a partly bonded force-field. Stillinger-Weber and Vashishta are non-bonded three-body potentials. We investigate different system sizes to challenge the different devices.

#### Lennard-Jones (Ar)
We simulate Lennard-Jonesium (e.g. Argon) using the Lennard-Jones potential, as first suggested by [A. Rahman][1]. Our initial system is a face-centered cube with 2,916 particles, and is simulated at 1197K (10000 steps). See [src/lennardjones/in.lammps](src/lennardjones/in.lammps) for LAMMPS input script.

#### Stillinger-Weber (Si)
Silicon is simulated using the Stillinger-Weber potential and the original parameterization by [Stillinger and Weber][2]. The system consists of 64,000 particles initialized in crystal structure and is simulated at 1000K (10000 steps). See [src/stillingerweber/in.lammps](src/stillingerweber/in.lammps) for LAMMPS input script.

#### TIP4P/2005 (H2O)
Water is simulated using the popular TIP4P potential and the universal parameterization by [Abascal and Vega][3], known as TIP4P/2005. 6,000 water molecules (24,000 particles) are initialized on a grid, and simulated at 300K (1000 steps). See [src/tip4p/in.lammps](src/tip4p/in.lammps) for LAMMPS input script.

#### Vashishta (SiC)

#### Vashishta (SiO2)
Finally, we simulate quartz using the Vashishta potential and the initial parameterization by [Vashishta et al.][4]. The system is initialized with 3,000,000 SiO2 molecules (9,000,000 particles), and simulated at 2000K (100 steps). See [src/sio2/in.lammps](src/sio2/in.lammps) for LAMMPS input script.

## Devices
The devices were not, by any rule, picked cleverly and they do not spawn out the device space in any possible way. In fact, the devices presented here are just the ones that were available for me when doing the comparison.

## References
[1]: [A. Rahman, Phys. Rev. A, 136, 405 (1964)](https://journals.aps.org/pr/abstract/10.1103/PhysRev.136.A405)  
[2]: [F. H. Stillinger and T. A. Weber, Phys. Rev. B, 31, 5262 (1985)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.31.5262)  
[3]: [J. L. F. Abascala) and C. Vega, J. Chem. Phys., 123, 234505 (2005)](https://aip.scitation.org/doi/10.1063/1.2121687)  
[4]: [P. Vashishta, R. K. Kalia and J. P. Rino, Phys. Rev. B, 41, 12197 (1990)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.41.12197)  
