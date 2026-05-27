# Assumptions and Limitations — Rate Shock Loan Affordability & Refinance Dashboard

**Type**: Project documentation
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Dataset-Driven Values

These values come directly from the FRED/Freddie Mac `MORTGAGE30US` data:

- Historical weekly 30-year fixed mortgage rates
- Current rate (most recent data point)
- Historical min, max, and average rates
- Rate percentile context

The dataset is public and free. It does not include regional variation — it is a national weekly average.

---

## Configurable Assumptions (Model Inputs)

These live in the `Assumptions` sheet and can be changed by the user:

| Input | Description |
|---|---|
| Loan amount | Principal borrowed |
| Loan term | Years (typically 30) |
| Current mortgage rate | Rate for the base scenario |
| Rate shock scenarios | Range of rates to model (e.g., ±1%, ±2%, ±3%) |
| Monthly payment budget | Fixed budget for affordability modeling |
| Refinance rate | New rate being considered |
| Closing costs | Upfront cost of refinancing |
| Remaining loan term | Months left on current loan |

---

## What the Workbook Does NOT Model

These items are explicitly excluded. Do not claim they are included.

| Excluded Item | Reason |
|---|---|
| Income | Not modeled — no DTI calculation |
| Debt-to-income ratio (DTI) | Not modeled |
| Credit score | Not modeled — rate is a direct input, not credit-derived |
| Property taxes | Not included in payment calculation |
| Homeowner's insurance | Not included |
| Private mortgage insurance (PMI) | Not included |
| HOA fees | Not included |
| ARM loans | Fixed-rate only |
| Regional housing prices | National rate series only |
| Closing cost financing | Closing costs treated as upfront cash |
| Tax deductibility of mortgage interest | Not modeled |

---

## Scope Statement

This workbook models the **financial mechanics of a fixed-rate mortgage** using a **configurable set of borrower assumptions** and a **public national rate series**. It is a decision-support tool for understanding payment sensitivity, lifetime cost, purchasing power, and refinance tradeoffs.

It is not a mortgage qualification tool, a lender underwriting model, or a production financial advisor.

---

## Related Notes

- [[workbook-architecture]] — sheet structure
- [[business-questions]] — what the model does answer
- [[decision-support-model]] — what makes this a decision-support tool
