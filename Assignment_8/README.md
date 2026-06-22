# Assignment 8: NLP Pipeline and Text Classification

**Course:** MBAI 5310G – AI Programming  
**Student:** Clement Kwesi Yorke  

---

## Dataset Description

**File:** `data/NLP_Dataset_2.xlsx`  
**Records:** 120  
**Columns:** 9

This dataset contains synthetic customer support tickets for NorthStar Telecom. Each row represents one inbound support message submitted across five channels (Email, Chat, Call Center, Mobile App, Web Form). Features include ticket metadata (TicketID, TicketDate, Source, City, PlanType, CustomerType, Priority) and the raw message text used as the NLP input.

---

## Target Variable

`IssueCategory` — Six-class text classification label  
- Billing  
- Internet_Service  
- Mobile_App  
- Technical_Support  
- Account_Access  
- Cancellation  

**Class distribution:** Perfectly balanced — 20 records per class. No class imbalance handling required.

---

## NLP Pipeline

**Text column:** `MessageText`  
**Preprocessing steps applied:**

1. **Lowercasing** — normalise text to remove case sensitivity
2. **Punctuation removal** — strip non-alphabetic characters using regex
3. **Tokenization** — split text into individual tokens using `nltk.word_tokenize`
4. **Stopword removal** — remove common filler words (NLTK English stopword list)
5. **Lemmatization** — reduce words to their base dictionary form using `WordNetLemmatizer`

**Feature extraction:** TF-IDF vectorization (`max_features=500`, `ngram_range=(1,2)`) — fitted on training data only to prevent data leakage.

---

## Model Used

**Logistic Regression** (scikit-learn)  
- Train/test split: 80% training (96 tickets), 20% testing (24 tickets)  
- `stratify=y` used to ensure proportional class representation in both splits  
- `max_iter=1000`, `random_state=42`, `C=1.0`

---

## Main Evaluation Results

| Metric | Score |
|---|---|
| Accuracy | 100% |
| Precision (macro avg) | 1.00 |
| Recall (macro avg) | 1.00 |
| F1-Score (macro avg) | 1.00 |

All six categories achieved perfect scores on the 24-sample test set.

> **Note:** 100% accuracy is expected for a synthetic, template-based dataset with consistent and distinctive vocabulary per category. Realistic accuracy on real customer support messages would be in the range of **75–90%**.

---

## Main Business Interpretation

The model predicts the `IssueCategory` of each incoming NorthStar Telecom customer support message, enabling automatic ticket routing to the appropriate support team.

**Priority metric — Recall:** For this use case, recall is more critical than precision. A missed classification (ticket routed to the wrong team) delays resolution and risks customer churn, particularly for Billing and Account_Access. A false alarm (incorrect team receives the ticket) is correctable with lower cost.

**Key limitation:** The dataset is synthetic and template-based. Real customer messages contain spelling errors, abbreviations, mixed issues, and informal language. The model requires retraining on real, labelled data before production deployment.

---

## Responsible AI Reflection

- **Channel bias:** Customers using Call Center may use different language patterns than those submitting typed messages, leading to uneven performance across customer groups.
- **Language and literacy bias:** Customers writing in fragmented English or mixing languages may receive lower classification accuracy.
- **Human oversight:** A confidence-threshold system is recommended — tickets exceeding 90% predicted probability are auto-routed; lower-confidence tickets are flagged for manual review.
- **PII handling:** Customer messages may contain names, account numbers, and payment details. All production pipelines must include PII detection and redaction before model training or retraining.

---

## Repository Structure

```
Assignment_8/
├── data/
│   └── NLP_Dataset_2.xlsx
├── notebooks/
│   └── Assignment_8_NLP_Pipeline.ipynb
├── reports/
│   └── Assignment_8_NLP_Pipeline_Report.docx
│   └── Assignment_8_NLP_Pipeline_Report.pdf
└── README.md
```
