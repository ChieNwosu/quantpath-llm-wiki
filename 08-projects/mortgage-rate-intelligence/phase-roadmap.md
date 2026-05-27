# Phase Roadmap — QuantPath Mortgage Rate Intelligence Stack

**Type**: Project planning
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Roadmap

| Phase | Name | Description | Status |
|---|---|---|---|
| 1 | Rate Shock Loan Affordability & Refinance Dashboard | Excel financial model using MORTGAGE30US data | ✅ Complete |
| 2 | R Time-Series Analysis Layer | Statistical analysis of the mortgage-rate series in R | 🗓 Planned |
| 3 | SQL Analytics Layer | Reproducible SQL queries on the rate dataset | 🔮 Future |
| 4 | Interactive Presentation Layer | Streamlit app for scenario exploration | 🔮 Future |
| 5 | Agent Assistant Prototype | Explanation agent for formulas, outputs, and scenarios | 🔮 Future |

---

## Phase 1 — Complete

**Deliverable**: Excel workbook with 7 sheets, 5 business questions answered, stakeholder dashboard.
**Data**: FRED/Freddie Mac `MORTGAGE30US`
**Tools**: Excel (PMT, PV, CUMIPMT, PPMT, IPMT, structured tables, named ranges, dashboard charts)
**Repo**: https://github.com/ChieNwosu/quantpath-mortgage-rate-intelligence

Do not modify the Phase 1 workbook unless explicitly requested.

---

## Phase 2 — Planned

**Goal**: Study the behavior of the mortgage-rate series itself using R.
**Connection**: IBM Data Analytics with Excel and R Professional Certificate + NCCU Applied Time Series Analysis
**Scope**:
- Data loading and cleaning in R
- Time-series visualization
- Rolling averages and rolling volatility
- Stationarity testing (ADF, KPSS)
- Seasonality checks
- Rate-regime analysis
- Historical percentile analysis
- Affordability implications by rate regime
- Optional: baseline forecasting (exploratory only — not a prediction system)

See [[r-phase-2-plan]] for full planning note.

---

## Phase 3 — Future

**Goal**: SQL analytics layer on the mortgage-rate dataset.
**Likely tools**: DuckDB (free, local) or Databricks Free Edition; Athena-compatible SQL as future AWS extension.
**Scope**: Beginner to advanced SQL business questions on the rate series (see context layer for full question list).

---

## Phase 4 — Future

**Goal**: Lightweight interactive app for scenario exploration.
**Likely tool**: Streamlit
**Scope**: User inputs assumptions → app returns payment, lifetime interest, affordability, refinance outputs using deterministic formulas (not LLM guesses).

---

## Phase 5 — Future

**Goal**: Agent assistant prototype for explaining outputs.
**Likely tools**: Strands Agents, Ollama (local/open-source baseline).
**Constraint**: No paid cloud dependencies unless explicitly requested.

---

## Related Notes

- [[project-index]] — full project hub
- [[r-phase-2-plan]] — Phase 2 detailed plan
- [[package-map]] — R packages for Phase 2
