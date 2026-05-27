# Workbook Architecture — Rate Shock Loan Affordability & Refinance Dashboard

**Status**: ✅ Phase 1 Complete
**Type**: Technical documentation
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Overview

The workbook has seven sheets. Data flows left to right: raw data → assumptions → models → outputs → dashboard.

```
Rate_Data → Assumptions → Rate_Shock_Model → Dashboard
                       → Amortization_Schedule
                       → Refinance_Analysis → Dashboard
Project_Map (navigation only)
```

---

## Sheet-by-Sheet Breakdown

### 1. `Project_Map`
**Role**: Navigation and orientation
- Explains the workbook purpose and structure
- Lists each sheet and its function
- Intended for any reader opening the workbook for the first time
- Not a data or calculation sheet

---

### 2. `Rate_Data`
**Role**: Raw data layer
- Contains the FRED/Freddie Mac `MORTGAGE30US` weekly rate series
- Cleaned and structured as a table
- Provides historical context: min, max, average, current rate
- Source for rate environment analysis and dashboard charts
- **Do not modify this sheet's structure** — downstream sheets reference it

---

### 3. `Assumptions`
**Role**: Configurable model inputs
- All borrower and refinance assumptions live here
- Key inputs: loan amount, loan term, current rate, refinance rate, closing costs, monthly budget
- Changing values here propagates through all model sheets
- Named ranges are used so formulas reference assumption names, not cell addresses

---

### 4. `Rate_Shock_Model`
**Role**: Payment sensitivity and affordability analysis
- Applies `PMT` across a range of rate scenarios
- Calculates monthly payment, lifetime interest (`CUMIPMT`), and affordable loan amount (`PV`) at each rate
- Answers Business Questions 2, 3, and 4
- Core analytical sheet

---

### 5. `Amortization_Schedule`
**Role**: Full loan amortization table
- Month-by-month breakdown of principal (`PPMT`) and interest (`IPMT`) payments
- Shows how the principal/interest split shifts over the loan term
- Supports lifetime interest calculation and visualization
- Answers Business Question 3 in detail

---

### 6. `Refinance_Analysis`
**Role**: Refinance decision framework
- Compares current loan payment to refinanced payment
- Calculates monthly savings, break-even months, and net benefit
- Includes a decision flag (refinance recommended / not recommended)
- Answers Business Question 5

---

### 7. `Dashboard`
**Role**: Stakeholder-facing summary
- Charts and key metrics drawn from all model sheets
- Designed for non-technical readers
- Shows rate history, payment sensitivity, affordability curve, and refinance summary
- No raw data or formulas visible — outputs only

---

## Design Principles

- **Single source of truth**: All inputs flow from `Assumptions`. No hardcoded values in model sheets.
- **Named ranges**: Formulas reference names, not cell addresses, for readability and maintainability.
- **Structured tables**: Data ranges are formatted as Excel tables for reliable referencing.
- **Separation of concerns**: Raw data, inputs, calculations, and outputs are on separate sheets.

---

## Related Notes

- [[formula-logic]] — formula explanations
- [[assumptions-and-limitations]] — what's configurable, what's excluded
- [[business-questions]] — which sheet answers which question
