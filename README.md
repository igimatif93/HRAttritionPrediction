# Employee Attrition Prediction using Machine Learning

**Internship Project — Week 2**
**Author:** Shaik Atif Furkan

---

## Overview

This project uses machine learning to predict which employees are most likely to leave a company, and identifies the key factors driving attrition. Built on the IBM HR Analytics dataset of 1,470 employees, the goal is to give HR teams an early-warning system so they can act before valuable employees walk out the door.

---

## Repository Structure

```
Employee-Attrition-Prediction/
├── analysis.ipynb                        # Full notebook — all 7 tasks with outputs
├── WA_Fn-UseC_-HR-Employee-Attrition.csv # IBM HR Analytics dataset
├── summary.docx                          # Technical summary of findings
├── summary_HR_Director.docx              # Non-technical summary for HR leadership
├── charts/
│   ├── chart1_attrition_dept_role.png    # Attrition by Department & Job Role
│   ├── chart2_income_overtime.png        # Income box plot + Overtime impact
│   ├── chart3_confusion_matrix.png       # Confusion matrix — best model
│   ├── chart4_feature_importance.png     # Top 10 feature importances
│   └── chart5_roc_curve.png              # ROC curve comparing all 3 models
└── README.md
```

---

## Dataset

| Property | Value |
|---|---|
| Source | [IBM HR Analytics — Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset) |
| Rows | 1,470 employees |
| Columns | 35 features |
| Target | `Attrition` (Yes / No) |
| Class balance | 84% stayed, 16% left — **imbalanced** |

---

## Project Workflow (7 Tasks)

| Task | Description |
|---|---|
| **Task 1** | Data loading & exploration — shape, types, attrition rate, missing values |
| **Task 2** | Data cleaning & preprocessing — encoding, scaling, dropping constant columns |
| **Task 3** | Exploratory Data Analysis — attrition by dept, role, income, WLB, tenure |
| **Task 4** | Model building — Logistic Regression, Random Forest, Gradient Boosting |
| **Task 5** | Model evaluation — Precision, Recall, F1, ROC-AUC, confusion matrix, feature importance |
| **Task 6** | Visualization — 5 charts saved to `charts/` folder |
| **Task 7** | HR insights & business recommendations |

---

## Model Results

| Model | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|
| **Logistic Regression ✅ Best** | 0.341 | 0.617 | 0.439 | **0.799** |
| Random Forest | 0.375 | 0.064 | 0.109 | 0.752 |
| Gradient Boosting | 0.588 | 0.213 | 0.313 | 0.794 |

**Best model: Logistic Regression**

Logistic Regression achieved the highest ROC-AUC (0.799) and the best Recall (0.617) — meaning it correctly identified 61.7% of employees who actually left. For an HR attrition use-case, **Recall matters most**: missing someone about to leave is far more costly than a false alarm. Logistic Regression also wins on explainability — its coefficients can be directly interpreted by HR teams without a data science background.

---

## Top 10 Features Driving Attrition

| Rank | Feature | Importance |
|---|---|---|
| 1 | JobRole — Laboratory Technician | 0.798 |
| 2 | OverTime — Yes | 0.766 |
| 3 | BusinessTravel — Travel Frequently | 0.719 |
| 4 | Job Level | 0.659 |
| 5 | Total Working Years | 0.657 |
| 6 | JobRole — Sales Representative | 0.553 |
| 7 | BusinessTravel — Travel Rarely | 0.512 |
| 8 | EducationField — Life Sciences | 0.507 |
| 9 | Years Since Last Promotion | 0.500 |
| 10 | Department — Sales | 0.482 |

---

## Key EDA Findings

- **Sales Representatives** have a **39.8% attrition rate** — the highest of any role, nearly 2.5× the company average of 16.1%
- **Overtime employees** leave at **30.5%** vs **10.4%** for non-overtime staff — nearly 3× higher risk
- Employees who left earned **30% less on average** ($4,787/month vs $6,833), but salary ranked below overtime and job role in model importance
- Employees rating their **work-life balance at 1 (worst)** leave at **31.3%** — nearly double the company average
- **Early-tenure employees** (avg 5.1 years) leave more than those who stay (avg 7.4 years) — the critical retention window is the first 3–5 years

---

## HR Recommendations

1. **Introduce an Overtime Review Programme** — Flag any employee working overtime for 3+ consecutive months for a manager conversation about workload or team resourcing. Target: reduce overtime-linked attrition from 30.5% to below 15%.

2. **Launch a Sales Representative Retention Programme** — Implement structured check-ins at 90 and 180 days, with visible career pathways to Senior Sales Executive. Research Directors (2.5% attrition) demonstrate that career progression is a powerful retention anchor.

---

## Tools & Libraries

| Tool | Purpose |
|---|---|
| Python 3 | Programming language |
| Pandas | Data loading and cleaning |
| Scikit-learn | Model building and evaluation |
| Matplotlib / Seaborn | Charts and visualization |
| Jupyter Notebook | Development environment |

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/igimatif93/Employee-Attrition-Prediction.git
cd Employee-Attrition-Prediction

# 2. Install dependencies
pip install pandas scikit-learn matplotlib seaborn jupyter

# 3. Launch the notebook
jupyter notebook analysis.ipynb
```

Make sure `WA_Fn-UseC_-HR-Employee-Attrition.csv` is in the same folder as the notebook before running.

---

## Model Limitation

This model was trained on a single company's historical HR data and achieves ROC-AUC ~0.80, meaning roughly 20% of predictions will be wrong. It cannot capture factors outside the dataset — personal circumstances, team dynamics, management quality, or external job market conditions. HR teams should use model predictions as **one input among several**, not as the sole basis for intervention decisions.
