---
title: Mixed Traffic AVP
subtitle: Automated Valet Parking in Mixed Traffic Conditions
layout: project
date: 2023-08-01
end_date: 2024-02-01
thumbnail: https://img.youtube.com/vi/MenUcENcZ2c/maxresdefault.jpg
video: MenUcENcZ2c
tags: [AVP, LiDAR, CenterPoint, ROS, MPC]
organization: ViaLab, Pusan National University
---

Developed an autonomous valet parking system operating in **mixed traffic conditions** with other vehicles and pedestrians. The system handles complex scenarios where the parking lot is shared with other traffic participants. Tested and verified on actual autonomous vehicle platform in ROS environment.

## Key Technologies

### Perception & Localization
- **Dual LiDAR System**: VLP-16 and OS1-64 sensors integrated for robust environment perception
- **Virtual Laser Scan**: Innovative approach for parking lot road sign detection
- **AMCL Localization**: **Improved standard ROS AMCL package by implementing Ackermann motion model** (from probabilistic robotics) for **four-wheeled car-like vehicles**, replacing the default differential drive-only support. Also integrated **road marker detection using dual LiDARs** for enhanced localization accuracy in unstructured parking environments
- **CenterPoint 3D Object Detection**: Deep learning-based detection for vehicles, pedestrians, and obstacles

### Planning & Control
- **Nonlinear MPC**: Model Predictive Control for dynamic obstacle avoidance and trajectory optimization
- **Real-time Path Planning**: A* and Hybrid A* algorithms for parking slot approach
- **Trajectory Optimization**: Smooth path generation considering vehicle kinematics

## Implementation Details

- C++, Python, and ROS for system integration
- Gazebo simulation for initial development and testing
- Real vehicle platform validation with full sensor suite
- Modular architecture for easy component updates

## Results

Successfully demonstrated autonomous valet parking with:
- **80% road sign detection accuracy** in parking lot environments
- Safe navigation among moving vehicles and pedestrians
- Robust localization in partially mapped environments

## Publications

- "Development of CASE System for Automated Valet Parking" - ICS 2023 Symposium
- "Representing Dynamic Objects from 3D Object Detection Network for Autonomous Driving in ROS Navigation Framework" - KSAE 2023

## Video Demo

<iframe width="560" height="315" src="https://www.youtube.com/embed/MenUcENcZ2c" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>