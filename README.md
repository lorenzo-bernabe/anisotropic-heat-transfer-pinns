# Predicting Heat Transfer in Fibre-Reinforced Anisotropic Composite Materials using Physics-Informed Neural Networks (PINNs)

This repository contains the implementation and experiments for the paper:

**"Predicting heat transfer in fibre-reinforced anisotropic composite materials using physics-informed neural networks (PINNs)"**

---

## Overview

This project investigates the application of Physics-Informed Neural Networks (PINNs) for solving parametric heat transfer problems in anisotropic fibre-reinforced composite materials.

The focus is on comparing different training strategies to improve convergence stability and prediction accuracy in anisotropic heat conduction problems.

---

## Problem Description

We solve the parametric anisotropic heat conduction equation in composite materials, where thermal conductivity differs along different material directions due to fibre reinforcement. A ceramic matrix composite is considered as a representative material system, and its thermophysical properties are incorporated into the numerical model. The geometry and material parameters are then nondimensionalized.

The goal is to approximate the temperature field using PINNs without relying on classical mesh-based solvers.

---

## Repository Structure

```
notebooks/
    01_random_training.ipynb                    # Random fibre orientation sampling strategy
    02_sequential_training.ipynb                # Sequential single-angle training strategy
    03_combined_training.ipynb                  # Combined multi-angle training strategy
    04_combined_training_minimumpointnumber.ipynb  # Optimized combined training (fewer points)
comsol_data/                                    # Reference FEM solutions from COMSOL Multiphysics
figures/                                        # Output figures (comparisons, loss curves, temperature fields)
requirements.txt                                # Python package dependencies
```

---

## Training Strategies Compared

We evaluate three different training approaches and optimize the one with the best results:

1. **Random Training** (`01_random_training.ipynb`)
   - This approach follows the idea of non-parametric PINNs, where random collocation points are created over the sample domain. Each point is assigned not only a random spatial location and time, but also a random fibre orientation, which changes every new epoch.

2. **Sequential Training** (`02_sequential_training.ipynb`)
   - This approach trains the PINN sequentially over a predefined list of fibre orientations. For each orientation, a dedicated sample domain is generated and training is performed independently before moving to the next angle.

3. **Combined Training** (`03_combined_training.ipynb`)
   - This approach generates multiple sample domains, each with a different randomly selected fibre orientation. The losses from all domains are summed and used collectively for each training step.

4. **Combined Training – Optimized Minimum Point Number** (`04_combined_training_minimumpointnumber.ipynb`)
   - Optimized version of combined training with reduced sampling points (N = 300 edge samples, M = 3000 collocation points vs. N = 1000, M = 10000 in the other approaches).

---

## Installation

Install the dependencies with `pip install -r requirements.txt`. Each notebook also contains a Colab badge to run it directly in the browser without any local setup.

---

## COMSOL Reference Data

The `comsol_data/` folder contains steady-state and transient temperature fields computed with COMSOL Multiphysics for fibre orientations of −60°, −45°, −30°, 0°, 30°, 45°, 60°, and 90°. These are used to validate PINN predictions in the error analysis cells of each notebook.
