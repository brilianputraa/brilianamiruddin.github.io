---
title: AI-based AHU Energy Analysis
subtitle: Predictive Maintenance for Air Handling Units
layout: project
date: 2025-08-01
gradient: linear-gradient(135deg, #00b894 0%, #00cec9 100%)
tags: [ML, LLM, RAG, Predictive Maintenance, IoT]
organization: Daewoong ENG
---

Developing a **predictive maintenance system** for Air Handling Units (AHU) and core production utility equipment using machine learning and LLM-based anomaly detection. The system enables proactive maintenance scheduling and minimizes production downtime risks.

## System Overview

Integrated CatBoost machine learning model with RAG-LLM pipeline for:
- **Anomaly Detection**: Real-time monitoring of sensor data for early warning signs
- **Fault Diagnosis**: Automated analysis of potential causes when anomalies detected
- **Predictive Alerts**: Proactive notifications before equipment failure

## Technologies

### Machine Learning & AI
- **CatBoost**: Gradient boosting for energy consumption prediction and anomaly classification
- **RAG/LLM Pipeline (Qdrant)**: Knowledge retrieval for fault diagnosis and maintenance recommendations
- **Vector Database**: Historical maintenance logs and equipment manuals indexed for quick retrieval

### Data Infrastructure
- **Airflow**: Data pipeline orchestration for sensor data collection
- **SQL**: Historical data storage and querying

### User Interface
- **Next.js + TypeScript + Tailwind**: Modern dashboard for real-time monitoring
- **Telegram Bot**: Instant alerts to maintenance team

## Key Contributions

### Maintenance Operations
- GMP-compliant preventive maintenance for:
  - Air Handling Units (AHU)
  - Air compressors
  - Constant temperature/humidity units
  - BMS/EMS systems

### Monitoring & Analytics
- Real-time dashboard tracking:
  - Heating/cooling valve positions
  - Fan power consumption
  - Temperature and humidity levels
- Energy efficiency analysis and optimization recommendations

### System Improvements
- **Minimized Downtime**: Predictive alerts reduce unplanned shutdowns
- **Cost Optimization**: Better spare parts management and maintenance scheduling
- **Compliance**: Full GMP documentation and audit trail