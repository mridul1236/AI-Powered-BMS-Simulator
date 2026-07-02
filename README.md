# 🔋 AI-Powered Battery Management System Simulator

> **Machine Learning Assisted Battery Management System (BMS) with SoH Estimation, SoC Tracking, Cell Failure Prediction, and 282-Cycle Early Warning using the NASA Li-ion Battery Dataset.**

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange.svg)
![XGBoost](https://img.shields.io/badge/XGBoost-Enabled-green.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)

---

## 📌 Overview

This project implements an **AI-powered Battery Management System (BMS)** capable of monitoring lithium-ion battery health using machine learning and physics-based modeling.

The simulator predicts:

- 🔋 State of Health (SoH)
- ⚡ State of Charge (SoC)
- 🚨 Cell Failure
- 📈 Remaining Useful Life (RUL)
- 🧠 Battery Health Report

The project is validated on the **NASA Li-ion Battery Degradation Dataset** and demonstrates **282-cycle early warning before battery end-of-life**.

---

# 📷 Results

## Battery Health Dashboard

![Battery Dashboard](images/battery_health_dashboard.png)

---

## Pack Health Dashboard

![Pack Dashboard](images/pack_health_dashboard.png)

---

## Early Failure Warning

![Early Warning](images/early_warning.png)

---

## Future SoH Prediction

![Future SoH](images/future_soh_prediction.png)

---

## ROC Comparison

![ROC](images/roc_rf_vs_bilstm.png)

---

# 🏆 Performance Summary

| Task | Best Model | Performance |
|------|------------|------------|
| SoH Estimation | Random Forest + GPR | **R² = 0.808** |
| SoC Estimation | BiLSTM + Attention | **R² = 0.877** |
| Cell Failure Prediction | BiLSTM | **ROC-AUC = 0.967** |
| Physics Baseline | Extended Kalman Filter | **R² = 0.621** |

---

## 🚀 Key Achievement

✅ Early battery failure detected **282 cycles before actual End-of-Life** on NASA Battery **B0006**.

---

# ✨ Features

- Machine Learning Assisted Battery Management System
- State of Health (SoH) Prediction
- State of Charge (SoC) Estimation
- Cell Failure Prediction
- Remaining Useful Life Estimation
- Extended Kalman Filter Implementation
- Hybrid Physics + AI Framework
- 8-Cell Battery Pack Simulation
- Battery Health Report Generation
- Manufacturing Variation Simulation
- Gaussian Noise Injection
- Confidence Interval Estimation using Gaussian Process Regression

---

# 🧠 Project Architecture

```
NASA Battery Dataset
        │
        ▼
Data Cleaning
        │
        ▼
Feature Engineering
(19 Battery Features)
        │
        ▼
Battery-wise Train/Test Split
        │
        ├──────────────┐
        │              │
        ▼              ▼
SoH Models        SoC Models
(RF/XGB/LSTM)     (EKF/LSTM)
        │              │
        └──────┬───────┘
               ▼
8-Cell Battery Pack Simulation
               ▼
Cell Failure Prediction
               ▼
Battery Health Report
               ▼
Early Warning System
```

---

# 🤖 Machine Learning Models

## State of Health (SoH)

- Random Forest
- XGBoost
- Random Forest + Gaussian Process Regression
- BiLSTM + Attention

---

## State of Charge (SoC)

- Extended Kalman Filter
- BiLSTM + Attention

---

## Cell Failure Classification

- Random Forest
- Support Vector Machine
- Logistic Regression
- BiLSTM + Attention

---

# 📊 Model Comparison

| Model | Accuracy | F1 Score | ROC-AUC |
|--------|-----------|----------|---------|
| Random Forest | 82.6% | 0.892 | 0.890 |
| SVM | 82.0% | 0.887 | 0.882 |
| Logistic Regression | 81.6% | 0.886 | 0.891 |
| **BiLSTM + Attention** | **95.9%** | **0.979** | **0.967** |

---

# ⚙ Technical Highlights

- Battery-wise train/test split (No data leakage)
- Physics-informed feature engineering
- Extended Kalman Filter
- Gaussian Process Regression uncertainty estimation
- Resistance normalization
- Attention-based Deep Learning
- Synthetic battery degradation simulation
- Manufacturing variation modeling (±5%)

---

# 📂 Repository Structure

```
AI-Powered-BMS-Simulator
│
├── bms_models/
│
├── bms_outputs/
│   ├── plots/
│   ├── model_comparison.csv
│   ├── classifier_comparison.csv
│   └── pack_health_report.csv
│
├── images/
│
├── BMS_Simulator_NASA.ipynb
├── README.md
├── LICENSE
└── requirements.txt
```

---

# 📦 Installation

Clone the repository

```bash
git clone https://github.com/mridul1236/AI-Powered-BMS-Simulator.git
```

Move into the project

```bash
cd AI-Powered-BMS-Simulator
```

Install dependencies

```bash
pip install -r requirements.txt
```

Run

```bash
jupyter notebook
```

Open

```
BMS_Simulator_NASA.ipynb
```

Run all cells.

---

# 📁 Dataset

**NASA Li-ion Battery Degradation Dataset**

Batteries Used

- B0005
- B0006
- B0007
- B0018

Rows after preprocessing

```
1984
```

Synthetic samples

```
10000+
```

---

# 🛠 Technology Stack

- Python
- PyTorch
- Scikit-Learn
- XGBoost
- NumPy
- Pandas
- Matplotlib
- Joblib
- Jupyter Notebook

---

# 📈 Outputs

The simulator automatically generates

- Battery Health Dashboard
- Pack Health Dashboard
- Future SoH Prediction
- Early Failure Warning
- ROC Curves
- Model Comparison Tables
- Classifier Comparison
- Pack Health Report

---

# 🎯 Applications

- Electric Vehicles (EVs)
- Battery Analytics
- Battery Health Monitoring
- Battery Digital Twins
- Energy Storage Systems
- Predictive Maintenance
- Smart Battery Packs
- Embedded Battery Management Systems

---

# 📚 References

1. NASA Ames Prognostics Center Battery Dataset
2. Plett, G.L., Extended Kalman Filtering for Battery Management Systems
3. Hu et al., Equivalent Circuit Modeling of Lithium-Ion Batteries
4. Zhao et al., State of Health Estimation Methods
5. Park et al., LSTM-Based Battery Remaining Useful Life Prediction

---

# 👨‍💻 Author

**Mridul Mahajan**

Electronics & Communication Engineering

Thapar Institute of Engineering and Technology

Interested in

- Battery Management Systems
- Machine Learning
- Electric Vehicles
- Embedded Systems
- Digital Electronics

---

# ⭐ Support

If you found this project useful,

⭐ Star this repository.

It helps the project reach more people.

---

# 📜 License

This project is licensed under the **MIT License**.
