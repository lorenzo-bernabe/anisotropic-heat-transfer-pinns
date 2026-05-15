# Predicting Heat Transfer in Fibre-Reinforced Anisotropic Composite Materials using Physics-Informed Neural Networks (PINNs)

This repository contains the implementation and experiments for the paper:

**"Predicting heat transfer in fibre-reinforced anisotropic composite materials using physics-informed neural networks (PINNs)"**

---

## Overview

This project investigates the application of Physics-Informed Neural Networks (PINNs) for solving parametric heat transfer problems in anisotropic fibre-reinforced composite materials.

The focus is on comparing different training strategies to improve convergence stability and prediction accuracy in anisotropic heat conduction problems.

---

## Problem Description

We solve the parametric anisotropic heat conduction equation in composite materials, where thermal conductivity differs along different material directions due to fibre reinforcement.

The goal is to approximate the temperature field using PINNs without relying on classical mesh-based solvers.

---

## Training Strategies Compared

We evaluate three different training approaches and optimize the one with the best results:

1. **Random Training**
   - This approach follows the idea of non-parametric PINNs, where random collocation points are created over the sample domain. Each point is assigned not only a random spatial location and time, but also a random fibre orientation, which changes every new epoch

2. **Sequential Training**
   - This approach first generates a random sample domain with a fixed, randomly selected angle. Once training with that sample domain is completed, a new random sample domain with a different fixed angle is generated and training continues with this new sample domain

3. **Combined Training**
   - This approach begins by generating random sample domains, each with a different, fixed, and randomly selected angle. Instead of training the PINN on each domain separately, the loss for each domain is first calculated, subsequently summed and then used collectively for training

4. **Combined Training (Optimized Minimum Point Number)**
   - Optimized version of combined training with reduced sampling points
