# 2D-Ising-Model-Simulation-using-Monte-Carlo-Methods

This repository contains a Python implementation of the 2D Ising Model simulation using Monte Carlo methods (Metropolis algorithm). 

## Overview
The simulation is implemented in a Jupyter Notebook (`main.ipynb`) and uses `numba` to optimize performance. 
It simulates a square grid with periodic boundary conditions and calculates physical properties such as:
- Magnetization
- Average Energy
- Specific Heat

The notebook also includes visualizations for:
- Spin Configurations at different temperatures
- Magnetization vs Temperature
- Energy Histograms
- Heat Capacity vs Temperature

## Requirements
- Python 3.x
- Jupyter Notebook
- NumPy
- Numba
- Matplotlib