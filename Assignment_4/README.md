# Assignment 4: Decision Tree Model and Business Interpretation

**Course:** MBAI 5310G-001: AI Programming
**Institution:** Ontario Tech University
**Student:** Clement Yorke
**Lecturer:** Zahra Atf

---

## Overview

This assignment applies supervised machine learning: specifically Decision Tree classification: to two real-world business problems. Each part of the assignment is based on a separate business plan and dataset, and follows a consistent analytical workflow from raw data to business interpretation.

The goal is not only to build a working model, but to understand what the model is saying and translate its outputs into actionable business insights.

---

## Repository Structure

```
Assignment_4/
├── Assignment_4_Evergreen.ipynb                    # Notebook: Evergreen Bank
├── Assignment_4_AdVantage_Growth_Studio.ipynb      # Notebook: AdVantage Growth Studio
├── Assignment_4_Evergreen_Bank_Report.pdf          # Full report: Evergreen Bank
├── Assignment_4_AdVantage_Growth_Studio_Report.pdf # Full report: AdVantage Growth Studio
├── evergreen_bank_credit_card_upgrade_dataset.xlsx # Dataset: Evergreen Bank
├── marketing_campaign_decision_tree_dataset.xlsx   # Dataset: AdVantage Growth Studio
└── README.md
```

---

## Part 1: Evergreen Bank: Credit Card Upgrade

### Business Problem

Evergreen Bank wants to predict which of its existing credit card customers are likely to accept a premium card upgrade offer. Rather than sending the offer to every customer, the bank wants to focus its outreach on customers most likely to say yes: saving marketing costs and improving customer experience.

### Dataset

| Property | Detail |
|----------|--------|
| File | `evergreen_bank_credit_card_upgrade_dataset.xlsx` |
| Records | 340 synthetic customer profiles |
| Features | 20 input features |
| Target variable | `Accepted_Card_Upgrade` (Yes / No) |

Features cover five categories: customer profile (age, income band, region), banking relationship (tenure, product count), card usage (credit utilization, spend shares), digital engagement (app logins, online banking), and credit risk (credit score, missed payments).

### Analytical Workflow

**Step 1: Data Loading and Initial Exploration**
Load the dataset with `pandas`, inspect shape, column names, data types, and class distribution. Use `df.head()` and `df.tail()` to verify data loaded correctly.

**Step 2: Exploratory Data Analysis (EDA)**
Check for missing values, duplicates, and class balance. Use `df.describe()` for numerical summaries and `value_counts()` for categorical columns.

**Step 3: Preprocessing**
- Drop non-predictive columns (e.g. `Customer_ID`)
- Handle any missing values
- Apply one-hot encoding (`pd.get_dummies`) to categorical features
- Apply label encoding (`LabelEncoder`) to the target variable

**Step 4: Train/Test Split**
Split data 80/20 using `train_test_split` with `stratify=y` and `random_state=42` to ensure reproducibility and balanced class representation in both sets.

**Step 5: Model Training**
Train a `DecisionTreeClassifier` with `random_state=42` (no depth constraint initially).

**Step 6: Decision Tree Visualization**
Plot the tree using `sklearn.tree.plot_tree` with feature names and class names labelled.

**Step 7: Model Evaluation**
Generate predictions on the test set. Evaluate using:
- Confusion matrix
- Accuracy, Precision, Recall, F1-Score (via `classification_report`)

**Step 8: Overfitting Check**
Compare training accuracy vs. testing accuracy. A large gap indicates overfitting: the model memorised the training data instead of learning generalizable patterns.

**Step 9: Controlling Complexity with max_depth**
Re-train the model with `max_depth=4`. Re-evaluate on the test set to measure the improvement in generalization.

**Step 10: Feature Importance**
Extract `.feature_importances_` from the trained model. Plot a horizontal bar chart showing which features contributed most to the model's decisions.

**Step 11: Limitations, Responsible AI, and Conclusion**
Discuss model limitations, potential bias in features like `Income_Band` and `Region`, and the importance of human oversight before deployment.

### Results

| Metric | Unconstrained Model | max_depth=4 |
|--------|-------------------|-------------|
| Training Accuracy | 100.0% |: |
| Testing Accuracy | 63.2% | **69.1%** |
| Precision (Yes) | 51.9% |: |
| Recall (Yes) | 53.8% |: |
| F1-Score (Yes) | 52.8% |: |
| False Positives | 13 |: |
| False Negatives | 12 |: |

**Train/test gap (unconstrained):** ~36.8 percentage points: severe overfitting.
**Gap with max_depth=4:** reduced to ~30.9 points.

### Top Predictors

1. `Credit_Utilization_Pct`: customers with moderate utilization are more likely to upgrade
2. `Travel_Spend_Share_Pct`: high travel spenders are strong upgrade candidates
3. `Dining_Spend_Share_Pct`: lifestyle spending patterns signal premium card interest
4. `Avg_Monthly_Card_Spend`: active card users are more likely to value premium benefits
5. `Reward_Points_Balance`: engaged rewards users are primed for an upgrade

### Priority Metric

**Precision**: the bank wants to avoid sending upgrade offers to customers who won't accept, as this wastes marketing budget and risks annoying customers. False positives are the primary cost to minimize.

---

## Part 2: AdVantage Growth Studio: Marketing Campaign Conversion

### Business Problem

AdVantage Growth Studio runs digital marketing campaigns and wants to predict which customers are likely to convert (make a purchase) after receiving a campaign. Knowing this in advance allows the studio to allocate campaign budget more efficiently and avoid spending on customers who are unlikely to respond.

### Dataset

| Property | Detail |
|----------|--------|
| File | `marketing_campaign_decision_tree_dataset.xlsx` |
| Records | 600 synthetic customer records |
| Features | 18 input features (after cleaning) |
| Target variable | `Converted` (Yes / No) |

Features cover customer demographics, campaign channel and type, engagement behavior (email opens, clicks), and purchase history (loyalty score, days since last purchase, annual income).

### Analytical Workflow

Follows the same 11-step structure as Part 1, with the following differences:

- **Dropped columns:** Both `Customer_ID` (identifier) and `Campaign_Date` (date string with no predictive value in this format) were removed during preprocessing.
- **Duplicate handling:** 5 duplicate records were identified and removed.
- **Priority metric:** F1-Score rather than Precision, because both wasted campaign budget (false positives) and missed conversions (false negatives) carry equal business cost.

### Results

| Metric | Unconstrained Model | max_depth=4 |
|--------|-------------------|-------------|
| Training Accuracy | 100.0% |: |
| Testing Accuracy | 62.3% | **66.7%** |
| Precision (Yes) | 62.0% |: |
| Recall (Yes) | 58.2% |: |
| F1-Score (Yes) | 60.0% |: |
| False Positives | 20 |: |
| False Negatives | 23 |: |

**Train/test gap (unconstrained):** ~37.7 percentage points: severe overfitting.
**Gap with max_depth=4:** reduced to ~33.3 points.

### Top Predictors

1. `Loyalty_Score`: loyal customers are significantly more likely to convert
2. `Average_Order_Value`: higher spenders are more receptive to premium campaign offers
3. `Days_Since_Last_Purchase`: recent buyers are more responsive to campaigns
4. `Annual_Income`: income level influences purchasing readiness
5. `Social_Media_Engagement_Score`: active social media users respond better to digital campaigns

### Priority Metric

**F1-Score**: both false positives (wasted spend) and false negatives (missed revenue) are costly. F1 balances precision and recall equally, making it the right metric for this business context.

---

## How to Replicate This Work

### Prerequisites

```
Python 3.8+
pandas
numpy
matplotlib
seaborn
scikit-learn
openpyxl
jupyter
```

Install all dependencies:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl jupyter
```

### Steps

1. Clone the repository:

```bash
git clone https://github.com/cyorke001/MBAI5310G-AI-Programming-Clement-Yorke.git
cd MBAI5310G-AI-Programming-Clement-Yorke/Assignment_4
```

2. Launch Jupyter:

```bash
jupyter notebook
```

3. Open either notebook:
   - `Assignment_4_Evergreen.ipynb`
   - `Assignment_4_AdVantage_Growth_Studio.ipynb`

4. Run all cells in order from top to bottom (`Kernel → Restart & Run All`).

Both notebooks are fully self-contained. All data files are included in the same folder.

---

## Key Takeaways

Both models exhibited severe overfitting in their unconstrained form: training accuracy hit 100% while test accuracy was significantly lower. This is a classic sign that the tree memorized the training data rather than learning patterns that generalize.

Applying `max_depth=4` improved test accuracy in both cases and reduced the train/test gap, demonstrating how a simple hyperparameter constraint can meaningfully improve a model's real-world reliability.

However, both datasets are synthetic and small. Features such as `Income_Band`, `Age_Group`, `Region`, and `Annual_Income` could introduce demographic bias if deployed in a real setting. A fairness review and human oversight process are essential before either model is used to make real business decisions.

---

## Reports

Full written reports with business context, model output interpretation, feature analysis, and responsible AI discussion are available as PDF files in this folder:

- `Assignment_4_Evergreen_Bank_Report.pdf`
- `Assignment_4_AdVantage_Growth_Studio_Report.pdf`
