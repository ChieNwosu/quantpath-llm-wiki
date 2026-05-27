# Risk Register — Mortgage Rate Intelligence Stack

**Type**: PM artifact
**Visibility**: PORTFOLIO_SAFE
**Last updated**: 2025-07-10
**Part of**: [[project-index]]

---

## Risk Register

| # | Risk | Likelihood | Impact | Mitigation | Status |
|---|---|---|---|---|---|
| R1 | Scope creep — adding income, DTI, or credit modeling to Phase 1 | Medium | High | Explicit exclusion list in [[assumptions-and-limitations]]; scope locked in [[project-charter]] | Mitigated |
| R2 | Overclaiming — presenting the workbook as a production financial advisor | Medium | High | Caveat language in README, workbook, and all documentation | Mitigated |
| R3 | Data staleness — MORTGAGE30US data not updated | Low | Medium | Note data download date in `Rate_Data` sheet; refresh before publishing | Monitor |
| R4 | Formula errors — incorrect PMT/PV/CUMIPMT arguments | Medium | High | Formula logic documented in [[formula-logic]]; test with known values | Mitigated |
| R5 | Phase 2 overclaim — presenting R analysis as complete before it is | Medium | Medium | Phase status labels used throughout; [[phase-roadmap]] is explicit | Mitigated |
| R6 | Workbook modified after Phase 1 finalization | Low | High | Kiro rule: do not modify workbook unless explicitly requested | Mitigated |
| R7 | IBM certificate framing — presenting project as official IBM capstone | Low | Medium | Preferred framing documented in context layer; applied learning language used | Mitigated |
| R8 | GitHub repo becomes outdated relative to wiki notes | Medium | Low | Wiki notes are independent of repo; repo changes require explicit request | Monitor |

---

## Risk Definitions

- **Likelihood**: Low / Medium / High
- **Impact**: Low / Medium / High
- **Status**: Open / Mitigated / Monitor / Closed

---

## Related Notes

- [[project-charter]] — scope and objectives
- [[assumptions-and-limitations]] — exclusion documentation
- [[decision-log]] — decisions that reduced risk
