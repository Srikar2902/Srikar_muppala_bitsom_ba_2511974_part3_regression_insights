# Final Recommendation: Monthly Sales Drivers

**To:** Leadership Team  
**From:** Business Analytics  
**Date:** June 2026  
**Subject:** Regression Analysis — What Drives Monthly Store Sales?

---

## Executive Summary

Regression analysis of 320 store-month records (80 stores, Jan–Apr 2025) identifies **footfall**, **inventory availability**, and **marketing spend** as the strongest operational drivers of monthly sales. Store format and region also matter significantly. The recommended action is to **prioritize footfall-driving initiatives and inventory optimization** while reallocating marketing spend toward stores with the highest footfall potential.

---

## Which Factors Are Most Strongly Associated with Monthly Sales?

| Rank | Factor | Evidence | Strength |
|------|--------|----------|----------|
| 1 | **Footfall** | Coef = +$33.85/visitor, p < 0.001, R² = 0.736 alone | Very strong |
| 2 | **Inventory availability** | Coef = +$2,916 per 1%, p < 0.001 | Strong |
| 3 | **Marketing spend** | Coef = +$1.18 per $1, p < 0.001 | Moderate (in full model) |
| 4 | **Store type (Residential)** | Coef = −$38,860 vs Airport, p < 0.001 | Strong structural effect |
| 5 | **Region (South, West)** | Coef = +$18.9K and +$18.6K vs East, p < 0.05 | Moderate structural effect |

**Not significant:** `avg_discount_pct` (p = 0.235) — discounting does not appear to drive sales in this dataset.

---

## What Leadership Should Focus On

### 1. Drive footfall (highest priority)

Footfall is the dominant sales driver. Each 100 additional monthly visitors is associated with roughly **$3,385–$3,568** in additional sales. Actions:

- Improve store visibility and signage
- Run local promotions to attract walk-in traffic
- Optimize store locations and hours
- Partner with nearby businesses for cross-traffic

### 2. Improve inventory availability

Each 1% improvement in inventory availability is linked to **$2,916** more monthly sales. Actions:

- Reduce stockouts on high-demand items
- Improve supply chain forecasting
- Prioritize inventory investment in high-footfall stores

### 3. Allocate marketing spend strategically

Marketing is positively associated with sales (+$1.18 per $1 spent in the full model), but its standalone explanatory power is weak (R² = 0.167). Actions:

- Target marketing to stores with strong footfall potential
- Measure marketing ROI alongside footfall impact
- Avoid blanket marketing increases without footfall support

### 4. Review underperforming store formats

Residential stores (−$38,860 vs Airport) and High Street stores (−$22,300 vs Airport) sell significantly less after controlling for operational metrics. Actions:

- Evaluate whether Residential and High Street formats need format-specific strategies
- Study Airport store best practices for replication
- Consider format conversion or closure for persistently underperforming locations

---

## What Should NOT Be Over-Interpreted

| Variable | Why |
|----------|-----|
| **avg_discount_pct** | Not statistically significant (p = 0.235); increasing discounts may not boost sales and could erode margins |
| **customer_rating** | R² = 0.0007 in simple regression; customer satisfaction alone does not explain sales variation |
| **region_North** | Not significant (p = 0.232); North region effect is indistinguishable from East |
| **stype_Mall** | Not significant (p = 0.293); Mall format effect is unclear after controlling for other factors |

---

## Recommended Business Action

**Primary recommendation:** Launch a **footfall and inventory improvement program** across the store network, prioritizing:

1. Stores in South and West regions (positive regional coefficients)
2. Stores with high footfall potential but low inventory availability
3. Marketing spend increases only where footfall infrastructure can support additional traffic

**Secondary recommendation:** Conduct operational reviews at **West-region High Street stores** identified in residual analysis as underperforming relative to expectations.

**Do not recommend:** Blanket discount increases — the data does not support discounting as a sales driver.

---

## Risks and Limitations

1. **Association, not causation** — regression shows which variables move together with sales, but cannot prove that increasing footfall *causes* higher sales. External factors (seasonality, competition, local economy) may drive both.
2. **Limited time window** — 4 months of data may not capture seasonal patterns or long-term trends.
3. **Missing variables** — competitor intensity, staff quality, and local demographics are not modeled.
4. **Multicollinearity** — marketing spend and footfall may be correlated; individual coefficient estimates should be interpreted cautiously.
5. **Small sample for some segments** — Airport stores (28 records) serve as reference category with limited data.
6. **Residual patterns** — model systematically under-predicts East-region stores and over-predicts West-region stores, suggesting unmeasured regional factors.

---

## Why Regression Shows Association, Not Causation

Regression identifies **statistical relationships** — variables that tend to move together. It does **not** prove that changing one variable will cause sales to change because:

- **Confounding:** A third factor (e.g., store location quality) may drive both footfall and sales.
- **Reverse causation:** High sales may attract more footfall rather than footfall causing sales.
- **Omitted variables:** Unmeasured factors (competition, weather, local events) may explain the relationship.
- **Time dynamics:** This analysis uses cross-sectional/monthly data without tracking changes over time.

Leadership should use regression insights to **prioritize hypotheses for further testing** (e.g., pilot footfall initiatives and measure impact) rather than treating coefficients as guaranteed causal effects.

---

## Next Steps

1. Pilot footfall improvement program in 10 high-potential stores and measure sales impact over 3 months.
2. Audit inventory availability at stores with largest negative residuals.
3. Review marketing spend allocation — shift budget toward stores with strong footfall infrastructure.
4. Conduct qualitative review of East-region outperformers and West-region underperformers.
5. Build a follow-up model including seasonality and competitor distance as predictors.

---

*Supporting evidence: `outputs/regression_summary.xlsx`, `analysis/regression_workbook.xlsx`, `outputs/model_equations.md`, and screenshots in `screenshots/`.*
