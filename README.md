# Urban Traffic Flow Prediction

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-Gradient%20Boosting-189FDD)](https://xgboost.readthedocs.io/)
[![CRISP-DM](https://img.shields.io/badge/Methodology-CRISP--DM-5B2C6F)](https://www.ibm.com/docs/en/spss-modeler/saas?topic=dm-crisp-help-overview)

## Project Overview

This project predicts traffic-flow congestion levels in **Porto** using supervised multiclass classification. It uses real-world traffic-sensor and meteorological data collected between July 2018 and October 2019, with 6,812 observations.

The project was developed for the **Data and Machine Learning (DAA)** course in the **Master's in Artificial Intelligence at the University of Minho (UMinho)** and received a final grade of **16/20**. The target variable, `AVERAGE_SPEED_DIFF`, is mapped to five ordinal classes: `None`, `Low`, `Medium`, `High`, and `Very_High`.

## Key Features and Pipeline

- **CRISP-DM workflow:** business understanding, data understanding, preparation, modeling, evaluation, and deployment-oriented conclusions.
- **Data quality:** removed `AVERAGE_RAIN` due to over 90% missing values, along with constant or non-informative features.
- **Feature engineering:** normalized cloudiness categories, encoded luminosity, and decomposed `record_date` into year, month, day, hour, weekday, and `is_weekend`.
- **Leakage-safe preprocessing:** applied consistent train/test transformations to avoid dimensionality mismatches and inconsistent encodings.
- **Model selection:** benchmarked eight classifiers and selected XGBoost after systematic five-fold `GridSearchCV` tuning.
- **Primary signal:** `AVERAGE_TIME_DIFF` was identified as the most predictive feature.

## Results Summary

| Metric | Result |
|---|---:|
| Test accuracy | **81.41%** |
| Macro F1-score | **0.81** |
| Weighted F1-score | **0.81** |

Final XGBoost configuration:

```text
max_depth=5
learning_rate=0.05
n_estimators=200
subsample=0.8
colsample_bytree=0.7
```

The model performs particularly well on the extreme classes (`None` and `Very_High`). Most errors occur between neighboring congestion levels, especially `None`/`Low`, where class boundaries are naturally less distinct.

## Repository Structure

```text
traffic-flow-prediction-ml/
├── ProjetoDAA_2.ipynb        # Analysis, preprocessing, training and evaluation
├── training_data.csv         # Training dataset
├── test_data.csv             # Test dataset
├── Relatório_DAA_grupo48.pdf # Academic project report
├── README.md
└── requirements.txt
```

## Quick Start

### PowerShell

```powershell
py -3.10 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab .\ProjetoDAA_2.ipynb
```

### Bash

```bash
python3.10 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
jupyter lab ProjetoDAA_2.ipynb
```

The required `training_data.csv` and `test_data.csv` files are included in the repository. Running the notebook generates the model outputs and `submission.csv`.

## Authorship

Academic project developed for the DAA course unit of the **Master's in Artificial Intelligence, University of Minho**.

**Final grade:** 16/20
