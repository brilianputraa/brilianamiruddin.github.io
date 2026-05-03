---
title: Exclusive Traffic AVP
subtitle: Automated Valet Parking in Controlled Environment
layout: project
date: 2022-09-01
end_date: 2023-07-01
thumbnail: https://img.youtube.com/vi/KxvLOT3hLbA/maxresdefault.jpg
video: KxvLOT3hLbA
tags: [AVP, MPC, Parking, ROS]
organization: ViaLab, Pusan National University
---

Developed autonomous parking system using **linear MPC algorithm** with structured parking space management. Built a controlled environment where only autonomous vehicles operate, enabling systematic development and testing. Tested on actual autonomous vehicle platform in ROS environment.

## Key Technologies

### Control System
- **Linear MPC**: Model Predictive Control for precise path tracking and trajectory execution
- **Stanley Controller**: Alternative path tracking for comparison
- **Pure Pursuit**: Benchmark algorithm for performance evaluation

### Parking Management
- **Structured Parking Management**: System for organizing and allocating parking slots
- **Slot Detection**: Vision-based identification of available parking spaces
- **Approach Planning**: Optimized trajectories for parking entry

## Implementation Details

- C++, Python, and ROS integration
- Gazebo simulation environment for controlled testing
- Real vehicle platform validation
- Comprehensive unit and integration testing

## System Architecture

- **Perception**: LiDAR-based localization and slot detection
- **Planning**: Path planning for parking approach and execution
- **Control**: MPC-based trajectory tracking
- **Management**: Parking slot allocation and coordination

## Video Demo

<iframe width="560" height="315" src="https://www.youtube.com/embed/KxvLOT3hLbA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>