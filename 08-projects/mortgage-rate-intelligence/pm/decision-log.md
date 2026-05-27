# Decision Log — Mortgage Rate Intelligence Stack

**Type**: PM artifact
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Decision Log

| # | Date | Decision | Rationale | Alternatives Considered |
|---|---|---|---|---|
| D1 | Phase 1 | Use Excel as Phase 1 tool | Aligns with IBM Data Analytics with Excel and R certificate; accessible to non-technical stakeholders; no environment setup required | Python (deferred to future), R (deferred to Phase 2) |
| D2 | Phase 1 | Use FRED/Freddie Mac MORTGAGE30US as data source | Public, free, authoritative, weekly frequency, long history (1971–present) | Zillow rate data, Bankrate scraping (less reliable) |
| D3 | Phase 1 | Scope to fixed-rate 30-year loans only | Keeps model focused; ARM modeling adds significant complexity without proportional learning value at this stage | Include ARM (deferred to future) |
| D4 | Phase 1 | Exclude income, DTI, credit score, taxes, insurance, PMI | These require lender-specific data and underwriting logic; including them would overclaim the model's scope | Include partial DTI (rejected — too complex for Phase 1) |
| D5 | Phase 1 | Use named ranges for all formula inputs | Improves readability, maintainability, and documentation quality | Cell references only (rejected — harder to audit) |
| D6 | Phase 1 | Build a stakeholder-facing dashboard sheet | Demonstrates communication design, not just analytical skill | No dashboard (rejected — reduces portfolio value) |
| D7 | Phase 1 | Frame as applied learning, not official IBM capstone | Accurate framing; avoids misrepresentation | Capstone framing (rejected — not accurate) |
| D8 | Phase 2 | Use R for time-series analysis layer | Aligns with IBM certificate R track and NCCU Applied Time Series Analysis course | Python (possible future extension) |
| D9 | Phase 3 | Use DuckDB as first SQL implementation | Free, local, no cloud setup required; Athena-compatible SQL as future extension | Athena directly (deferred — requires AWS setup) |

---

## Related Notes

- [[project-charter]] — scope decisions
- [[risk-register]] — risks addressed by these decisions
- [[phase-roadmap]] — phase decisions
