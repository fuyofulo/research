# Accounts Payable (AP) — A Vendor-Neutral Primer

Compiled 2026-06-06 from 4 parallel deep-research streams. **The goal: understand AP as a discipline — end to end — before comparing how any specific company does it.** No company comparisons here; those live in `companies/`. This is the foundation you read first.

---

## What AP is, in 30 seconds

Accounts Payable is **the money a business owes its suppliers for goods/services already received but not yet paid for** — and the function that gets that money out the door correctly. The whole discipline is about doing one thing under control: **pay the right vendor, the right amount, for what was actually received, once, on time** — while preserving cash, capturing discounts, preventing fraud, and leaving an auditable trail.

The deeper you go, three things turn out to be true across the whole field:
1. **The hard parts aren't the payment — they're the edges:** vendor onboarding + tax (only ~7% automated), clean three-way matching (a data-hygiene problem), and **ERP sync** (the real engineering moat).
2. **The honest automation reality is modest:** the average org is only **~33% touchless**, not the 80–95% vendors advertise.
3. **Payment timing is a financial weapon** (DPO, discounts, float) — and *who holds the money in transit earns the float*, which is the structural reason some platforms profit from being slow middlemen.

## Read in order

1. **[01_what_is_ap.md](./01_what_is_ap.md)** — what AP is, the accounting, AP vs accruals/AR/payroll/treasury, where it sits (P2P / S2P).
2. **[02_the_ap_lifecycle.md](./02_the_ap_lifecycle.md)** — the complete end-to-end workflow (12 stages + diagram), 2/3/4-way matching, PO vs non-PO, the key documents, manual-AP pain points.
3. **[03_payments_rails_crossborder_tax.md](./03_payments_rails_crossborder_tax.md)** — every payment rail, cross-border/FX, float & working capital (DPO/discounting/SCF/FBO), vendor onboarding, US tax (W-9/W-8/1099/1042-S), the global e-invoicing-mandate wave, stablecoins in B2B AP.
4. **[04_controls_fraud_roles_audit.md](./04_controls_fraud_roles_audit.md)** — roles (clerk→CFO→treasury→auditor), internal controls (SoD, DoA, three-way match, SOX), the fraud taxonomy + real stats, how AP is audited, record retention.
5. **[05_automation_ai_metrics_market.md](./05_automation_ai_metrics_market.md)** — the six automation waves, what's automated by stage, the AI/agentic shift + touchless reality, KPIs/benchmarks, the six vendor categories, ERP integration as the moat.
6. **[06_ap_in_one_view.md](./06_ap_in_one_view.md)** — **the whole discipline as diagrams**: a master lifecycle flowchart (stages + control gates + rails + float/tax/AI/ERP overlays in one picture), the money-&-float flow, and the conceptual layer stack. Includes a rendered infographic [`ap_in_one_view.png`](./ap_in_one_view.png). Start *or* end here.
7. **[glossary.md](./glossary.md)** — every term defined, for quick reference.

## The "real vs" — how companies solve it

Once the blueprint is internalized, see **[how-companies-solve-it/](./how-companies-solve-it/)** — the AP pipeline run *down the rows* against 8 companies (Bill.com, Tipalti, Stampli, Vic.ai, Ramp, Request Finance, Routable, Altitude): a master matrix + per-stage teardowns + a **build spec** (build vs buy/partner per stage, the architecture sequence, where the white space is). This is the bridge from "understand AP" to "build the pipeline."

## How this connects to the rest of the workspace

- Once this is internalized, the eventual **"vs"** becomes legible: each company in `companies/` (bill-com, tipalti, request-finance, melio, routable, stampli, vic-ai, altitude, + the crypto-payroll cluster) is really *"which slice of this lifecycle do they own, on which rails, monetized how?"*
- The recurring **table-stakes** this primer surfaces — tax compliance (W-8/W-9/1099/1042-S), multi-entity, deep ERP sync — are exactly the capabilities the company research flags as hard-to-skip.

## Sourcing note

Built from authoritative sources: accounting bodies + ERP docs (Oracle/NetSuite, CFI) for definitions/lifecycle; NACHA/Fed/SWIFT/Peppol + IRS + EU tax authorities for rails/tax/e-invoicing; ACFE *Report to the Nations*, AFP Payments Fraud Survey, FBI IC3 for fraud stats; Ardent Partners *State of ePayables*, APQC, IOFM, Hackett for benchmarks. Figures that are vendor/analyst-sourced or in flux (all-in check cost, FX spreads, stablecoin volumes, market sizing, the 1099 $2,000 threshold effective year, GENIUS Act specifics) are flagged as uncertain in the individual files. Full source URLs are listed at the end of each stream's underlying research (not reproduced here to keep the primer readable).
