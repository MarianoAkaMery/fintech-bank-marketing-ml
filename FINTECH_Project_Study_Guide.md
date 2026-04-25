# Study Guide — FINTECH Bank Marketing Project

This guide explains the notebook section by section. Use it to understand what each part does, why it is included, and how to explain it during a discussion or presentation.

---

## Recommended repository / file structure

```text
fintech-bank-marketing-ml/
├── FINTECH_Project_Bank_Marketing_Salvatore_Librici_Annotated.ipynb
├── Dataset4.csv
├── README.md
└── FINTECH_Project_Study_Guide.md
```

---

# 1. Big picture of the project

The business problem is a binary classification problem.

The bank wants to estimate the probability that a customer subscribes a term deposit after a marketing campaign.

The target variable is:

```text
y = yes  -> customer subscribed
y = no   -> customer did not subscribe
```

The machine learning task is therefore:

```text
customer and campaign variables -> probability of subscription
```

The final project logic is:

```text
Data understanding
→ Data preprocessing
→ Baseline model
→ Logistic Regression
→ Random Forest
→ Model comparison
→ Threshold analysis
→ Feature selection
→ Interpretability
→ Business conclusions
```

---

# 2. Notebook map

| Notebook cells | Section | What happens | Why it matters |
|---:|---|---|---|
| 0–2 | Title and Drive mounting | Project title, setup and optional Google Drive mount | Prepares the Colab environment |
| 3–4 | Colab setup | Defines paths and finds `Dataset4.csv` | Ensures the notebook can load the dataset |
| 5–6 | Import libraries | Imports pandas, plots, sklearn, SHAP | Provides all tools used later |
| 7–8 | Load dataset | Reads the CSV and displays first rows | Confirms data loaded correctly |
| 9–13 | Initial overview | Shape, column names, info, numerical/categorical summaries | First diagnostic view of the data |
| 14–19 | Data quality checks | Missing values, duplicates, categorical values | Verifies whether cleaning is needed |
| 20–24 | Target analysis | Counts and plots `yes` vs `no` | Shows class imbalance |
| 25–30 | Numerical analysis | Histograms, boxplots, skewness | Detects outliers and distributions |
| 31–35 | Numerical vs target | Boxplots and medians by target | Checks whether subscribers differ from non-subscribers |
| 36–41 | Categorical analysis | Category counts and subscription rates | Finds business patterns by job, month, contact, etc. |
| 42–44 | Cramér's V | Association between categorical variables and target | Measures categorical predictive relevance |
| 45–48 | Correlation | Numerical correlation heatmaps | Checks linear relationships and redundancy |
| 49–54 | Business EDA | Marketing-oriented plots | Converts EDA into business insights |
| 55–58 | Preprocessing | X/y split, train/val/test split, preprocessors | Prepares data for models without leakage |
| 59–60 | Evaluation functions | Defines reusable metric functions | Makes model evaluation consistent |
| 61–62 | Baseline model | Predicts most frequent class | Shows why accuracy alone is misleading |
| 63–65 | Logistic Regression | First real classifier | Interpretable benchmark |
| 66–68 | Random Forest | Nonlinear ensemble model | Captures interactions and nonlinear effects |
| 69–74 | Metric cheat sheet and comparison | ROC, PR curves, comparison table | Selects best model using several metrics |
| 75–77 | Hyperparameter tuning | GridSearchCV for RF | Improves Random Forest settings |
| 78–80 | Threshold analysis | Tests thresholds from 0.10 to 0.90 | Connects probability outputs to campaign strategy |
| 81–83 | Final test evaluation | Evaluates selected model on test set | Gives unbiased final estimate |
| 84–93 | Feature selection | Feature importance, Top-K selection, retraining | Reduces noise and improves interpretability |
| 94–96 | Permutation importance | Model-agnostic feature importance | Validates which original features matter |
| 97–101 | SHAP interpretability | Global and local explanations | Explains Random Forest predictions |
| 102–104 | Without duration | Robustness check excluding `duration` | Tests realistic pre-call targeting |
| 105–107 | Final conclusions | Saves results and writes business conclusions | Converts technical work into final message |

---

# 3. Section-by-section explanation

## Cells 7–13 — Load data and initial overview

### What you do
You load the dataset and inspect:

- number of rows and columns
- column names
- data types
- descriptive statistics

### Why you do it
Before training any model, you need to understand the raw data. This avoids training models blindly.

### What you should be able to say
> I first inspected the dataset structure, variable types and basic descriptive statistics to understand the available information before preprocessing and modeling.

---

## Cells 14–19 — Data quality checks

### What you do
You check:

- missing values
- duplicated rows
- categorical variable levels

### Why you do it
Missing values or duplicate rows can distort model training. Categorical variables also need to be understood before one-hot encoding.

### What you should be able to say
> The data quality check was used to verify whether imputation, duplicate removal or special cleaning steps were necessary.

---

## Cells 20–24 — Target variable analysis

### What you do
You count how many observations are `yes` and how many are `no`.

### Why you do it
The dataset is imbalanced: most customers do not subscribe. This has a direct impact on model evaluation.

### Important idea
A model that always predicts `no` can have high accuracy, but it is useless because it never finds subscribers.

### What you should be able to say
> Since the positive class is relatively rare, accuracy alone is not sufficient. For this reason, I also used precision, recall, F1-score, ROC-AUC and PR-AUC.

---

## Cells 25–35 — Numerical variables

### What you do
You plot and compare numerical variables such as:

- `age`
- `balance`
- `duration`
- `campaign`
- `pdays`
- `previous`

### Why you do it
You want to see skewness, outliers and possible relationships with the target.

### Important note on `duration`
`duration` is usually very predictive, but it is known only after the phone call. This means it is useful for explaining subscription behavior, but it may be less useful if the bank wants to choose who to call before making the call.

### What you should be able to say
> Numerical EDA showed that some variables are highly skewed and that duration is likely very predictive, although it has an operational limitation because it is observed after the call begins.

---

## Cells 36–54 — Categorical and business EDA

### What you do
You analyze variables such as:

- `job`
- `marital`
- `education`
- `contact`
- `month`
- `poutcome`

### Why you do it
Categorical variables often contain important business information. For example, the previous campaign outcome can be highly informative.

### What you should be able to say
> The categorical analysis helped identify segments and campaign characteristics associated with higher subscription rates.

---

## Cells 55–58 — Preprocessing

### What you do
You split the data into:

- training set
- validation set
- test set

Then you define preprocessing rules:

- numerical scaling for Logistic Regression
- no numerical scaling for Random Forest
- one-hot encoding for categorical variables

### Why you do it
Models need numerical input. Categorical strings must be converted to dummy variables. Logistic Regression also benefits from scaling.

### Important idea
The split is stratified to preserve the same class balance in train, validation and test sets.

### What you should be able to say
> I used a stratified train-validation-test split to preserve the proportion of subscribers in each subset and avoid biased evaluation.

---

## Cells 59–60 — Evaluation functions

### What you do
You define functions to compute metrics and confusion matrices.

### Why you do it
All models should be evaluated with the same logic and the same metrics.

### What you should be able to say
> I used common evaluation functions to compare models consistently.

---

# 4. How to read the metrics

## Confusion matrix

For this project:

```text
Actual no / Predicted no   = True Negative
Actual no / Predicted yes  = False Positive
Actual yes / Predicted no  = False Negative
Actual yes / Predicted yes = True Positive
```

In business terms:

- False positive = bank contacts a client who does not subscribe
- False negative = bank misses a client who would have subscribed

## Accuracy
Percentage of all correct predictions.

Problem: in imbalanced datasets it can be misleading.

## Precision
Among customers predicted as subscribers, how many actually subscribed.

High precision means fewer wasted calls.

## Recall
Among actual subscribers, how many were found by the model.

High recall means fewer missed opportunities.

## F1-score
A balance between precision and recall.

Useful when both false positives and false negatives matter.

## ROC-AUC
Measures how well the model ranks subscribers above non-subscribers across all thresholds.

- 0.50 = random
- 0.70 = acceptable
- 0.80 = good
- 0.90+ = very good

## PR-AUC
Precision-Recall area. Very useful when the positive class is rare.

---

# 5. Cells 61–68 — Baseline, Logistic Regression, Random Forest

## Baseline
The baseline predicts the most frequent class.

It is useful because it proves that high accuracy alone is not enough.

## Logistic Regression
This is the interpretable benchmark.

Strengths:

- simple
- fast
- interpretable
- good baseline for binary classification

Weakness:

- mainly linear decision boundary
- may miss nonlinear interactions

## Random Forest
This is the more flexible model.

Strengths:

- captures nonlinear relationships
- captures interactions
- robust for tabular data
- provides feature importance

Weakness:

- less directly interpretable than Logistic Regression
- can be computationally heavier

### What you should be able to say
> Logistic Regression was used as an interpretable benchmark, while Random Forest was used to capture nonlinear patterns and interactions in customer behavior.

---

# 6. Cells 70–83 — Model comparison, tuning and threshold analysis

## Model comparison
You compare models on the validation set.

The key idea is not simply “which accuracy is highest”, but which model gives the best trade-off between precision, recall, F1-score, ROC-AUC and PR-AUC.

## Hyperparameter tuning
GridSearchCV tests several Random Forest configurations.

Examples:

- number of trees
- maximum depth
- minimum leaf size
- max features considered at each split

## Threshold analysis
The model outputs probabilities. You can choose the probability threshold.

Example:

```text
threshold = 0.50 -> predict yes only if probability >= 50%
threshold = 0.40 -> predict yes if probability >= 40%
```

Lower threshold:

- higher recall
- more contacted clients
- more false positives

Higher threshold:

- higher precision
- fewer contacted clients
- more false negatives

### What you should be able to say
> Threshold analysis is important because the bank can decide how aggressive the marketing campaign should be. A lower threshold increases campaign reach, while a higher threshold focuses on more likely subscribers.

---

# 7. Cells 84–93 — Feature selection

## What you do
You select the most important original features and retrain the Random Forest using only those variables.

## Why you do it
Feature selection can:

- reduce noise
- improve interpretability
- reduce complexity
- sometimes improve performance

## What your results showed
In your current outputs, the Random Forest using the Top 10 features performed very well and improved several metrics.

### What you should be able to say
> The feature selection step showed that a reduced set of informative variables can achieve equal or better performance than the full feature set, while making the model easier to interpret.

---

# 8. Cells 94–101 — Permutation importance and SHAP

## Permutation importance
This checks what happens if one feature is randomly shuffled.

If performance drops a lot, the feature is important.

## SHAP
SHAP explains model predictions.

In a SHAP summary plot:

- each row is a feature
- each dot is a customer
- dots on the right increase subscription probability
- dots on the left decrease subscription probability
- red means high feature value
- blue means low feature value

### What you should be able to say
> SHAP was used to explain the Random Forest predictions both globally and locally. It shows which variables push the predicted probability of subscription upward or downward.

---

# 9. Cells 102–104 — Robustness check without duration

## Why this matters
`duration` is the length of the call. It is very predictive, but it is only known after the call starts.

For a real pre-call targeting strategy, the bank may not have this variable in advance.

### What you should be able to say
> I included a robustness check without duration because duration may not be available at the moment when the bank decides which customers to call.

---

# 10. Cells 105–107 — Final conclusions

Your final conclusion should include four elements:

1. Dataset is imbalanced, so accuracy alone is not enough.
2. Random Forest performs better overall than Logistic Regression.
3. Feature selection improves or maintains performance with fewer variables.
4. Interpretability tools identify the main business drivers.

Example conclusion:

```text
The Random Forest model with selected features achieved the best overall performance, improving F1-score, ROC-AUC and PR-AUC compared with the full-feature model. The analysis also shows that accuracy alone is misleading because of class imbalance. Feature importance and SHAP indicate that duration, previous campaign outcome, balance and campaign-related variables are among the main drivers of subscription probability. From a business perspective, the model can support more efficient marketing campaigns by prioritizing customers with higher predicted subscription probability.
```

---

# 11. What you should personally study before presenting

Focus on these topics:

1. Why the dataset is imbalanced.
2. Why accuracy alone is misleading.
3. Difference between Logistic Regression and Random Forest.
4. Meaning of precision and recall in a marketing campaign.
5. Why threshold tuning matters.
6. Why feature selection was useful.
7. Why `duration` is powerful but operationally delicate.
8. How to read SHAP summary plots.

---

# 12. Very short oral explanation

You can use this as a compact presentation script:

```text
The goal of the project is to predict whether a client will subscribe a term deposit based on customer and campaign information. I started with exploratory data analysis to inspect data quality, class imbalance, numerical distributions and categorical subscription rates. Since the target is imbalanced, I did not rely only on accuracy, but also used recall, precision, F1-score, ROC-AUC and PR-AUC.

I compared Logistic Regression and Random Forest. Logistic Regression is useful as an interpretable benchmark, while Random Forest can capture nonlinear effects and interactions. The Random Forest achieved better overall performance, especially in ROC-AUC and PR-AUC.

I then performed threshold analysis, because in a marketing application the bank can choose how many clients to contact. A lower threshold increases recall but also increases the number of contacted clients, while a higher threshold improves precision.

Finally, I applied feature selection and interpretability methods. The reduced-feature Random Forest performed very well and was easier to interpret. Feature importance and SHAP helped identify the main drivers of subscription probability.
```

---

# 13. Common professor questions and good answers

## Why did you use Logistic Regression?
Because it is a simple, interpretable and standard benchmark for binary classification.

## Why did you use Random Forest?
Because customer subscription behavior may involve nonlinear relationships and interactions that a linear model may not capture.

## Why is accuracy not enough?
Because the dataset is imbalanced. A model predicting always `no` can get high accuracy but zero ability to detect subscribers.

## What is the meaning of precision here?
Among clients selected by the model for contact, the proportion who actually subscribe.

## What is the meaning of recall here?
Among all actual subscribers, the proportion found by the model.

## Why did feature selection improve the model?
Because it removed less informative variables, reducing noise and improving generalization and interpretability.

## Why is duration problematic?
Because it is known after the call starts, so it may not be available for deciding whom to call before the campaign.

## Why SHAP?
Because Random Forest is less transparent than Logistic Regression, and SHAP helps explain how each variable contributes to predictions.
