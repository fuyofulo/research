# Tipalti — Architecture

*Product SKUs, AI stack, money-movement model, integrations, API surface*
*Compiled 2026-06-06*

Confidence: ✅ high · 🟡 medium · 🔴 low / inferred.

---

## 1. Product / module breakdown

Tipalti is sold **modular**: customers start with core AP or Mass Payments and bolt on the rest. ✅

- **AP Automation (flagship).** Invoice intake, OCR scanning, GL coding, approval routing, PO matching, supplier onboarding, payment execution, ERP reconciliation. ✅
- **Mass Payments (the original product).** Global payouts to 200+ countries/territories, 120 currencies, 50+ payment methods, targeted at marketplaces / ad networks / creator & affiliate platforms paying many distributed payees. ✅
- **Procurement / PO Management** *(from Approve.com, Apr 2021)*. Purchase requisitions, multi-stage approvals, budget controls, 2-/3-way matching — the "ask-to-buy" front end *before* an invoice. ✅
- **Employee Expenses.** Receipt scanning (AI agent), expense reports, policy enforcement, multi-currency, integrated with Tipalti Card. ✅
- **Tipalti Card.** Virtual + physical corporate cards: AP/virtual cards (vendor invoice payments, subscriptions) and T&E cards (employee spend). For existing AP customers, unlimited cards at no extra cost; interchange-generating. ✅
- **Advanced / Multi-FX.** Hold/fund accounts in 30+ currencies, live-rate conversion, FX hedging to lock rates. Leverages aggregate platform spend for rates. ✅
- **Treasury** *(from Statement, Jun 2025)*. Real-time cash position, reconciliation, AI cash-flow forecasting across banks/ERPs/billing tools. Underpins newer "Tipalti AI" treasury features. ✅

**Moat shape:** global payment-rule validation + tax compliance + deep multi-entity NetSuite integration — *not* card-issuing.

## 2. AI stack

History: **Tipalti Pi (Payables Intelligence)** embedded GPT-4 in June 2023 → 2025 re-architecture into discrete **agents** + a conversational Assistant → reinforced by the Statement acquisition (AI treasury) and the **$200M Sept-2025 financing** explicitly earmarked for AI. ✅

**Tipalti AI Assistant** — conversational copilot combining workflow context (invoices, POs, purchase requests) with reasoning. ✅

**Named agents** (all on the finance-AI page) ✅:
- Invoice Capture Agent (OCR+NLP extraction)
- PO Matching Agent (contextual bill↔PO matching)
- Bill Approvers Agent (predicts correct approver)
- Purchase Request Agent (plain-English → full PR)
- Tax Form Scan Agent (W-9 extraction)
- Expense Receipt Scan Agent
- Reporting Agent (natural-language reports)
- ERP Sync Resolution Agent (diagnoses sync errors)
- Branded Experience Agent (branded payee onboarding)

Plus **Auto Coding** (OCR+NLP → GL codes from historical data) and **Duplicate Bill Detection** + vendor-bank-change flagging for fraud. ✅

**Competitive read** 🟡: All three (Tipalti / Bill.com / Ramp) converge on the same agent set. **Bill.com's** Invoice Coding Agent is more explicitly benchmarked (~99% field accuracy, last-5-bills + current doc, six fields). **Ramp** claims auto-coding ~60% of invoices at 99% precision and is shipping fastest. Tipalti's differentiator is **global payments + multi-entity ERP depth + AI treasury**, not the agents themselves. Tipalti is **reacting, not leading**, on AI velocity.

## 3. Supplier / payee onboarding

- **Supplier Hub** — self-service portal: payees submit contact info, complete **W-9 / W-8** forms online, pick a payment method, upload/update docs in real time; 27+ languages. ✅
- **The validation engine** — proprietary **~26,000 global payment rules** (marketing also cites "60,000+" and "3,000+" in places) validating SWIFT/IBAN/local banking details before submission; claims **66% fewer payment errors**. ✅ claim.
- **KYC / sanctions** — **OFAC screening before every payment** (not just at onboarding, because lists update frequently), KYC at onboarding. ✅
- **Tax** — determines W-9 vs W-8 variants (BEN/BEN-E/ECI/EXP/IMY) or Form 8233 by residency; 1,000+ tax-validation rules incl. IRS TIN matching. ✅

## 4. Money-movement model (the Decimal-relevant part)

### Rails
6 documented "primary" methods + virtual cards ✅:

| Method | What | Notes |
|---|---|---|
| US ACH | Domestic clearinghouse | ~$0.40/txn, US-only |
| **Global ACH / eCheck** | Local bank transfers over regional networks (SEPA, BACS/EFT, India NACH, etc.) | **The core cross-border rail** — free/negligible cost |
| Wire (SWIFT) | Correspondent banking | ~$26/intl wire; fallback where local rails absent |
| PayPal | E-wallet payout | Fast, unpredictable fees |
| Paper check | Physical check | Slow, costly |
| Prepaid debit / e-wallet | Underbanked regions | Alternative |
| Virtual Visa/MC card | Single-use card to supplier | Interchange-generating (see below) |

Coverage consistently claimed at **196–200 countries / 120 currencies / 50+ methods.** (The "12 payment methods" figure is not Tipalti's standard number — it more often says "50+" or breaks out "6 primary"; treat as marketing-variable.) 🟡

### Cross-border mechanics
Tipalti **prioritizes local clearing (Global ACH) over SWIFT** to cut cost — its own docs draw the contrast (local = "free or negligible," 1–3 days; SWIFT = $10–35, 3–5 days). Correspondent banks handle conversion/settlement; falls back to SWIFT where local rails aren't available. ✅/🟡

### FX — the real money lever
Per the **Tipalti Services Agreement** (v. 2025-10-14): a currency-conversion fee "set out in the Order Form" is **added to the exchange rate.** ✅ Third-party pricing analyses peg the embedded spread at **~1.5–3.5%** over mid-market (most cite 1.5–2.5%), buried inside the rate rather than shown as a line item. 🟡 (exact %, third-party-sourced; large customers negotiate). Worked example: $2M/month FX at 2.5% ≈ **$50K/month** in embedded currency fees.

### The float question — NO float for the customer ✅
This is the crucial contrast with Bill.com. The Tipalti Services Agreement + help docs state plainly:
- Customers **pre-fund** a "Tipalti Account" — a **"non-interest yielding account dedicated for remittances."** ✅
- *"Any electronic money held in the Tipalti Account is not a deposit, and **Tipalti does not pay Customer any interest** on the balance."* ✅
- ACH-funded deposits take **~4 business days** to land before disbursement — so a transit-float window **structurally exists** — but whether **Tipalti itself** earns interest on it is **NOT publicly disclosed** (private company, no SEC filings). 🔴

**Contrast with Bill.com:** Bill.com's model openly **depends on float** — it reports interest on funds-held as a material segment (~$161.8M cited recently, rate-sensitive). Tipalti **structures the account as non-interest-yielding to the customer and monetizes the FX spread + fees + interchange instead.** Both are middlemen that hold money in transit; the difference is **incentive and disclosure** — float *is* Bill.com's business; for Tipalti it's undisclosed and not the advertised engine.

### Revenue model
Subscription/platform fee (tiered, no per-user) + per-transaction (~$1–5/payment) + **FX spread (biggest payments lever)** + virtual-card interchange (shared as rebate w/ customer; can be net-negative cost). Float/interest is **not** a disclosed line. 🟡

## 5. ERP / accounting integrations

Native, certified: **NetSuite, Sage Intacct, QuickBooks Online, Xero**, + Microsoft Dynamics connector. ✅

- **NetSuite — deepest by far.** Real-time **bidirectional** GL-level sync; syncs suppliers, POs, GRNs, bills, payments, vendor credits; **multi-subsidiary OneWorld** with entity-specific sub-ledgers and consolidated HQ payer roll-up. Claims 25%+ faster close. ✅ **This is the single strongest piece of the moat.**
- **Sage Intacct** — Sage Tech Partner Plus; certified global AP across Intacct/Sage 50/100/200/300/X3. ✅
- **QuickBooks Online** (certified, iFrame+API), **Xero** (certified) — supplier onboarding, tax-form collection, multi-currency, reconciliation. ✅
- **Dynamics / Workday** — published AppSource listing for Business Central; others via API connectors, less depth. 🟡

**Depth ranking:** NetSuite ≫ Sage Intacct ≈ QuickBooks ≈ Xero > Dynamics > others.
**Caveat** 🟡: G2 reviewers repeatedly report **NetSuite sync failures** (~monthly), weak 3-way-match guardrails, and that **Tipalti doesn't actively monitor sync jobs** (customers must report failures; 3–4 day escalations). For a product whose moat *is* the integration, this is a reliability liability.

## 6. API & developer surface

- **Two API generations:** legacy **SOAP** (ProcessPayments, Payee API) + modern **REST** (payments, payees, separate Procurement REST API; JSON, sandbox, Developer Hub). ✅
- **Embedded / white-label:** the **Payout API** is marketed as embeddable — branded self-service payee onboarding (iFrame/API) + programmatic payee/payment management. A genuine differentiator for marketplaces/platforms. ✅
- **Docs quality** 🟡: help-center + sandbox; community Postman collection + third-party Elixir SDK exist. Generally **partner/integration-grade, not Stripe-grade self-serve.**

## 7. Tax compliance engine

- **KPMG-reviewed tax engine** at the core: enforces correct form (W-9 / W-8 family / 8233) + local TIN at registration; 1,000+ validation rules incl. **daily IRS TIN matching**; calculates withholding. ✅ (A genuine, defensible differentiator vs Ramp/Melio/BILL.)
- **1099 / 1042-S e-filing** via Zenwork's Tax1099.com — IRS e-file + recipient copies (electronic/USPS), year-end prep reports. ✅
- **VAT / international** — collects/validates local + VAT IDs across 60+ countries. ✅

---

## Technical architecture (publicly knowable) 🟡

Invoice flow: arrive (email/upload/API) → Invoice Capture Agent (OCR+NLP) → Auto Coding (GL) → PO Matching Agent (2-/3-way at header + line) → Bill Approvers Agent (routing) → execution via Mass Payments rails → reconcile to ERP via sync engine; ERP Sync Resolution Agent handles errors.

Core data-model concepts: **Payees/Suppliers, Bills/Invoices (w/ line items), POs + GRNs, Vendor Credits, Payments**, all keyed to **GL accounts** and (in OneWorld) **subsidiaries/entities** with per-entity sub-ledgers. A central **rules-engine-as-gateway** (~26K payment rules + 1K tax rules + OFAC) sits in front of payment execution. No public detail on language/framework/DB/cloud. 🔴
