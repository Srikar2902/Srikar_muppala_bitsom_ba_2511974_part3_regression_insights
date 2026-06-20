# Part 3: Regression-Based Business Insights & Model Interpretation

Regression analysis of monthly store sales for a retail chain. This repository identifies which operational and structural factors are most strongly associated with sales performance and delivers a data-supported business recommendation.

## Business Problem Summary

Leadership wants to understand what drives monthly sales across stores to support decisions on marketing spend, inventory investment, discounting strategy, staff allocation, and store format prioritization. Regression analysis was used to quantify associations between sales and controllable business factors.

## Dataset Description

| Attribute | Detail |
|-----------|--------|
| Source file | `data/business_regression_data.xlsx` |
| Records | 320 store-month observations |
| Stores | 80 unique stores |
| Time period | January – April 2025 |
| Granularity | One row per store per month |

### Variables

| Type | Variables |
|------|-----------|
| **Dependent** | `monthly_sales` |
| **Numerical (potential predictors)** | `marketing_spend`, `footfall`, `avg_discount_pct`, `staff_count`, `inventory_availability_pct`, `competitor_distance_km`, `holiday_flag`, `customer_rating` |
| **Categorical** | `region` (East, North, South, West), `store_type` (Airport, High Street, Mall, Residential) |
| **Identifiers / not for regression** | `store_id`, `month` |
| **Outcome (not used as predictor)** | `monthly_profit` — derived from sales, would create circularity |

### Data preparation

| Issue | Action |
|-------|--------|
| 6 missing `competitor_distance_km` | Median imputation |
| 8 missing `customer_rating` | Median imputation |
| No duplicate rows | No action needed |

## Regression Approach

1. **Exploratory review** — variable types, distributions, missing values
2. **Simple linear regression** — two models with one predictor each (`marketing_spend`, `footfall`)
3. **Dummy variable creation** — one-hot encoding for `region` and `store_type`
4. **Multiple regression** — combined numerical and dummy predictors
5. **Model comparison** — R-squared, significant variables, business usefulness
6. **Residual analysis** — predicted vs actual sales for the final model
7. **Business recommendation** — actionable insights with limitations

Analysis pipeline: `scripts/run_part3_regression.py`

## Dummy Variable Approach

| Categorical variable | Reference category | Dummy columns created |
|---------------------|-------------------|----------------------|
| `region` | **East** | `region_North`, `region_South`, `region_West` |
| `store_type` | **Airport** | `stype_High Street`, `stype_Mall`, `stype_Residential` |

One category per variable is dropped to avoid the dummy variable trap (perfect multicollinearity). Coefficients represent how much sales differ from the reference category, holding other predictors constant.

Details: `outputs/model_equations.md`

## Model Comparison Summary

| Model | Predictors | R-squared | Key Finding |
|-------|-----------|-----------|-------------|
| Simple: Marketing Spend | `marketing_spend` | 0.167 | Weak standalone predictor |
| Simple: Footfall | `footfall` | 0.736 | Strongest single driver |
| **Multiple: Full Model** | 4 numerical + 7 dummies | **0.828** | **Best model — selected as final** |

Full comparison: `analysis/model_comparison.md` | Table: `outputs/regression_summary.xlsx`

## Final Model Selected

**Multiple Regression — Full Model**

- **R-squared:** 0.828 (82.8% of sales variation explained)
- **Significant predictors:** `marketing_spend`, `footfall`, `inventory_availability_pct`, `region_South`, `region_West`, `stype_High Street`, `stype_Residential`
- **Not significant:** `avg_discount_pct`, `region_North`, `stype_Mall`

Equation and coefficient interpretation: `outputs/model_equations.md`

## Business Recommendation

1. **Prioritize footfall** — strongest sales driver ($33.85 per visitor)
2. **Improve inventory availability** — $2,916 per 1% improvement
3. **Allocate marketing strategically** — positive association but low standalone explanatory power
4. **Review Residential and High Street formats** — significantly lower sales vs Airport baseline
5. **Do not rely on discounting** — not statistically significant as a sales driver

Full memo: `outputs/final_recommendation.md`

## Assumptions and Limitations

1. Linear relationships between predictors and sales
2. Independent observations (store-months treated independently)
3. No major omitted variable bias — but competition, seasonality, and staff quality are not modeled
4. Multicollinearity among predictors (condition number ~1.1M)
5. 4-month window may not capture seasonal effects
6. **Association does not prove causation** — coefficients show statistical relationships, not guaranteed causal effects

Residual patterns suggest regional bias: model under-predicts East-region stores and over-predicts West-region stores. See `analysis/residual_analysis.md`.

## Screenshots Included

| File | Content |
|------|---------|
| `screenshots/simple_regression_output.png` | Simple regression (footfall) output table |
| `screenshots/multiple_regression_output.png` | Multiple regression full model output |
| `screenshots/residuals_preview.png` | Predicted values and largest residuals |
| `screenshots/model_comparison_preview.png` | Model comparison table |

## Tools Used

- **Python 3.9** — analysis pipeline (`scripts/run_part3_regression.py`)
- **pandas / openpyxl** — data preparation and Excel outputs
- **statsmodels** — OLS regression
- **matplotlib** — screenshot generation

## Reproduce All Outputs

```bash
pip install pandas openpyxl xlsxwriter matplotlib scipy statsmodels
python scripts/run_part3_regression.py
```

## Repository Structure

```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md
```

> **Note:** Rename the GitHub repository to `studentname_studentid_part3_regression_insights` before submission (e.g., `srikarmuppala_12345_part3_regression_insights`).
