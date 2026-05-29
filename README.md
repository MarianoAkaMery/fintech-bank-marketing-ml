# Bank Marketing Subscription Prediction - FinTech Project

**Author:** Salvatore Mariano Librici  
**Email:** salvatoremariano.librici@mail.polimi.it

## Overview

This repository contains the final project for the **FinTech** course at Politecnico di Milano.

The objective is to predict whether a bank client will subscribe to a term deposit based on historical data from direct marketing campaigns conducted by a Portuguese banking institution.

The problem is framed as a **binary classification task**, where the target variable is:

- `yes`: the client subscribed to the term deposit;
- `no`: the client did not subscribe to the term deposit.

The project follows a complete machine learning workflow: exploratory data analysis, preprocessing, model training, model comparison, feature selection, threshold analysis, and interpretability.

---

## Files for Evaluation

The main notebook for evaluation is:

```text
Salvatore_Librici_FINTECH_Bank_Marketing_Submit.ipynb
```

An HTML export is also provided for easier reading without running the notebook:

```text
Salvatore_Librici_FINTECH_Bank_Marketing_Submit.html
```

---

## Repository Structure

```text
.
|-- README.md
|-- Salvatore_Librici_FINTECH_Bank_Marketing_Submit.ipynb
|-- Salvatore_Librici_FINTECH_Bank_Marketing_Submit.html
`-- content/
    `-- Dataset4.csv
```

---

## Assignment Compliance

| Requirement | Implementation in this project |
|---|---|
| Create two different ML algorithms to compute the probability that a client will subscribe to a term deposit | Logistic Regression and Random Forest Classifier are trained and evaluated using predicted probabilities. |
| Compare the algorithms | Models are compared on validation data using accuracy, balanced accuracy, precision, recall, F1-score, ROC-AUC and PR-AUC. |
| Propose a strategy to decrease the number of features | Random Forest feature importance is aggregated at original-variable level and used to select the top predictors. |
| Study the impact of feature selection on predictions | The selected-feature Random Forest is retrained and compared with the full-feature Random Forest on validation and test data. |
| Provide interpretability results for the preferred algorithm | Feature importance, permutation importance and SHAP explanations are provided for the preferred Random Forest model. |
| Explain why the preferred model was selected | Random Forest is selected because it achieves the strongest validation ROC-AUC and PR-AUC among the compared models, while also providing better precision than Logistic Regression. |

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

## Main Results

The Random Forest model provides the strongest validation ROC-AUC and PR-AUC among the compared models. This makes it the preferred model, since the task is not only to classify clients but also to estimate and rank subscription probabilities.

Feature selection shows that a reduced set of important variables can preserve a similar level of predictive performance. This improves interpretability and supports a more compact model specification.

Permutation importance and SHAP analysis identify the main drivers of subscription probability. Variables such as `duration`, `month`, `contact`, `housing`, and `poutcome` are among the most relevant predictors.

---

## Business Interpretation

The model can support the bank in improving marketing campaign efficiency by ranking clients according to their estimated probability of subscription.

This allows the bank to:

- prioritize high-probability clients;
- reduce unnecessary contacts;
- improve allocation of call-center resources;
- design more targeted marketing strategies;
- better understand the drivers of client subscription behavior.

The variable `duration` should be interpreted carefully because it is only known after the phone call starts. For a real pre-campaign targeting strategy, the model without `duration` is more realistic.

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

If execution is not required, open the HTML export:

```text
Salvatore_Librici_FINTECH_Bank_Marketing_Submit.html
```

---

## Author

**Salvatore Mariano Librici**  
salvatoremariano.librici@mail.polimi.it  
Politecnico di Milano  
FinTech Course - 2025/2026

---

## Disclaimer

This project was developed for academic purposes as part of the FinTech course. The results should be interpreted as an educational application of machine learning techniques to a marketing classification problem.

