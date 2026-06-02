# MBAI5310G AI Programming
**Student Name:** Clement Yorke  
**Course:** MBAI 5310G - AI Programming  
**Institution:** Ontario Tech University  
**Term:** Spring 2026  

---

## About This Repository
This repository contains my weekly coding assignments and final AI programming project for MBAI 5310G - AI Programming. The repository includes Jupyter/Colab notebooks, code, outputs, README files, and documentation for reproducibility.

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
- **Privacy:** The dataset contains sensitive financial information. Personal data should never be uploaded publicly to GitHub.
- **Fairness:** The model should be checked to ensure it does not perform differently across groups such as age or employment status.
- **Human Judgment:** The model should be used as a decision-support tool only. Human review is essential for fairness and accountability.

---

## Assignment 4 — Decision Tree Model and Business Interpretation

### Project Overview
This assignment builds and evaluates a Decision Tree classification model for two separate business problems, each based on a provided dataset and business plan. Results are interpreted from a business perspective.

---

### Part 1 — Evergreen Bank: Credit Card Upgrade

#### Business Problem
Evergreen Bank wants to predict which existing credit card customers are likely to accept a premium card upgrade offer, so that marketing outreach can be targeted efficiently rather than sent to all customers.

#### Dataset
**Evergreen Bank Credit Card Upgrade Dataset**
- 340 synthetic customer records, 20 input features
- Target variable: `Accepted_Card_Upgrade` (Yes / No)
- Features include: Credit_Utilization_Pct, Travel_Spend_Share_Pct, Avg_Monthly_Card_Spend, Credit_Score_Band, Customer_Satisfaction_Score, and more

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

#### Results
| Metric | Unconstrained Tree | max_depth=4 |
|--------|--------------------|-------------|
| Training Accuracy | 100.0% | 72.9% |
| Testing Accuracy | 52.5% | 58.3% |
| Precision (Yes) | 50.98% | — |
| Recall (Yes) | 44.83% | — |
| F1-Score (Yes) | 47.71% | — |

**Top Predictors:** Loyalty_Score (19.4%), Days_Since_Last_Purchase (13.2%), Annual_Income (9.6%)

### Responsible AI Reflection
- **Fairness:** Demographic features such as income, age, and region may produce unequal targeting outcomes. Fairness audits are required before deployment.
- **Transparency:** Decision Trees are interpretable — managers can follow the rules and explain predictions, supporting accountability.
- **Human Oversight:** Model outputs should support human decision-making, not replace it.

---

## Assignment 5 — K-Means Clustering and Employee Segmentation

### Project Overview
This assignment applies K-Means clustering to discover natural employee segments within the TalentWorks People Analytics dataset. Results are interpreted from an HR retention perspective.

### Dataset
**TalentWorks Employee Attrition Dataset**
- 286 records (280 after cleaning), 23 columns
- Features include: Age, Monthly_Income, Tenure_Months, Job_Satisfaction, Work_Life_Balance, Engagement_Score, Performance_Rating, Commute_Time_Minutes, and more

### Main Steps
| Step | Description |
|------|-------------|
| 1 | Understand the Business Problem |
| 2 | Load and Inspect the Dataset |
| 3 | Clean the Data (remove 6 duplicates, fill missing values) |
| 4 | Select 12 numerical features for clustering |
| 5 | Scale features using StandardScaler |
| 6 | Elbow Method to choose k |
| 7 | Train K-Means model (k=3) |
| 8 | Add cluster labels to dataset |
| 9 | Analyze cluster characteristics |
| 10 | Visualizations (Elbow, Scatter, Bar Chart, Box Plot) |
| 11 | Business Interpretation |
| 12 | Limitations and Responsible AI Reflection |
| 13 | Final Conclusion |

### Results
| Cluster | Label | Size | Key Characteristics |
|---------|-------|------|---------------------|
| 0 | Strained Commuters | 108 | Longest commutes (70.69 min), lowest satisfaction and performance, highest attrition risk |
| 1 | Experienced High Earners | 51 | Highest income ($6,595), longest tenure (81 months), best work-life balance |
| 2 | High-Performing Locals | 121 | Shortest commutes (26.74 min), highest performance and training hours, lowest work-life balance |

### Business Recommendation
- **Cluster 0:** Offer remote work or flexible hours; provide manager check-ins and early career development support.
- **Cluster 1:** Focus on recognition, succession planning, and knowledge transfer programs.
- **Cluster 2:** Address work-life balance and compensation gaps; make promotion pathways visible.

### How to Run
1. Place `talentworks_employee_attrition_dataset.xlsx` in the same folder as the notebook
2. Open `Assignment_5_TalentWorks.ipynb`
3. Run all cells from top to bottom

---

## Tools and Libraries
- Python 3
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- Jupyter Notebook
