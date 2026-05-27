# Mortgage Rate Shock

**Summary**: A significant upward or downward movement in mortgage rates that materially changes monthly payments, lifetime borrowing cost, and purchasing power.
**Type**: Atomic note
**Sources**: (source: phase-1-excel-model-summary)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

A mortgage rate shock is a meaningful change in the prevailing mortgage rate — typically 0.5% or more — that has measurable financial consequences for borrowers. The term is used in financial modeling to describe scenario analysis across a range of rate levels.

---

## Why It Matters

- A 1% rate increase on a $300,000 loan adds roughly $170–$200/month to the payment.
- Over 30 years, that same 1% increase adds $60,000–$70,000 in lifetime interest.
- Rate shocks also reduce purchasing power: the same monthly budget supports a smaller loan at higher rates.
- Rate shocks are not hypothetical — the 2022–2023 rate cycle moved rates from ~3% to ~7% in under two years.

---

## How It Appears in the Excel Workbook

The `Rate_Shock_Model` sheet applies `PMT` and `PV` across a range of rate scenarios (e.g., current rate ± 1%, ± 2%, ± 3%). This creates a sensitivity table showing:
- Monthly payment at each rate
- Lifetime interest at each rate
- Affordable loan principal at each rate

See [[formula-logic]] for the formula details.
See [[workbook-architecture]] for the sheet context.

---

## Extensions

**R (Phase 2)**: Analyze the historical distribution of rate changes to understand how common different shock magnitudes are. Rolling volatility quantifies how much rates move in a given window.

**SQL (Future)**: Query rate-shock events (e.g., weeks where rate changed by more than X%) from the MORTGAGE30US dataset.

---

## Related Notes

- [[amortization]]
- [[purchasing-power-erosion]]
- [[refinance-break-even]]
- [[project-index]]
- [[moc-quant-finance]]
