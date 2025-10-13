# Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints

> Reproducible implementation and experimental results for  
> **“Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints”**

---

## 🚗 Overview

This repository contains the **Kaggle-executed experiments** and complete **Digital Twin (DT) pipeline** for real-time **driver behavior and route anomaly detection** using the **DBRA24 Dataset**.  
The project couples **CAN-bus signal modeling**, **V2X link conditioning**, and **edge-deployable AI** for **fault detection and diagnosis (FDD)**.

---

## 🧠 System Components

| Module | Description | Framework |
|---------|--------------|------------|
| **CAN–Twin** | Learns temporal CAN traffic patterns using 1D convolutions and temporal context | PyTorch / TCN-Lite |
| **Comm–Twin** | Generates latency, packet-loss, and bitrate context aligned with 5G NR-V2X standards | Simulated / ETSI MEC 030 |
| **V2X–Aware Calibrator** | Adjusts model confidence using link conditions to ensure reliable probability estimates | PyTorch / MLP |
| **Execution Orchestrator** | Routes inference between vehicle ECU (local) and MEC (edge) for optimal latency-energy balance | TensorRT / ONNX Runtime |

---

## 📊 Dataset: [DBRA24 – Driver Behavior & Route Anomaly Detection](https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24)

| Property | Description |
|-----------|--------------|
| **Records** | 120,000 |
| **Features** | 26 |
| **Region** | California |
| **Period** | January 2023 |
| **Use Cases** | Driver profiling, route anomaly detection, logistics optimization |

Each trip entry includes speed, acceleration, RPM, steering angle, trip distance, fuel consumption, lane deviation, brake usage, route anomaly flags, and behavioral consistency indices.

---

## ⚗️ Kaggle Execution

All experiments were executed in **Kaggle Notebooks** using the DBRA24 dataset.  
The folder `Codes/` contains cleaned and exported `.ipynb` versions:

| Notebook | Description |
|-----------|--------------|
| `1-dbra24-visualization.ipynb` | Exploratory Data Analysis and feature distribution graphs |
| `2-dbra24-ablations-complete.ipynb` | Model ablation comparisons across 10 variants (A1–A10) |
| `3-dbra24-DeLong-AUC-significance-test.ipynb` | Statistical tests for AUROC differences |
| `4-dbra24-paper-graphs.ipynb` | IEEE-style figures for publication |
| `train-loss-results-all-ablations.txt` | Aggregated training logs for reproducibility |

---

## 📁 Repository Layout

```
EdgeAware-DigitalTwin-V2X/
│
├── Codes/
│   ├── 1-dbra24-visualization.ipynb
│   ├── 2-dbra24-ablations-complete.ipynb
│   ├── 3-dbra24-DeLong-AUC-significance-test.ipynb
│   ├── 4-dbra24-paper-graphs.ipynb
│   └── train-loss-results-all-ablations.txt
│
├── DABRA24-Graphs/
│   ├── dist_acceleration.png
│   ├── dist_brake_usage.png
│   ├── dist_speed.png
│   ├── dist_route_deviation_score.png
│   ├── dist_anomalous_event.png
│   ├── dist_lane_deviation.png
│   ├── dist_fuel_consumption.png
│   ├── dist_geofencing_violation.png
│   ├── dist_trip_duration.png
│   └── ... (20 total feature distributions)
│
├── Results/
│   ├── DBRA24_results.xlsx
│   ├── deployment_metrics.xlsx
│   └── train-loss-results-all-ablations.txt
│
├── Trained-Models/
│   ├── A1_best.pt ... A10_best.pt
│   ├── BiLSTM_Full_best.pt
│   └── (PyTorch weights for all ablations)
│
└── README.md
```

---

## 📈 Experimental Results

### **Model Comparison (DBRA24)**
| Model | PR–AUC | F1 | ECE ↓ | TTD (s) ↓ | FP/h ↓ | Rank |
|--------|--------:|----:|-------:|-----------:|--------:|------:|
| **V2X–Boost (A1)** | **0.9825** | **0.9588** | 0.019 | 1.25 | 0.04 | 🥇 |
| **Focal–Lite (A6)** | 0.9591 | 0.9240 | 0.036 | 1.78 | 0.06 | 🥈 |
| **BiLSTM–Full** | 0.9510 | 0.9184 | 0.052 | 2.02 | 0.07 | 🥉 |

---

### **Deployment Metrics (Edge vs MEC)**

| Placement | Latency p50 (ms) | p95 (ms) | FLOPs (M) | Params (M) | Energy (J) |
|------------|----------------:|----------:|-----------:|-------------:|------------:|
| **Edge–Local (TensorRT)** | 8.3 | 8.4 | 0.130 | 0.012 | 0.019 |
| **MEC–Remote (ONNX-INT8)** | 32.4 | 36.0 | 1.821 | 0.031 | 1.46 |

> *Inference optimized via quantization (INT8) and layer fusion. Measured on Kaggle Tesla T4.*

---

## 🖼️ Sample Graphs

| Variable | Distribution |
|-----------|--------------|
| Acceleration | ![Acceleration](./DABRA24-Graphs/dist_acceleration.png) |
| Steering Angle | ![Steering Angle](./DABRA24-Graphs/dist_steering_angle.png) |
| Brake Usage | ![Brake Usage](./DABRA24-Graphs/dist_brake_usage.png) |
| Route Deviation Score | ![Route Deviation](./DABRA24-Graphs/dist_route_deviation_score.png) |
| RPM | ![RPM](./DABRA24-Graphs/dist_rpm.png) |

> Each distribution plot shows normalized frequency with KDE overlay to depict driving and route dynamics variability.

---

## ⚙️ Reproducibility

**Run the experiments on Kaggle:**
1. Upload `/Codes` notebooks to Kaggle.
2. Attach the [DBRA24 dataset](https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24).
3. Execute cells sequentially.
4. Outputs (metrics + figures) are saved to `/Results2` automatically.

---

## 📦 Model Deployment

**Export Formats**
- ONNX: `onnx.export(model, sample, "model.onnx")`
- TensorRT: `trtexec --onnx=model.onnx --int8`

**MEC Integration**
- Supports ETSI GS MEC-003 and MEC-030 APIs.
- REST endpoint `/api/v2xdt/infer` for calibrated anomaly scores.

---

## 📜 Citations

```bibtex
@article{ajmal2025edgeawareDT,
  title={Edge-Aware Digital Twin for Real-Time Driver Behavior and Route Anomaly Prediction under 5G–V2X Constraints},
  author={Ajmal, Muhammad and Khan, Misha Urooj and Suleman, Ahmad},
  journal={IEEE Transactions on Intelligent Transportation Systems},
  year={2025}
}

@dataset{dbra24,
  author={Dataset Engineer},
  title={Driver Behavior and Route Anomaly Detection (DBRA24)},
  year={2024},
  publisher={Kaggle},
  url={https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24}
}
```

---

## 🧾 License

- **Code** — MIT License  
- **Data** — Licensed under [Kaggle Terms of Use](https://www.kaggle.com/datasets/datasetengineer/driver-behavior-and-route-anomaly-dataset-dbra24)

---

## 🧑‍💻 Authors

| Name | Affiliation | Email |
|------|--------------|--------|
| **Muhammad Ajmal** | IMSIU | [email protected] |
| **Misha Urooj Khan** | CERN | misha.urooj.khan@cern.ch |
| **Ahmad Suleman** | CRD | [email protected] |

---

## 🧩 Acknowledgment

This research was performed on **Kaggle GPUs (Tesla T4)** under the  
**DigitalTwin-Fault Project**, with support from the  
**Deanship of Scientific Research, IMSIU (Grant IMSIU-DDRSP2504).**

---

## 🌐 Repository Snapshot

![Project Summary](./docs/repo_overview.png)
