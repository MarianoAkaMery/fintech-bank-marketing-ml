# Bank Marketing Subscription Prediction - FinTech Project

## Overview

This repository contains the final project for the **FinTech** course at Politecnico di Milano.

The objective is to predict whether a bank client will subscribe to a term deposit based on historical data from direct marketing campaigns conducted by a Portuguese banking institution.

The problem is framed as a **binary classification task**, where the target variable is:

- `yes`: the client subscribed to the term deposit
- `no`: the client did not subscribe to the term deposit

The project follows a complete machine learning workflow: exploratory data analysis, preprocessing, model training, model comparison, feature selection, threshold analysis, and interpretability.

---

## Repository Structure

```text
.
|-- README.md
|-- Salvatore_Librici_FINTECH_Bank_Marketing_Submit.ipynb
|-- Salvatore_Librici_FINTECH_Bank_Marketing_Study.ipynb
`-- content/
    `-- Dataset4.csv
```

The `Submit` notebook is the clean version intended for evaluation.  
The `Study` notebook is a more commented version used for studying and preparing the presentation.

---

## Project Goals

The assignment requires the following tasks:

1. Build two different machine learning algorithms to estimate the probability that a client subscribes to a term deposit.
2. Compare the predictive performance of the models.
3. Propose a feature selection strategy and evaluate its impact on predictions.
4. Provide interpretability results for the preferred model and explain why it was selected.

---

## Dataset

The dataset contains information related to direct marketing campaigns of a Portuguese banking institution. The campaigns were based on phone calls, and in some cases multiple contacts were required for the same client.

The input variables include:

- demographic and financial information, such as age, job, marital status, education, balance, housing loan, and personal loan;
- information related to the current campaign, such as contact type, month, day, duration, and number of contacts;
- previous campaign information, such as previous contacts and previous campaign outcome.

The target variable is `y`, indicating whether the client subscribed to the term deposit.

---

## Methodology

### 1. Exploratory Data Analysis

The notebook starts with data loading, data quality checks, target distribution analysis, numerical and categorical feature analysis, business-oriented visualizations, and correlation analysis.

The target variable is imbalanced, with many more non-subscribers than subscribers. For this reason, accuracy alone is not sufficient to evaluate model quality.

### 2. Preprocessing

The preprocessing workflow includes:

- target encoding;
- stratified train-validation-test split;
- scaling of numerical variables for Logistic Regression;
- one-hot encoding of categorical variables;
- separate preprocessing pipelines for Logistic Regression and Random Forest.

### 3. Models

Two main models are compared:

- **Logistic Regression**, used as an interpretable benchmark for binary classification;
- **Random Forest Classifier**, used to capture nonlinear effects and interactions between variables.

A baseline model is also included to show why accuracy alone can be misleading with an imbalanced target.

### 4. Model Evaluation

The models are evaluated using:

- Accuracy
- Balanced Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC
- Confusion Matrix

Because the dataset is imbalanced, particular attention is given to balanced accuracy, recall, precision, F1-score, ROC-AUC and PR-AUC.

### 5. Threshold Analysis

The default classification threshold of 0.50 is compared with alternative thresholds.

This is relevant from a business perspective because the bank may prefer different trade-offs between contacting more potential subscribers and reducing unnecessary calls.

### 6. Feature Selection and Importance

Feature importance is studied using:

- Random Forest feature importance;
- aggregated feature importance by original variable;
- permutation importance.

A reduced-feature model is then trained to evaluate whether a smaller set of predictors can preserve most of the predictive performance.

### 7. Interpretability

The preferred model is interpreted using global and local interpretability tools, including SHAP values. The analysis focuses on understanding which variables drive the predicted probability of subscription.

Special attention is given to `duration`, since it is highly predictive but only known after the call takes place. For this reason, the notebook also includes a robustness check without `duration`.

---

## Main Findings

The Random Forest model is expected to provide stronger overall predictive performance than Logistic Regression because it can capture nonlinear relationships and interactions among customer, campaign, and previous-contact variables.

The threshold analysis shows that the optimal operational threshold depends on the bank's business objective. A lower threshold increases recall and contacts more clients, while a higher threshold increases precision and focuses on fewer clients.

The interpretability analysis helps identify the main drivers of subscription probability and supports the business explanation of the selected model.

---

## Business Interpretation

The model can support the bank in improving marketing campaign efficiency by ranking clients according to their estimated probability of subscription.

This allows the bank to:

- prioritize high-probability clients;
- reduce unnecessary contacts;
- improve allocation of call-center resources;
- design more targeted marketing strategies;
- better understand the drivers of client subscription behavior.

---

## Technologies Used

- Python
- Google Colab / Jupyter Notebook
- pandas
- NumPy
- matplotlib
- seaborn
- scikit-learn
- SHAP

---

## How to Run

1. Open `Salvatore_Librici_FINTECH_Bank_Marketing_Submit.ipynb` in Google Colab or Jupyter Notebook.
2. Make sure `content/Dataset4.csv` is available in the repository.
3. Run all cells sequentially.

---

## Author

**Salvatore Mariano Librici**  
Politecnico di Milano  
FinTech Course - 2025/2026

---

## Disclaimer

This project was developed for academic purposes as part of the FinTech course. The results should be interpreted as an educational application of machine learning techniques to a marketing classification problem.
