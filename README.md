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
├── Assignment_2/
│   ├── Assignment_2_Loan_Default.ipynb
│   ├── finance_loan_default_dataset.xls
│   └── outputs/
│
├── Assignment_3/
│   ├── Assignment_3_Loan_Default.ipynb
│   ├── finance_loan_default_dataset.xls
│   └── outputs/
│
├── Assignment_4/
│   ├── Assignment_4_Evergreen.ipynb
│   ├── Assignment_4_AdVantage_Growth_Studio.ipynb
│   ├── Assignment_4_Evergreen_Bank_Report.docx
│   ├── Assignment_4_AdVantage_Growth_Studio_Report.docx
│   ├── evergreen_bank_credit_card_upgrade_dataset.xlsx
│   ├── marketing_campaign_decision_tree_dataset.xlsx
│   └── README.md
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

## Assignment 4 — Decision Tree Model and Business Interpretation

### Project Overview
This assignment builds and evaluates a Decision Tree classification model for two separate business problems, each based on a provided dataset and business plan. Results are interpreted from a business perspective.

---

### Part 1 — Evergreen Bank: Credit Card Upgrade

#### Business Problem
Evergreen Bank wants to predict which existing credit card customers are likely to accept a premium card upgrade offer, so that marketing outreach can be targeted efficiently.

#### Dataset
**Evergreen Bank Credit Card Upgrade Dataset**
- 340 synthetic customer records, 20 input features
- Target variable: `Accepted_Card_Upgrade` (Yes / No)
- Features include: Credit_Utilization_Pct, Travel_Spend_Share_Pct, Avg_Monthly_Card_Spend, Credit_Score_Band, Customer_Satisfaction_Score, and more

#### Main Steps
| Step | Description |
|------|-------------|
| 1 | Understand the Business Problem |
| 2 | Load and Inspect the Dataset |
| 3 | Clean the Data |
| 4 | Handle Missing Values |
| 5 | Define Features and Target Variable |
| 6 | One-Hot Encode Categorical Features |
| 7 | Train/Test Split (80/20, stratified) |
| 8 | Introduction to Decision Trees |
| 9 | Train the Decision Tree Model |
| 10 | Visualize the Decision Tree |
| 11 | Evaluate — Training vs Testing Accuracy |
| 12 | Confusion Matrix |
| 13 | Precision, Recall, F1-Score |
| 14 | Overfitting Analysis |
| 15 | Control Complexity with max_depth=4 |
| 16 | Feature Importance |
| 17 | Business Interpretation |
| 18 | Limitations and Responsible AI Reflection |
| 19 | Final Conclusion |

#### Results
| Metric | Unconstrained Tree | max_depth=4 |
|--------|--------------------|-------------|
| Training Accuracy | 100.0% | 84.6% |
| Testing Accuracy | 63.2% | 69.1% |
| Precision (Yes) | 51.9% | — |
| Recall (Yes) | 53.8% | — |
| F1-Score (Yes) | 52.8% | — |

**Top Predictors:** Credit_Utilization_Pct (26.3%), Travel_Spend_Share_Pct (10.9%), Dining_Spend_Share_Pct (9.5%)

---

### Part 2 — AdVantage Growth Studio: Marketing Campaign

#### Business Problem
AdVantage Growth Studio wants to predict which customers are likely to convert after receiving a marketing campaign, so that campaign resources can be focused on the most promising customers.

#### Dataset
**Marketing Campaign Decision Tree Dataset**
- 600 records (after cleaning), 18 input features
- Target variable: `Converted` (Yes / No)
- Features include: Loyalty_Score, Days_Since_Last_Purchase, Annual_Income, Social_Media_Engagement_Score, Previous_Purchases, and more

#### Main Steps
| Step | Description |
|------|-------------|
| 1 | Understand the Business Problem |
| 2 | Load and Inspect the Dataset |
| 3 | Clean the Data (remove 5 duplicates, fill missing values) |
| 4 | Define Features and Target Variable |
| 5 | One-Hot Encode Categorical Features |
| 6 | Train/Test Split (80/20, stratified) |
| 7 | Introduction to Decision Trees |
| 8 | Train the Decision Tree Model |
| 9 | Visualize the Decision Tree |
| 10 | Evaluate — Training vs Testing Accuracy |
| 11 | Confusion Matrix |
| 12 | Precision, Recall, F1-Score |
| 13 | Overfitting Analysis |
| 14 | Control Complexity with max_depth=4 |
| 15 | Feature Importance |
| 16 | Business Interpretation |
| 17 | Limitations and Responsible AI Reflection |
| 18 | Final Conclusion |

#### Results
| Metric | Unconstrained Tree | max_depth=4 |
|--------|--------------------|-------------|
| Training Accuracy | 100.0% | 72.9% |
| Testing Accuracy | 52.5% | 58.3% |
| Precision (Yes) | 50.98% | — |
| Recall (Yes) | 44.83% | — |
| F1-Score (Yes) | 47.71% | — |

**Top Predictors:** Loyalty_Score (19.4%), Days_Since_Last_Purchase (13.2%), Annual_Income (9.6%)

### How to Run
1. Place the dataset file in the same folder as the notebook
2. Open the relevant `.ipynb` file
3. Run all cells from top to bottom

### Notes and Limitations
Both models show severe overfitting without depth constraints. Applying `max_depth=4` significantly reduced the train/test gap in both cases. Both datasets are synthetic and small, limiting real-world applicability. Features like Income_Band, Age_Group, and Region may introduce demographic bias and require a fairness review before any real deployment.

### Responsible AI Reflection
- **Fairness:** Demographic features such as income, age, and region may produce unequal targeting outcomes across customer groups. Fairness audits are required before deployment.
- **Transparency:** Decision Trees are interpretable — managers can follow the rules and explain predictions. This supports accountability in financial and marketing contexts.
- **Human Oversight:** Model outputs should support human decision-making, not replace it. Eligibility checks, affordability assessments, and customer consent must be verified by humans before acting on model predictions.

---

## Tools and Libraries
- Python 3
- pandas
- numpy
- scikit-learn
- matplotlib
- Jupyter Notebook
