# Purchasing Power Erosion

**Summary**: The reduction in the loan principal a borrower can afford when mortgage rates rise, given a fixed monthly payment budget.
**Type**: Atomic note
**Sources**: (source: formula-logic), (source: business-questions)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

When mortgage rates rise, a fixed monthly payment budget supports a smaller loan. This is purchasing power erosion — the same income buys less house as rates increase.

The Excel `PV` function quantifies this directly:

```
=PV(rate/12, nper, -monthly_budget)
```

As `rate` increases, `PV` (affordable principal) decreases.

---

## Why It Matters

- Rate discussions often focus on monthly payment changes. Purchasing power erosion shows the other side: how much less you can borrow.
- A move from 3% to 7% on a $2,000/month budget reduces affordable principal by roughly $150,000–$180,000.
- This is why housing affordability deteriorates rapidly in rising-rate environments even when home prices haven't changed.

---

## Example

| Rate | Affordable Principal (30yr, $2,000/month budget) |
|---|---|
| 3% | ~$474,000 |
| 5% | ~$373,000 |
| 7% | ~$300,000 |

*Approximate values for illustration. Exact figures depend on term and budget.*

---

## How It Appears in the Excel Workbook

The `Rate_Shock_Model` sheet uses `PV` to calculate affordable principal at each rate scenario. The `Dashboard` visualizes the affordability curve — showing how purchasing power declines as rates rise.

See [[formula-logic]] for formula details.
See [[business-questions]] — Business Question 4.

---

## Extensions

**R (Phase 2)**: Plot the historical affordable principal curve using the MORTGAGE30US series and a fixed budget assumption. Shows how purchasing power has changed over decades.

**SQL (Future)**: Calculate affordable principal for each week in the rate history — a useful window function exercise.

---

## Related Notes

- [[mortgage-rate-shock]]
- [[amortization]]
- [[refinance-break-even]]
- [[formula-logic]]
- [[moc-quant-finance]]
