# Routable (routable.com) — Research Folder

Compiled 2026-06-06. Researched as the **API-first / embeddable mass-payouts** player — architecturally the closest TradFi analog to a programmatic stablecoin AP/payout product.

Confidence: ✅ high · 🟡 medium · 🔴 low/incorrect-premise.

---

## Headline finding

Routable is an **API-first AP automation + mass-payouts platform** that lets platforms/marketplaces/finance teams programmatically send large volumes of B2B payments (vendor/contractor/seller disbursements) across many rails and 220+ countries from one REST API or a white-label payee portal. ✅ It's **well-built but sub-scale** (~$20.7M revenue 2024, ~80 employees, ~$46M raised, no megaround since 2021). ✅

**The most strategically important finding:** Routable **already shipped stablecoin payouts via a Brale partnership (Jul 2025)** — stablecoin is just another swappable rail behind its payouts API, where *the payee chooses* local-currency bank transfer or USD via stablecoin. **This empirically proves the durable value sits in the orchestration / onboarding / tax / ERP-sync layer, NOT the rail.** ✅

The honest one-liner: *a well-built but sub-scale API-first AP-and-mass-payouts platform whose real moat is payee onboarding + tax + ERP sync wrapped around swappable rails — the cleanest TradFi template for what an embedded stablecoin payout product would have to replicate.*

## Fundamentals (premise corrections)

- Founders **Omri Mor (CEO) + Tom Harel (CTO)**, founded **2017**, HQ San Francisco (Seattle roots, remote). Mor's prior company was the **ZIIBRA** artist marketplace (not "Routable/Kanback"). 🔴 corrected.
- **Funding:** Series A $12M (Aug 2020, Addition/Lee Fixel) → **Series B $30M (Apr 2021, led by Sam & Jack Altman** — NOT Lightspeed 🔴; no valuation ever disclosed). **Total ~$46.2M across ~4 rounds.** (Aggregator "$96M/Series B1" figures appear erroneous.) ✅
- **2023–26 status:** alive and shipping, no layoffs/pivot/acquisition found. Added FX (Convera, Dec 2025), **FedNow (Aug 2025)**, **Brale stablecoin (Jul 2025)**, OCR + vendor risk screening (2024). ✅

## Product & money model

- **AP automation** (OCR intake, approvals, PO-matching, vendor screening vs 6,000+ watchlists) + **AR** + **mass payouts** (100→100,000+ payouts via API/CSV, **no volume minimum** — a deliberate contrast to Tipalti/Trolley). ✅
- **API / DX (the core):** REST, "integrate in <3 dev days," 14 webhook events, idempotency; **white-label payee onboarding portal** that holds vendor PII/tax/bank data so the platform never touches it. ERP sync (QBO, NetSuite, Xero, Sage Intacct), claimed 99.8% accuracy. ✅
- **Rails:** ACH, same/next-day ACH, **RTP + FedNow**, wire, check, SWIFT (220+ countries/140+ currencies), **stablecoin (via Brale)**. ✅
- **Float:** a prefunded **"Routable Balance"** funds expedited rails — functionally FBO-like; sponsor bank not named. ✅
- **Infra partners:** Dwolla (ACH), Currencycloud/Visa + Convera (FX), Plaid (verification), Check Issuing (checks), **Brale (stablecoins)**, AiPrise/Trulioo (KYB), OpenAI (OCR). ✅
- **Monetization:** subscription (Growth $1,250/mo; Scale/Enterprise custom) + per-transaction (undisclosed). No free tier; virtual-card/interchange not prominent. 🟡

## Customers & competitive

Named: Ticketmaster, Snackpass, RE/MAX, Mongabay (nonprofit paying journalists in 220+ countries, switched from BILL citing need for human support). Verticals: marketplaces, gig/delivery, creator royalties, logistics, real estate, nonprofits. ✅

Competitive: squeezed in the middle — too API-centric to beat BILL on SMB AP, too small to beat Tipalti on enterprise, faces **Stripe Connect's gravity** on embedded payouts (Routable's pitch: "disburse, not collect"; migrate payees without re-KYC). Closest direct analog is **Trolley** (Routable has no 100/mo minimum). ✅

## Relevance to Decimal — the single most useful comparable in the whole set

Routable is **the TradFi blueprint for exactly what Decimal is architecturally**: a programmatic, API-triggered payout engine where the platform calculates who-gets-paid and calls one endpoint; a prefunded balance you top up and draw down (≈ a stablecoin treasury); white-label payee onboarding holding KYC/tax/bank data; ERP sync. **The punchline for Decimal:** Routable's Brale move proves a stablecoin-native competitor isn't competing on "can you move USDC" — it's competing on **payee onboarding + tax (W-9/W-8/1099/1042) + ERP sync + the embed SDK**, which is precisely the layer Routable spent 8 years building. That's where Decimal must be excellent; the Solana/USDC rail alone is not the moat. Also a model for offering **payee choice** (local fiat vs stablecoin) behind one API.

---
Sources: [Routable about](https://www.routable.com/about/) · [Payouts API](https://www.routable.com/features/payouts-api/) · [Brale partnership](https://www.routable.com/press/brale-partnership/) · [FedNow](https://www.routable.com/press/routable-fednow-instant-payments/) · [sub-processors](https://www.routable.com/legal/sub-processors/) · [TechCrunch Series B (Altmans)](https://techcrunch.com/2021/04/15/altman-brothers-lead-b2b-payment-startup-routables-30m-series-b/) · [GetLatka](https://getlatka.com/companies/routable/funding) · [Stripe Connect alternatives](https://www.routable.com/resources/stripe-connect-alternatives/).
