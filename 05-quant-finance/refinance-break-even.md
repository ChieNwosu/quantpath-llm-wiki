# Refinance Break-Even

**Summary**: The number of months required for cumulative refinance savings to recover the upfront closing costs of refinancing.
**Type**: Atomic note
**Sources**: (source: formula-logic), (source: workbook-architecture)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

When refinancing a mortgage, the borrower pays closing costs upfront in exchange for a lower monthly payment. The break-even point is when the accumulated monthly savings equal those closing costs.

```
Break-even months = Closing costs / Monthly payment savings
```

If the borrower plans to stay in the home longer than the break-even period, refinancing is financially rational (all else equal).

---

## Why It Matters

- Refinancing is not always beneficial. A lower rate with high closing costs may take years to pay off.
- The break-even calculation is the minimum analysis needed before deciding to refinance.
- Rate environment matters: refinancing from 7% to 6.5% has a different break-even than 7% to 5%.

---

## How It Appears in the Excel Workbook

The `Refinance_Analysis` sheet calculates:
- Current monthly payment (`PMT` at current rate)
- Refinanced monthly payment (`PMT` at new rate)
- Monthly savings (difference)
- Break-even months (closing costs ÷ monthly savings)
- Decision flag: refinance recommended if break-even < remaining loan term

See [[formula-logic]] for formula details.
See [[workbook-architecture]] for sheet context.

---

## Caveats

- This model assumes the borrower stays in the home for the full remaining term.
- It does not model the opportunity cost of the closing cost cash.
- It does not model tax implications of mortgage interest deduction changes.
- It does not model cash-out refinancing.

---

## Extensions

**R (Phase 2)**: Break-even analysis can be run across historical rate pairs to identify periods when refinancing would have been most beneficial.

**SQL (Future)**: Query historical rate data to find periods where a refinance from the prior year's rate to the current rate would have broken even within 24 months.

---

## Related Notes

- [[amortization]]
- [[mortgage-rate-shock]]
- [[purchasing-power-erosion]]
- [[formula-logic]]
- [[moc-quant-finance]]
