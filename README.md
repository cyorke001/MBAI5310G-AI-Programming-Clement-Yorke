# MBAI5310G AI Programming
**Student Name:** Clement Yorke  
**Course:** MBAI 5310G - AI Programming  
**Institution:** Ontario Tech University  
**Term:** Spring 2026  

---

## About This Repository
This repository contains my weekly coding assignments and final AI programming project for MBAI 5310G - AI Programming.
The repository will include Jupyter/Colab notebooks, code, outputs, README files, and documentation for reproducibility.

---

## Repository Structure
```
MBAI5310G-AI-Programming-ClementYorke/
│
├── Assignment_2_Loan_Default.ipynb
├── Assignment_3_Loan_Default.ipynb
├── finance_loan_default_dataset.xls
│
├── outputs/
│   ├── cleaned_loan_default_dataset.csv
│   ├── model_comparison_results.csv
│   └── classification_outputs.csv
│
└── README.md
```

---

## Course Information
| Field | Details |
|-------|---------|
| Course Code | MBAI 5310G |
| Course Name | AI Programming |
| Instructor | Zahra Atf |
| Term | Spring 2026 |

---

## Assignment 2 — End-to-End Machine Learning Pipeline

### Project Overview
This project builds a complete end-to-end machine learning pipeline to predict whether a loan applicant will default on their loan.

### Dataset
**Finance Loan Default Dataset**
- 356 applicant records, 14 columns
- Target variable: `Loan_Default` (Yes / No)
- Features include: Age, Annual Income, Credit Score, Loan Amount, Savings Balance, Employment Status, and more

### Main Steps
| Step | Description |
|------|-------------|
| 1 | Load the Dataset |
| 2 | Inspect the Dataset |
| 3 | Clean the Data |
| 4 | Define Features and Target |
| 5 | Train/Test Split |
| 6 | Preprocessing (StandardScaler + OneHotEncoder) |
| 7 | Train the Model (Logistic Regression) |
| 8 | Evaluate the Model |

### Results
| Metric | Score |
|--------|-------|
| Accuracy | 0.800 |
| Precision | 0.700 |
| Recall | 0.389 |
| F1 Score | 0.500 |

### How to Run
1. Place `finance_loan_default_dataset.xls` in the same folder as the notebook
2. Open `Assignment_2_Loan_Default.ipynb`
3. Run all cells from top to bottom

### Notes and Limitations
The model struggles to detect actual defaults due to class imbalance — 75% of applicants did not default. Future improvements could include SMOTE oversampling or class-weight adjustment.

---

## Assignment 3 — Classification Model Comparison

### Project Overview
This project trains and compares two classification models — Logistic Regression and SVM — to predict loan default, and interprets the results.

### Dataset
**Finance Loan Default Dataset**
- 356 applicant records, 14 columns
- Target variable: `Loan_Default` (Yes / No)
- Features include: Age, Annual Income, Credit Score, Loan Amount, Savings Balance, Employment Status, and more

### Main Steps
| Step | Description |
|------|-------------|
| 1 | Load the Dataset |
| 2 | Inspect the Dataset |
| 3 | Clean the Data |
| 4 | Define Features and Target |
| 5 | Train/Test Split |
| 6 | Preprocessing (StandardScaler + OneHotEncoder) |
| 7 | Train and Evaluate — Logistic Regression |
| 8 | Train and Evaluate — SVM |
| 9 | Compare Both Models |

### Results
| Model | Accuracy | Precision | Recall | F1 Score |
|-------|----------|-----------|--------|----------|
| Logistic Regression | 0.800 | 0.700 | 0.389 | 0.500 |
| SVM (RBF) | 0.871 | 0.909 | 0.556 | 0.690 |

### How to Run
1. Place `finance_loan_default_dataset.xls` in the same folder as the notebook
2. Open `Assignment_3_Loan_Default.ipynb`
3. Run all cells from top to bottom

### Notes and Limitations
Both models are biased towards predicting No Default due to class imbalance. SVM performed better overall but still missed nearly half of actual defaults.

### Responsible AI Reflection
This model makes predictions about loan applicants using financial and demographic data. There are important ethical considerations:
- **Privacy:** The dataset contains sensitive financial information. In real projects, personal data should never be uploaded publicly to GitHub.
- **Fairness:** The model should be checked to ensure it does not perform differently across groups such as age or employment status. Biased predictions could unfairly deny loans to creditworthy applicants.
- **Human Judgment:** The model should be used as a decision-support tool only. A bank should not rely solely on a machine learning model to approve or reject loan applications — human review is essential for fairness and accountability.

---

## Tools and Libraries
- Python 3
- pandas
- scikit-learn
- matplotlib
- Jupyter Notebook

---
