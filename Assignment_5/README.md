# Assignment 5: Clustering and Employee Segmentation

**Course:** MBAI 5310G-001 - AI Programming  
**Institution:** Ontario Tech University  
**Lecturer:** Zahra Atf  
**Student:** Clement Yorke

---

## Folder Structure

```
Assignment_5/
├── notebooks/
│   └── Assignment_5_TalentWorks.ipynb
├── data/
│   └── talentworks_employee_attrition_dataset.xlsx
├── reports/
│   └── Assignment_5_TalentWorks_Report.docx
└── README.md
```

---

## Business Problem

TalentWorks People Analytics is an HR analytics consulting unit supporting mid-sized service and retail organizations. The business has observed increasing employee turnover across departments. Replacing employees is costly, requiring time and money for hiring, onboarding, and training. The goal is to use unsupervised machine learning to segment employees into meaningful groups based on workplace experience, satisfaction, and performance, enabling targeted retention strategies.

---

## Dataset

**File:** `talentworks_employee_attrition_dataset.xlsx`  
**Records:** 286 employees (280 after cleaning)  
**Features:** 23 columns including Age, Monthly_Income, Tenure_Months, Job_Satisfaction, Work_Life_Balance, Engagement_Score, Performance_Rating, and more.  
**Note:** Dataset contains intentional missing values and duplicate rows for data cleaning practice.

---

## Clustering Method

- **Algorithm:** K-Means Clustering
- **Features used:** 12 numerical features (Age, Monthly_Income, Tenure_Months, Distance_From_Home_km, Commute_Time_Minutes, Job_Satisfaction, Work_Life_Balance, Training_Hours_Last_Year, Absences_Last_Quarter, Performance_Rating, Manager_Feedback_Score, Engagement_Score)
- **Scaling:** StandardScaler applied before clustering
- **Number of clusters:** k=3 (selected using the Elbow Method)

---

## Main Results

Three distinct employee segments were identified:

| Cluster | Label | Size | Key Characteristics |
|---------|-------|------|---------------------|
| 0 | Strained Commuters | 108 | Long commutes (avg. 70.69 min), lowest satisfaction and performance, highest attrition risk |
| 1 | Experienced High Earners | 51 | Highest income ($6,595), longest tenure (81 months), best work-life balance |
| 2 | High-Performing Locals | 121 | Short commutes (avg. 26.74 min), highest performance and training hours, lowest work-life balance |

---

## Business Recommendation

- **Cluster 0 (Strained Commuters):** Offer remote work or flexible hours; provide manager check-ins and early career development support.
- **Cluster 1 (Experienced High Earners):** Focus on recognition, succession planning, and knowledge transfer programs.
- **Cluster 2 (High-Performing Locals):** Address work-life balance and compensation gaps; make promotion pathways visible.

By segmenting employees with K-Means, TalentWorks can replace informal HR judgment with data-driven signals and allocate retention resources more effectively.
