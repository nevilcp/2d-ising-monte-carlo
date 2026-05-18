# 2D Ising Model: Monte Carlo Simulation

## Abstract
This repository contains the computational implementation of a two-dimensional (2D) Ising model simulated via Monte Carlo methods. The primary objective of this project is to investigate the ferromagnetic phase transitions and critical phenomena inherent in statistical mechanics. By employing the Metropolis-Hastings algorithm, the simulation models the stochastic dynamics of interacting magnetic dipole moments (spins) on an $L \times L$ square lattice, enabling the empirical derivation of macroscopic thermodynamic observables such as magnetization, internal energy, specific heat capacity, and magnetic susceptibility as functions of temperature.

## Methodology
The core simulation logic is grounded in the standard theoretical framework of the Ising model, defined by the Hamiltonian:

$$ H = -J \sum_{\langle i, j \rangle} s_i s_j - h \sum_i s_i $$

where $J$ is the exchange interaction energy, $s_i \in \{-1, +1\}$ represents the discrete spin states, $\langle i, j \rangle$ denotes nearest-neighbor interactions, and $h$ is the external magnetic field. The computational approach utilizes:
1. **Lattice Initialization:** Random or aligned uniform initialization of spin states on a 2D grid.
2. **Boundary Conditions:** Periodic boundary conditions (PBC) are enforced to mitigate finite-size effects and simulate the thermodynamic limit.
3. **Metropolis Algorithm:** A Markov Chain Monte Carlo (MCMC) method is used to sample the canonical ensemble. At each Monte Carlo Step (MCS), single spin-flip attempts are evaluated based on the Boltzmann probability factor, $P(\Delta E) = \exp(-\Delta E / k_B T)$.
4. **Thermalization and Measurement:** The system is allotted a predefined thermalization period to reach equilibrium before time-averaging the variables for observable extraction.

## Simulation Parameters
With system configurations generated dynamically, the primary independent variables and specific input parameters used in this repository's primary notebook are defined as follows:
* **Lattice Size ($N$):** Fixed lattice dimensions of $50 \times 50$ ($N=50$).
* **External Magnetic Field ($H$):** A predefined external magnetic field $H = 0.2$ is applied to the system.
* **Temperature ($T$):** Swept across a range from $0.1$ to $5.0$ in reduced units $\frac{k_B T}{J}$ (increments of $0.1$).
* **Monte Carlo Steps (MCS):** Configuration limits set to $10,000$ thermalization sweeps for equilibration and $1,000$ measurement sweeps for accurate statistical sampling.

## Results & Discussion
The simulation maps key thermodynamic and microscopic properties across the temperature range. It is particularly interesting to analyze the system with an applied external magnetic field ($H = 0.2$), which smooths the expected second-order phase transition compared to a zero-field system.
* **Spin Configurations (Microstates):** Snapshots of the lattice configuration at selected temperatures (below $T_c$, near $T_c$, and above $T_c$) visually indicate macroscopic domain formation, critical opalescence (fractal-like clusters), and thermal disorder.
* **Magnetization:** The presence of the external magnetic field breaks the symmetry, resulting in an expected nonzero residual magnetization even above the standard critical temperature $T_c \approx 2.269$.
* **Specific Heat & Energy Fluctuations:** The heat capacity exhibits a peak associated with the underlying phase transition, directly corresponding to variance in the energy histograms, mapping the thermal fluctuations at varying temperatures.
