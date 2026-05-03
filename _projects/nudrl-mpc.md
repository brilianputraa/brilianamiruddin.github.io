---
title: NUDRL-MPC
subtitle: Deep Reinforcement Learning-Guided Non-Uniform Model Predictive Control
layout: project
date: 2024-03-01
end_date: 2024-12-01
thumbnail: /assets/projects/nudrl-mpc.png
gradient: linear-gradient(135deg, #1a1a2e 0%, #4a4e69 100%)
tags: [MPC, Deep RL, Control, Low-Speed, Autonomous Driving]
github: https://github.com/vialabpnu/path-following-datasets
---

**Master's Thesis** - Developed a novel control technique that dynamically optimizes sampling intervals for non-uniform model predictive control (MPC) using deep reinforcement learning, specifically designed for **low-speed autonomous driving in unstructured environments** like parking lots.

## Problem Addressed

The approach addresses **prediction horizon problems** while considering the vehicle's computational constraints - a key challenge in real-world autonomous driving applications where processing power is limited. In **unstructured environments** like parking lots, traditional uniform MPC struggles with balancing prediction accuracy and computational efficiency.

## Technical Approach

- **Deep RL Agent**: Learns to select optimal non-uniform sampling intervals based on current state and environment conditions
- **Non-uniform MPC**: Adapts prediction horizon dynamically, using finer sampling near the vehicle and coarser sampling further ahead
- **Low-speed Optimization**: **Specifically designed for low-speed scenarios** (parking, maneuvering) where precision matters more than speed
- **Unstructured Environments**: Robust performance in parking lots and other irregular environments without predefined paths
- **Benchmark Validation**: Tested on custom path-following datasets in simulation

## Implementation

Built using Python and PyTorch for the reinforcement learning component, integrated with MPC solver for real-time control. **Custom datasets were developed using Hybrid A* path planning algorithm** to generate realistic reference trajectories for training and evaluation in unstructured parking environments. The dataset is publicly accessible via the GitHub repository below.

## Key Results

Achieved **90% path tracking success rate** in unstructured environments, demonstrating clear superiority over conventional uniform MPC methods.

## Publications

- "Optimal Path Tracking Control for Autonomous Vehicles using Deep Reinforcement Learning-based Non-Uniform Model Predictive Control" - KSAE Fall Conference 2024

## Resources

- [GitHub Repository - Path Following Datasets](https://github.com/vialabpnu/path-following-datasets)