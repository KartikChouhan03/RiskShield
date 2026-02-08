RiskShield – Fraud Risk Scoring System

Overview

RiskShield is a machine learning–based fraud risk scoring system designed to identify suspicious credit card transactions and support informed decision-making.
Instead of making a binary fraud / not fraud decision, the system assigns a risk score and categorizes transactions into LOW, MEDIUM, or HIGH risk.

This project focuses on real-world ML challenges such as extreme class imbalance, cost-sensitive decisions, and deployment consistency.

🎯 Problem Statement

Credit card fraud is a rare but highly costly event.
Traditional rule-based systems often fail to detect evolving fraud patterns or generate excessive false positives.

The challenge is to:

Detect fraudulent transactions early

Minimize inconvenience to genuine users

Provide explainable and risk-aware decisions

🧠 Solution Approach

RiskShield models fraud detection as a risk assessment problem, not a pure classification task.

The system:

Learns patterns from historical transaction data

Outputs a fraud probability score

Converts probability into risk categories

Maps risk levels to system actions

This mirrors how real financial systems operate.

📂 Dataset

Source: Credit Card Fraud Detection Dataset (European cardholders)

Transactions: 284,807

Fraud Cases: 492 (≈ 0.17%)

Features:

Time (seconds since first transaction)

V1–V28 (PCA-transformed anonymized features)

Amount

Target: Class (1 = Fraud, 0 = Genuine)

The extreme imbalance reflects real-world fraud scenarios and makes accuracy an unreliable metric.

🏗️ System Architecture
Transaction Data
↓
Preprocessing & Scaling
↓
Machine Learning Model
↓
Fraud Risk Score (0–1)
↓
Risk Categorization
↓
Decision Logic

🧪 Machine Learning Pipeline

1. Data Preprocessing

Stratified train–test split

Feature scaling using StandardScaler

No synthetic oversampling (to avoid data leakage)

2. Models Evaluated

Logistic Regression (baseline)

Logistic Regression (class-weighted)

Random Forest

Gradient Boosting

Isolation Forest (unsupervised anomaly detection)

3. Final Model Selection

Balanced Logistic Regression was chosen due to:

Strong ROC-AUC performance

Stability on PCA-transformed data

High interpretability

Suitability for risk-based decisions

📊 Evaluation Metrics

Due to class imbalance, accuracy is misleading.
The project emphasizes:

Recall (Fraud class)

Precision

ROC-AUC

Confusion Matrix

The goal is to reduce fraud loss while controlling false positives.

⚖️ Risk Scoring Logic
Risk Score Risk Level System Decision
< 0.20 LOW Allow
0.20 – 0.70 MEDIUM Require Verification

> 0.70 HIGH Flag for Review

This allows graduated responses instead of hard rejections.

🔍 Explainability

Logistic Regression coefficients provide global interpretability

SHAP values explain individual transaction decisions

Each flagged transaction can be justified to analysts

🖥️ User Interface

A lightweight Streamlit UI demonstrates the fraud decision engine.

Features:

Demo mode with pre-filled internal features

Manual input for advanced users

Displays:

Fraud risk score

Risk level

Recommended system action

Since the dataset uses PCA-based anonymized features, the UI represents internal transaction signals, not raw card details.

📁 Project Structure
RiskShield/
├── app.py # Streamlit UI
├── src/
│ ├── preprocess.py # Data loading & scaling
│ ├── train.py # Model training & saving
│ ├── evaluate.py # Evaluation utilities
│ └── risk_logic.py # Risk & decision logic
├── data/
│ └── raw/creditcard.csv
├── results/
│ ├── final_model.pkl
│ └── scaler.pkl
├── notebooks/ # EDA & experimentation
├── requirements.txt
└── README.md

How to Run

1. Install dependencies
   pip install -r requirements.txt

2. Train the model
   python run_pipeline.py

3. Launch the UI
   streamlit run app.py

⚠️ Limitations

Fraud patterns evolve over time (concept drift)

Performance depends on historical data quality

False positives may inconvenience users

Periodic retraining is required in production systems

🚀 Future Improvements

Adaptive threshold tuning

Cost-based optimization

Real-time streaming integration

Model retraining pipeline

Dashboard for analysts

🏁 Conclusion

RiskShield demonstrates how machine learning can be applied responsibly to fraud detection by combining:

Statistical learning

Risk-aware decision logic

Explainability

Deployment consistency

It reflects industry-relevant ML practices, not just model training.

👤 Author

Kartik
