# Project Charter — QuantPath Mortgage Rate Intelligence Stack

**Type**: PM artifact
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Problem Statement

Mortgage-rate changes are widely reported as macroeconomic news, but their household-level financial impact — on monthly payments, lifetime borrowing cost, purchasing power, and refinance decisions — is rarely quantified in an accessible, reusable format. There is no standard personal-finance tool that translates a public rate series into a structured decision-support model.

---

## Project Objective

Build a phased financial analytics system that translates the FRED/Freddie Mac `MORTGAGE30US` rate series into practical household finance outputs, starting with an Excel decision-support model and expanding into R-based time-series analysis and future analytics layers.

---

## Scope

### In Scope — Phase 1
- Excel workbook with 7 sheets
- Five business questions answered
- Configurable borrower and refinance assumptions
- Stakeholder-facing dashboard
- GitHub repository with documentation

### Out of Scope — Phase 1
- Income, DTI, credit score modeling
- Taxes, insurance, PMI, HOA fees
- ARM loans
- Regional housing price data
- R analysis, SQL, Streamlit, cloud deployment

### Future Phases (Planned / Future)
- Phase 2: R time-series analysis
- Phase 3: SQL analytics layer
- Phase 4: Streamlit interactive app
- Phase 5: Agent assistant prototype

---

## Stakeholders

| Stakeholder | Role |
|---|---|
| Chiemela Nwosu | Project owner, analyst, developer |
| Technical reviewers | GitHub audience, portfolio reviewers |
| Non-technical stakeholders | LinkedIn audience, recruiters |
| Instructors | IBM certificate, NCCU coursework |
| Future self | Reuse and extension of this work |

---

## Success Criteria — Phase 1

- [ ] All five business questions answered in the workbook
- [ ] Dashboard is readable by a non-technical stakeholder
- [ ] All assumptions are configurable (no hardcoded values in model sheets)
- [ ] GitHub repo is public with a polished README
- [ ] Workbook does not claim features it does not have
- [ ] LinkedIn post published

---

## Learning Connections

- IBM Data Analytics with Excel and R Professional Certificate — applied Excel skills
- NCCU Applied Time Series Analysis — Phase 2 R connection
- QuantPath portfolio — flagship project demonstrating phased analytical delivery

---

## Related Notes

- [[requirements-traceability]]
- [[risk-register]]
- [[decision-log]]
- [[retrospective]]
