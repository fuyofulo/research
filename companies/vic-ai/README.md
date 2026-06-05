# Vic.ai (vic.ai) — Research Folder

Compiled 2026-06-06. Researched as the **purest "AI does the AP autonomously" play** — the test case for "is AI invoice processing a moat or a commodity?"

Confidence: ✅ high · 🟡 medium · 🔴 low/unverified.

---

## Headline finding

Vic.ai is an **AI-native AP automation platform** whose **"Autopilot"** aims to process invoices end-to-end — extraction, GL coding, approval routing, payment — **autonomously rather than via rules**, for high-volume mid-market/enterprise finance teams on modern ERPs. ✅ It is the highest-conviction "remove the human from AP" pitch, built on proprietary deep-learning models ("trained on >1B invoices"). Claims: 97% accuracy out-of-box → 99% over time; **~85% "no-touch" / ~70% full "Autopilot" by month 6.** 🟡 (vendor-defined, unaudited, mature-state — not day-one).

The honest one-liner: *the highest-conviction "let the AI run AP itself" platform for high-volume enterprises on modern ERPs — impressive proprietary-data-driven autonomy, but selling unaudited month-6 touchless rates into a market where extraction is commoditizing and bigger players are bolting on the same "agentic" pitch.*

## Fundamentals

- Founders **Alexander Hagerup (CEO) + Kristoffer Roil (COO)** — Norwegian. Founded **2017** (Norway), HQ New York + Oslo roots. ✅
- **Funding:** Seed 2017 (Cowboy Ventures) → A $11.2M (2019, GGV) → **B $50M (Sep 2021, ICONIQ Growth)** → **C $52M (Dec 2022, GGV + ICONIQ)**. **Total $115M; no valuation disclosed.** ✅
- **2024–26:** **No raise since Dec 2022** (~3.5 yrs, notable in an AI funding boom); flat-to-declining headcount (~87–102); est. revenue ~$19M (third-party). 🟡 No layoffs/acquisition found.

## Product & the AI story

- **Autopilot** (touchless straight-through processing) + **PO matching** (2-/3-way, "Autopilot for PO invoices" 2025) + continuous learning from corrections.
- **2025 "agentic" relaunch (Jun 2025):** **Victoria™** orchestration layer + **VicAgents™** (VicInbox live; Contract Agent + Analytics Agent in beta) + **VicPay 2.0** (payments) + Vendor Portal (Plaid-verified onboarding). CEO: "not copilots or dashboards — autonomous AI partners." (Aspirational; several agents still beta.) ✅/🟡

**Is the autonomy real / a moat?** Directionally real but vendor-defined and unaudited; note "no-touch" (~85%) ≠ full "Autopilot" (~70%), and these are month-6 mature-state figures. **The key strategic read: extraction is commoditizing fast** (frontier LLMs + RAG read invoices ~99% out-of-box; inference costs collapsed ~280× in two years). The durable moat shifts to **(1) proprietary AP data + per-customer correction loops, (2) deep ERP integration, (3) the orchestration/agent layer + money movement** — which is exactly why Vic.ai pushed into VicPay + VicAgents in 2025.

## Money model, ERP, customers

- **VicPay 2.0** moves money (ACH/check/virtual card/international) over "its own rails" via a funding account; **no transaction fees on US payments** → likely monetizes via **interchange/rebates + float/FX** (banking partner & model undisclosed 🔴). Core = enterprise SaaS subscription (custom, volume-based).
- **ERP:** NetSuite, Oracle Fusion, SAP, MS Dynamics, Workday, PeopleSoft, Sage Intacct, Coupa. ✅
- **Target:** upper-mid-market/enterprise (300–5,000+ employees, 1,000+ invoices/mo), accounting firms, PE-backed portfolios. Named: HSB, Intercom, Armanino, Diesel Direct. ✅
- **Position:** focused, well-regarded but **mid-sized** independent; outgunned on scale/distribution by BILL/Ramp/Tipalti/Stampli + native ERP AI, all now marketing "agentic AI." Edge = autonomy depth + proprietary data; weakness = distribution + no raise since 2022.

## Relevance to Decimal — the "is AI a moat" answer

Vic.ai is **the cleanest test of the thesis baked into Decimal's own strategic doc ("extraction is no longer a moat").** Vic.ai bet the company on autonomy, and the market verdict is converging: **extraction/coding is commoditizing; the moat moved to proprietary data + ERP depth + the orchestration layer + money movement.** For Decimal this validates two decisions: (1) **don't pitch AI extraction as the moat** — pitch the agent-with-tools orchestration + code-enforced execution; (2) Vic.ai's scramble down-stack into payments (VicPay) mirrors the gravity Decimal already lives in (the agent drafts, code/multisig executes). The differentiator Vic.ai *lacks* and Decimal *has* is **deterministic code-enforced execution at a multisig gate** — Vic.ai's autonomy makes mistakes *into payments* with only software controls; Decimal's multisig + spend rules make agent mistakes structurally un-executable. That contrast is worth sharpening in Decimal's positioning.

---
Sources: [Vic.ai how-it-works](https://www.vic.ai/how-it-works) · [VicPay/VicAgents launch](https://www.vic.ai/news/vic-ai-launches-vicpay-vendor-portal-and-vicagents-accelerating-the-shift-to-autonomous-finance) · [Series C $52M](https://techcrunch.com/2022/12/13/vic-ai-shows-that-automating-accounting-processes-can-be-profitable-raises-52m/) · [Series B $50M/ICONIQ](https://techcrunch.com/2021/09/01/autonomous-accounting-platform-vic-ai-raises-50m-round-led-by-iconiq-growth/) · [payments](https://www.vic.ai/payments) · [AI commoditization](https://www.amadeuscapital.com/ai-commoditisation-curve/) · [Stampli vs Vic.ai](https://www.kenfromfinance.com/blog/stampli-vs-vic-ai).
