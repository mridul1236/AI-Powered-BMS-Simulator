# AI-Powered Battery Management System Simulator

> **282 cycles early warning before battery end-of-life — validated on NASA dataset**

A complete machine learning assisted Battery Management System (BMS) simulator 
built entirely in Python. No hardware required. Validated on the NASA Li-ion 
Battery Degradation Dataset (B0005, B0006, B0007, B0018).

---

## Results at a Glance

| Task | Model | R² | MAE |
|---|---|---|---|
| SoH Estimation | Random Forest + GPR | 0.808 | 0.010 |
| SoC Estimation | BiLSTM + Attention | 0.877 | 0.052 |
| Cell Failure (AUC) | BiLSTM Classifier | 0.967 | — |
| SoC Physics Baseline | Extended Kalman Filter | 0.621 | 0.111 |

**Key Result: Early failure warning triggered 282 cycles before actual 
end-of-life on NASA Battery B0006.**

---

## What This Project Does

This simulator replicates what a real BMS chip does inside an EV battery pack:

1. **Estimates State of Health (SoH)** — how much capacity the battery has left
2. **Estimates State of Charge (SoC)** — how full the battery is right now  
3. **Predicts cell failure** — which cell will fail and when
4. **Simulates an 8-cell pack** — with realistic manufacturing variation (±5%)
5. **Gives early warning** — flags failing cells before performance drops

---

## Project Architecture

```
NASA Dataset (B0005–B0018)
        ↓
ECM Parameter Fitting (Thevenin Model: R0, R1, C1)
        ↓
19-Feature Engineering (resistance, rolling stats, degradation trends)
        ↓
Battery-wise Train/Test Split (3 train / 1 test — no leakage)
        ↓
┌─────────────────────────────────────┐
│ SoH Models                          │
│ Random Forest → GPR Correction      │
│ XGBoost                             │  
│ BiLSTM + Attention                  │
└─────────────────────────────────────┘
        ↓
┌─────────────────────────────────────┐
│ SoC Models                          │
│ Extended Kalman Filter (physics)    │
│ BiLSTM + Attention (data-driven)    │
└─────────────────────────────────────┘
        ↓
8-Cell Pack Simulator (±5% variation)
        ↓
Cell Failure Classifier (RF + SVM + LR + BiLSTM)
        ↓
Early Warning Detection on Real NASA Data
        ↓
predict_pack_health() — Integrated BMS Report
```

---

## Models Implemented

### SoH Estimation
- **Random Forest** — R²=0.808, MAE=0.010
- **XGBoost** — R²=0.312
- **Hybrid RF + GPR** — R²=0.808 with 95% confidence intervals
- **BiLSTM + Attention** — sequence-based, MAE=0.027

### SoC Estimation  
- **Extended Kalman Filter** — physics-based, R²=0.621
- **BiLSTM + Attention** — data-driven, R²=0.877

### Cell Failure Classification
| Model | Accuracy | F1 | ROC-AUC |
|---|---|---|---|
| Random Forest | 0.826 | 0.892 | 0.890 |
| SVM (RBF) | 0.820 | 0.887 | 0.882 |
| Logistic Regression | 0.816 | 0.886 | 0.891 |
| **BiLSTM + Attention** | **0.959** | **0.979** | **0.967** |

---

## Key Design Decisions

- **No target leakage** — Capacity excluded from all ML inputs
- **Battery-wise split** — model tested on completely unseen battery
- **Resistance normalisation** — Re/Re_BOL removes manufacturing variation
- **GPR uncertainty** — 95% confidence intervals on every SoH prediction
- **Physics + ML hybrid** — ECM features feed into data-driven models
- **Noise injection** — Gaussian + drift + spike simulation during training

---

## Dataset

**NASA Li-ion Battery Degradation Dataset**  
Source: [Kaggle — mystifoe77/nasa-battery-data-cleaned](https://www.kaggle.com/datasets/mystifoe77/nasa-battery-data-cleaned)  
Batteries: B0005, B0006, B0007, B0018  
Rows after cleaning: 1,984  
Synthetic samples generated: 10,000 (failure classification)

---

## Installation & Running

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/AI-Powered-BMS-Simulator.git

# Install dependencies
pip install -r requirements.txt

# Open in Jupyter or Google Colab
# Run all cells top to bottom
```

**Recommended: Run on Google Colab** (free GPU available)  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_LINK)

---

## Repository Structure

```
AI-Powered-BMS-Simulator/
│
├── BMS_Simulator.ipynb          # Main notebook — run this
├── requirements.txt             # Python dependencies
├── README.md                    # This file
│
└── outputs/
    ├── plots/
    │   ├── soh_degradation.png
    │   ├── battery_health_dashboard.png
    │   ├── pack_health_dashboard.png
    │   ├── early_warning.png
    │   ├── classifier_roc.png
    │   ├── roc_rf_vs_bilstm.png
    │   ├── future_soh_prediction.png
    │   ├── rul_prediction.png
    │   └── pack_simulator.png
    ├── model_comparison.csv
    └── pack_health_report.csv
```

---

## Saved Models

| File | Size | Purpose |
|---|---|---|
| soh_rf.pkl | 4.7 MB | SoH Random Forest |
| soh_xgb.pkl | 483 KB | SoH XGBoost |
| soh_gpr_residual.pkl | 2.0 MB | GPR residual corrector |
| soh_bilstm_best.pt | 582 KB | SoH BiLSTM weights |
| soc_bilstm_best.pt | 562 KB | SoC BiLSTM weights |
| failure_rf_classifier.pkl | 4.6 MB | Failure classifier RF |
| failure_bilstm_best.pt | 552 KB | Failure BiLSTM weights |
| failure_scaler.pkl | 0.7 KB | Feature scaler |
| soh_scaler.pkl | 1.0 KB | SoH feature scaler |

---

## Technical Stack

```
Python 3.10+ | PyTorch | Scikit-learn | XGBoost
NumPy | Pandas | Matplotlib | Seaborn | Joblib
```

---

## Project Context

**B.Tech Final Year Project**  
Electronics and Communication Engineering  
Thapar Institute of Engineering and Technology  

Project Title: *Design and Implementation of a Machine Learning Assisted 
Battery Management System for Lithium-Ion Batteries using NASA Battery Dataset*

---

## References

1. Plett, G.L. (2004). Extended Kalman filtering for battery management systems. *Journal of Power Sources*
2. Saha, B. & Goebel, K. (2007). Battery Data Set. NASA Ames Prognostics Data Repository
3. Hu, X., Li, S. & Peng, H. (2012). A comparative study of equivalent circuit models. *Journal of Power Sources*
4. Zhao, R. et al. (2017). A review of Li-ion battery SoH estimation methods. *IEEE Trans. Transportation Electrification*
5. Park, S. et al. (2020). LSTM-based battery RUL prediction. *Applied Energy*
