# Formula Logic — Rate Shock Loan Affordability & Refinance Dashboard

**Type**: Technical reference
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Core Excel Functions

### `PMT` — Monthly Payment

```
=PMT(rate/12, nper, -pv)
```

- **What it does**: Calculates the fixed monthly principal-and-interest payment for a loan.
- **Inputs**: Annual interest rate (divided by 12 for monthly), number of periods (months), loan principal (negative because it's a cash outflow).
- **Used in**: `Rate_Shock_Model` — calculates payment at each rate scenario.
- **Key insight**: Payment is nonlinear with rate. A 1% rate increase at 3% has a different dollar impact than a 1% increase at 7%.

---

### `PV` — Present Value / Affordable Loan Amount

```
=PV(rate/12, nper, -pmt)
```

- **What it does**: Solves for the maximum loan principal affordable at a given monthly payment budget and interest rate.
- **Inputs**: Rate, term, fixed monthly payment (negative).
- **Used in**: `Rate_Shock_Model` — answers "how much loan can I afford at this rate?"
- **Key insight**: As rates rise, the same monthly budget supports a smaller loan. This is purchasing power erosion.
- **Concept note**: [[purchasing-power-erosion]]

---

### `CUMIPMT` — Cumulative Interest Paid

```
=CUMIPMT(rate/12, nper, pv, start_period, end_period, type)
```

- **What it does**: Calculates total interest paid between two periods of a loan.
- **Used in**: `Rate_Shock_Model` — calculates lifetime interest cost across rate scenarios.
- **Key insight**: Lifetime interest differences across rate scenarios are often far larger than monthly payment differences suggest.

---

### `PPMT` — Principal Portion of a Payment

```
=PPMT(rate/12, per, nper, pv)
```

- **What it does**: Returns the principal portion of a specific monthly payment.
- **Used in**: `Amortization_Schedule` — builds the month-by-month principal column.
- **Key insight**: Early payments are mostly interest. Principal paydown accelerates over time.

---

### `IPMT` — Interest Portion of a Payment

```
=IPMT(rate/12, per, nper, pv)
```

- **What it does**: Returns the interest portion of a specific monthly payment.
- **Used in**: `Amortization_Schedule` — builds the month-by-month interest column.
- **Key insight**: Together with `PPMT`, this shows the amortization curve — how the principal/interest split shifts over the loan life.

---

## Derived Calculations

### Refinance Break-Even

```
Break-even months = Closing costs / Monthly payment savings
```

- **What it does**: Calculates how many months it takes for refinance savings to recover the upfront closing costs.
- **Used in**: `Refinance_Analysis`
- **Decision rule**: If break-even months < remaining loan term, refinancing is financially rational (all else equal).
- **Concept note**: [[refinance-break-even]]

---

### Rate Shock Scenarios

- The `Rate_Shock_Model` applies `PMT` and `PV` across a range of rates: e.g., current rate, current ± 1%, ± 2%, ± 3%.
- This creates a sensitivity table showing how payment and affordability change across the rate environment.
- **Concept note**: [[mortgage-rate-shock]]

---

### Affordability Modeling

- Affordability is modeled as: given a fixed monthly budget, what loan principal does `PV` return at each rate?
- This reframes the rate question from "what is my payment?" to "what can I afford to borrow?"
- The gap between affordable principal at a low rate vs. a high rate is the purchasing power erosion.

---

## Notes on Formula Design

- All rate inputs are annual percentages divided by 12 inside formulas.
- All formulas reference named ranges from the `Assumptions` sheet — no hardcoded values.
- `IFERROR` wraps formulas where division-by-zero or missing inputs could occur.
- `IF` is used for the refinance decision flag logic.

---

## Related Notes

- [[workbook-architecture]] — where each formula lives
- [[amortization]] — concept behind PPMT/IPMT
- [[refinance-break-even]] — concept behind break-even logic
- [[purchasing-power-erosion]] — concept behind PV affordability modeling
