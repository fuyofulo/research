# How Companies Solve AP — The Real "Vs" (Problem → Solutions)

Compiled 2026-06-06 from 6 parallel teardown streams, source-grounded in `companies/` + the AP primer.

**This is the "real vs" — not solution-vs-solution, but PROBLEM → how each company solves it.** We took the AP blueprint (what AP *is*, stage by stage) and ran it down the rows, asking for each problem in the pipeline: *how does each company actually solve this?* The output is a menu of solutions per problem — the build spec for assembling your own pipeline.

## The company set (spanning all six vendor categories)

| Company | Archetype |
|---|---|
| **Bill.com** | SMB incumbent · FBO float · CPA channel |
| **Tipalti** | mid-market global · tax + NetSuite depth |
| **Stampli** | AI-native UX leader · no-float · collaboration-on-invoice |
| **Vic.ai** | autonomous-AP ("Autopilot") |
| **Ramp** | spend-suite · agent-with-tools · interchange |
| **Request Finance** | crypto-native AP (EVM-first) · non-custodial |
| **Routable** | API-first mass payouts · embeddable |
| **Altitude** | Solana stablecoin account · code-enforced custody |
| *+ Trolley / Toku / Rise* | crypto-payroll & payee-tax specialists (Stage 4) |
| *+ Melio / Brex / Mercury* | pulled in where distinctive |

## Read order

- **[00_master_matrix.md](./00_master_matrix.md)** — **the one-view grid**: every AP stage × every company, with "who's strongest per problem." Start here.
- **[01_intake_capture_code.md](./01_intake_capture_code.md)** — intake → extraction → GL coding (*extraction is commodity; coding-flywheel is the moat*).
- **[02_match_exception_approval.md](./02_match_exception_approval.md)** — matching → exceptions → approval (*the crypto-native differentiator: multisig AS approval*).
- **[03_pay_rails_float.md](./03_pay_rails_float.md)** — rails, money-movement model, monetization (*float-middleman vs no-float vs self-custodial*).
- **[04_onboarding_tax_compliance.md](./04_onboarding_tax_compliance.md)** — the least-automated, table-stakes layer (*sharpest build-vs-partner line; crypto-native is thinnest here*).
- **[05_erp_sync_record_close.md](./05_erp_sync_record_close.md)** — ERP sync + close (*the real moat AND the #1 complaint — the Tipalti irony*).
- **[06_ai_layer_and_architecture.md](./06_ai_layer_and_architecture.md)** — the AI/agent layer (*agent-with-tools + code-enforced execution = the defensible combination*).
- **[07_build_implications.md](./07_build_implications.md)** — **the build spec**: build vs buy/partner per stage, the architecture sequence, where the white space is.

## The headline

Across all six stages, three findings repeat:
1. **The rail is not the moat** (Routable's Brale stablecoin add proves rails are swappable).
2. **Extraction is commoditized**; the moat moved to proprietary coding data + deep ERP sync + agent orchestration + code-enforced execution.
3. **No incumbent has all four defensible layers.** TradFi has data + ERP depth but software-only enforcement + domestic rails; crypto-native has self-custody + code-enforcement but is thin on tax + ERP + matching.

→ **The build thesis:** agent-with-tools + code-enforced multisig core on Solana/Squads (un-copyable) · nail onboarding + ERP sync + exception UX (the boring moat + the opening against Tipalti's flaky sync) · partner the regulated liability layer (tax, KYB, off-ramp, e-invoicing). Full detail in [07](./07_build_implications.md).

*Caveat: the single-README companies (Stampli, Vic.ai, Routable, Melio) are thinner in the source corpus than the full-folder ones (Bill.com, Tipalti, Request Finance, Altitude); all vendor automation/touchless numbers are vendor-claimed (the only audited anchor is Ardent's ~32.6% average); per-stage gaps are flagged at the end of each file.*
