# Assignment 5: K-Means Clustering and Employee Segmentation

**Course:** MBAI 5310G-001: AI Programming
**Institution:** Ontario Tech University
**Student:** Clement Yorke
**Lecturer:** Zahra Atf

---

## Overview

This assignment applies unsupervised machine learning — specifically K-Means clustering — to discover natural employee segments within a workforce dataset. Unlike the supervised models in previous assignments, K-Means does not use a target variable. It finds structure in the data on its own by grouping employees based on similarity across multiple features.

The goal is to segment TalentWorks employees into meaningful groups that HR managers can use to design targeted retention strategies, rather than applying the same intervention to everyone.

---

## Repository Structure

```
Assignment_5/
├── notebooks/
│   └── Assignment_5_TalentWorks.ipynb
├── data/
│   └── talentworks_employee_attrition_dataset.xlsx
├── reports/
│   └── Assignment_5_TalentWorks_Report.pdf
└── README.md
```

---

## Business Problem

TalentWorks People Analytics is a fictional HR analytics consulting unit supporting mid-sized service and retail organizations. The business has observed increasing employee turnover across departments. Replacing employees is costly, requiring time and money for hiring, onboarding, training, and temporary staffing. High turnover also reduces service quality and team morale.

The goal is to use K-Means clustering to segment employees into natural groups based on their workplace experience, satisfaction, performance, and commute patterns. These segments help HR managers identify which groups are at highest attrition risk and which need targeted support.

**Key question:** What natural groups exist within the workforce, and what does each group need from the organization?

---

## Dataset

| Property | Detail |
|----------|--------|
| File | `talentworks_employee_attrition_dataset.xlsx` |
| Records | 286 employee records (280 after cleaning) |
| Features | 23 columns |
| Target variable | None (unsupervised learning) |
| Note | Dataset contains intentional missing values and duplicate rows |

Features span six categories:

- **Employee profile:** Age, Education_Level, Marital_Status
- **Work arrangement:** Employment_Type, Remote_Work_Available, Commute_Time_Minutes, Distance_From_Home_km
- **Job experience:** Tenure_Months, Department, Job_Role
- **Workplace experience:** Job_Satisfaction, Work_Life_Balance, Manager_Feedback_Score, Engagement_Score
- **Performance and workload:** Performance_Rating, Workload_Level, Overtime, Absences_Last_Quarter
- **Development:** Training_Hours_Last_Year, Promotion_Last_2_Years, Monthly_Income

---

## Analytical Workflow

**Step 1: Understand the Business Problem**
Read the business plan. Identify what problem TalentWorks is trying to solve, why employee segmentation is valuable, and what HR decisions the analysis should support.

**Step 2: Load the Dataset**
Load the Excel file using `pandas`. Verify it loaded correctly using `df.head()` and `df.tail()`.

**Step 3: Inspect the Dataset**
Check shape, column names, data types, missing values per column, duplicate row count, and summary statistics using `df.describe()` and `df.dtypes`. Value counts were checked for categorical columns to understand class distributions.

**Step 4: Clean the Dataset**
- Dropped `Employee_ID` — a row identifier with no analytical value
- Removed 6 duplicate rows (286 reduced to 280)
- Filled missing values in all numerical columns with their column medians (affected columns: `Monthly_Income`: 2 nulls, `Work_Life_Balance`: 3, `Training_Hours_Last_Year`: 6, `Manager_Feedback_Score`: 5, `Engagement_Score`: 5)

**Step 5: Select Features for Clustering**
Selected 12 numerical features for clustering: `Age`, `Monthly_Income`, `Tenure_Months`, `Distance_From_Home_km`, `Commute_Time_Minutes`, `Job_Satisfaction`, `Work_Life_Balance`, `Training_Hours_Last_Year`, `Absences_Last_Quarter`, `Performance_Rating`, `Manager_Feedback_Score`, `Engagement_Score`.

Categorical features such as `Department`, `Job_Role`, and `Workload_Level` were excluded because K-Means requires numerical input and encoding these would add noise rather than meaningful distance signal.

**Step 6: Scale Features**
Applied `StandardScaler` to all 12 features before clustering. This ensures no single feature dominates due to differences in scale (e.g. `Monthly_Income` ranges in the thousands while `Job_Satisfaction` ranges from 1 to 5).

**Step 7: Elbow Method**
Trained K-Means for k=1 through k=10 and recorded inertia (total within-cluster sum of squared distances) for each. Plotted inertia vs. k to identify the elbow — the point where adding more clusters yields diminishing returns. The elbow occurred at k=3.

**Step 8: Train the Final K-Means Model**
Trained `KMeans(n_clusters=3, random_state=42, n_init=10)` on the scaled feature matrix. Added the resulting cluster labels back to the original dataset as a new `Cluster` column.

**Step 9: Analyze Cluster Characteristics**
Calculated per-cluster mean values for all 12 features using `groupby("Cluster").mean()`. Compared clusters across key dimensions to identify what makes each group distinct.

**Step 10: Visualize the Clusters**
Created four visualizations to support the analysis:
- **Elbow Method plot:** inertia curve with red dashed line at k=3
- **Scatter plot:** Monthly Income vs. Tenure Months, coloured by cluster
- **Bar chart:** average Job_Satisfaction, Work_Life_Balance, Performance_Rating, Manager_Feedback_Score by cluster
- **Box plot:** commute time distribution by cluster

**Step 11: Business Interpretation**
Translated cluster characteristics into HR strategies for each segment, answering: what patterns were found, how can the business use them, and what retention actions are recommended?

**Step 12: Limitations and Responsible AI Reflection**
Discussed dataset limitations, K-Means assumptions, potential for bias if clusters are used without human review, and why human judgment must remain central to any HR decision.

**Step 13: Final Conclusion**
Summarized the full analysis, key findings, and business value of the clustering approach.

---

## Results

### Elbow Method

| k | Inertia | k | Inertia |
|---|---------|---|---------|
| 1 | 3360.00 | 6 | 2411.97 |
| 2 | 2962.33 | 7 | 2324.62 |
| 3 | 2739.05 | 8 | 2271.60 |
| 4 | 2616.49 | 9 | 2204.99 |
| 5 | 2498.76 | 10 | 2152.28 |

The steepest drop occurs from k=1 to k=3. After k=3, reductions in inertia become gradual, confirming k=3 as the optimal choice.

### Cluster Summary

| Feature | Cluster 0 | Cluster 1 | Cluster 2 |
|---------|-----------|-----------|-----------|
| Size | 108 employees | 51 employees | 121 employees |
| Age | 35.98 | 34.82 | 36.25 |
| Monthly_Income | $4,905.69 | $6,594.67 | $4,682.18 |
| Tenure_Months | 23.43 | 81.33 | 22.59 |
| Distance_From_Home_km | 26.76 | 14.73 | 8.50 |
| Commute_Time_Minutes | 70.69 | 42.47 | 26.74 |
| Job_Satisfaction | 3.06 | 3.39 | 3.54 |
| Work_Life_Balance | 3.24 | 3.53 | 2.95 |
| Training_Hours_Last_Year | 18.85 | 16.98 | 25.00 |
| Absences_Last_Quarter | 2.22 | 3.37 | 2.89 |
| Performance_Rating | 3.19 | 3.69 | 3.70 |
| Manager_Feedback_Score | 3.18 | 3.13 | 3.54 |
| Engagement_Score | 65.92 | 65.75 | 67.09 |

### Cluster Interpretation

**Cluster 0: Strained Commuters (108 employees)**
Long commutes (avg. 70.69 min), furthest from workplace (26.76 km), lowest job satisfaction (3.06), lowest performance ratings (3.19), short tenure (23 months). Highest attrition risk group.

**Cluster 1: Experienced High Earners (51 employees)**
Longest tenure (81.33 months, nearly 7 years), highest income ($6,595), strongest work-life balance (3.53), strong performance (3.69). Most stable and organizationally valuable segment.

**Cluster 2: High-Performing Locals (121 employees)**
Closest to workplace (8.50 km), shortest commutes (26.74 min), highest performance (3.70), highest training hours (25.00), strongest manager feedback (3.54). But lowest work-life balance (2.95) and lowest income ($4,682) — risk of burnout and disengagement.

---

## Business Recommendations

| Cluster | Strategy |
|---------|----------|
| Cluster 0: Strained Commuters | Offer remote work or flexible hours; provide manager check-ins, workload review, and early career development support before resignation occurs |
| Cluster 1: Experienced High Earners | Focus on recognition, succession planning, and mentoring programs; conduct stay interviews; protect institutional knowledge |
| Cluster 2: High-Performing Locals | Address work-life balance immediately; review compensation given strong performance output; make promotion pathways visible to prevent disengagement |

---

## Key Takeaways

- K-Means clustering successfully identified three meaningfully distinct employee segments, each with a different risk profile and set of HR needs.
- The Elbow Method is a practical but subjective tool for choosing k. The analyst must interpret the curve and consider business context alongside the mathematical signal.
- Feature scaling is essential before K-Means. Without it, high-magnitude features like `Monthly_Income` would dominate the distance calculations and distort the clusters.
- Clustering cannot prove causation. The fact that Cluster 0 has long commutes and low satisfaction does not prove commutes cause dissatisfaction — but it does identify a group that warrants closer HR attention.
- Cluster labels should never be used to make automated decisions about individual employees without human review.

---

## How to Replicate

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
cd MBAI5310G-AI-Programming-Clement-Yorke/Assignment_5
```

2. Launch Jupyter:

```bash
jupyter notebook
```

3. Open `notebooks/Assignment_5_TalentWorks.ipynb` and run all cells top to bottom (`Kernel -> Restart & Run All`).

The notebook is fully self-contained. All data files are included in the `data/` folder.

---

## Report

A full written report with business context, cluster analysis, visualizations with interpretations, business recommendations, limitations, and responsible AI discussion is available as a PDF:

`reports/Assignment_5_TalentWorks_Report.pdf`
