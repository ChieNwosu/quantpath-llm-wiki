# Financial Modeling Template

**Summary**: Reusable structural principles for building financial models in Excel that are readable, maintainable, and portfolio-ready.
**Type**: Molecule note
**Sources**: (source: workbook-architecture), (source: formula-logic)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Core Structural Principles

### 1. Separate Data, Inputs, Models, and Outputs

| Layer | Sheet Role | Example |
|---|---|---|
| Data | Raw source data, read-only | `Rate_Data` |
| Inputs | Configurable assumptions | `Assumptions` |
| Models | Calculations referencing inputs | `Rate_Shock_Model`, `Amortization_Schedule` |
| Outputs | Results and communication | `Dashboard` |

Never mix raw data with calculations. Never hardcode values in model sheets.

---

### 2. Use Named Ranges

- Name all key inputs in the `Assumptions` sheet.
- Reference names in formulas, not cell addresses.
- Makes formulas readable: `=PMT(AnnualRate/12, LoanTermMonths, -LoanAmount)` is clearer than `=PMT(B3/12, B4, -B2)`.

---

### 3. Use Structured Tables

- Format data ranges as Excel Tables (Ctrl+T).
- Tables auto-expand, support structured references, and are easier to maintain.

---

### 4. Document Exclusions Explicitly

- Every financial model has a scope boundary.
- Document what the model does NOT include in a dedicated sheet or note.
- This prevents misuse and overclaiming.

---

### 5. Build a Communication Layer

- A model without a dashboard is only half-finished for portfolio purposes.
- The dashboard should show key outputs without exposing formulas or raw data.
- Design for a non-technical reader.

---

### 6. Test with Known Values

- Before trusting a financial model, verify formulas with manually calculated examples.
- For `PMT`: verify against an online mortgage calculator.
- For `CUMIPMT`: verify total interest against a known amortization table.

---

## Applied in the Mortgage Rate Project

The Rate Shock Loan Affordability & Refinance Dashboard follows all six principles:
- 7-sheet architecture separates data, inputs, models, and outputs
- Named ranges in `Assumptions` sheet
- Structured tables in `Rate_Data`
- Explicit exclusion list in [[assumptions-and-limitations]]
- Stakeholder dashboard
- Formulas verified against known mortgage calculations

---

## Extensions

**R (Phase 2)**: The same structural principles apply to R scripts — separate data loading, cleaning, analysis, and visualization into distinct script sections or files.

**SQL (Future)**: Separate raw data tables from analytical views. Use CTEs to layer calculations.

---

## Related Notes

- [[decision-support-model]]
- [[workbook-architecture]]
- [[formula-logic]]
- [[assumptions-and-limitations]]
