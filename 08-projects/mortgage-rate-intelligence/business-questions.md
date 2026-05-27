# Business Questions — Mortgage Rate Intelligence Stack

**Status**: ✅ Phase 1 Complete
**Type**: Project documentation
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## The Five Business Questions

These are the questions Phase 1 was designed to answer. Each maps to a specific workbook sheet.

---

### Q1: How have 30-year fixed mortgage rates changed historically, and where does the latest rate sit relative to the past?

**Answered in**: `Rate_Data` sheet, `Dashboard`
**Approach**: Load and visualize the full MORTGAGE30US series. Calculate historical min, max, average, and current percentile rank.
**Why it matters**: Context for all other analysis. A rate that feels "high" may be historically average, or vice versa.

---

### Q2: How much does a mortgage rate increase or decrease change the monthly payment on a representative loan?

**Answered in**: `Rate_Shock_Model` sheet, `Dashboard`
**Approach**: Apply `PMT` across a range of rate scenarios (e.g., current rate ± 1%, ± 2%, ± 3%) for a fixed loan amount and term.
**Why it matters**: Quantifies the payment sensitivity that households actually experience when rates move.
**Concept note**: [[mortgage-rate-shock]]

---

### Q3: How does the interest-rate environment affect total interest paid over the full life of the loan?

**Answered in**: `Rate_Shock_Model`, `Amortization_Schedule`, `Dashboard`
**Approach**: Use `CUMIPMT` to calculate total interest across rate scenarios. Show lifetime cost, not just monthly payment.
**Why it matters**: Monthly payment differences look small; lifetime interest differences are often tens of thousands of dollars.
**Concept note**: [[amortization]]

---

### Q4: Given a fixed monthly payment budget, how much loan principal is affordable at different mortgage rates?

**Answered in**: `Rate_Shock_Model`, `Dashboard`
**Approach**: Use `PV` to solve for affordable principal given a fixed payment budget and varying rates.
**Why it matters**: Rising rates don't just increase payments — they reduce purchasing power. This quantifies that erosion.
**Concept note**: [[purchasing-power-erosion]]

---

### Q5: Under what conditions does refinancing become financially attractive, and how long does it take to break even?

**Answered in**: `Refinance_Analysis`, `Dashboard`
**Approach**: Compare current loan payment to refinanced payment. Calculate monthly savings, closing cost recovery period, and net benefit.
**Why it matters**: Refinancing has upfront costs. Break-even analysis determines whether the long-term savings justify those costs.
**Concept note**: [[refinance-break-even]]

---

## Traceability

Full requirements-to-output mapping: [[requirements-traceability]]
