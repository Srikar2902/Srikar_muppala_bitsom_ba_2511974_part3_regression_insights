# Model Equations

## Simple Regression Models

### Model 1: monthly_sales ~ marketing_spend

```
monthly_sales = 560,777.35 + 2.1296 × marketing_spend
```

| Component | Value | Interpretation |
|-----------|-------|----------------|
| Intercept | $560,777 | Baseline sales when marketing spend is zero |
| Coefficient | +2.13 | Each additional $1 in marketing spend is associated with $2.13 more in monthly sales |
| R-squared | 0.167 | Explains 16.7% of sales variation |
| P-value | < 0.001 | Statistically significant |

**Business meaning:** Marketing has a positive association with sales, but alone it explains little variation. A $10,000 increase in marketing is linked to roughly $21,300 more sales — but many other factors also matter.

---

### Model 2: monthly_sales ~ footfall

```
monthly_sales = 446,410.58 + 35.6780 × footfall
```

| Component | Value | Interpretation |
|-----------|-------|----------------|
| Intercept | $446,411 | Baseline sales when footfall is zero |
| Coefficient | +35.68 | Each additional store visitor is associated with $35.68 more in monthly sales |
| R-squared | 0.736 | Explains 73.6% of sales variation |
| P-value | < 0.001 | Statistically significant |

**Business meaning:** Footfall is the strongest single driver. Increasing store traffic by 100 visitors per month is associated with roughly $3,568 more in sales. Driving footfall should be a top priority.

---

## Multiple Regression Model (Final Model)

```
monthly_sales = 152,100
    + 1.1798 × marketing_spend
    + 33.8479 × footfall
    + 2,916.36 × inventory_availability_pct
    − 43,850 × avg_discount_pct
    + 8,467 × region_North
    + 18,870 × region_South
    + 18,570 × region_West
    − 22,300 × stype_High Street
    − 10,260 × stype_Mall
    − 38,860 × stype_Residential
```

| Variable | Coefficient | P-value | Direction | Business Meaning |
|----------|-------------|---------|-----------|------------------|
| Intercept | $152,100 | 0.001 | — | Baseline for reference categories (East, Airport) |
| marketing_spend | +1.18 | < 0.001 | Positive | Each $1 in marketing associated with $1.18 in sales (holding other factors constant) |
| footfall | +33.85 | < 0.001 | Positive | Each visitor associated with $33.85 in sales — strongest operational driver |
| inventory_availability_pct | +2,916 | < 0.001 | Positive | Each 1% improvement in inventory availability linked to $2,916 more sales |
| avg_discount_pct | −43,850 | 0.235 | Negative (not sig.) | Higher discounts weakly associated with lower sales — not statistically significant |
| region_North | +8,467 | 0.232 | Positive (not sig.) | North stores sell ~$8.5K more than East (reference), not significant |
| region_South | +18,870 | 0.009 | Positive | South stores sell ~$18.9K more than East |
| region_West | +18,570 | 0.004 | Positive | West stores sell ~$18.6K more than East |
| stype_High Street | −22,300 | 0.018 | Negative | High Street stores sell ~$22.3K less than Airport (reference) |
| stype_Mall | −10,260 | 0.293 | Negative (not sig.) | Mall stores sell ~$10.3K less than Airport, not significant |
| stype_Residential | −38,860 | < 0.001 | Negative | Residential stores sell ~$38.9K less than Airport |

**R-squared:** 0.828 | **Adjusted R-squared:** 0.822 | **N:** 320

---

## Dummy Variable Approach

### Region dummies

| Setting | Detail |
|---------|--------|
| Categorical variable | `region` (East, North, South, West) |
| Method | One-hot encoding with `drop_first=True` |
| **Reference category** | **East** |
| Dummy columns created | `region_North`, `region_South`, `region_West` |

When a dummy = 1, the store is in that region; when 0, it is in the reference region (East). Coefficients show how much sales differ from East-region stores, holding other variables constant.

### Store type dummies

| Setting | Detail |
|---------|--------|
| Categorical variable | `store_type` (Airport, High Street, Mall, Residential) |
| Method | One-hot encoding with `drop_first=True` |
| **Reference category** | **Airport** |
| Dummy columns created | `stype_High Street`, `stype_Mall`, `stype_Residential` |

Airport stores serve as the baseline. Negative coefficients for Residential (−$38,860) and High Street (−$22,300) indicate these formats generate substantially lower sales than Airport stores after controlling for operational metrics.

### Why drop one category?

Including all categories would create **perfect multicollinearity** (dummy variable trap) — the model could not uniquely estimate coefficients. Dropping one reference category allows all other categories to be interpreted relative to that baseline.

---

## Final Model Selected

**Model:** Multiple Regression — Full Model

**Reason for selection:**

1. Highest explanatory power (R² = 0.828 vs 0.167 and 0.736 for simple models)
2. Captures both operational levers (marketing, footfall, inventory) and structural factors (region, store type)
3. Provides actionable coefficients for multiple business decisions
4. Significant predictors align with intuitive business drivers

Simple models are useful for quick insights but miss critical context. The multiple model gives leadership a more complete picture for resource allocation.
