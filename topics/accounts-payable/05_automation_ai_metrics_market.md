# 5 — Automation, AI, Metrics & Market

*How AP got automated, what AI actually does, the honest benchmark numbers, and the vendor landscape as categories.*

## The six waves of AP automation

Each wave automated a bottleneck and left a residual problem for the next:

1. **Manual / paper** (baseline) — key data, walk approvals, cut checks. Touchless ~0–20%. Early-2000s cost could exceed $20/invoice, cycle >20 days.
2. **EDI** (1980s–2000s) — structured machine-to-machine (X12 810 invoice) over value-added networks. Data born digital, but expensive + rigid → only large suppliers; the long tail stayed on paper.
3. **OCR / template extraction** (1990s–2010s) — read scanned invoices by field position. Brittle: a new vendor or changed layout breaks the template.
4. **Workflow automation** (2000s–2010s) — rules route coding/approval + post to ERP. Static rules; routes exceptions to humans. Touchless ceiling ~35–55%.
5. **AI/ML coding & IDP** (mid-2010s–2024) — **Intelligent Document Processing** (OCR + ML + NLP) reads *any* layout template-free; ML predicts GL codes/approvers. Still "extraction + suggestion"; flags a human when unsure. Touchless ~55–75%.
6. **Agentic AI / "autonomous AP"** (2024–26) — shift from *suggesting* to *acting within guardrails*: an agent investigates an exception (pulls contract/PO/history), decides, takes the next action. Touchless ceiling ~80–95%. **Money movement stays gated.**

The throughline: each wave moves the human further downstream — from keying data → handling exceptions → (now) reviewing the agent's decisions and authorizing payment.

## What gets automated, stage by stage (and maturity)

Ardent Partners 2024 "fully automated" adoption is the best objective maturity gauge:

| Stage | Automation | Maturity (Ardent "fully automated") |
|---|---|---|
| Invoice capture (OCR/IDP) | Reads any layout, extracts header+line | receipt 17%; OCR adopted by 55% |
| GL coding prediction | Predicts account/cost center from history | ~24% (within "invoice processing") |
| PO matching (2/3/4-way) | Matches invoice↔PO↔receipt | ~24% |
| Approval routing | Routes by rules/learned patterns | 44% |
| Fraud/duplicate detection | Flags anomalies, dupes, bank changes | embedded; 2025 priority |
| Payment execution | ACH/vCard/check/cross-border | execution 36%, scheduling 45% |
| Reconciliation / ERP sync | Posts to GL, reconciles | data mgmt 12% |
| **Vendor onboarding** | Self-service portal, bank/tax data | **only 7% fully automated** |
| Tax-form collection | W-9/W-8, TIN validation, 1099 | embedded; immature |

**Mature:** capture/IDP, approval routing. **Still hard:** clean **three-way matching** (a *data-hygiene* problem — vendor naming mismatches, partial deliveries, tolerance decisions — not a math problem); GL coding for novel/ambiguous spend; and **vendor onboarding + tax forms (7%)** — the least-automated stage, because it requires validating bank details (a top fraud vector) and collecting the correct tax form + TIN validation.

## AI in AP — and the touchless reality check

The 2024–26 shift is **"extraction → action."** An "AP agent" does intelligent matching with variance tolerance, dynamic GL assignment, supplier-learning that cuts exceptions over time, fraud/duplicate detection, and ERP posting + payment release.

**The single most over-claimed metric is the touchless rate.** The honest, source-of-record number:

> **Average organization touchless rate ≈ 32.6%** (Ardent, *AP Metrics that Matter in 2025*).

Tier ceilings (read as best-in-class, not averages): manual 0–20% · basic 20–35% · workflow 35–55% · AI-assisted 55–75% · **agentic target 80–95%**. The 90%+ figures vendors cite are exceptional cases.

**Why humans stay in the loop / money movement is gated:**
1. **Fraud risk** — 79% of orgs faced payments fraud in 2024; automating payments *without* bank-change verification + duplicate detection *increases* exposure.
2. **Irreversibility** — once ACH/wire leaves, recovery is hard; approval + payment *release* are the gated steps.
3. **Errors compound** into the GL and tax filings (1099/VAT).

Even bullish analysts say an all-AI AP department is "years away," and benefits accrue fastest to enterprises that *already* have core automation.

## KPIs / benchmarks (Ardent 2025 unless noted)

| Metric | Definition | Average | Best-in-Class |
|---|---|---|---|
| **Cost per invoice** | Fully-loaded cost to process one invoice | **$9.40** | **$2.78** (vs $12.88 others) |
| **Cycle time** | Receipt → approval/payment-ready | **9.2 days** | **3.1 days** (vs 17.4) |
| **Touchless rate** | % end-to-end with zero human touch | **32.6%** | 60–95% (agentic) |
| **Exception rate** | % that can't process straight-through | **14%** | lower; "#1 challenge" cited by 53% |
| **ePayments share** | % of payments made electronically | **68.3%** | — |
| **DPO** | (AP ÷ COGS) × days | ~**40 days** (APQC median) | higher = more working capital |
| **Early-pay discount capture** | % of available discounts captured | ~**15%** of invoices in window (APQC) | 85–95% (automated/centralized) |
| **Invoices per FTE** | Throughput per AP staffer | — | top performers ~3× bottom; ~3.3 FTE/$1B rev vs 14.4 |

**Benchmark sources:** Ardent Partners *State of ePayables* (the canonical averages + Best-in-Class splits), APQC Open Standards Benchmarking, IOFM, Hackett Group, Levvel (ex-PayStream). *Best-in-Class vs the rest is a ~4× gap on cost and cycle time — automation is the differentiator.*

## The vendor landscape — six converging categories

(Vendors named as category examples only — full profiles live in `companies/`.)

- **A. ERP-native AP modules** — built into the accounting system; zero integration gap (it *is* the system of record) but weaker capture/payments/AI. *NetSuite AP, SAP, Sage Intacct, QuickBooks Bill Pay.*
- **B. Standalone AP automation** — best-of-breed capture→code→approve→pay on top of an ERP; deep workflow + ERP connectors. *Stampli, AvidXchange, Rillion, Quadient.*
- **C. Spend-management suites (AP + cards + expense)** — unify all non-payroll spend; land via cards, expand to AP. *Ramp, BILL, Brex.*
- **D. Mass-payout / global-payables** — pay *many* payees across *many* countries; cross-border rails + payee self-onboarding + heavy tax automation (W-9/W-8, 1099/1042-S). *Tipalti, Routable.*
- **E. Procure-to-Pay / Source-to-Pay suites** — automation starts *upstream* at procurement (the PO/receipt data that make matching possible); enterprise. *Coupa, SAP Ariba, Oracle, GEP, Ivalua.*
- **F. E-invoicing / compliance networks** — network reach + regulatory coverage for government mandates. *Peppol access points, Tradeshift, Pagero, Basware.*

**Convergence:** card vendors add AP, AP vendors add payments/global rails, everyone adds AI agents — the prize is the single system touching *all* supplier spend. **Market size** (treat as directional — definitions differ wildly): ~$2–7B in 2026, ~8–12% CAGR. Demand drivers: **e-invoicing mandates + real-time rails + AI FOMO**.

## ERP integration — the real moat

The **GL inside the ERP is the system of record**; an AP tool is a workflow layer on top. Every invoice must post to the correct GL accounts and every payment must reconcile in the ERP — or the books are wrong and the audit fails. **Sync is hard** because it must be two-way/real-time/bidirectional (pull vendors, COA, POs, dimensions; push bills + payments), every ERP models AP differently (a NetSuite connector ≠ an SAP connector), master-data names rarely match cleanly (what breaks auto-matching), and closed-period locks must be respected. **A huge share of an AP vendor's engineering moat is the quality/breadth of its ERP connectors, not its UI** — buyers test for "deep, two-way, real-time GL sync."

The major ERPs: **QuickBooks/Xero** (SMB; shallow native AP → the add-on ecosystem thrives), **Sage Intacct** (mid-market, finance-led), **NetSuite** (the dominant mid-market ERP standalone/global-payables vendors target), **MS Dynamics 365**, **SAP S/4HANA + Ariba** (large enterprise), **Oracle Fusion**.

→ Next: [glossary.md](./glossary.md)
