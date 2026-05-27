# Amortization

**Summary**: The process of paying off a loan through scheduled, fixed payments where the proportion of principal and interest shifts over time.
**Type**: Atomic note
**Sources**: (source: formula-logic), (source: workbook-architecture)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

Amortization is the gradual repayment of a loan through equal periodic payments. Each payment covers both interest (calculated on the remaining balance) and principal (reducing the balance). Early payments are mostly interest; later payments are mostly principal.

---

## The Math

For a fixed-rate loan:
- **Monthly payment** = `PMT(rate/12, nper, -pv)` — fixed for the life of the loan
- **Interest portion** = `IPMT(rate/12, period, nper, pv)` — decreases each month
- **Principal portion** = `PPMT(rate/12, period, nper, pv)` — increases each month
- **Remaining balance** = previous balance − principal payment

The total payment is constant; the split between interest and principal shifts every month.

---

## Why It Matters

- Borrowers who sell or refinance early pay more interest than they realize — they've been in the high-interest early phase.
- Lifetime interest cost is not obvious from the monthly payment alone. `CUMIPMT` reveals it.
- Understanding amortization is essential for evaluating refinance decisions — you need to know where you are in the amortization curve.

---

## How It Appears in the Excel Workbook

The `Amortization_Schedule` sheet builds a full month-by-month table using `PPMT` and `IPMT`. It shows:
- Principal paid each month
- Interest paid each month
- Remaining balance after each payment

The `Rate_Shock_Model` uses `CUMIPMT` to summarize lifetime interest across rate scenarios without building the full schedule.

See [[formula-logic]] for formula details.

---

## Extensions

**R (Phase 2)**: Amortization math can be reproduced in R for scenario modeling. The `FinancialMath` or base R functions can replicate the schedule.

**SQL (Future)**: A recursive CTE can generate an amortization schedule in SQL — a useful advanced SQL exercise.

---

## Related Notes

- [[mortgage-rate-shock]]
- [[refinance-break-even]]
- [[formula-logic]]
- [[moc-quant-finance]]
