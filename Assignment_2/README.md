# Assignment 2: End-to-End Machine Learning Pipeline

**Course:** MBAI 5310G-001: AI Programming
**Institution:** Ontario Tech University
**Student:** Clement Yorke
**Lecturer:** Zahra Atf

---

## Overview

This assignment builds a complete end-to-end machine learning pipeline for a binary classification problem. The goal is to predict whether a loan applicant will default on their loan, using a Logistic Regression model as the baseline classifier. The pipeline covers every stage from raw data to evaluated model output.

---

## Repository Structure

```
Assignment_2/
├── notebooks/
│   └── Assignment_2_Loan_Default.ipynb   # Full pipeline notebook
├── data/
│   ├── finance_loan_default_dataset.xls  # Raw dataset
│   ├── cleaned_loan_default_dataset.csv  # Cleaned dataset (output)
│   └── classification_outputs.csv        # Model predictions (output)
└── README.md
```

---

## Business Problem

A financial institution needs to assess loan applications and identify which applicants are likely to default. Manually reviewing every application is time-consuming and inconsistent. A machine learning model trained on historical applicant data can flag high-risk applications automatically, allowing loan officers to focus their review on the cases that matter most.

**Target variable:** `Loan_Default` (Yes = defaulted, No = did not default)

---

## Dataset

| Property | Detail |
|----------|--------|
| File | `finance_loan_default_dataset.xls` |
| Records | 356 loan applicant records |
| Features | 14 columns |
| Target variable | `Loan_Default` (Yes / No) |

Features cover applicant demographics, financial profile, and credit history:

- **Demographics:** Age
- **Financial:** Annual_Income, Loan_Amount, Loan_Term_Months, Existing_Debt, Savings_Balance, Debt_to_Income_Ratio
- **Credit history:** Credit_Score, Late_Payments_Last_Year, Has_Credit_Card
- **Categorical:** Employment_Status, Account_Type

---

## Pipeline Steps

**Step 1: Load the Dataset**
Load the data using `pandas`. The file uses a `.xls` extension but is stored as CSV, so `read_csv` is used.

**Step 2: Inspect the Dataset**
Check column names, data types, missing values, duplicates, and summary statistics to understand the data before making any changes.

**Step 3: Clean the Data**
Remove duplicate rows. Fill missing numerical values with the column median. Fill missing categorical values with the most frequent value (mode).

**Step 4: Define Features and Target**
Exclude `Applicant_ID` (a row identifier with no predictive value). Assign 12 remaining columns as features. Encode the target: `Yes` = 1, `No` = 0.

**Step 5: Train/Test Split**
Split 80/20 using `train_test_split` with `stratify=y` and `random_state=42` to ensure reproducibility and balanced class distribution in both sets.

**Step 6: Preprocessing**
Apply `StandardScaler` to numerical features and `OneHotEncoder` to categorical features via a `ColumnTransformer`. The preprocessor is fitted on training data only and applied to the test set to prevent data leakage.

**Step 7: Train the Model**
Train a `LogisticRegression` model (`max_iter=1000`, `random_state=42`) on the preprocessed training data.

**Step 8: Evaluate the Model**
Evaluate on the test set using accuracy, precision, recall, F1-score, a full classification report, and a confusion matrix.

---

## Results

| Metric | Score |
|--------|-------|
| Accuracy | ~80% |
| Priority Metric | Recall |

**Recall** is the priority metric for this business problem. Missing an actual default (false negative) is far more costly than a false alarm (false positive). A bank that fails to flag a genuine default risks significant financial loss, while a false alarm only causes a slightly slower application process.

---

## Key Takeaways

- Logistic Regression serves as a solid, interpretable baseline for binary classification problems like loan default prediction.
- Preprocessing is critical: scaling numerical features and encoding categoricals before training prevents the model from being misled by differences in feature magnitude.
- Stratified splitting ensures the train and test sets have the same proportion of default vs. non-default cases, giving a fair evaluation of model performance.

---

## How to Replicate

### Prerequisites

```
Python 3.8+
pandas
scikit-learn
matplotlib
jupyter
```

Install dependencies:

```bash
pip install pandas scikit-learn matplotlib jupyter
```

### Steps

1. Clone the repository:

```bash
git clone https://github.com/cyorke001/MBAI5310G-AI-Programming-Clement-Yorke.git
cd MBAI5310G-AI-Programming-Clement-Yorke/Assignment_2
```

2. Launch Jupyter:

```bash
jupyter notebook
```

3. Open `notebooks/Assignment_2_Loan_Default.ipynb` and run all cells top to bottom (`Kernel -> Restart & Run All`).
