# Requirements Traceability — Mortgage Rate Intelligence Stack

**Type**: PM artifact
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Traceability Matrix

Maps each business question to its workbook sheet, formula(s), output, and acceptance criteria.

| # | Business Question | Sheet(s) | Formula(s) | Output | Acceptance Criteria |
|---|---|---|---|---|---|
| BQ1 | How have rates changed historically, and where is the current rate? | `Rate_Data`, `Dashboard` | Min/Max/Average | Historical chart, current rate context | Current rate visible; historical range shown; percentile context present |
| BQ2 | How does a rate change affect monthly payment? | `Rate_Shock_Model`, `Dashboard` | `PMT` | Payment at each rate scenario | Payments shown for at least 5 rate scenarios; current rate included |
| BQ3 | How does the rate environment affect lifetime interest? | `Rate_Shock_Model`, `Amortization_Schedule`, `Dashboard` | `CUMIPMT`, `PPMT`, `IPMT` | Lifetime interest by rate scenario; amortization table | Lifetime cost shown for each scenario; amortization schedule complete for base case |
| BQ4 | How much loan is affordable at a fixed monthly budget? | `Rate_Shock_Model`, `Dashboard` | `PV` | Affordable principal by rate scenario | Affordable amount shown for each rate scenario; budget input is configurable |
| BQ5 | When does refinancing make sense, and what is the break-even? | `Refinance_Analysis`, `Dashboard` | `PMT`, break-even formula | Monthly savings, break-even months, decision flag | Break-even months calculated; decision flag present; closing costs are configurable |

---

## Assumption Traceability

| Assumption | Location | Configurable? |
|---|---|---|
| Loan amount | `Assumptions` sheet | Yes |
| Loan term | `Assumptions` sheet | Yes |
| Current rate | `Assumptions` sheet | Yes |
| Rate shock range | `Assumptions` sheet | Yes |
| Monthly budget | `Assumptions` sheet | Yes |
| Refinance rate | `Assumptions` sheet | Yes |
| Closing costs | `Assumptions` sheet | Yes |
| Remaining term | `Assumptions` sheet | Yes |

---

## Exclusion Traceability

| Excluded Item | Documented In |
|---|---|
| Income / DTI | [[assumptions-and-limitations]] |
| Credit score | [[assumptions-and-limitations]] |
| Taxes / insurance / PMI | [[assumptions-and-limitations]] |
| ARM loans | [[assumptions-and-limitations]] |
| Regional housing prices | [[assumptions-and-limitations]] |

---

## Related Notes

- [[business-questions]] — full question descriptions
- [[workbook-architecture]] — sheet structure
- [[formula-logic]] — formula explanations
- [[assumptions-and-limitations]] — exclusions
