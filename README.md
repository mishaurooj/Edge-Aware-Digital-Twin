# 🚗 Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints

> **Official Kaggle Implementation and Results Repository**  
> _Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints_  

---

## 📘 Overview

This repository contains complete **Kaggle-executed experiments**, **graphs**, **trained models**, and **deployment metrics** for the DBRA24 dataset.  
The project integrates **CAN bus analytics**, **V2X link context**, and **edge deployment profiling** into a unified **Digital Twin (DT)** framework for real-time driver behavior and route anomaly detection.

---

## 📊 Dataset: [DBRA24 – Driver Behavior and Route Anomaly Detection](https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24)

- **Records:** 120,000  
- **Features:** 26  
- **Location:** California  
- **Collected:** January 2023  
- **Applications:** Driver behavior analysis, route anomaly detection, and fleet optimization  

---

## 🧠 Digital Twin Components

| Module | Description | Framework |
|---------|--------------|------------|
| **CAN–Twin** | Learns temporal CAN traffic patterns (speed, RPM, braking) | TCN-Lite / Transformer-Tiny |
| **Comm–Twin** | Models 5G NR–V2X link context (latency, loss, bitrate, AoI) | Simulated / ETSI MEC-030 |
| **Calibrator** | V2X-conditioned reliability mapping (ECE, NLL optimization) | PyTorch MLP |
| **Orchestrator** | Schedules MEC vs edge inference with adaptive timing | TensorRT / ONNX Runtime |

---

## 🖼️ DBRA24 Feature Distributions

Below are the feature-wise distributions generated from the Kaggle notebook (`1-dbra24-visualization.ipynb`).  
These show variability across trips and drivers.

| Feature | Visualization |
|----------|----------------|
| Acceleration | ![dist_acceleration](./DABRA24-Graphs/dist_acceleration.png) |
| Acceleration Variation | ![dist_acceleration_variation](./DABRA24-Graphs/dist_acceleration_variation.png) |
| Anomalous Events | ![dist_anomalous_event](./DABRA24-Graphs/dist_anomalous_event.png) |
| Behavioral Consistency | ![dist_behavioral_consistency_index](./DABRA24-Graphs/dist_behavioral_consistency_index.png) |
| Brake Usage | ![dist_brake_usage](./DABRA24-Graphs/dist_brake_usage.png) |
| Driver ID | ![dist_driver_id](./DABRA24-Graphs/dist_driver_id.png) |
| Fuel Consumption | ![dist_fuel_consumption](./DABRA24-Graphs/dist_fuel_consumption.png) |
| Geofencing Violations | ![dist_geofencing_violation](./DABRA24-Graphs/dist_geofencing_violation.png) |
| Heading | ![dist_heading](./DABRA24-Graphs/dist_heading.png) |
| Lane Deviation | ![dist_lane_deviation](./DABRA24-Graphs/dist_lane_deviation.png) |
| Latitude | ![dist_latitude](./DABRA24-Graphs/dist_latitude.png) |
| Longitude | ![dist_longitude](./DABRA24-Graphs/dist_longitude.png) |
| Route Anomaly | ![dist_route_anomaly](./DABRA24-Graphs/dist_route_anomaly.png) |
| Route Deviation Score | ![dist_route_deviation_score](./DABRA24-Graphs/dist_route_deviation_score.png) |
| RPM | ![dist_rpm](./DABRA24-Graphs/dist_rpm.png) |
| Speed | ![dist_speed](./DABRA24-Graphs/dist_speed.png) |
| Steering Angle | ![dist_steering_angle](./DABRA24-Graphs/dist_steering_angle.png) |
| Stop Events | ![dist_stop_events](./DABRA24-Graphs/dist_stop_events.png) |
| Trip Distance | ![dist_trip_distance](./DABRA24-Graphs/dist_trip_distance.png) |
| Trip Duration | ![dist_trip_duration](./DABRA24-Graphs/dist_trip_duration.png) |
| Trip ID | ![dist_trip_id](./DABRA24-Graphs/dist_trip_id.png) |
| Vehicle ID | ![dist_vehicle_id](./DABRA24-Graphs/dist_vehicle_id.png) |

---

## 🧾 Comprehensive Detection, Calibration, and Event-Level Responsiveness Summary

| Model / Ablation | PR-AUC(A) | F1(A) | PR-AUC(B) | RMSE(C) | ECE | Mean TTD (s) ↓ | FP/h ↓ | ΔAUC vs Full | Remarks |
|------------------|-----------:|------:|-----------:|--------:|----:|----------------:|-------:|--------------:|----------|
| 🥇 **V2X-Boost (A1)** | **0.983** | **0.959** | **0.985** | **0.033** | 0.064 | **0.161** | **30.9** | **+0.010** | Best overall responsiveness and accuracy |
| A2 – Chrono-Base | 0.954 | 0.914 | 0.955 | 0.042 | 0.042 | 0.363 | 61.6 | +0.005 | Context-aware and stable convergence |
| 🟥 A3 – Gate-Off | 0.785 | 0.839 | 0.790 | 0.062 | 0.102 | 0.000 | 200.0 | -0.027 | No gating → unstable calibration |
| A4 – LagSense | 0.951 | 0.909 | 0.956 | 0.063 | 0.089 | 0.531 | 54.7 | -0.022 | Delayed under jittered signals |
| A5 – MiniSeq | 0.949 | 0.904 | 0.953 | 0.065 | 0.081 | 0.416 | 68.1 | -0.016 | Fast but noise-sensitive |
| 🥈 A6 – Sync-Net | 0.959 | 0.924 | 0.962 | 0.036 | 0.040 | 0.340 | 52.1 | +0.009 | Fast, well-calibrated detection |
| A7 – Lag-Robust | 0.959 | 0.924 | 0.962 | 0.064 | 0.036 | 0.340 | 52.1 | +0.009 | Robust to temporal jitter |
| A8 – Focal-Core | 0.972 | 0.951 | 0.968 | 0.061 | 0.078 | 0.230 | 34.1 | -0.028 | Better rare-fault sensitivity |
| 🟥 A9 – Tempo-CNN | 0.864 | 0.846 | 0.862 | 0.066 | 0.114 | 0.316 | 150.0 | -0.019 | Limited temporal capacity |
| 🥉 A10 – Deep-Core | 0.959 | 0.926 | 0.958 | 0.065 | 0.057 | 0.366 | 49.3 | +0.001 | High accuracy, moderate latency |
| A11 – Fusion-Core | 0.947 | 0.901 | 0.945 | 0.064 | 0.050 | 0.453 | 68.8 | +0.002 | Full contextual fusion (Calibrator + Comm–Twin + Orchestrator) |

---

## ⚙️ Deployment Profiling Summary (Edge / MEC)

| Model | p50 (ms) | p95 (ms) | p99 (ms) | Throughput (win/s) | FLOPs (M) | Params (M) | Energy (J) |
|--------|----------:|----------:|----------:|-------------------:|-----------:|------------:|------------:|
| **A1** | 32.38 | 33.76 | 36.05 | 15682.7 | 0.001 | 0.012 | 1.457 |
| **A2** | 8.32 | 8.39 | 8.42 | 7698.2 | 130.01 | 2.161 | 0.018 |
| **A3** | 8.32 | 8.40 | 8.42 | 7690.2 | 130.01 | 2.161 | 0.019 |
| **A4** | 8.35 | 8.51 | 8.64 | 7685.3 | 130.01 | 2.161 | 0.019 |
| **A5** | 8.34 | 8.42 | 8.44 | 7681.6 | 130.01 | 2.161 | 0.019 |
| **A6** | 8.32 | 8.40 | 8.44 | 7689.8 | 130.01 | 2.161 | 0.019 |
| **A7** | 8.31 | 8.38 | 8.44 | 7706.9 | 130.01 | 2.161 | 0.019 |
| **A8** | 8.35 | 8.41 | 8.43 | 7668.8 | 130.01 | 2.161 | 0.019 |
| **A9** | 8.36 | 8.46 | 8.50 | 7651.6 | 130.01 | 2.161 | 0.019 |
| **A10** | 59.66 | 61.01 | 65.85 | 1067.7 | 1.821 | 0.031 | 0.061 |
| **A11** | 8.32 | 8.40 | 8.46 | 7690.4 | 130.01 | 2.161 | 0.019 |

---

## 🧑‍💻 Authors

| Name | Affiliation | Email |
|------|--------------|--------|
| **Muhammad Ajmal** | IMSIU | [email protected] |
| **Misha Urooj Khan** | CERN | misha.urooj.khan@cern.ch |
| **Ahmad Suleman** | CRD | [email protected] |

---

## 🧩 Acknowledgment

This work was executed on **Kaggle Tesla T4 GPUs** under the **DigitalTwin-Fault Project**.  
Supported by the **Deanship of Scientific Research, Imam Mohammad Ibn Saud Islamic University (IMSIU)** — Grant **IMSIU-DDRSP2504**.

---

## 📜 License

- **Code**: MIT License  
- **Dataset**: [Kaggle DBRA24 Terms of Use](https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24)

---
