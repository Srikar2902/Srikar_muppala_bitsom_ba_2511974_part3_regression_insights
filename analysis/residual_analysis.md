# Residual Analysis

## Method

Using the **final multiple regression model** (R² = 0.828), predicted monthly sales were calculated for all 320 store-month records. Residuals were computed as:

**Residual = Actual monthly_sales − Predicted monthly_sales**

- **Positive residual** → model under-predicted (store sold more than expected)
- **Negative residual** → model over-predicted (store sold less than expected)

---

## Largest Positive Residuals (Model Under-Predicted)

| Store | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|-------|--------|------------|--------------|-----------------|----------|
| STR-1073 | East | Residential | $813,317 | $702,328 | +$110,988 |
| STR-1028 | East | Mall | $713,611 | $606,503 | +$107,108 |
| STR-1026 | East | Mall | $625,514 | $526,671 | +$98,843 |
| STR-1050 | North | Residential | $735,787 | $636,997 | +$98,789 |
| STR-1019 | East | Residential | $788,088 | $690,047 | +$98,041 |

### Business interpretation

These stores **outperformed** what the model expected based on their marketing spend, footfall, inventory, region, and store type. Possible explanations:

1. **Local market strength** — East region stores dominate this list; there may be unmeasured East-region advantages (demographics, local partnerships).
2. **Mall and Residential formats** — several outperformers are Mall or Residential stores that may benefit from location-specific traffic patterns not fully captured by footfall alone.
3. **Operational excellence** — staff performance, merchandising, or customer service may exceed what inventory and marketing metrics suggest.
4. **Temporary demand spikes** — holiday effects or local events not modeled may have boosted sales.

Leadership should study these stores for **replicable best practices** rather than assuming the model is wrong.

---

## Largest Negative Residuals (Model Over-Predicted)

| Store | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|-------|--------|------------|--------------|-----------------|----------|
| STR-1017 | West | High Street | $685,379 | $852,088 | −$166,709 |
| STR-1023 | South | Mall | $627,172 | $763,599 | −$136,427 |
| STR-1012 | West | Residential | $595,468 | $724,345 | −$128,877 |
| STR-1007 | West | Mall | $800,452 | $911,201 | −$110,749 |
| STR-1014 | West | High Street | $463,534 | $563,910 | −$100,376 |

### Business interpretation

These stores **underperformed** relative to model expectations. Possible explanations:

1. **West region underperformance** — four of five largest negative residuals are West-region stores, suggesting regional challenges (competition, economic conditions) not fully captured by dummy variables.
2. **High Street format struggles** — STR-1017 and STR-1014 are High Street stores with large negative residuals; street-level retail may face headwinds in certain locations.
3. **Execution gaps** — high footfall or marketing spend may not translate to sales due to poor in-store execution, stockouts, or staffing issues.
4. **Competitive pressure** — nearby competitors may be capturing demand despite favorable store metrics.

These stores warrant **operational review** — the model suggests they should be performing better.

---

## Under-Prediction vs Over-Prediction Patterns

| Pattern | Observation |
|---------|-------------|
| **Under-predicting** | Primarily **East** region, **Mall** and **Residential** store types |
| **Over-predicting** | Primarily **West** region, **High Street** and **Mall** formats |
| **Regional bias** | Model may not fully capture West-region headwinds or East-region advantages |
| **Store type bias** | Residential stores in East outperform; West High Street stores underperform |

---

## Model Fit Assessment

| Metric | Value |
|--------|-------|
| Mean residual | Near zero (OLS property) |
| R-squared | 0.828 |
| Largest positive residual | +$110,988 (~16% above prediction) |
| Largest negative residual | −$166,709 (~20% below prediction) |

The model fits well overall but has systematic patterns in residuals by region and store type. This suggests **additional regional or format-specific variables** (competition intensity, local demographics) could improve future models.

---

## Evidence

See `analysis/regression_workbook.xlsx` (predictions_residuals sheet) and `screenshots/residuals_preview.png`.
