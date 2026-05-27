# Phase 1: Rate Shock Loan Affordability & Refinance Dashboard

**Status**: ✅ Complete
**Type**: Project summary
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Purpose

Translate the FRED/Freddie Mac `MORTGAGE30US` weekly 30-year fixed mortgage rate series into practical household finance scenarios. The workbook is a reusable decision-support template — not just a calculator.

---

## Data Source

**FRED / Freddie Mac `MORTGAGE30US`**
- Weekly 30-year fixed mortgage rate
- Public, free, downloadable from FRED (Federal Reserve Bank of St. Louis)
- Provides historical rate context and current rate environment

---

## Workbook Sheets

| Sheet | Role |
|---|---|
| `Project_Map` | Navigation guide and project overview |
| `Rate_Data` | Raw MORTGAGE30US data, cleaned and structured |
| `Assumptions` | Configurable borrower and refinance inputs |
| `Rate_Shock_Model` | Payment sensitivity and affordability at multiple rate scenarios |
| `Amortization_Schedule` | Full month-by-month amortization table |
| `Refinance_Analysis` | Refinance savings, break-even, and decision flag |
| `Dashboard` | Stakeholder-facing summary charts and key outputs |

Full sheet-by-sheet explanation: [[workbook-architecture]]

---

## Main Outputs

- Monthly principal-and-interest payment at current and shock rates
- Lifetime interest cost over the full loan term
- Affordable loan principal at a fixed monthly budget
- Full amortization schedule (principal/interest split by month)
- Refinance monthly savings
- Refinance break-even timing (months)
- Refinance decision flag (yes/no with rationale)
- Dashboard visualizations for stakeholder communication

---

## Why It Is a Decision-Support Tool, Not Just a Calculator

A calculator returns one answer for one input. This workbook:
- Shows payment sensitivity across a **range of rate scenarios** simultaneously
- Connects rate changes to **lifetime cost**, not just monthly payment
- Frames affordability as **purchasing power** (how much loan a fixed budget can support)
- Provides a **refinance decision framework** with break-even analysis
- Uses configurable assumptions so any borrower scenario can be modeled
- Includes a **stakeholder-facing dashboard** for communication

---

## Key Excel Features Used

- `PMT`, `PV`, `CUMIPMT`, `PPMT`, `IPMT`
- `IF`, `IFERROR`
- Structured tables and named ranges
- Conditional formatting
- Dashboard charts

Formula explanations: [[formula-logic]]

---

## What the Workbook Does Not Model

See [[assumptions-and-limitations]] for the full list. Key exclusions:
- Income, DTI, credit score
- Taxes, insurance, PMI, HOA fees
- ARM loans
- Regional housing prices
