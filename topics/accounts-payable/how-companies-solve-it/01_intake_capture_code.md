# Stage 1 — Intake → Capture/Extraction → GL Coding

*The problem: how invoices get in, how their data is read, and how they get coded to the GL.*

## The problem

Three hard sub-problems before an invoice can be matched/approved/paid: **intake** (consolidate heterogeneous channels — paper, PDF-email, portal, EDI, e-invoice, API, on-chain request — into one normalized pipeline), **capture/extraction** (template-free reading of header + the harder line items; manual baseline ~111 sec / ~105 keystrokes per invoice, ~12.5% rework), and **GL coding** (a *prediction*: which account/cost-center/project this spend belongs to — hardest for novel/non-PO spend).

**Framing fact:** extraction is **commoditizing** — frontier LLMs + RAG read invoices ~99% out-of-box, inference costs fell ~280× in two years. Capture/IDP and approval routing are *mature*; GL coding for novel spend and clean matching remain *hard*. Differentiation has moved off "can you read the invoice" onto **proprietary coding data + ERP-sync depth + the agentic action layer**.

## How each company solves it

| Company | Intake | Capture | GL coding |
|---|---|---|---|
| **Bill.com** | email-forward inbox, BILL Inbox upload, BILL Network direct send | AI Coding Agent (doc-type → header ~99% → line-item weaker → confidence scoring) | ML from last ~5 bills/vendor + COA patterns + **250M-bill corpus**; high-conf auto-codes |
| **Tipalti** | email/upload/API + Supplier Hub | Invoice Capture Agent (OCR+NLP, header+line) | Auto-coding from history; PO Matching Agent; self-describes as *reacting not leading* on AI |
| **Stampli** | invoice-centric hub | **Billy the Bot** (since ~2018, earliest AP AI) | learns *each customer's* GL patterns; 2025 "agentic" reframe (~86% of finance work, unaudited) |
| **Vic.ai** | VicInbox agent + modern-ERP feed | Autopilot, proprietary DL "trained on >1B invoices," 97→99% | ML + continuous correction loops; ~85% no-touch / ~70% Autopilot **by month 6** (unaudited) |
| **Ramp** | email/upload | **vision model + OCR fallback**; GPT-since-2023 | Agents for AP code line items; ~60% auto @99% precision (claim); fastest shipper |
| **Request Finance** | **invoice = on-chain Request** + web + CSV | "Smart Invoice Capture" AI OCR | via native **Request Accounting** (ex-Consola); ML-from-history depth *not documented* |
| **Routable** | **API-first** + CSV + white-label portal | OCR via OpenAI; "99.8%" sync | PO-matching + ERP sync; ML-coding depth *not documented* — strength is onboarding/sync |
| **Altitude** | Bill Pay PDF upload + CSV batch (new 2026) | light OCR (vendor/amount/IBAN) | minimal; accounting integrations "referenced but not public" |

*Brex's own architecture note nails the thesis: "The hard part is not generating text. The hard part is mapping spend to the right legal entity, department, budget, GL code, and policy state with enough confidence for accounting."*

## Crypto-native difference

- **Request:** the invoice is itself an **on-chain object** (Request ID) — tamper-proof audit trail built in — but still has a TradFi-style OCR layer for PDFs; coding served by its own crypto-accounting engine. **EVM-first (Solana ~6%, not in API)** — the clearest gap a Solana-native entrant exploits.
- **Altitude:** account-led, not AP-led. Bill Pay is a thin convenience feature with light OCR; **no deep IDP, no ML coding-from-history.** Differentiation is custody + rails, not capture.

## Spectrum

1. **Commodity OCR + rules** (brittle, ~35–55% touchless ceiling) — the floor; no one wins here.
2. **Frontier-LLM/vision extraction** (~99% out-of-box) — **commoditizing, NOT the moat** (Ramp, BILL, Vic.ai cluster here).
3. **Proprietary-data coding + agentic action + ERP depth** — where differentiation lives: correction-loop data flywheels (BILL 250M corpus, Stampli per-customer learning, Vic.ai loops) + deep two-way ERP sync.

*Honest read: every vendor cites ~99% extraction / 60–95% touchless, almost all unaudited and mature-state. The canonical org average is **~32.6% touchless** (Ardent).*

## Build implication

- **Buy/commodity:** extraction. Use a vision-LLM (Claude/GPT/Gemini) + OCR fallback (Ramp's pattern; Routable literally uses OpenAI). Don't build proprietary OCR or pitch extraction as the edge.
- **Build (the hard part):** **GL-coding via RAG over the customer's own vendor/coding history** + LLM + confidence gate; the moat is the *correction-loop flywheel*, compounding per customer. Plus deep two-way ERP sync (Stage 5).
- **The genuinely hard part:** not reading the invoice (solved) — **predicting the right GL code for novel/non-PO spend AND reconciling it cleanly into a real ERP.** A data + integration problem, not a model problem.
- **Crypto-native edge:** pair the agent with **code-enforced execution at a multisig gate** so a mis-code can't auto-execute into a payment (Stage 2/6).

*Gaps: Stampli/Vic.ai/Routable/Request coding mechanics under-documented locally; no independently-audited accuracy numbers exist (only Ardent averages); e-invoicing/Peppol intake not mapped per-company.*
