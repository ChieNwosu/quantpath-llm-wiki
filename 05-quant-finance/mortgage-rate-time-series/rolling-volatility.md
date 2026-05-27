# Rolling Volatility

**Summary**: A time-varying measure of how much a series fluctuates over a moving window — used to identify periods of rate stability vs. turbulence.
**Type**: Atomic note
**Sources**: (source: r-phase-2-plan)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

Rolling volatility is the standard deviation of a series calculated over a sliding window of fixed length. As the window moves forward in time, the volatility estimate updates, producing a time series of volatility values.

For mortgage rates, rolling volatility shows when rates were stable (low volatility) vs. when they were moving rapidly (high volatility).

---

## Why It Matters

- Periods of high rate volatility are periods of high uncertainty for borrowers and lenders.
- Rolling volatility contextualizes the current rate environment — is this a stable or turbulent period?
- Volatility regimes often correspond to macroeconomic events (Fed policy changes, recessions, inflation shocks).

---

## R Implementation

```r
library(zoo)

# 12-week rolling standard deviation
rolling_vol <- rollapply(mortgage_ts, width = 12, FUN = sd, fill = NA)

# Plot
plot(rolling_vol, main = "12-Week Rolling Volatility — MORTGAGE30US")
```

Common window sizes for weekly data:
- 4 weeks (~1 month)
- 12 weeks (~1 quarter)
- 52 weeks (~1 year)

---

## Connection to Phase 2

Rolling volatility is part of Step 3 in the [[r-phase-2-plan]] (rolling statistics). It feeds into [[rate-regimes]] analysis — high-volatility periods often mark regime transitions.

---

## Extensions

**SQL (Future)**: Rolling standard deviation using window functions:
```sql
STDDEV(rate) OVER (ORDER BY date ROWS BETWEEN 11 PRECEDING AND CURRENT ROW) AS rolling_vol_12w
```

---

## Related Notes

- [[stationarity-testing]]
- [[rate-regimes]]
- [[r-phase-2-plan]]
- [[package-map]]
