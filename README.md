# Student Performance Analysis & Churn Prediction
**Rochester Institute of Technology (RIT) × Excelerate | Dec 2025 – Jan 2026**

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)](https://python.org)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat-square)](https://powerbi.microsoft.com)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?style=flat-square)](https://scikit-learn.org)

---

## 1. Business Problem

Rochester Institute of Technology wanted to reduce student withdrawal rates across its online programmes. The challenge: **by the time a student dropped out, it was already too late to intervene.** The institution needed a way to identify at-risk students 6–8 weeks *before* withdrawal, giving academic advisors a practical window to offer support.

> *"Can we predict which students are likely to disengage before they formally withdraw — and which factors drive that risk?"*

---

## 2. Data

| Source | Description | Size |
|--------|-------------|------|
| Enrolment records | Student registration, programme, cohort year | 3 cohort years |
| LMS activity logs | Login frequency, assignment submissions, forum posts | Weekly cadence |
| Assessment results | Grades across early and mid-term checkpoints | Per student/module |
| Outcome labels | Graduated, withdrawn, ongoing | Binary churn label |

**Data challenges addressed:**
- Missing LMS data for students who disengaged early (imputed using median by programme-cohort)
- Inconsistent outcome labelling across cohort years (standardised to binary: `churned` / `retained`)
- Class imbalance (~23% churn rate) — addressed with SMOTE oversampling during training

---

## 3. Approach

```
Raw enrolment + LMS data
        ↓
ETL & data wrangling (Pandas)
        ↓
Feature engineering (engagement score, early grade delta, submission rate)
        ↓
Exploratory data analysis (Seaborn, Matplotlib)
        ↓
Model training — Logistic Regression, Random Forest, Gradient Boosting
        ↓
Evaluation — Accuracy, Precision, Recall, F1, AUC-ROC
        ↓
Best model: Random Forest → 89% accuracy
        ↓
Power BI dashboard for academic leadership
```

**Feature engineering highlights:**
- `submission_rate_wk4` — % of assignments submitted by week 4 (strongest single predictor)
- `login_delta_wk2_wk4` — change in weekly login frequency between weeks 2–4
- `early_grade_z` — z-score of first assessment grade relative to cohort
- `forum_engagement_bin` — binary flag: any forum participation in first 3 weeks

---

## 4. Key Findings

- **89% model accuracy** (Random Forest, 5-fold cross-validation, AUC = 0.91)
- **Three features explain 74% of churn variance:**
  1. Assignment submission rate by week 4
  2. LMS login frequency drop (week 2 → week 4)
  3. First assessment score relative to cohort mean
- Students with submission rate < 60% by week 4 churned at **3.4× the baseline rate**
- Programme type mattered: async-only programmes showed 40% higher churn vs hybrid
- Early intervention flag: students scoring ≥2 risk factors by week 4 had 78% churn probability

---

## 5. Recommendations

| Priority | Recommendation | Expected Impact |
|----------|---------------|-----------------|
| High | Auto-flag students hitting ≥2 risk factors at week 4 for advisor outreach | Reduce churn ~15–20% |
| High | Add a mandatory check-in prompt for students with 0 forum activity at week 2 | Improve early engagement |
| Medium | Redesign async-only modules to include at least one synchronous touchpoint | Address programme-type gap |
| Low | Rebalance cohort-level grading benchmarks to reduce early-assessment anxiety | Reduce grade-shock exits |

---

## 6. Files in This Repository

```
├── notebooks/
│   ├── 01_eda.ipynb              # Exploratory data analysis
│   ├── 02_feature_engineering.ipynb
│   └── 03_modelling.ipynb        # Model training & evaluation
├── reports/
│   └── Student-Performance-Analysis.pdf   # Full slide report
├── dashboard/
│   └── student_kpi_dashboard.pbix         # Power BI file
└── README.md
```

---

## 7. Tools & Libraries

| Tool | Use |
|------|-----|
| Python 3.10 | Core analysis language |
| Pandas / NumPy | Data wrangling, feature engineering |
| Scikit-learn | Model training, evaluation, SMOTE |
| Matplotlib / Seaborn | EDA visualisation |
| Power BI | Executive KPI dashboard |

---

## 8. How to Run

```bash
# Clone the repository
git clone https://github.com/jamesenet/My-Portfolio-

# Install dependencies
pip install pandas numpy scikit-learn matplotlib seaborn imbalanced-learn

# Run notebooks in order
jupyter notebook notebooks/01_eda.ipynb
```

---

*Case study by Cornelius Enetomhe · [LinkedIn](https://www.linkedin.com/in/cornelius-enetomhe-01688a266/) · [Portfolio](https://jamesenet.github.io/CorneliusEnetomhe.github.io/)*
