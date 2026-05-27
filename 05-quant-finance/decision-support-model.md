# Decision-Support Model

**Summary**: An analytical tool designed to help a decision-maker understand tradeoffs and evaluate options — not to make the decision for them.
**Type**: Atomic note
**Sources**: (source: phase-1-excel-model-summary)
**Last updated**: 2025-07-10
**Visibility**: PORTFOLIO_SAFE

---

## Definition

A decision-support model is a structured analytical system that:
- Presents a range of scenarios, not just one answer
- Makes assumptions explicit and configurable
- Connects outputs to the decisions the user actually faces
- Communicates results in a way the decision-maker can act on

It is distinct from a calculator (one input → one output) and from a prediction system (claims to know what will happen).

---

## Why It Matters

- Most financial tools are calculators. Decision-support models are more valuable because they show the landscape of outcomes.
- Making assumptions configurable means the model is reusable across different borrower situations.
- A stakeholder-facing dashboard is part of the decision-support design — it translates analytical outputs into communication.

---

## How It Appears in the Excel Workbook

The Rate Shock Loan Affordability & Refinance Dashboard is a decision-support model because:
- It shows payment, lifetime cost, and affordability across **multiple rate scenarios** simultaneously
- All borrower assumptions are **configurable** in the `Assumptions` sheet
- The `Dashboard` translates model outputs into **stakeholder-readable charts**
- The refinance analysis includes a **decision flag** with break-even context

See [[phase-1-excel-model-summary]] for the full summary.

---

## Design Principles for Decision-Support Models

1. **Scenario range over single answer** — show the space of outcomes
2. **Configurable assumptions** — no hardcoded values in model sheets
3. **Explicit exclusions** — document what the model does not cover
4. **Communication layer** — dashboard or summary for non-technical readers
5. **Honest scope** — do not claim the model makes decisions; it informs them

---

## Extensions

**R (Phase 2)**: R-based time-series analysis extends the decision-support layer by adding historical context — where does the current rate sit relative to history?

**Streamlit (Future)**: An interactive app version of the same model, allowing users to adjust assumptions in a browser.

---

## Related Notes

- [[financial-modeling-template]]
- [[phase-1-excel-model-summary]]
- [[assumptions-and-limitations]]
- [[moc-quant-finance]]
