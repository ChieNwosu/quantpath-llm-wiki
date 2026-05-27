# Project Index: QuantPath Mortgage Rate Intelligence Stack

**Status**: Phase 1 Complete | Phase 2 Planned
**Type**: Project index
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**GitHub repo**: https://github.com/ChieNwosu/quantpath-mortgage-rate-intelligence

---

## What This Project Is

A phased financial analytics project that begins with an Excel decision-support model and expands into R-based time-series analysis, SQL analytics, and future interactive presentation layers.

The core message:
> Mortgage-rate changes are usually discussed as macroeconomic headlines, but households experience them through monthly payments, lifetime borrowing cost, purchasing power, and refinance tradeoffs. This project translates a public mortgage-rate series into a reusable decision-support system that makes those financial impacts easier to understand.

---

## Phase Roadmap

| Phase | Description | Status |
|---|---|---|
| Phase 1 | Rate Shock Loan Affordability & Refinance Dashboard (Excel) | ✅ Complete |
| Phase 2 | R-based time-series analysis of the mortgage-rate series | 🗓 Planned |
| Phase 3 | SQL analytics layer (DuckDB / Athena-compatible) | 🔮 Future |
| Phase 4 | Interactive presentation layer (Streamlit) | 🔮 Future |
| Phase 5 | Agent assistant prototype (Strands / Ollama) | 🔮 Future |

---

## Data Source

**FRED / Freddie Mac `MORTGAGE30US`** — Weekly 30-year fixed mortgage rate series (public, free).

---

## Project Notes

### Phase 1 — Excel Model
- [[phase-1-excel-model-summary]] — workbook purpose, sheets, outputs
- [[business-questions]] — five business questions and where each is answered
- [[workbook-architecture]] — seven-sheet structure and data flow
- [[formula-logic]] — PMT, PV, CUMIPMT, PPMT, IPMT, break-even, affordability
- [[assumptions-and-limitations]] — what's included, what's excluded
- [[phase-roadmap]] — full phase plan with honest status labels
- [[linkedin-post-draft]] — Phase 1 LinkedIn post draft

### PM Artifacts
- [[project-charter]]
- [[requirements-traceability]]
- [[risk-register]]
- [[decision-log]]
- [[retrospective]]

---

## Concept Notes (Evergreen)

- [[mortgage-rate-shock]]
- [[amortization]]
- [[refinance-break-even]]
- [[purchasing-power-erosion]]
- [[decision-support-model]]
- [[financial-modeling-template]]

---

## Phase 2 — R Time-Series (Planned)

- [[r-phase-2-plan]]
- [[stationarity-testing]]
- [[rolling-volatility]]
- [[rate-regimes]]
- [[package-map]]

---

## Learning Connections

**IBM Data Analytics with Excel and R Professional Certificate**
- [[certification-index]] — certificate overview
- [[applied-learning-map]] — skills mapped to certificate objectives
- [[project-connections]] — how Phase 1 and Phase 2 connect to the certificate

**NCCU Applied Time Series Analysis**
- Phase 2 R analysis connects directly to this course
- See [[r-phase-2-plan]] for course-relevant package mapping

---

## QuantPath Connection

This is the current flagship project in the QuantPath analytics portfolio. It demonstrates:
- Excel financial modeling with real public data
- Decision-support design (not just calculation)
- Phased delivery with honest scope management
- Applied learning connected to IBM certificate and NCCU coursework
- Foundation for future R, SQL, and cloud analytics layers

See also: [[moc-quant-finance]], [[moc-projects]]
