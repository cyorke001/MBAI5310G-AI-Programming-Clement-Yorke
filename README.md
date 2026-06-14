# MBAI 5310G: AI Programming

**Student:** Clement Yorke
**Course:** MBAI 5310G - AI Programming
**Institution:** Ontario Tech University
**Instructor:** Zahra Atf
**Term:** Spring 2026

---

## Repository Overview

This repository contains all coding assignments for MBAI 5310G. Each assignment folder is organised into subfolders (notebooks, data, reports) and includes its own detailed README.

---

## Repository Structure

```
MBAI5310G-AI-Programming-Clement-Yorke/
├── Assignment_2/                                       # End-to-End ML Pipeline (Logistic Regression)
│   ├── notebooks/
│   │   └── Assignment_2_Loan_Default.ipynb
│   ├── data/
│   │   ├── finance_loan_default_dataset.xls
│   │   ├── cleaned_loan_default_dataset.csv
│   │   └── classification_outputs.csv
│   └── README.md
├── Assignment_3/                                       # Classification Model Comparison (LR vs SVM)
│   ├── notebooks/
│   │   └── Assignment_3_Loan_Default.ipynb
│   ├── data/
│   │   ├── finance_loan_default_dataset.xls
│   │   ├── cleaned_loan_default_dataset.csv
│   │   ├── classification_outputs.csv
│   │   └── model_comparison_results.csv
│   └── README.md
├── Assignment_4/                                       # Decision Tree Model and Business Interpretation
│   ├── notebooks/
│   │   ├── Assignment_4_Evergreen_Bank.ipynb
│   │   └── Assignment_4_AdVantage_Growth_Studio.ipynb
│   ├── reports/
│   │   ├── Assignment_4_Evergreen_Bank_Report.pdf
│   │   └── Assignment_4_AdVantage_Growth_Studio_Report.pdf
│   ├── data/
│   │   ├── evergreen_bank_credit_card_upgrade_dataset.xlsx
│   │   └── marketing_campaign_decision_tree_dataset.xlsx
│   └── README.md
├── Assignment_5/                                       # K-Means Clustering and Employee Segmentation
│   ├── notebooks/
│   │   └── Assignment_5_TalentWorks.ipynb
│   ├── reports/
│   │   └── Assignment_5_TalentWorks_Report.pdf
│   ├── data/
│   │   └── talentworks_employee_attrition_dataset.xlsx
│   └── README.md
├── Assignment_6/                                       # Model Evaluation, Explainability, and Fairness
│   ├── notebooks/
│   │   └── Assignment6_Event_Attendance.ipynb
│   ├── reports/
│   │   └── Assignment6_Event_Attendance_Report.docx
│   ├── data/
│   │   └── event_registration_attendance_dataset.csv
│   └── README.md
└── README.md
```

---

## Assignments at a Glance

| Assignment | Topic | Method | Dataset |
|------------|-------|--------|---------|
| 2 | Loan Default Prediction | Logistic Regression | Finance Loan Default (356 records) |
| 3 | Model Comparison | Logistic Regression vs SVM | Finance Loan Default (356 records) |
| 4 | Credit Card Upgrade + Campaign Conversion | Decision Tree | Evergreen Bank (340) + AdVantage (600) |
| 5 | Employee Segmentation | K-Means Clustering (k=3) | TalentWorks Attrition (286 records) |
| 6 | Model Evaluation, Explainability & Fairness | Decision Tree + SHAP + LIME | Event Registration & Attendance (380 records) |

See each assignment folder's README for full details on the business problem, dataset, methodology, results, and how to run the notebook.

---

## Tools and Libraries

Python 3, pandas, numpy, scikit-learn, matplotlib, seaborn, shap, lime, Jupyter Notebook, openpyxl
