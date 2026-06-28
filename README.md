---
title: Fraud Detection Platform
emoji: 🛡️
colorFrom: blue
colorTo: indigo
sdk: docker
app_file: app.py
pinned: false
---

# Fraud Detection Platform

A Flask-based web application for credit card fraud detection using multiple machine learning models with a case workflow management system.

## Features

- Upload and validate the Kaggle Credit Card Fraud Detection dataset
- Preprocess data with scaling and SMOTE (applied only on training data)
- Train and compare 4 models: Logistic Regression, Random Forest, XGBoost, Neural Network
- Evaluate models: Accuracy, Precision, Recall, F1-score, ROC-AUC, Confusion Matrix
- Interactive dashboard with Plotly charts
- Full fraud case workflow: create, assign, escalate, resolve cases
- Audit trail for all case changes

## Quick Start

### 1. Create virtual environment

```bash
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Linux/Mac
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the application

```bash
python app.py
```

Then open [http://localhost:5000](http://localhost:5000).

### 4. Workflow

1. **Upload** — Go to `/upload` and upload `creditcard.csv`
2. **Train** — Go to `/train` and click "Train All Models"
3. **Results** — View model comparison at `/results`
4. **Dashboard** — Monitor case statistics at `/dashboard`
5. **Cases** — Manage fraud cases at `/cases`

## Project Structure

```
fraud-detection-platform/
├── app.py                  # Flask application factory + routes
├── config.py               # Configuration
├── requirements.txt
├── data/
│   ├── raw/                # Place creditcard.csv here
│   └── processed/          # Preprocessed data outputs
├── src/
│   ├── database.py         # SQLAlchemy models
│   ├── preprocessing.py    # Data loading, scaling, SMOTE
│   ├── train_models.py     # Train LR, RF, XGB, NN
│   ├── evaluate_models.py  # Metrics + comparison
│   ├── predict.py          # Inference + risk level
│   ├── model_utils.py      # Load/check saved models
│   ├── case_manager.py     # Case CRUD + audit log
│   └── dashboard_utils.py  # Plotly chart generators
├── templates/              # Jinja2 HTML templates
├── static/                 # CSS, JS, images
├── models/                 # Saved .pkl / .h5 model files
├── instance/               # SQLite database
└── tests/                  # pytest test suite
```

## Dataset

Download `creditcard.csv` from [Kaggle](https://www.kaggle.com/mlg-ulb/creditcardfraud) and place it in `data/raw/`.

Expected columns: `Time`, `V1`–`V28`, `Amount`, `Class` (0=legitimate, 1=fraud).

## Running Tests

```bash
pytest tests/ -v
```

## Case Workflow

| Status | Description |
|--------|-------------|
| New | Newly created case |
| In Review | Under investigation |
| Escalated | Escalated to senior analyst |
| Resolved | Investigation complete |
| Closed | Case closed |

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/cases` | List all fraud cases |
| POST | `/api/predict` | Predict fraud for transaction features |
| GET | `/api/dashboard/stats` | Dashboard statistics JSON |
