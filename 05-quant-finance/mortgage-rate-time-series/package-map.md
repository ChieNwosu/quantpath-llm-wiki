# R Package Map — Mortgage Rate Time-Series Analysis

**Type**: Reference note
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[r-phase-2-plan]]

---

## Package-to-Use-Case Map

| Package | Primary Use in Phase 2 | Notes |
|---|---|---|
| `TSA` | ARIMA-style modeling, ACF/PACF plots, residual diagnostics | Core time-series modeling package; use for optional baseline forecasting |
| `tseries` | Stationarity testing — ADF test, KPSS test | Essential for Step 4 of Phase 2 plan |
| `uroot` | Seasonal unit-root testing (HEGY, OCSB tests) | Use if seasonal patterns are detected |
| `locfit` | Nonlinear smoothing, long-run trend visualization | Useful for visualizing the secular decline and rise in rates without assuming linearity |
| `leaps` | Variable selection for engineered affordability features | Use if building a regression model with multiple rate-derived features |
| `MTS` | Multivariate time-series modeling | Future extension — use if adding macro variables (CPI, Fed Funds Rate, unemployment) |

---

## Supporting Packages (Not Course-Specific)

| Package | Use |
|---|---|
| `zoo` | Rolling statistics (rolling mean, rolling SD) |
| `xts` | Time-series data structures |
| `ggplot2` | Visualization |
| `dplyr` | Data manipulation |
| `lubridate` | Date parsing and manipulation |
| `readr` | CSV import |

---

## Installation

```r
install.packages(c("TSA", "tseries", "uroot", "locfit", "leaps", "MTS",
                   "zoo", "xts", "ggplot2", "dplyr", "lubridate", "readr"))
```

---

## Package Notes

- `TSA` is the Cryer & Chan textbook package — commonly used in applied time-series courses.
- `uroot` provides seasonal unit-root tests not available in `tseries`.
- `locfit` is less commonly taught but useful for visualizing nonlinear trends without overfitting.
- `MTS` is the multivariate extension of `TSA` — defer until Phase 2 is complete and macro variables are added.

---

## Related Notes

- [[r-phase-2-plan]]
- [[stationarity-testing]]
- [[rolling-volatility]]
- [[rate-regimes]]
