# Carbon-BiomassML
Machine learning for Biomass estimation using Rimba Raya carbon biomass data culminating in a stacked ensemble learning model.  

This repository presents a research project exploring stacked ensemble learning approaches for above-ground carbon biomass (AGC) estimation using soil and environmental variables.  
This work focuses on **soil composition, moisture, precipitation, and peatland extent** as predictive features — all derived from open-access Earth Engine datasets.

---

## Project Overview

- **Objective:** Estimate above-ground carbon (AGC) using ML models trained on soil and environmental datasets.
- **Target variable:** AGC (machine-learning-derived estimates of above-ground carbon)
- **Predictor variables:** Soil granularity (clay, silt, sand), peatland fraction, root zone soil moisture, precipitation, and elevation.
- **Tools:** Google Earth Engine for data extraction, Python for preprocessing, modeling, and analysis.

---

## 🌍 Data Sources

All predictor variables were sourced from **Google Earth Engine (GEE)** using publicly available global datasets:

| Feature | Description | Source |
|----------|--------------|--------|
| **Clay, Silt, Sand (%)** | Soil granularity fractions (0–5 cm depth) | [SoilGrids - ISRIC](https://soilgrids.org) (`projects/soilgrids-isric`) |
| **Peatland Fraction** | Percentage of area classified as peatland | [ML Global Peatland Extent Dataset](https://developers.google.com/earth-engine/datasets/catalog/projects_sat-io_open-datasets_ML-GLOBAL-PEATLAND-EXTENT) |
| **Elevation** | Digital elevation data (SRTM 90m) | [CGIAR/SRTM90_V4](https://developers.google.com/earth-engine/datasets/catalog/CGIAR_SRTM90_V4) |
| **Root Zone Soil Moisture** | Daily average soil moisture in the root zone | [NASA GLDAS CLSM V022](https://developers.google.com/earth-engine/datasets/catalog/NASA_GLDAS_V022_CLSM_G025_DA1D) |
| **Precipitation** | Daily rainfall totals | [CHIRPS Daily Precipitation](https://developers.google.com/earth-engine/datasets/catalog/UCSB-CHG_CHIRPS_DAILY) |

> All data were extracted at an **8 km spatial resolution** using a point-by-point sampling method for improved robustness across the study region.

---
## 🧩 Repository Structure

```
ml-biomass-estimation/
│
├── dissertation.ipynb           # Main notebook for data extraction, modeling, and results
│
├── data/                        # Folder for input and processed data
│   ├── raw/                     # Original data (e.g., CSVs, shapefiles, downloaded sources)
│   └── processed/               # Cleaned and merged datasets used for modeling
│
├── models/                      # Trained or saved ML models (optional)
│   ├── xgboost_model.pkl
│   └── random_forest_model.pkl
│
├── results/                     # Output figures, performance metrics, and visualizations
│   ├── feature_importance.png
│   ├── model_comparison.csv
│   └── agc_predictions_map.png
│
├── scripts/                     # Python scripts (if you later modularize your notebook)
│   ├── data_preprocessing.py
│   ├── model_training.py
│   └── evaluation.py
│
├── requirements.txt             # List of dependencies
├── LICENSE                      # MIT License or other
└── README.md                    # Project documentation (this file)
```

---

## ⚙️ Methodology Summary

1. **Data Acquisition**  
   Extraction of soil and hydrological features via Earth Engine APIs.
2. **Preprocessing**  
   Cleaning, normalization, and merging of static and temporal datasets into a unified training table.
3. **Modeling**  
   Evaluation of multiple regression models (Random Forest, XGBoost, SVR, Neural Network, Linear Regression) for AGC prediction.
4. **Validation**  
   Comparison using R², RMSE, MAE, and feature importance.

---

## 📊 Results Summary

Five machine learning models were tested for predicting Above-Ground Carbon (AGC):

| Model | Description | R² | RMSE | MAE |
|--------|--------------|----|------|------|
| **Random Forest Regressor** | Ensemble of decision trees; robust and interpretable | ~0.87 | Moderate | Low |
| **XGBoost Regressor** | Gradient-boosted trees; strong performance on tabular data | ~0.89 | Lowest | Lowest |
| **Support Vector Regressor (SVR)** | Kernel-based regression for nonlinear relationships | ~0.82 | Moderate | Moderate |
| **Linear Regression** | Baseline linear model | ~0.68 | High | High |
| **Neural Network (MLP)** | Multi-layer perceptron capturing nonlinear relationships | ~0.84 | Moderate | Moderate |

**Key Insights**
- **XGBoost** delivered the highest predictive performance (R² ≈ 0.89), but was severely overfitted.  
- **Soil and environmental variables alone** provided strong predictive capacity for AGC.  


---

## 🧾 Installation & Usage

```bash
# Clone this repository
git clone https://github.com/Harriet-101/Carbon-BiomassML.git

cd ml-biomass-estimation

# Install dependencies
pip install -r requirements.txt


