# Fraud Detection

A machine learning proof-of-concept for detecting fraudulent credit card transactions using Random Forest on a heavily imbalanced real-world dataset.

## Results

| Metric | Score |
|---|---|
| Precision (fraud) | 91% |
| Recall (fraud) | 79% |
| F1 Score (fraud) | 84% |
| False alarms | 10 out of 85,308 normal transactions |
| Fraud caught | 106 out of 135 fraud cases |

> Standard accuracy reported 99.96% — but this metric is misleading on imbalanced data. This project uses **precision and recall** as the primary evaluation metrics.

## Why This Problem Is Challenging

- Only **0.17% of 284,807 transactions** are fraudulent (492 fraud cases total)
- A naive model that predicts everything as "normal" still gets 99.8% accuracy — but catches **zero fraud**
- Missing real fraud is far more costly than a false alarm
- Solution: evaluated using recall as the primary metric and applied `class_weight='balanced'` to handle the imbalance

## Dataset

- **Source:** [Kaggle — Credit Card Fraud Detection](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Size:** 284,807 transactions over 2 days
- **Fraud rate:** 492 cases (0.17%)
- **Features:** V1–V28 are PCA-transformed for user privacy, plus `Amount` and `Time`
- **Target:** `Class` — 0 for normal, 1 for fraud

## Project Overview

This repository contains a Jupyter notebook used to explore the dataset, train a Random Forest classifier, and evaluate it using fraud-appropriate metrics.

Key decisions made in this project:

- Dropped the `Time` column — does not contribute to fraud pattern detection
- Used `stratify=y` in train/test split to preserve the fraud ratio in both sets
- Used `class_weight='balanced'` to prevent the model from ignoring the minority fraud class
- Evaluated with classification report and confusion matrix instead of raw accuracy
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
- Separating features and target, dropping `Time`
- Splitting data into 70% train / 30% test
- Training a Random Forest classifier
- Evaluating with precision, recall, F1, and confusion matrix
- Visualizing the top 15 most important features
- Saving the trained model to `FraudDetectionModel.pkl`

## Notes

- The dataset and trained model are excluded from version control via `.gitignore`
- All 29 features (V1–V28 + Amount) were used; `Time` was dropped as it does not contribute to fraud patterns
- No feature scaling was applied — Random Forest uses threshold-based comparisons, not distance calculations, so scaling has no effect on results
