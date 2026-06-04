# Tipalti (tipalti.com) — Research Folder

Compiled 2026-06-06 via the deep-dive playbook (5 parallel research streams). Added because Tipalti was missing from the company set despite being named alongside Bill.com as "the bar" in Decimal's strategic doc — and it's the most cross-border-native of the TradFi AP incumbents, making it the most directly relevant comparison for Decimal's cross-border wedge.

---

## Headline finding

**Tipalti is the international, NetSuite-heavy AP + mass-payments engine for the mid-market.** Founded 2010 (Foster City CA + Tel Aviv R&D), it owns the "scaling company that pays many distributed/international payees" niche — above Bill.com's SMB turf, below SAP/Coupa enterprise. Its moat is **cross-border licensed rails (196 countries / 120 currencies) + a KPMG-grade tax/compliance engine + deep multi-entity NetSuite OneWorld integration.** ✅

The honest one-liner: *a strong but expensive, slow-to-implement global AP engine for multi-entity mid-market finance teams on NetSuite — a 2021 unicorn that peaked at $8.3B, has since lost ~70% of its value (secondary ~$2–3B), is defending itself with debt (only debt raised since 2021) and three layoff rounds (2023/2025/2026), and is squeezed by faster/cheaper/more-AI-native card-first rivals (Ramp/Brex/BILL) above and cheap payout networks (Wise/Payoneer) below.*

**The single fact that matters most for Decimal:** unlike Bill.com, **Tipalti does not run on float** — its funding account is contractually *non-interest-yielding to the customer*, and it monetizes the **FX spread (~1.5–3.5%)** + transaction fees + card interchange instead. So Decimal's "we removed the float middleman" wedge lands on Bill.com, not Tipalti. Against **Tipalti** the wedge is the **FX spread** (USDC cross-border at ~$0.001) and the **implementation / UX / AI-velocity tax** (6–18mo NetSuite integrations, ~monthly sync failures).

---

## Folder structure

```
companies/tipalti/
├── README.md                   ← you are here
├── deep_dive.md                ← history, founders, funding, M&A, regulatory
├── architecture.md             ← product SKUs, AI stack, money-movement model, integrations, API
├── product_flow.md             ← end-to-end money + data flow with failure cases
├── use_cases_and_examples.md   ← ICP, verticals, named customers, personas
├── marketing_vs_reality.md     ← claim audit, competitive map, bear case
├── explain_like_new_teammate.md ← plain-English explainer
└── transcripts/                ← (empty; founder interview .txt files would go here)
```

## Quick facts

| | |
|---|---|
| Founded | 2010 · Foster City CA (HQ) + Tel Aviv (R&D) |
| Founders | Chen Amit (CEO), Oren Zeev (Chairman, Zeev Ventures) |
| Peak valuation | $8.3B (Series F, Dec 2021, led by G Squared) |
| Current estimate | ~$2–3B (secondary; no priced round since 2021) |
| Funding | ~$700M+ equity, ~$900M incl. debt; last 2 raises debt-only |
| ARR / volume | ~$200M ARR · ~$70B/yr processed · 4,000+ customers |
| Acquisitions | Approve.com (procurement, 2021) · Statement (AI treasury, 2025) |
| Regulatory | MSB (US) · EMI (UK/EU, DNB) · FINTRAC (Canada); banks: Citi/JPM/Wells Fargo/Visa |
| Money model | Non-interest funding account; revenue = subscription + per-txn + **FX spread** + card interchange |
| Moat | Cross-border rails + KPMG tax engine + multi-entity NetSuite |
| Weak spots | Price, 6–18mo implementation, NetSuite sync reliability, support, AI velocity |

## How to use this folder

- **30 seconds:** read the headline above.
- **5 minutes:** README + `marketing_vs_reality.md`.
- **Comparing to Bill.com / for Decimal positioning:** `deep_dive.md` §"Bottom line for Decimal" + `architecture.md` §4 (money-movement) + `marketing_vs_reality.md` §"What this means for Decimal."
- **Understanding the product:** `architecture.md` + `product_flow.md`.
- **Sizing the market / who buys:** `use_cases_and_examples.md`.

Source URLs are cited inline throughout each file (Tipalti primary docs, Services Agreement, press releases, TechCrunch/PRNewswire/PaymentsDive, G2/Capterra/Gartner reviews, Contrary/Sacra/GetLatka, Stampli/Ramp/Wise comparison pages). Caveat: comparison pages from competitors (Stampli/Ramp/Wise) were used only for verbatim reviewer quotes, not their conclusions; "99% retention," "66% error reduction," payment-volume, and current-valuation figures are vendor-reported or secondary-market estimates, not audited.
