# Assignment 3: Classification Model Comparison

**Course:** MBAI 5310G-001: AI Programming
**Institution:** Ontario Tech University
**Student:** Clement Yorke
**Lecturer:** Zahra Atf

---

## Overview

This assignment extends the Assignment 2 pipeline by introducing a second classifier and comparing both models head-to-head. Logistic Regression (baseline from Assignment 2) is trained alongside a Support Vector Machine (SVM), and the two are evaluated on the same dataset using consistent metrics. The goal is to determine which model is better suited for loan default prediction and justify that choice in business terms.

---

## Repository Structure

```
Assignment_3/
├── notebooks/
│   └── Assignment_3_Loan_Default.ipynb      # Full comparison notebook
├── data/
│   ├── finance_loan_default_dataset.xls     # Raw dataset
│   ├── cleaned_loan_default_dataset.csv     # Cleaned dataset (output)
│   ├── classification_outputs.csv           # Model predictions (output)
│   └── model_comparison_results.csv         # Side-by-side metric comparison
└── README.md
```

---

## Business Problem

The same financial institution from Assignment 2 needs a more reliable way to flag loan applicants likely to default. Having established Logistic Regression as the baseline, this assignment asks: can a more powerful model do better? SVM is introduced as the challenger, and both models are compared systematically to guide a real deployment decision.

**Target variable:** `Loan_Default` (Yes = defaulted, No = did not default)

---

## Dataset

| Property | Detail |
|----------|--------|
| File | `finance_loan_default_dataset.xls` |
| Records | 356 loan applicant records |
| Features | 14 columns |
| Target variable | `Loan_Default` (Yes / No) |

Same dataset and features as Assignment 2. Features cover applicant demographics, financial profile, and credit history:

- **Demographics:** Age
- **Financial:** Annual_Income, Loan_Amount, Loan_Term_Months, Existing_Debt, Savings_Balance, Debt_to_Income_Ratio
- **Credit history:** Credit_Score, Late_Payments_Last_Year, Has_Credit_Card
- **Categorical:** Employment_Status, Account_Type

---

## Pipeline Steps

**Steps 1-6** follow the same structure as Assignment 2 (load, inspect, clean, define features, split, preprocess). See Assignment 2 README for details.

**Step 7: Train and Evaluate — Logistic Regression**
Train `LogisticRegression` (`max_iter=1000`, `random_state=42`). Evaluate using accuracy, precision, recall, F1-score, classification report, and confusion matrix.

**Step 8: Train and Evaluate — SVM**
Train `SVC` with an RBF kernel (`random_state=42`). Apply the same evaluation metrics as Step 7 for a fair comparison.

**Step 9: Compare Both Models**
Build a side-by-side comparison table of all metrics. Identify which model performs better and why, in both statistical and business terms.

---

## Results

| Metric | Logistic Regression | SVM |
|--------|--------------------|----|
| Accuracy | ~80% | ~87% |
| Priority Metric | Recall | Recall |

**SVM outperformed Logistic Regression across all metrics.** It achieved higher accuracy and — more importantly — higher recall on the Default class, meaning it caught more actual defaults. For a bank, missing a genuine default (false negative) carries far greater financial risk than a false alarm (false positive), making recall the priority metric.

---

## Key Takeaways

- SVM with an RBF kernel is better suited to this dataset than Logistic Regression, likely because the decision boundary between defaulters and non-defaulters is non-linear.
- Recall is the most business-critical metric here: a missed default costs far more than an incorrect flag.
- Model comparison is an essential step before deployment. A single model result is never sufficient to make a confident deployment decision.
- Both models use the same preprocessing pipeline, ensuring the comparison is fair and the performance difference is attributable to the model itself, not data handling differences.

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
cd MBAI5310G-AI-Programming-Clement-Yorke/Assignment_3
```

2. Launch Jupyter:

```bash
jupyter notebook
```

3. Open `notebooks/Assignment_3_Loan_Default.ipynb` and run all cells top to bottom (`Kernel -> Restart & Run All`).
