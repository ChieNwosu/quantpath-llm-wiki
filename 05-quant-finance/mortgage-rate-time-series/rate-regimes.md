# Rate Regimes

**Summary**: Distinct historical periods characterized by a consistent direction or level of mortgage rates — used to contextualize current rates and analyze affordability by era.
**Type**: Atomic note
**Sources**: (source: r-phase-2-plan)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

A rate regime is a period during which mortgage rates exhibit a consistent pattern — rising, falling, high, or low. Regime analysis segments the historical rate series into meaningful periods for comparison and context.

---

## Why It Matters

- The current rate environment only makes sense in historical context.
- Affordability, purchasing power, and refinance behavior differ dramatically across regimes.
- Regime analysis answers: "Is this rate high or low by historical standards?"

---

## Historical Mortgage Rate Regimes (Approximate)

| Period | Regime | Approximate Rate Range |
|---|---|---|
| 1971–1981 | Rising | 7% → 18% |
| 1981–1986 | Falling from peak | 18% → 10% |
| 1986–2000 | Moderate, volatile | 7% → 11% |
| 2000–2012 | Gradual decline | 8% → 3.5% |
| 2012–2021 | Historic lows | 3% → 4% |
| 2022–2023 | Rapid rise | 3% → 7%+ |
| 2024–present | Elevated, uncertain | 6%–7% range |

*Approximate — verify against actual MORTGAGE30US data.*

> **Note**: Historical rate-regime labels in this note are preliminary. Final regime boundaries should be recalculated from the MORTGAGE30US dataset during Phase 2 R analysis.

---

## Analytical Approach in R

1. Define regime boundaries (manually or algorithmically)
2. Label each observation with its regime
3. Calculate summary statistics by regime (mean rate, volatility, affordability)
4. Visualize regime transitions on the rate history chart

```r
# Simple manual regime labeling
mortgage_df <- mortgage_df %>%
  mutate(regime = case_when(
    date < as.Date("1981-01-01") ~ "Rising",
    date < as.Date("2012-01-01") ~ "Declining",
    date < as.Date("2022-01-01") ~ "Historic Low",
    TRUE ~ "Elevated"
  ))
```

---

## Connection to Phase 2

Rate-regime analysis is Step 6 in the [[r-phase-2-plan]]. It provides the historical context layer that the Excel workbook lacks.

---

## Related Notes

- [[rolling-volatility]]
- [[stationarity-testing]]
- [[purchasing-power-erosion]]
- [[r-phase-2-plan]]
- [[package-map]]
