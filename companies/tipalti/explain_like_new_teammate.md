# Tipalti — Explain Like a New Teammate

*A dumb-questions explainer for someone who must understand Tipalti by tomorrow.*

## What does Tipalti do in one sentence?

Tipalti is a 16-year-old global accounts-payable + mass-payments platform that lets a scaling mid-market company onboard, tax-validate, and pay thousands of suppliers/creators/affiliates across 196+ countries and 120 currencies from one system — and unlike pure software, it holds and moves the money itself as a licensed money transmitter, making most of its payments margin on the FX spread rather than (like Bill.com) on float.

## What problem existed before it?

Stripe/PayPal/Square solved *collecting* money. Nobody solved *paying out* at scale. A marketplace paying 5,000 creators in 40 countries had to: collect each one's bank + tax details by hand, figure out W-8 vs W-9, validate IBANs, wire money one-by-one (or batch through a bank portal), eat SWIFT fees and FX, then reconcile it all into NetSuite manually. Tipalti automated that entire payout-and-payables pipeline.

## Who buys it?

Mid-market companies, ~50–1,000 employees, that **pay lots of distributed/international payees** — marketplaces, ad networks, affiliate platforms, creator economy, gaming/e-sports, multi-entity SaaS. The buyer is the CFO/Controller/AP Manager whose pain is "we're scaling and drowning in global supplier payments + tax forms, and I don't want to hire 3 more AP people." It is explicitly **NOT** for tiny domestic-only SMBs — that's Bill.com's turf, and Tipalti is overkill/too pricey/too slow to implement there.

## How is it different from Bill.com? (the question that matters most here)

Three things:
1. **Global vs domestic.** Bill.com is US-domestic-heavy with a strong accountant channel. Tipalti is built for cross-border — 196 countries, local clearing rails, multi-currency, deep international tax.
2. **Float vs FX.** Bill.com's business *runs on float* — it holds your money in transit and earns ~$162M/yr in interest. Tipalti's funding account is **non-interest-yielding to you**, and it makes its payments money on the **FX spread (~1.5–3.5%)** baked into the exchange rate instead.
3. **Mid-market multi-entity vs SMB single-entity.** Tipalti's moat is deep **NetSuite OneWorld** integration — paying across many subsidiaries with entity-level GL coding. Bill.com is simpler/single-entity.

## How does one payment actually work?

1. The payee self-onboards in the **Supplier Hub** — enters bank details, completes their tax form (W-9 or W-8), gets validated (TIN match, OFAC, ~26,000 payment rules).
2. An invoice arrives → AI captures it, auto-codes the GL, matches it to a PO, routes it to the right approver.
3. You **pre-fund** a Tipalti account (ACH takes ~4 days). The money sits in a non-interest account at Citi/JPMorgan/Wells Fargo.
4. On approval, Tipalti screens the payment, then disburses via the cheapest viable rail — usually **local bank transfer** (Global ACH), or SWIFT wire, PayPal, check, prepaid, or a virtual card.
5. If currency conversion is needed, Tipalti adds its FX spread to the rate.
6. The payment + reconciliation syncs back into NetSuite/Intacct/QuickBooks/Xero.

## Why is this hard to build?

- **Licensed money movement** — MSB (US) + EMI (UK/EU) + FINTRAC (Canada), tier-1 bank relationships, OFAC/AML ops.
- **The payee identity + validation graph** — ~26,000 payment rules across countries; getting an Indian IFSC or EU IBAN right before money moves.
- **Global tax** — W-9/W-8/1099/1042-S/VAT across 60+ countries, KPMG-reviewed, daily IRS TIN matching.
- **Deep ERP sync** — real-time bidirectional NetSuite OneWorld integration (also its most-complained-about feature).

## What's genuinely impressive?

- The **KPMG-grade tax/compliance engine** — a real differentiator Ramp/Melio/BILL don't match at this depth.
- **Multi-entity NetSuite depth** — the stickiest part of the moat.
- **196-country licensed rails** preferring cheap local clearing over SWIFT.
- The **embedded/white-label Payout API** for marketplaces.

## What's the catch / what's wrong?

- **Valuation down ~70%** from its $8.3B 2021 peak (secondary estimates ~$2–3B), **three layoff rounds** (2023/2025/2026), **only debt since 2021** (no priced equity — avoiding a down-round), **no IPO.**
- **Slow, fragile implementation** (6–18 months) and **NetSuite sync that fails ~monthly** with slow support — ironic for a product whose moat is the integration.
- **Expensive and opaque** (FX spread buried in the rate, pre-funding drag, real implementation fees).
- **AI commoditization** — invoice extraction is now table-stakes; Tipalti is reacting (bought Statement, "$200M for AI"), not leading. Ramp/Brex ship faster.

## The mental model

Think of Tipalti as: **the international, NetSuite-heavy AP engine for mid-market companies that pay armies of global payees — a regulated money-mover that profits on FX spread, with a genuine tax/compliance + multi-entity moat, but priced and paced like enterprise software and now defending a deflated 2021 unicorn valuation with debt and layoffs.**

Or: **Bill.com's bigger, more global, more expensive cousin — strong where Bill.com is weak (cross-border, multi-entity, tax) and weak where the neo-fintechs are strong (price, speed, UX, AI velocity).**

## Why it matters for Decimal

Tipalti is the closest TradFi analog to Decimal's cross-border ambition — and it proves "pay many global payees" is a billion-dollar market. The opening against it is **cost + speed on cross-border** (USDC at ~$0.001 vs an embedded 1.5–3.5% FX spread; instant on-chain settlement vs days + months of implementation) plus a **reliability story** (provable on-chain status vs stuck sync jobs). The thing Decimal must eventually answer to take Tipalti-style accounts: **global tax compliance + multi-entity consolidation** — currently out of Decimal's scope, but exactly what these customers buy.

## Related files

- [deep_dive.md](./deep_dive.md) — history, founders, funding, M&A, regulatory
- [architecture.md](./architecture.md) — product SKUs, AI stack, money-movement model, integrations, API
- [product_flow.md](./product_flow.md) — end-to-end money + data flow with failure cases
- [use_cases_and_examples.md](./use_cases_and_examples.md) — ICP, verticals, named customers, personas
- [marketing_vs_reality.md](./marketing_vs_reality.md) — claim audit, competitive map, bear case
