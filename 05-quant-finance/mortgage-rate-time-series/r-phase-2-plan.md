# R Phase 2 Plan — Mortgage Rate Time-Series Analysis

**Status**: 🗓 Planned
**Type**: Project planning note
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Purpose

Phase 2 extends the Excel workbook into an R-based time-series research layer. The goal is to study the behavior of the `MORTGAGE30US` rate series itself — not to predict rates, but to understand their statistical properties, historical patterns, and affordability implications.

---

## Learning Connections

- **IBM Data Analytics with Excel and R Professional Certificate** — R track
- **NCCU Applied Time Series Analysis** — course-relevant methods and packages

---

## Scope

### In Scope
- Data loading and cleaning in R
- Time-series visualization
- Rolling averages and rolling volatility
- Stationarity testing (ADF, KPSS)
- Seasonality checks
- Rate-regime analysis
- Historical percentile analysis
- Affordability implications by rate regime
- Optional: baseline forecasting (exploratory only)

### Out of Scope
- Reliable mortgage-rate prediction — do not overclaim
- Production forecasting system
- Real-time data feeds

---

## Planned Analysis Steps

1. **Load and clean data** — import MORTGAGE30US CSV, parse dates, handle missing values
2. **Visualize the series** — full history plot, recent period zoom, rate-of-change plot
3. **Rolling statistics** — 4-week, 12-week, 52-week rolling mean and standard deviation
4. **Stationarity testing** — ADF test (`tseries`), KPSS test (`tseries`), seasonal unit-root (`uroot`)
5. **Seasonality check** — decompose series, check for seasonal patterns
6. **Rate-regime analysis** — identify historical low/high/rising/falling regimes
7. **Historical percentile analysis** — where does the current rate rank historically?
8. **Affordability by regime** — apply `PV` logic in R to show purchasing power by rate regime
9. **Optional baseline forecast** — ARIMA or simple trend model, clearly labeled as exploratory

---

## R Package Map

See [[package-map]] for full package-to-use-case mapping.

Key packages:
- `TSA` — ARIMA modeling, ACF/PACF, residual diagnostics
- `tseries` — stationarity testing (ADF, KPSS)
- `uroot` — seasonal unit-root testing
- `locfit` — nonlinear smoothing, long-run trend visualization
- `leaps` — variable selection for engineered affordability features
- `MTS` — future multivariate macro-financial extension

---

## Output Artifacts (Planned)

- R script(s) in the GitHub repo
- Visualizations (rate history, rolling volatility, regime chart, affordability curve)
- R Markdown report or README section
- Wiki notes for each analytical concept

---

## Related Notes

- [[stationarity-testing]]
- [[rolling-volatility]]
- [[rate-regimes]]
- [[package-map]]
- [[project-index]]
- [[phase-roadmap]]
