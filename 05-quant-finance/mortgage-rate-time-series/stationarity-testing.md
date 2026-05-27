# Stationarity Testing

**Summary**: Statistical tests that determine whether a time series has constant mean, variance, and autocorrelation structure over time — a prerequisite for many time-series models.
**Type**: Atomic note
**Sources**: (source: r-phase-2-plan)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

A stationary time series has:
- Constant mean over time
- Constant variance over time
- Autocorrelation that depends only on lag, not on time

Most time-series models (ARIMA, etc.) assume stationarity. If a series is non-stationary, it typically needs to be differenced or transformed before modeling.

---

## Why It Matters for Mortgage Rates

The `MORTGAGE30US` series is likely non-stationary in levels — rates trended down from the 1980s to the 2020s, then rose sharply. Testing for stationarity is the first analytical step before any modeling.

---

## Key Tests

### ADF (Augmented Dickey-Fuller)
- **Null hypothesis**: Series has a unit root (non-stationary)
- **Reject null** → evidence of stationarity
- **R package**: `tseries::adf.test()`

### KPSS (Kwiatkowski-Phillips-Schmidt-Shin)
- **Null hypothesis**: Series is stationary
- **Reject null** → evidence of non-stationarity
- **R package**: `tseries::kpss.test()`

Using both ADF and KPSS together gives a more complete picture — they test opposite null hypotheses.

### Seasonal Unit Root (HEGY / OCSB)
- Tests for seasonal non-stationarity
- **R package**: `uroot`

---

## Typical Findings for Rate Series

- Levels: likely non-stationary (unit root present)
- First differences (week-over-week change): likely stationary
- This means modeling rate changes, not rate levels, is often more appropriate

---

## R Code Sketch

```r
library(tseries)

# ADF test
adf.test(mortgage_ts)

# KPSS test
kpss.test(mortgage_ts)

# First differences
diff_ts <- diff(mortgage_ts)
adf.test(diff_ts)
```

---

## Connection to Phase 2

Stationarity testing is Step 4 in the [[r-phase-2-plan]]. Results determine whether to model the rate series in levels or differences.

---

## Related Notes

- [[r-phase-2-plan]]
- [[rolling-volatility]]
- [[rate-regimes]]
- [[package-map]]
