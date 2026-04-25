# Bank Marketing Subscription Prediction – FinTech Project

## Overview

This repository contains the final project for the **FinTech** course at Politecnico di Milano.

The objective of the project is to predict whether a bank client will subscribe to a term deposit based on historical data from direct marketing campaigns conducted by a Portuguese banking institution.

The problem is framed as a **binary classification task**, where the target variable is:

- `yes`: the client subscribed to the term deposit
- `no`: the client did not subscribe to the term deposit

The project follows a complete machine learning workflow, including exploratory data analysis, preprocessing, model training, model comparison, feature selection, threshold analysis, and interpretability.

---

## Repository Structure

```text
.
├── Dataset4.csv
├── FINTECH_Project_Bank_Marketing_Salvatore_Librici.ipynb
├── README.md
└── presentation/
    └── final_presentation.pptx
```

> Note: the presentation file may be added after completing the final PowerPoint deliverable.

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

- client demographic and financial information, such as age, job, marital status, education, balance, housing loan, and personal loan;
- information related to the current campaign, such as contact type, month, day, duration, and number of contacts;
- previous campaign information, such as previous contacts and previous campaign outcome.

The target variable is `y`, indicating whether the client subscribed to the term deposit.

---

## Methodology

### 1. Exploratory Data Analysis

The notebook begins with a detailed exploratory analysis, including:

- dataset shape and variable types;
- missing values and duplicate checks;
- target distribution analysis;
- numerical feature distributions;
- categorical feature analysis;
- subscription rates by job, month, contact type, and previous campaign outcome;
- correlation analysis among numerical variables.

The target variable is imbalanced, with a significantly larger number of clients not subscribing to the term deposit. For this reason, accuracy alone is not sufficient to evaluate model quality.

---

### 2. Preprocessing

The preprocessing pipeline includes:

- separation of numerical and categorical variables;
- one-hot encoding for categorical variables;
- scaling of numerical variables when required;
- stratified train-validation-test splitting to preserve the target distribution.

---

### 3. Models

Two main models are compared:

#### Logistic Regression

Logistic Regression is used as an interpretable baseline model. It is useful for understanding the linear relationship between predictors and the probability of subscription.

#### Random Forest Classifier

Random Forest is used as a more flexible nonlinear model. It is able to capture interactions among variables and more complex customer behavior patterns.

---

### 4. Model Evaluation

The models are evaluated using several classification metrics:

- Accuracy
- Balanced Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- PR-AUC
- Confusion Matrix

Because the dataset is imbalanced, particular attention is given to precision, recall, F1-score, ROC-AUC, and PR-AUC.

---

### 5. Threshold Analysis

The default classification threshold of 0.50 is compared with alternative thresholds.

This analysis is important from a business perspective because the bank may prefer different trade-offs between:

- contacting more potential subscribers;
- reducing unnecessary calls;
- improving campaign efficiency.

A lower threshold increases recall but also increases the number of contacted clients, while a higher threshold increases precision but misses more potential subscribers.

---

### 6. Feature Selection and Importance

Feature importance is studied using:

- Random Forest feature importance;
- aggregated feature importance by original variable;
- permutation importance.

The most relevant predictors include:

- call duration;
- month of contact;
- previous campaign outcome;
- contact type;
- balance;
- age.

Special attention is given to `duration`, since it is highly predictive but only known after the call takes place. This creates an important operational consideration when using the model for ex-ante campaign targeting.

---

### 7. Interpretability

The preferred model is interpreted through global and local interpretability tools. The analysis focuses on understanding which features drive the predicted probability of subscription and how they affect the model output.

Interpretability is essential in financial applications because model users must understand the drivers of predictions and the limitations of the model.

---

## Main Findings

The Random Forest model provides stronger overall predictive performance than Logistic Regression, especially in terms of ROC-AUC and PR-AUC.

The results suggest that customer subscription behavior is not purely linear and may depend on interactions between customer characteristics, campaign timing, previous campaign outcomes, and contact-related variables.

The threshold analysis shows that the optimal operational threshold depends on the bank's business objective. If the goal is to maximize the number of potential subscribers reached, a lower threshold may be preferable. If the goal is to reduce unnecessary calls, a higher threshold may be more appropriate.

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

1. Clone the repository:

```bash
git clone <repository-url>
```

2. Open the notebook in Google Colab or Jupyter Notebook.

3. Make sure `Dataset4.csv` is available in the expected path.

4. Run all cells sequentially.

---

## Author

**Salvatore Mariano Librici**  
Politecnico di Milano  
FinTech Course – 2025/2026

---

## Disclaimer

This project was developed for academic purposes as part of the FinTech course. The results should be interpreted as an educational application of machine learning techniques to a marketing classification problem.
"# fintech-bank-marketing-ml" 
