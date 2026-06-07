# Fraud Detection

A machine learning proof-of-concept for detecting fraudulent credit card transactions using Random Forest on a heavily imbalanced real-world dataset.

## Results

| Metric | Score |
|---|---|
| Precision (fraud) | 96% |
| Recall (fraud) | 80% |
| F1 Score (fraud) | 87% |
| False alarms | 3 out of 56,864 normal transactions |
| Fraud caught | 78 out of 98 fraud cases |

> Standard accuracy reported 99.94% — but this metric is misleading on imbalanced data. This project uses **precision and recall** as the real evaluation metrics.

## Why This Problem Is Challenging

- Only **0.17% of 284,807 transactions** are fraudulent (492 fraud cases total)
- A model that predicts everything as "normal" still gets 99.8% accuracy — but catches **zero fraud**
- Missing real fraud is far more costly than a false alarm
- Solution: used `class_weight='balanced'` and evaluated using recall as the primary metric

## Dataset

- **Source:** [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions over 2 days
- **Fraud rate:** 492 cases (0.17%)
- **Features:** V1–V28 are PCA-transformed for user privacy, plus `Amount` and `Time`
- **Target:** `Class` — 0 for normal, 1 for fraud

## Project Overview

This repository contains a Jupyter notebook used to explore the dataset, train a Random Forest classifier, and evaluate it with fraud-appropriate metrics.

Key decisions made in this project:

- Dropped the `Time` column — not useful for fraud pattern detection
- Used `stratify=y` in train/test split to preserve fraud ratio in both sets
- Used `class_weight='balanced'` to handle extreme class imbalance
- Evaluated using classification report and confusion matrix instead of accuracy
- Visualized top 15 most important features to understand what the model learned
- Saved the trained model with `joblib` for future deployment

## Files

- `Train_Model.ipynb` — Main notebook: data exploration, model training, evaluation, and feature importance
- `creditcard.csv` — Credit card transaction dataset (excluded from version control)
- `FraudDetectionModel.pkl` — Serialized trained model artifact (excluded from version control)
- `requirements.txt` — Python package dependencies
- `.gitignore` — Git ignore rules for local environments and generated files

## Setup

1. Create a Python virtual environment.

```bash
python -m venv .venv
```

2. Activate the environment.

- On Windows:
  ```bash
  .venv\Scripts\activate
  ```
- On macOS/Linux:
  ```bash
  source .venv/bin/activate
  ```

3. Install dependencies.

```bash
pip install -r requirements.txt
```

## Usage

Download `creditcard.csv` from [Kaggle](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud) and place it in the project root, then open and run `Train_Model.ipynb` in Jupyter Notebook or JupyterLab.

The notebook covers:

- Loading and inspecting the dataset
- Checking for missing values and class distribution
- Splitting data with stratification
- Training a Random Forest with balanced class weights
- Evaluating with precision, recall, F1, and confusion matrix
- Visualizing the top 15 most important features
- Saving the trained model to `FraudDetectionModel.pkl`

## Notes

- The dataset and trained model are excluded from version control via `.gitignore`
- All 30 features (V1–V28 + Amount) were used; `Time` was dropped as it does not contribute to fraud patterns
- No feature scaling was applied — Random Forest uses threshold-based splits, not distance calculations, so scaling has no effect
