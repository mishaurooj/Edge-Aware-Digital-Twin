# 🚗 Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints

> **Official Kaggle Implementation and Results Repository**  
> _Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints_  

---

## 📘 Overview

This repository contains complete **Kaggle-executed experiments**, **graphs**, **trained models**, and **deployment metrics** for the DBRA24 dataset.  
The project integrates **CAN bus analytics**, **V2X link context**, and **edge deployment profiling** into a unified **Digital Twin (DT)** framework for real-time driver behavior and route anomaly detection.

![Banner](DigitalTwin_Edge_Aware1.jpg)
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

This repository contains:
- Full TCN–DT model
- Ablation variants (A1–A11)
- Training & evaluation pipelines
- Deployment-ready MEC/edge model (“TCN–DT–Edge”)
- Results, trained models & graphs

---

## 📊 Key Results

### **Table 1 — Detection, Calibration & Event Responsiveness (DBRA24)**
(Formatted from paper)

| Model | PR‑AUC_yA | F1_yA | PR‑AUC_yB | RMSE_yC | ECE_yC | TTD (s) | FP/h |
|------|-----------|-------|-----------|---------|--------|----------|------|
| A1 – GBM (Static) | **0.983** | **0.959** | **0.985** | **0.033** | 0.064 | **0.16** | 30.9 |
| A2 – TCN–DT–Context | 0.954 | 0.914 | 0.955 | 0.066 | 0.042 | 0.36 | 61.6 |
| A3 – TCN–DT–NoGate | 0.785 | 0.839 | 0.790 | 0.062 | 0.102 | 0.01 | 199.5 |
| A4 – TCN–DT–Big | 0.959 | 0.926 | 0.958 | 0.065 | 0.057 | 0.37 | 49.3 |
| A5 – TCN–DT–Lag | 0.951 | 0.909 | 0.956 | 0.063 | 0.089 | 0.53 | 54.7 |
| A6 – TCN–DT–ShortSeq | 0.949 | 0.904 | 0.953 | 0.064 | 0.081 | 0.42 | 68.1 |
| A7 – TCN–DT–LagRobust | 0.959 | 0.924 | 0.962 | 0.064 | **0.036** | 0.34 | 52.1 |
| A8 – TCN–DT–MapFree | 0.954 | 0.914 | 0.955 | 0.064 | **0.025** | 0.46 | 56.0 |
| A9 – TCN–DT–Focal | 0.972 | 0.951 | 0.968 | **0.061** | 0.078 | **0.23** | **34.1** |
| A10 – TCN–DT–Edge | 0.864 | 0.846 | 0.862 | 0.066 | 0.114 | 0.32 | 150.5 |
| **A11 – TCN–DT–Full (Proposed)** | 0.947 | 0.901 | 0.945 | 0.064 | **0.050** | 0.45 | 68.8 |

---

### **Table 2 — Efficiency & Orchestration Profiling**

| Model | p50 | p95 | p99 | Throughput | FLOPs | Params | Energy |
|------|-----|-----|-----|------------|--------|--------|--------|
| A1 – GBM | 32.38 | 33.76 | 36.05 | **15682.7** | **0.001M** | 0.012M | **1.46J** |
| A2 – Context | 8.32 | 8.39 | 8.42 | 7698.2 | 130M | 2.16M | 0.0184J |
| A3 – NoGate | 8.32 | 8.40 | 8.42 | 7690.2 | 130M | 2.16M | 0.0187J |
| A4 – Big | 59.66 | 61.01 | 65.85 | 1067.7 | 1821M | 0.031M | 0.061J |
| A5 – Lag | ... | ... | ... | ... | ... | ... | ... |
| **A11 – Full** | 8.32 | 8.40 | 8.46 | 7690.4 | 130M | 2.16M | 0.0193J |

---

### **Table 3 — Ablation Mapping**

| ID | Variant | Objective | Active Modules | Phase |
|----|---------|-----------|----------------|--------|
| A1 | GBM | Static baseline | – | Benchmark |
| A2 | Context | Remove env. context | P1, P3–P4 | P1 |
| A3 | NoGate | Disable gates | P1–P3 | P3 |
| ... | ... | ... | ... | ... |
| **A11** | **Full** | **Complete unified DT** | **P1–P4** | **Full integration** |

---

## 🧠 Architecture

### **Unified Digital Twin Pipeline**
![Architecture](DigitalTwin_Models_Architecture.jpg)

### **Edge-Aware MEC Deployment**
![Edge](DigitalTwin_Edge_Aware1.jpg)

---
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
