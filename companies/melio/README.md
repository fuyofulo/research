# Melio (meliopayments.com) — Research Folder

Compiled 2026-06-06 (single comprehensive stream). Researched as the SMB embedded-AP gap on the TradFi side.

Confidence: ✅ high · 🟡 medium · 🔴 low/unverified.

---

## Headline finding (two big corrections to the original premise)

1. **Melio no longer powers QuickBooks Bill Pay.** Intuit ran "Bill Pay powered by Melio" only ~2023→**May 2024**, then **in-sourced** its own native QuickBooks Bill Pay and dropped Melio. The embed was a bridge, not a moat. ✅
2. **Melio is no longer independent.** **Xero acquired it for ~$2.5B (closed Oct 15, 2025**; $2.15B cash + ~$360M stock + up to $500M retention). Co-founder **Matan Bar now runs Xero's entire US business.** ✅

So Melio's lesson is the cautionary tale of **embed dependence**: the platform owner (Intuit) absorbed the capability; Melio then sold itself to Intuit's arch-rival (Xero) to become Xero's US payments + AI weapon against QuickBooks.

The honest one-liner: *a well-built, cheap SMB bill-pay engine whose real product is distribution-as-a-service (white-labeling AP to banks/platforms) — it got burned when Intuit in-sourced the embed, then sold to Xero for $2.5B.*

## Fundamentals

- **Founded** 2018 by **Matan Bar (CEO), Ilan Atias (CTO), Ziv Paz (COO)** — Israeli founders. HQ NYC + Tel Aviv R&D + Denver. ~600 employees. ✅
- **Funding:** Seed/A ~$16M → B $48M (Mar 2020) → C $80M+$110M (2020→Jan 2021, $1.3B) → **D $250M (Sep 2021, ~$4B peak)** → **E $150M (Oct 2024, $2B down-round, led by Fiserv** w/ Shopify + Capital One Ventures). Total raised ~$650M. ✅
- **Exit:** Xero, ~$2.5B, Oct 2025. ✅

## Product & money model

- SMB **AP bill pay** (OCR capture, recurring, approvals) + **AR/get-paid**; methods: **ACH free**, **card 2.9%**, check, same-day ACH (~1%), instant (~1.5%). Deep QuickBooks + Xero sync. ✅
- **AI:** OCR capture + **"Agent Mel"** conversational assistant (launched Jan 2026); now feeds Xero's AI-agent roadmap. ✅
- **Money model — FBO:** customer funds held in trust at **Evolve Bank & Trust** (+ JPMorgan, SVB/First Citizens) during processing, then disbursed. **Monetizes via card take-rate (the workhorse), same-day/instant fees, float, and syndication (~35% of revenue).** Free ACH is a loss-leader; card + international >60% of revenue. ✅

## Distribution (the real moat)

White-label / embedded is the actual business: **Fiserv "CashFlow Central"** (~3,500 US banks, ~18M SMBs), **Shopify Bill Pay**, **Capital One**, and now **Xero** (parent + flagship embed). Direct SMB acquisition is expensive; the channel carries reach. ✅

## Scale (FY ended Mar 2025)

~80K–100K business clients · ~$30B processed in FY25 ($100B+ lifetime, 40M+ bills, 2M+ vendors) · ~$153M revenue (~$187M run-rate at deal time) · crossed $100M ARR in 2024. ✅

## Competitive position

- **vs BILL:** the cheaper, simpler, down-market alternative (~$22–68/mo vs BILL's $45–79/user). Both *lost* the Intuit embed when Intuit in-sourced. Post-Xero, Melio is now baked into a direct QuickBooks rival's ecosystem → real competitive pressure on BILL's low end.
- **vs Ramp/Brex:** different wedge — Melio leads with vendor bill-pay for businesses without a card program; Ramp/Brex lead with cards + spend.

## Relevance to Decimal

**Melio is the embedded-distribution lesson, not a direct competitor.** Two takeaways: (1) **Embed dependence is fatal** — the platform owner can in-source you (Intuit→Melio). If Decimal ever pursues embedded/white-label distribution (e.g., inside a Solana wallet or neobank), own the customer relationship or expect to be absorbed. (2) **Melio's "free ACH, monetize the card/float" model is exactly the float/interchange game Decimal's self-custodial USDC model bypasses** — another data point that the TradFi AP business is really a payments-monetization business, which is the thing crypto-native rails disrupt. Pure TradFi, US-domestic, no cross-border or stablecoin relevance beyond that.

---
Sources: [Xero acquisition PR](https://www.prnewswire.com/news-releases/xero-to-acquire-melio-a-leading-us-smb-bill-pay-solution-to-accelerate-global-growth-302490268.html) · [Payments Dive (deal)](https://www.paymentsdive.com/news/melio-xero-acquisition-payments-deal/751600/) · [Intuit drops Melio](https://insightfulaccountant.com/accounting-tech/general-ledger/intuit-discontinues-melio-powered-bill-pay-in-qbo/) · [Series E $2B](https://www.calcalistech.com/ctechnews/article/s1ajjsrg1e) · [Agent Mel](https://www.businesswire.com/news/home/20260128029190/en/) · [how Melio makes money](https://productmint.com/how-does-melio-make-money/) · [Series D $4B](https://www.prnewswire.com/news-releases/melio-raises-250m-to-fuel-expansion-of-its-b2b-payments-platform-and-forge-new-partnerships-tripling-valuation-to-4b-301376128.html).
