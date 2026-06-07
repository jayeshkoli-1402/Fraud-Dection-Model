# Fraud Dection

A fraud detection proof-of-concept using a credit card transaction dataset and a machine learning model.

## Project Overview

This repository contains a Jupyter notebook used to train and evaluate a fraud detection model on credit card transaction data.

## Results

| Metric         | Score  |
|----------------|--------|
| Precision      | 96%    |
| Recall         | 80%    |
| F1 Score       | 87%    |
| False Alarms   | 3 out of 56,864 normal transactions |
| Fraud Caught   | 78 out of 98 fraud cases |

### Key Challenge
Only 0.17% of 284,807 transactions were fraudulent.
Standard accuracy metric gives 99.8% by predicting
everything as normal — catching zero fraud.
This project uses precision and recall instead.

## Files

- `Train_Model.ipynb` - Main notebook for exploring the dataset, training the model, and evaluating performance.
- `creditcard.csv` - Dataset containing credit card transaction records. This file is intentionally excluded from version control.
- `FraudDetectionModel.pkl` - Serialized trained model artifact. This file is also excluded from version control.
- `requirements.txt` - Python package dependencies for reproducing the analysis.
- `.gitignore` - Git ignore rules for local environments and generated files.

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
python -m pip install -r requirements.txt
```

## Usage

Open and run `Train_Model.ipynb` in Jupyter Notebook or JupyterLab.

The notebook covers:

- loading and inspecting the credit card dataset
- preprocessing data
- training a machine learning model
- evaluating model metrics for fraud detection
- persisting the model to `FraudDetectionModel.pkl`

## Notes

- The dataset and trained model artifact are excluded from version control in `.gitignore`.
- If you want to reproduce the work, make sure to place `creditcard.csv` in the project root before running the notebook.
- The notebook is the primary interface for this project.
