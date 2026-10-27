# Prediction of Agriculture Crop Production in India

**Domain:** Machine Learning / Data Science — Agriculture  
**Internship:** upskill Campus / The IoT Academy / UniConverge Technologies (UCT)  
**Student:** Pochampally Akshara

## Overview
This project explores Indian crop-production data and develops a machine-learning workflow for estimating crop production from available agricultural attributes. The supplied weekly reports document data cleaning, exploratory analysis, feature engineering, baseline regression, model tuning, feature-importance analysis and model persistence.

## Objectives
- Prepare a consistent, analysis-ready crop-production dataset.
- Explore production patterns by state, crop, season and year where those columns exist.
- Build a reproducible preprocessing and regression pipeline.
- Compare models using MAE, RMSE and R².
- Save a trained pipeline for later prediction and interpretation.

## Technologies
Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, joblib; XGBoost was also reported as part of the tuning work in the weekly reports.

## Repository structure
```text
.
├── data/
│   └── README.md
├── docs/
│   └── figures/
│       ├── workflow.png
│       ├── architecture.png
│       └── model_comparison.png
├── reports/
├── src/
│   ├── train_model.py
│   └── predict.py
├── requirements.txt
└── README.md
```

## Dataset
The weekly reports describe Indian agriculture crop-production data (2001–2014), sourced from data.gov.in, with fields including Crop, Variety, State, Quantity, Production, Season, Unit, Cost and Recommended Zone. The CSV was not attached to the supplied reports. Download the appropriate dataset from its authorized source and place it at `data/crop_production.csv`. Check column names and units before running the model.

## Setup
```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

## Train and evaluate
```bash
python src/train_model.py --data data/crop_production.csv
```
The script reports test-split MAE, RMSE and R² and writes `artifacts/model_metrics.csv` plus a saved model. **Actual numerical results are generated from the dataset at runtime; no scores are claimed in this repository before execution.**

## Generate predictions
Create a CSV containing the same predictor columns used during training, then run:
```bash
python src/predict.py --input data/new_crop_inputs.csv --output predictions.csv
```

## Methodology
1. Load CSV and standardize column names.
2. Remove duplicate records and rows with missing target production.
3. Parse common numeric fields and inspect units.
4. Split data into training and test sets.
5. Fit imputers, numeric scaling and categorical encoding within the pipeline to reduce leakage risk.
6. Train baseline regression models and compare MAE, RMSE and R².
7. Save the selected model and use it for predictions.

## Reported progress from weekly reports
- Data cleaning: missing-value handling, standardization of state/crop names and exploratory plots.
- Feature engineering: yield/cost/season features were explored; target encoding was considered, with leakage risk identified.
- Models: Linear Regression, Decision Tree and Random Forest were trained; XGBoost tuning was also reported.
- Model selection: the weekly report states that a tuned ensemble had the lowest RMSE and highest R² among models tried, and that log transformation improved errors on skewed high-production records.
- Interpretation: feature-importance analysis identified State, Crop and Season as dominant predictors.
- Model performance numbers were not present in the supplied reports, so this README does not invent them.

## Limitations and responsible use
- Crop production depends on weather, soil, irrigation, pests, prices, policy and measurement practices that may not be represented in the dataset.
- Units must be checked carefully; quantity, production and area/yield fields may not be directly comparable.
- Historical relationships may not generalize to new years or regions.
- Use predictions as analytical support, not as a substitute for agronomic expertise or official statistics.

## Future work
- Add weather, soil, rainfall, irrigation and market features when reliable data is available.
- Validate on a time-based holdout and test generalization across states/crops.
- Add robust unit normalization and data-quality checks.
- Build a simple dashboard for exploratory analysis and predictions.
- Record model versions, data provenance and reproducible evaluation results.

## References
1. data.gov.in — dataset source described in the weekly progress reports; use the exact dataset page and access date in the final report.
2. scikit-learn documentation — https://scikit-learn.org/stable/
3. Pandas documentation — https://pandas.pydata.org/docs/
4. Matplotlib documentation — https://matplotlib.org/stable/
