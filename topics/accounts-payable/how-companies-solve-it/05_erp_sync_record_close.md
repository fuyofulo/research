# Stage 5 — ERP/GL Sync → Reconciliation → Record & Close

*"ERP sync is the real moat" — and, per the research, the most-complained-about feature in the category. The Tipalti irony: the thing that *is* the moat is the thing customers hate most.*

## The problem

**The GL inside the ERP is the system of record; an AP tool is just a workflow layer on top.** Every invoice must post to the right GL accounts and every payment reconcile in the ERP — or the books are wrong and the audit fails. What makes 2-way real-time sync hard:
- **Different ERP data models** — a NetSuite connector ≠ an SAP connector; you pull vendors/COA/POs/dimensions *and* push bills/payments/credits mapped to each ERP's object graph.
- **Master-data mismatch** — vendor names/GL codes/dimensions rarely match cleanly; this is what breaks auto-matching/coding (data-hygiene, not math).
- **Closed-period locks** — the sync must respect period locks, route late items to accruals.
- **The double-write failure mode** — any failure leaves subledger and GL out of balance → "ghost transactions," manual cleanup.

**Reconciliation/close:** post subledger → GL; reconcile AP aging (subledger) to the GL AP control account; enforce cutoff; book accruals; document the tie-out. Maturity: reconciliation/ERP-sync is only **~12% fully automated** (Ardent) — the moat is real *because* it's unsolved at scale.

## How each company solves it

| Company | ERPs | Depth | Recon/close |
|---|---|---|---|
| **Tipalti** | NetSuite, Intacct, QBO, Xero, Dynamics | **deepest: real-time bidirectional NetSuite OneWorld, multi-subsidiary, entity sub-ledgers** | 25%+ faster close — **but sync fails ~monthly, unmonitored, 3–4d escalations** |
| **Bill.com** | QBO, Xero, NetSuite, Intacct, Dynamics 365 BC (2-way) | 2-way (near-real-time, queued); import-only for Acumatica/Sage 50/100 | recon report (matched/unmatched); **sync break = most common failure** |
| **Stampli** | **70+ ERPs** | **breadth + speed: "keep your ERP, deploy 4–6 weeks"** (vs Tipalti 6–18mo) | ERP-sync recon; no AR module |
| **Vic.ai** | NetSuite, Oracle, SAP, Dynamics, Workday, PeopleSoft, Intacct, Coupa | **autonomous posting** (extract→code→route→post STP) | correction-loop; recon mechanics not detailed |
| **Ramp** | 30+ (NetSuite, QBO, Intacct, Xero, Workday, Dynamics, Acumatica, Oracle) | real-time NetSuite/Intacct gated to Plus ($15/user) | **AI month-end close shipped Q3 2025** (recon 5–6h → <30min in cases) |
| **Request Finance** | QBO, Xero, NetSuite (2-way; NetSuite = top tier) + **native Request Accounting** | 2-way to 3 SMB/mid ERPs; crypto-accounting native (vs depending on Cryptio/Bitwave) | **tamper-proof on-chain record per invoice + one-click auditor export** |
| **Routable** | QBO, NetSuite, Xero, Intacct | "99.8% accuracy"; API-first; depth not specified | recon via sync + 14 webhook events |
| **Altitude** | **none shipped** ("coming soon") | **GAP — no ERP/GL sync today** | on-chain record only; **no documented bridge to a customer's GL** |

*Melio: deep QBO+Xero (SMB) — and the cautionary tale (Intuit in-sourced QuickBooks Bill Pay, dropped Melio May 2024; Melio sold to Xero ~$2.5B): the ERP/platform owner can absorb the AP layer entirely.*

## The crypto-native duality

The pitch is **on-chain settlement as an automatic, verifiable audit trail** (every payment a signed, timestamped, immutable tx). Request operationalizes it: "tamper-proof on-chain record per invoice... one-click auditor export." Native crypto-accounting (Request Accounting/Consola, Cryptio, Bitwave) handles cost-basis fiat ERPs can't.

**But the duality is the whole point:** the same companies *still must sync to the customer's QBO/NetSuite/Xero* — Request, the purest crypto-native AP product, built 2-way sync to exactly those three, because **the customer's books live there, not on-chain.** On-chain settlement is a *better source document*, not a substitute for posting to the GL control account. A crypto-native product gets a superior audit trail for free and **still owes the entire ERP-connector + reconciliation + close burden.**

## The Tipalti irony

The thing that *is* the moat is the thing customers complain about most. Tipalti's deepest, stickiest asset is real-time bidirectional NetSuite OneWorld sync — and its most-cited complaint is *that same sync* ("≥1 integration complication each month," "doesn't monitor their sync jobs," "cannot recommend Tipalti to anyone integrating with NetSuite"). For a product whose moat *is* the integration, "fails ~monthly, support takes 3–4 days" is existential. It's structural (BILL's "sync break" is its most common failure too): **the connector is hard to build, hard to keep working, brutal to support — which is exactly why it's defensible.**

## Build implication

- **ERP connectors are the make-or-break engineering moat, not the UI.** Buyers test for "deep, two-way, real-time GL sync." The Tipalti reliability gap is the clearest opening in the whole set: *"your money's status is provable on-chain, not stuck in a sync job."*
- **Build vs buy:** unified accounting-integration APIs (**Merge / Codat / Rutter**) ship breadth fast (Stampli-style 70+ ERPs without building 70 connectors) — but rarely the *depth* that wins enterprise (multi-entity OneWorld, period locks, dimension mapping). **Pragmatic path: buy the long tail via an aggregator, hand-build the 2–3 ERPs your ICP runs (NetSuite first for mid-market).**
- **Operational reliability is a feature, not plumbing.** The complaints are about *unmonitored sync jobs + slow escalation* — active sync-job monitoring, auto-retry, recon dashboards, fast support are a differentiator because incumbents under-invest there.
- **Crypto-native:** map on-chain tx hashes → GL journal entries → AP-control-account reconciliation, respecting period locks. Native crypto-accounting (cost-basis) is a real edge — but *additive to*, not a replacement for, GL sync.
- **The hard part:** master-data mapping (vendor + COA + dimensions across mismatched models), respecting closed-period locks, and the double-write balance guarantee. Every incumbent bleeds here, and **the chain doesn't reconcile your customer's NetSuite for you.**

*Gaps: Stampli/Vic.ai/Routable per-ERP depth (1-way vs bidirectional, period-lock handling) not specified locally; Altitude confirmed no shipped ERP integration (product gap); Request fiat-GL close depth thin beyond "2-way + CSV."*
