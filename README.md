# Student Academic Performance Analysis
**Exploratory Data Analysis & BI Dashboard | Python · Power BI · Pandas**

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)](https://python.org)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat-square)](https://powerbi.microsoft.com)
[![Pandas](https://img.shields.io/badge/Pandas-EDA-green?style=flat-square)](https://pandas.pydata.org)

> **Note:** This is a standalone portfolio project focused on EDA and BI dashboarding.
> It is distinct from the [RIT Student Churn Prediction](./README_RIT_Churn_Prediction.md)
> project, which was a supervised ML engagement with Rochester Institute of Technology.

---

## 1. Business Problem

School administrators and curriculum leads often make resource allocation decisions — which subjects to invest in, which teachers to support, which assessment formats to prioritise — based on intuition rather than data. This project asks:

> *"Which combination of factors — subject type, teacher assignment, student demographics, or assessment format — most strongly predicts academic outcomes? And what should a department head do differently based on what the data shows?"*

The goal is an interactive Power BI dashboard that lets non-technical decision-makers explore performance drivers by cohort, subject, and assessment type without needing to run queries.

---

## 2. Data

| Dimension | Fields | Notes |
|-----------|--------|-------|
| Student demographics | Age, gender, socioeconomic band | Anonymised |
| Academic results | Scores by subject, term, assessment type | Formative vs summative |
| Teacher assignment | Teacher ID, subject, class size | De-identified |
| Assessment metadata | Type (formative/summative), weight, timing | Per academic term |

**Data preparation steps:**
- Standardised score scales across subjects (some marked out of 50, others out of 100) → converted to % for comparability
- Removed records with > 3 missing assessment scores (< 4% of dataset)
- Created derived variables: `grade_band` (A/B/C/D/F), `assessment_type_flag`, `socioeconomic_quintile`
- Verified no systematic missingness by demographic group (important for bias checking)

---

## 3. Approach

```
Raw student records (scores, demographics, teacher, assessment)
        ↓
Data cleaning & standardisation (Pandas)
        ↓
Feature creation — grade bands, assessment type flag, socioeconomic quintile
        ↓
EDA — distribution plots, correlation matrix, group comparisons
        ↓
Hypothesis testing — ANOVA across teacher groups, t-test formative vs summative
        ↓
Power BI dashboard — slicers: cohort, subject, gender, assessment type
        ↓
Written recommendations for department leadership
```

---

## 4. Key Findings

### Finding 1 — Assessment format is the strongest predictor of grade variance
Assessment type (formative vs summative) explained **more grade variance** than subject area, teacher assignment, or student demographic group. Students assessed primarily through formative methods scored 18 percentage points higher on average than equivalent cohorts assessed through summative exams alone.

**Implication:** A curriculum shift toward more frequent formative checkpoints — rather than high-stakes end-of-term exams — is likely to improve overall grade distribution more than changing teacher assignments or subject content.

### Finding 2 — Teacher effect is real but concentrated
The teacher effect was statistically significant (ANOVA, p < 0.05) but concentrated: the top-quartile teachers outperformed median teachers by 11 percentage points. The *bottom quartile* showed no statistically significant difference from median — suggesting underperformance is diffuse rather than caused by a small number of outlier teachers.

**Implication:** Targeted support for mid-range teachers (not just underperformers) may have the highest return on investment.

### Finding 3 — Socioeconomic quintile interacts with assessment type
The performance gap between socioeconomic quintile 1 and quintile 5 was **2.3× larger** in summative-assessment-heavy subjects than in formative-heavy subjects. Students from lower socioeconomic backgrounds appear to benefit disproportionately from continuous assessment formats.

### Finding 4 — Class size threshold effect
No significant performance difference was found between class sizes of 20–35. However, classes above **36 students** showed a consistent 7-point grade drop, suggesting a threshold effect rather than a linear relationship.

---

## 5. Power BI Dashboard Features

The dashboard (`student_performance.pbix`) includes:

| Page | Content |
|------|---------|
| Overview | Grade distribution by cohort, key KPIs (avg score, pass rate, top/bottom subject) |
| By Subject | Score distribution per subject, formative vs summative split |
| By Teacher | Anonymised teacher performance ranking, class size overlay |
| By Demographics | Gender, socioeconomic band filters; assessment type interaction |
| Trend | Term-on-term grade movement per cohort |

All slicers are cross-filtering — selecting a demographic filters every chart simultaneously.

---

## 6. Recommendations

| Priority | For | Recommendation |
|----------|-----|---------------|
| High | Curriculum leads | Increase formative assessment weighting to ≥ 50% per subject — largest predicted impact on grade improvement |
| High | Equity leads | Prioritise formative reforms in subjects with highest socioeconomic grade gaps |
| Medium | HR / Department heads | Focus teacher development on mid-range performers, not only bottom quartile |
| Medium | Facilities | Cap class sizes at 35 — above this threshold is where performance impact becomes detectable |
| Low | Data team | Standardise all assessment scoring to percentage at point of entry — reduces cleaning overhead significantly |

---

## 7. Files in This Repository

```
├── Student-Performance-Analysis.pdf    # Full analysis report (slides)
├── notebooks/
│   ├── 01_cleaning.ipynb               # Data prep and standardisation
│   ├── 02_eda.ipynb                    # Exploratory analysis and charts
│   └── 03_hypothesis_testing.ipynb     # ANOVA, t-tests
├── dashboard/
│   └── student_performance.pbix        # Power BI dashboard file
└── README.md
```

---

## 8. Tools & Libraries

| Tool | Use |
|------|-----|
| Pandas / NumPy | Data cleaning, feature engineering |
| Matplotlib / Seaborn | EDA plots, correlation heatmaps |
| SciPy (stats) | ANOVA, t-tests for significance testing |
| Power BI (DAX) | Interactive dashboard, cross-filtering slicers |

---

## 9. How to Run

```bash
# Clone repository
git clone https://github.com/jamesenet/My-Portfolio-

# Install Python dependencies
pip install pandas numpy matplotlib seaborn scipy

# Run notebooks in order
jupyter notebook notebooks/01_cleaning.ipynb
```

Open `dashboard/student_performance.pbix` in Power BI Desktop to explore the dashboard.

---

## How This Differs from the RIT Churn Project

| | This project | RIT Churn Prediction |
|---|---|---|
| **Type** | Portfolio / EDA + BI | Internship / Supervised ML |
| **Focus** | What drives academic performance? | Which students will drop out? |
| **Methods** | EDA, hypothesis testing, dashboarding | ETL pipeline, Random Forest, classification |
| **Output** | Power BI dashboard for department heads | Predictive model + stakeholder report |
| **Client** | Self-directed | Rochester Institute of Technology & Excelerate |

---

*Case study by Cornelius Enetomhe · [LinkedIn](https://www.linkedin.com/in/cornelius-enetomhe-01688a266/) · [Portfolio](https://jamesenet.github.io/CorneliusEnetomhe.github.io/)*
