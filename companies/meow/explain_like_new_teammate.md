# Meow — Explain Like a New Teammate

*Compiled 2026-05-21. The "dumb questions" file. Written for a smart new teammate who knows nothing about Meow or the startup-treasury category.*

---

## What does Meow do, in one sentence?

Meow is a high-yield treasury platform for startups — it lets your $20M Series B sit in a U.S. Treasury bill ladder earning ~5% instead of in a Mercury checking account earning ~0%, with a Bridge-powered stablecoin send/receive product layered on top.

---

## What problem exists before this product?

A typical VC-backed startup has $20M in the bank after a Series A or B raise. That money sits in:
- **Mercury or Brex operating account:** earning 0% to ~2% APY, FDIC-insured (but the cash sits idle)
- **OR** spread across multiple accounts to maximize FDIC limits
- **OR** in some sweep MMF the CFO set up manually with the bookkeeper

The opportunity cost is real. With Fed funds at 5%+, a $20M idle balance is leaving **$1M+ of annual yield on the table.** For a startup burning $400K/month, that's the difference between 27 and 30 months of runway from the same raise.

Before Meow / Mercury Vault / Brex Treasury, the workflow to capture this yield was:
1. Set up a separate brokerage account at Schwab/Fidelity/Vanguard
2. Manually ladder T-bills via TreasuryDirect or a broker
3. Reconcile across multiple accounts in QuickBooks
4. Hope the brokerage UI doesn't trip you up
5. Lose 1-2 days of liquidity if you need to redeem

Treasury startups (Meow, Mercury Vault, Brex Treasury) collapse this into a one-click workflow.

---

## Who buys it?

Three buyer profiles:

1. **VC-backed startups (Series A to pre-IPO)** with $5M–$50M in idle cash. The CFO/operations lead is the buyer; the founder signs off. This is the bulk of customers.
2. **Crypto-native startups** (DeFi protocols, web3 infrastructure, AI x crypto) — these customers also want the stablecoin send/receive product (Bridge integration) to handle international contractor payouts in USDC.
3. **Multi-entity holdcos / SPVs** — operators who manage multiple LLCs and need treasury management per entity. Smaller segment.

---

## Who uses it day to day?

- **CFO or finance lead** — does the treasury allocation, monitors yield
- **Bookkeeper** — reconciles monthly statements to QuickBooks/Xero
- **CEO/founder (at smaller startups)** — approves wires above thresholds
- **CPA at year-end** — uses 1099-DIV/INT/B for tax filing

---

## What exactly happens, step by step, inside the product?

1. CFO signs up, completes KYB (heavier than Mercury — 2-7 days because broker-dealer KYC rules apply)
2. KYB approved → three sub-accounts created: operating cash (at Grasshopper Bank), brokerage (at Velox via Meow Markets LLC), stablecoin (via Bridge)
3. CFO funds via ACH from external bank → lands at Grasshopper
4. CFO directs allocation: e.g., $15M into a 4/8/13/26-week T-bill ladder, $5M into TTTXX (BlackRock Treasury Trust MMF) for liquidity
5. Meow Markets purchases T-bills/TTTXX shares in CFO's name at Velox
6. Daily yield accrues; CFO sees real-time balance in dashboard
7. CFO can: redeem MMF same-day; T-bills auto-mature on schedule and reinvest; wire out any amount with appropriate approvals
8. For international contractor payments, CFO uses Bridge integration: USD debits → USDC on Solana/Base → swaps to local currency (MXN/BRL/EUR/NGN) → recipient gets paid in minutes
9. At year-end, Meow generates 1099 tax forms; CFO exports to bookkeeper

---

## What data, money, or state moves through the system?

- **Money:** customer USD → Grasshopper → Velox → T-bills/MMF (customer-name custody) → yield credits → eventual redemption back through Grasshopper → external bank
- **Stablecoin:** customer USD → Bridge → USDC on-chain → swapped to local currency at last mile via Bridge's FX partners
- **Yield:** TTTXX dividends paid monthly; T-bill imputed interest realized at maturity
- **Tax data:** dividends, interest, sales tracked per customer; 1099-DIV/INT/B generated at year-end
- **Compliance data:** KYB approvals, sanctions flags, wire-approval thresholds, anomalous-activity flags

---

## Why is this hard?

1. **Owning a broker-dealer is expensive.** Most fintechs (Mercury, Brex) refer customers to a third-party RIA or broker. Meow chose to **become** the broker-dealer (Meow Markets LLC, FINRA CRD 322685), which captures more economics but requires net capital, compliance staff, Series 24 principals, FINRA exams, and FOCUS reporting.
2. **The yield-spread economics are tight.** Meow earns the spread between underlying MMF yield and customer APY — maybe 30 bps gross, 15 bps net after clearing fees. At $2B AUM that's $3-4M ARR from the core product. The economics are small per-customer; only scale + adjacent revenue (interchange, FX) makes it work.
3. **Single-partner-bank risk.** Grasshopper Bank is the sole banking partner. If Grasshopper exits the BaaS partnership (cf. Synapse/Evolve 2024), Meow has to rebuild plumbing.
4. **Trust overhang from the FTX collapse.** Meow was a crypto-yield product pre-November-2022 with direct FTX exposure. Surviving that with customer funds intact is a real moat, but some buyers (auditors, conservative boards) still flag the company's pre-pivot history.
5. **Stablecoin product creates re-entry risk.** The Bridge integration introduces crypto operations again. If any USDC product offers yield (vs just send/receive), the 2022 hazard reappears.
6. **Competitive squeeze.** Mercury Vault is the default for YC startups (distribution moat). Brex Treasury owns the premium segment. Meow's wedge — stablecoin-curious startups + slightly higher yield — is narrow and copyable.

---

## Why now?

- **Post-SVB collapse (March 2023)** sensitized every startup CFO to treasury management as a real discipline rather than an afterthought.
- **Fed funds at 5%+** made yield meaningfully matter. At 0% rates, the difference between Mercury and Meow is rounding error; at 5%+, it's hundreds of thousands of dollars per year.
- **Mercury and Brex are big enough that the yield wars are real.** Customers shop. Specialists like Meow can win on yield even when they lose on distribution.
- **The 2024 BaaS shakeout** (Synapse Chapter 11, Evolve cyber incident) made customers more attentive to who their actual partner banks are — which favors the more transparent setups.
- **Stablecoin rails went mainstream** with Stripe acquiring Bridge in October 2024. Suddenly "USDC for contractor payments" is a sensible feature, not a crypto-bro idea.

---

## What is actually impressive?

- **Surviving FTX with brand intact.** Of all startups with direct FTX/BlockFi/Genesis lending exposure in November 2022, Meow is one of a handful that (a) didn't shutter, (b) didn't leave customers underwater, (c) didn't get sued, (d) successfully pivoted. This is the strongest piece of brand equity Meow has.
- **Founder execution during the FTX week.** Arvanaghi's public communication in mid-November 2022 was transparent, fast, and accountability-taking — the opposite of BlockFi/Celsius/Voyager.
- **Owning the broker-dealer.** Vertical integration is unusual at Meow's scale. It captures more margin, reduces vendor dependency, and makes the tax/compliance flow cleaner.
- **Customer-name custody at Velox.** T-bills and MMF shares are in the customer's name, not pooled at Meow. If Meow disappears, customers transfer to another broker — they don't lose money. This is the architectural feature that distinguishes post-FTX Meow from pre-FTX Meow.
- **Bridge integration as a smart re-entry into crypto** via a Stripe-owned, regulatorily-clean wrapper instead of direct counterparty lending.

---

## What is still unclear or risky?

- **YC batch is contested** — stream 1 said S21, stream 4 said W22. Default to S21 but verify on YC's directory.
- **MMF identity is contested** — stream 2 said BlackRock TTTXX, stream 4 said Goldman FTGXX. Default to TTTXX but verify on Meow's brokerage agreement.
- **Broker-dealer/clearing arrangement** — stream 2 says Meow Markets LLC + Velox; stream 4 suggested Apex/Atomic. Default to Velox.
- **Card program** — disputed between streams; verify on meow.com.
- **NYAG settlement** — stream 3 mentioned it, no other stream corroborated. Possibly hallucinated.
- **Post-Series-A funding** — no priced round publicly disclosed since the $22M Tiger Global Series A in March 2022. Either profitable or struggling to raise — can't tell.
- **AUM definition** — "$2B managed" and "$10B moved" are self-reported, unaudited.
- **Yield spread** — Meow doesn't publish what % of underlying MMF yield they pass through. Estimated 30-75 bps captured.
- **FTX recovery economics** — Meow is a creditor in the FTX bankruptcy. How much they've recovered (likely 100%+ given the FTX bankruptcy economics) and whether that explains the absence of a dilutive raise is unknown.
- **Card program** existence and underlying issuer.
- **Headcount** — estimated 20-70 range depending on which stream, all LinkedIn-derived.

---

## The mental model: "Think of Meow as..."

**Think of Meow as Mercury Vault, but built and run by someone who watched FTX collapse from the inside, who owns their own broker-dealer to capture more economics, who pays customers slightly higher yield by accepting tighter spreads, and who quietly re-introduced stablecoin rails through Stripe-owned Bridge once it was safe to do so.**

The architectural distinction that matters: **customer T-bills and MMF shares are held in customer-name brokerage accounts at Velox, not pooled at Meow.** This is the structural feature that makes post-FTX Meow safer than pre-FTX Meow, and it's the same structural feature that limits how much economic damage a Meow failure could cause. Customer cash at Grasshopper (the small operating-balance portion) is the only piece structurally exposed to a Meow failure, and that's FDIC-insured.

Meow is **not a bank**, **not an RIA**, and **not a software company** — it's a **fintech overlay (UI/workflows) on top of a broker-dealer (its own) and a partner bank (Grasshopper) and a stablecoin rail (Bridge)**. The economics are services-heavy (yield spread is financial services margin, not software margin). At ~$2B AUM, the company likely runs $8-22M ARR with maybe 80-90% of revenue from yield spread + interchange + FX, and 10-20% from software-y functionality.

The most likely outcome is acquisition by Mercury, Brex, or a mid-tier bank in the $200-400M range within 18-24 months. The bull case is becoming the default stablecoin-treasury rail for crypto-adjacent startups, which depends on out-executing Mercury before Mercury ships parity. The bear case is a slow squeeze: Mercury copies the yield offering, Stripe copies the stablecoin offering via Bridge-native Stripe Treasury, and Meow becomes acqui-hire fodder.

If you want to understand Meow, the single most useful next action is to: (a) read Arvanaghi's mid-November 2022 X/Twitter threads explaining the FTX exposure and pivot, and (b) sign up for a Meow account and walk through onboarding to see how the broker-dealer KYC + dashboard actually feels. Everything else in this folder is description; those two are the experiences that matter.
