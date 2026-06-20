# Model Comparison

## Overview

Three regression models were built to explain monthly store sales. The goal is to identify which factors are most strongly associated with sales and which model is most useful for business decision-making.

---

## Model 1: Simple Regression — Marketing Spend

| Item | Detail |
|------|--------|
| **Model name** | Simple: Marketing Spend |
| **Dependent variable** | `monthly_sales` |
| **Independent variables** | `marketing_spend` |
| **R-squared** | 0.1672 |
| **Adjusted R-squared** | 0.1646 |
| **Significant variables** | `marketing_spend` (p < 0.001) |

### Business usefulness

Marketing spend is positively associated with sales — each additional $1 in marketing is linked to roughly $2.13 in sales. However, the model explains only **16.7%** of sales variation, so marketing alone is an incomplete picture. Useful as a directional signal but not sufficient for planning.

### Limitations

- Ignores footfall, inventory, store type, and regional differences.
- Does not account for diminishing returns on marketing spend.
- Low explanatory power limits forecasting accuracy.

---

## Model 2: Simple Regression — Footfall

| Item | Detail |
|------|--------|
| **Model name** | Simple: Footfall |
| **Dependent variable** | `monthly_sales` |
| **Independent variables** | `footfall` |
| **R-squared** | 0.7363 |
| **Adjusted R-squared** | 0.7355 |
| **Significant variables** | `footfall` (p < 0.001) |

### Business usefulness

Footfall is the strongest single predictor — each additional visitor is associated with roughly **$35.68** in monthly sales. The model explains **73.6%** of variation, making it far more useful than marketing spend alone for understanding sales drivers.

### Limitations

- Still ignores marketing effectiveness, inventory levels, and store characteristics.
- Footfall may be influenced by external factors (location, seasonality) not captured here.
- Does not distinguish between high-value and low-value visitors.

---

## Model 3: Multiple Regression — Full Model (Final Model)

| Item | Detail |
|------|--------|
| **Model name** | Multiple: Full Model |
| **Dependent variable** | `monthly_sales` |
| **Independent variables** | `marketing_spend`, `footfall`, `inventory_availability_pct`, `avg_discount_pct`, region dummies (North, South, West), store type dummies (High Street, Mall, Residential) |
| **R-squared** | 0.8276 |
| **Adjusted R-squared** | 0.8218 |
| **Significant variables (p < 0.05)** | `marketing_spend`, `footfall`, `inventory_availability_pct`, `region_South`, `region_West`, `stype_High Street`, `stype_Residential` |

### Business usefulness

This is the **most useful model** for decision-making. It explains **82.8%** of sales variation by combining operational drivers (footfall, inventory, marketing) with structural factors (region and store type). Leadership can use it to:

- Prioritize footfall-driving initiatives
- Evaluate marketing ROI alongside other levers
- Understand regional and store-type performance gaps
- Set realistic sales targets by store profile

### Limitations

- `avg_discount_pct` is not significant (p = 0.235) — discounting may not drive sales as expected in this dataset.
- `region_North` and `stype_Mall` are not significant at 5%.
- Condition number suggests some multicollinearity among predictors.
- Does not include seasonality, competitor effects, or staff count.
- Association does not prove causation.

---

## Side-by-Side Comparison

| Model | Variables | R-squared | Key Insight |
|-------|-----------|-----------|-------------|
| Simple: Marketing Spend | 1 numerical | 0.167 | Weak standalone predictor |
| Simple: Footfall | 1 numerical | 0.736 | Strong single driver |
| **Multiple: Full Model** | 4 numerical + 7 dummies | **0.828** | **Best overall — selected as final model** |

---

## Final Model Selection

**Selected model:** Multiple Regression — Full Model

**Reason:** Highest R-squared (0.828), includes both operational and structural factors, and provides actionable coefficient estimates for multiple business levers. Simple models are useful for intuition but miss important context that leadership needs for resource allocation.

See `outputs/regression_summary.xlsx` and `screenshots/model_comparison_preview.png` for tabular evidence.
