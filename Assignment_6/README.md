# Assignment 6: Model Evaluation, Explainability, and Fairness Reflection

**Course:** MBAI 5310G – AI Programming  
**Student:** Clement Kwesi Yorke  

---

## Dataset Description

**File:** `data/event_registration_attendance_dataset.csv`  
**Records:** 380  
**Columns:** 17

This dataset contains event registration records. Each row represents one person who registered for an event. Features include demographic information (age), engagement behaviour (email reminders opened, social media clicks), logistics factors (distance to venue, days before event registered), and ticket details (type, price). Three group-related columns — `gender`, `age_group`, and `region` — are retained for fairness analysis but excluded from model input.

---

## Target Variable

`attended_event` — Binary classification label  
- `1` = Attended the event  
- `0` = Did not attend the event  

**Class distribution:** 233 attended (61.3%), 147 did not attend (38.7%) — mildly imbalanced.

---

## Model Used

**Decision Tree Classifier** (scikit-learn)  
- Final (controlled) model: `max_depth=4`  
- Preprocessing: `Pipeline` + `ColumnTransformer` with `SimpleImputer` + `OneHotEncoder` — fitted on training data only to prevent data leakage.

---

## Main Evaluation Results

| Metric | Score |
|---|---|
| Accuracy | 81.58% |
| Precision | 0.8235 |
| Recall | 0.8936 |
| F1-Score | 0.8571 |
| CV Mean Accuracy (5-fold) | 65.46% |
| CV Std Dev | 0.0181 |
| Training Accuracy | 83.88% |
| Testing Accuracy | 81.58% |

All metrics are reported for the **controlled tree (max_depth=4)** — the final model used for all evaluations.

> **Note:** The single-split test accuracy (81.6%) is significantly higher than the 5-fold cross-validation mean (65.5%). The CV score is the more conservative and reliable estimate of generalisation performance.

---

## Main Business Interpretation

This model predicts which event registrants are likely to show up on the day of the event, enabling event managers to plan capacity, catering, and staffing more accurately.

The most important predictive features are: **prior event attendance history**, **number of email reminders opened**, **calendar invite acceptance**, **distance to the venue**, and **ticket price**. These reflect that past behaviour and active pre-event engagement are the strongest signals of attendance.

The most costly model error is a **False Negative** — predicting "will not attend" when the person actually shows up — because under-preparing for actual attendees leads to direct customer dissatisfaction (no seats, insufficient materials). The model should be tuned to minimise False Negatives (higher Recall) in production settings.

SHAP analysis confirms that `previous_events_attended` and `email_reminders_opened` are consistently the dominant positive drivers across the test set. LIME provides individual-level explanations that allow event staff to understand and act on specific at-risk predictions.

---

## Fairness and Bias

The model's performance was evaluated across three group columns: `gender`, `region`, and `age_group`. Where disparities in accuracy or predicted positive rates are observed, the model should not be used to make autonomous decisions for those groups. All model outputs should serve as decision-support for human event managers, not as automated gatekeeping.

---

## Limitation

The dataset contains only **380 records**, which limits the reliability of the model — especially for sub-group fairness analysis where some groups may have fewer than 20 test records. The model should be retrained on a larger, more representative sample before any production deployment.
