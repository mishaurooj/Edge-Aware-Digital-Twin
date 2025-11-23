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
