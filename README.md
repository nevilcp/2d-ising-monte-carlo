# 2D Ising Model: Monte Carlo Simulation

## Abstract
This repository contains the computational implementation of a two-dimensional (2D) Ising model simulated via Monte Carlo methods. The primary objective of this project is to investigate the ferromagnetic phase transitions and critical phenomena inherent in statistical mechanics. By employing the Metropolis-Hastings algorithm, the simulation models the stochastic dynamics of interacting magnetic dipole moments (spins) on an $N \times N$ square lattice, enabling the empirical derivation of macroscopic thermodynamic observables such as magnetization, internal energy, specific heat capacity, and entropy as functions of temperature, along with field-driven hysteresis loops.

## Getting Started
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab main.ipynb
```
The full notebook runs two temperature sweeps (about 1.3 billion spin-flip attempts each) plus the hysteresis loops, and takes roughly 6 minutes on a desktop CPU.

### Project Layout
* `main.ipynb`: the simulation, plots and analysis.
* `requirements.txt`: Python dependencies.
* `ruff.toml`: lint and format configuration. Check the code with `ruff check .` and `ruff format .` (install ruff with `pip install ruff`).

## Methodology
The core simulation logic is grounded in the standard theoretical framework of the Ising model, defined by the Hamiltonian:

$$ H = -J \sum_{\langle i, j \rangle} s_i s_j - H \sum_i s_i $$

where $J$ is the exchange interaction energy, $s_i \in \{-1, +1\}$ represents the discrete spin states, $\langle i, j \rangle$ denotes nearest-neighbor interactions, and $H$ is the external magnetic field. The computational approach utilizes:
1. **Lattice Initialization:** Random or aligned uniform initialization of spin states on a 2D grid.
2. **Boundary Conditions:** Periodic boundary conditions (PBC) are enforced via a ring of ghost cells, which reduces edge effects and approximates a bulk system.
3. **Metropolis Algorithm:** A Markov Chain Monte Carlo (MCMC) method is used to sample the canonical ensemble. One Monte Carlo sweep consists of $N^2$ single spin-flip attempts at randomly chosen sites. A flip is always accepted if it lowers the energy, and otherwise accepted with the Boltzmann probability $P(\Delta E) = \exp(-\Delta E / k_B T)$.
4. **Thermalization and Measurement:** The system is allotted a predefined thermalization period to reach equilibrium before time-averaging the variables for observable extraction.

## Simulation Parameters
With system configurations generated dynamically, the primary independent variables and specific input parameters used in this repository's primary notebook are defined as follows:
* **Lattice Size ($N$):** Fixed lattice dimensions of $50 \times 50$ ($N=50$).
* **External Magnetic Field ($H$):** The temperature sweep is run at $H = 0$ and at $H = 0.2$; hysteresis loops sweep $H$ over $[-1.5, 1.5]$.
* **Temperature ($T$):** Swept across a range from $0.1$ to $5.0$ in reduced units $\frac{k_B T}{J}$ (increments of $0.1$).
* **Monte Carlo Sweeps:** $10,000$ thermalization sweeps for equilibration and $1,000$ measurement sweeps for statistical sampling at each temperature. The hysteresis loops use $300$ relaxation and $300$ measurement sweeps per field value, at $T = 1.5, 2.2, 3.0$.

## Results & Discussion
The notebook runs the temperature sweep at both $H = 0$ and $H = 0.2$. The applied field smooths the second-order phase transition seen in the zero-field system.
* **Spin Configurations (Microstates):** Snapshots of the lattice at selected temperatures (below $T_c$, near $T_c$, and above $T_c$) visually indicate macroscopic domain formation, critical opalescence (fractal-like clusters), and thermal disorder.
* **Magnetization:** At $H = 0$, $|M|$ drops sharply near the critical temperature $T_c \approx 2.269$. Some low-temperature points fall well below 1 because random starts can freeze into striped domains that never fully order. The external field breaks the symmetry, resulting in a nonzero residual magnetization even above $T_c$.
* **Energy Histograms:** Histograms of the total energy at three temperatures show how the fluctuations broaden near the transition.
* **Specific Heat:** The heat capacity per spin, computed from the energy variance as $C_v = \mathrm{Var}(E) / (N^2 (k_B T)^2)$, exhibits a peak associated with the phase transition.
* **Hysteresis:** Sweeping $H$ up and down at fixed temperature produces an open loop below $T_c$ and a reversible curve above it.
* **Entropy:** Integrating $C_v / T$ over temperature gives the entropy per spin of the zero-field system, relative to the lowest simulated temperature.
