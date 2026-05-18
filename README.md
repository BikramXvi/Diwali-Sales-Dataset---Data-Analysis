# Diwali Sales Data Analysis
### CC5061NI – Applied Data Science | London Metropolitan University

**Student:** Bikram Tamang | **ID:** 24046576 | **Semester:** Spring 2026

---

## Project Overview

This project presents a comprehensive data science analysis of the **Diwali Sales Transaction Dataset**, a retail/e-commerce dataset capturing customer purchase behaviour during the Diwali festive season in India. The analysis follows a full data science pipeline — from data understanding and cleaning through to statistical testing and business recommendations.

---

## Repository Structure

```
├── 24046576_Bikram_Tamang.ipynb   # Main analysis notebook
├── DiwaliSalesData_264932.csv     # Source dataset (latin-1 encoded)
├── figure1_distributions.png     # KDE distribution curves
├── figure2_correlation_heatmap.png
├── figure3_top5_states.png
├── figure4_gender_product.png
├── figure5_age_amount.png
├── figure6_marital_orders.png
├── figure7_grouped_bar.png
└── README.md
```

---

## Dataset

| Property | Detail |
|---|---|
| Source | Diwali Sales Transaction Dataset |
| Raw rows | 11,251 |
| Rows after cleaning | 11,239 |
| Columns | 15 (raw) → 12 (after cleaning) |
| Encoding | latin-1 (ISO-8859-1) |
| Target variable | `Amount` (total purchase value in INR) |

**Key columns:** `Gender`, `Age Group`, `Marital_Status`, `State`, `Zone`, `Occupation`, `Product_Category`, `Orders`, `Amount`

---

## Analysis Pipeline

### 1. Data Understanding
- Dataset structure inspection via `df.info()` and `df.dtypes`
- Memory usage analysis
- Data quality challenges identified: 12 missing values in `Amount`, two entirely null artefact columns (`Status`, `unnamed1`), unordered `Age Group` strings

### 2. Data Preparation & Cleaning
- **Ordinal encoding** of `Age Group` into five life-stage labels: `Teen < Youth < Adult < Senior < Elder` using `pd.Categorical(ordered=True)`
- **Feature engineering**: `Purchase_Value_Category` column (Low / Medium / High) derived from 33rd and 66th percentile thresholds using `pd.cut()`
- **Dropped columns**: `Cust_name` (privacy), `Status` and `unnamed1` (entirely null artefacts)
- **Missing value handling**: 12 rows dropped from `Amount` column (deletion chosen over imputation as Amount is the primary outcome variable)

### 3. Data Analysis
- Extended descriptive statistics including skewness and kurtosis for `Age`, `Orders`, and `Amount`
- KDE distribution plots for all numerical columns
- Pearson correlation matrix and heatmap across all numerical variables

### 4. Data Exploration (Visualisations)
| Figure | Description |
|---|---|
| Figure 3 | Top 5 States by Total Sales Amount |
| Figure 4 | Gender Distribution across Product Categories |
| Figure 5 | Average Purchase Amount by Age Group |
| Figure 6 | Marital Status Impact on Average Orders |
| Figure 7 | Average Amount by Zone – Top 6 Product Categories |

### 5. Statistical Testing

**ANOVA Test – Amount by Occupation**
- H₀: Mean Amount is equal across all occupation groups
- Result: F = 2.4771, p = 0.0017 → **Reject H₀**
- Conclusion: Spending differs significantly across occupation groups

**Chi-Square Test – Product_Category vs Zone**
- H₀: No association between Product_Category and Zone
- Result: χ² = 1634.97, df = 68, p < 0.0001 → **Reject H₀**
- Conclusion: Purchasing patterns vary significantly by geographic zone

---

## Key Findings

- **Top revenue states:** Uttar Pradesh, Maharashtra, and Karnataka
- **Highest spending age group:** 26–35 (Adult segment)
- **Gender:** Female customers dominate most product categories; males lead in Electronics & Gadgets
- **Highest value categories:** Auto and Electronics & Gadgets across all zones
- **Occupation:** Government employees record the highest average spend (INR 9,973); Construction workers the lowest (INR 8,690)

---

## Requirements

```bash
pip install pandas numpy matplotlib seaborn scipy
```

| Library | Purpose |
|---|---|
| `pandas` | Data manipulation and cleaning |
| `numpy` | Numerical operations |
| `matplotlib` | Base plotting |
| `seaborn` | Statistical visualisations and heatmap |
| `scipy.stats` | ANOVA and Chi-Square testing |

---

## How to Run

1. Clone this repository
2. Place `DiwaliSalesData_264932.csv` in the same directory as the notebook
3. Open `24046576_Bikram_Tamang.ipynb` in Jupyter Notebook or JupyterLab
4. Run all cells in order (`Kernel → Restart & Run All`)

> **Note:** The dataset must use `latin-1` encoding. The notebook loads it automatically with `pd.read_csv('DiwaliSalesData_264932.csv', encoding='latin-1')`.

---

