## DataSprint 2026: Strathmore Data Community × iLab Africa

Predicting financial outcomes for Kenyan adults using the 2024 FinAccess Household Survey.


## The Task

Build a multiclass classification model that predicts whether a Kenyan adult's financial situation has **Improved**, **Stayed the same**, or **Worsened** compared to the previous year.

**Evaluation metric:** Weighted F1-Score (not accuracy).

---

## Repo Structure

```
datasprint2026/
├── finaccess2024_datasprint.xlsx     # Raw dataset, modify after asking
├── finaccess2024_clean.csv           # Cleaned dataset: use this for modelling
├── EDA_Cleaning.ipynb                # Completed: EDA & Cleaning
├── Modelling.ipynb                   # To do
├── README.md
```

---

## What Has Been Done (Paul)

The EDA and Cleaning notebook is complete and fully executed. It covers:

- Data inspection and descriptive statistics
- Cleaning: quotes/spaces in `education_level`, missing values in `barriers_bank`, duplicates, junk rows
- 13 charts covering target distribution, demographics, geography, income, financial health, behaviour, and correlations
- Clean dataset exported as `finaccess2024_clean.csv` — 20,857 rows, 28 columns, zero missing values

Key findings are documented inside the notebook with actual numbers.



## What Still Needs to Be Done

**Jimmy: Modelling** (`Modelling.ipynb`):
- Load `finaccess2024_clean.csv`
- Preprocess: encode categoricals, apply `log1p()` to `monthly_income`, scale numerics
- Train/test split with `test_size=0.2, random_state=42, stratify=y`
- Train at least one model — start with Logistic Regression or Decision Tree
- Evaluate using Weighted F1-Score, classification report, and confusion matrix
- Extract feature importances

**Jerry: Interpretation & Slides**:
- Use feature importances to answer the guiding question
- Build the 7-slide per the required structure

---

**Some Notes for Modeling**

| Item | Detail |
|---|---|
| Target column | `financial_status` — Worsened / Stayed the same / Improved |
| Class imbalance | 52.6% / 26.9% / 20.5% — use `class_weight='balanced'` |
| `monthly_income` | Apply `np.log1p()` — heavily right skewed |
| `barriers_bank` | Already filled with `'No barrier'` — encode as categorical |
| `barriers_mobile_money` | Already standardised to strings — encode as categorical |
| `household_size` | Consider binning into groups rather than using raw integer |
| Strong predictors (from EDA) | `experienced_shock`, `nfhi_11`, `nfhi_13`, `accessto_13k_1month`, `county` |
| Train/test split | Always use `stratify=y` because of class imbalance |



## Setup

```bash
pip install pandas numpy matplotlib seaborn scikit-learn openpyxl
```

Place both data files in the same folder as the notebooks before running.



## Data Source

2024 FinAccess Household Survey: Central Bank of Kenya, KNBS, FSD Kenya.
Kaggle: https://www.kaggle.com/datasets/davidpbriggs/kenya-finaccess-household-survey-2024