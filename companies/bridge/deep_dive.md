# Bridge — Deep Dive

> The stablecoin payment infrastructure company acquired by Stripe for $1.1B in October 2024. The highest-profile exit in stablecoin payments — until Mastercard acquired BVNK for up to $1.8B in March 2026.
> **Date:** 2026-05-03
> **Sources:** Three parallel research agent passes (company/acquisition, product/architecture, customers/competitive) + 3 founder transcripts (Cheeky Pint, Empire podcast, March 2026 Bridge volume update)

---

## TL;DR — what to know in 90 seconds

**Bridge ([bridge.xyz](https://bridge.xyz))** is a stablecoin payment infrastructure company founded in 2022 by **Zach Abrams (CEO)** and **Sean Yu (CTO)** — both repeat founders (Evenly → Square 2013) and ex-Coinbase (where Abrams ran USDC's launch). Originally launched as an NFT-payments product, pivoted to stablecoin orchestration after the FTX collapse and USDC depeg shook the market in 2023.

**Funding:** $58M total raised pre-acquisition. Seed (~$18M) led by Index + Haun + Coinbase Ventures at ~$40M post. Series A ($40M, March 2024) led by Sequoia + Ribbit at ~$200M post. **Sequoia reportedly cleared $100M+ from the Stripe deal.**

**The $1.1B Stripe acquisition:** Announced October 20, 2024, closed February 4, 2025. **Largest stablecoin/crypto-infrastructure acquisition by a non-crypto-native acquirer in history** — until Mastercard's $1.8B BVNK deal in March 2026. Pre-acquisition revenue was an estimated $5-15M ARR; deal multiple ~75-110x ARR. Stripe was buying *category leadership*, *founders*, *regulatory licenses*, and *strategic positioning ahead of the GENIUS Act* (which passed July 2025, 5 months post-close).

**Post-acquisition trajectory (Feb 2025 → today):**
- **May 2025:** Launched **USDB** stablecoin + **Stablecoin Financial Accounts** in 101 countries
- **June 2025:** Stripe acquired **Privy** (server wallets — adds non-custodial wallet primitives to the Bridge stack)
- **July 2025:** GENIUS Act signed — gives Bridge perfect regulatory tailwind
- **Sept 2025:** Stripe + Paradigm announced **Tempo blockchain** (with OpenAI, Anthropic, Deutsche Bank, Visa as partners)
- **Nov 2025:** Launched **Open Issuance** — let any platform issue its own stablecoin in days. First marquee customer: Sui's USDsui
- **Feb 2026:** **OCC conditional approval for federal national trust bank charter** — first stablecoin orchestrator with this regulatory status
- **March 2026:** Visa+Bridge announced expansion of stablecoin-linked cards to 100+ countries
- **Volume quadrupled in 2025** — implied ~$20-25B annualized run-rate

**Why the $1.1B price looks cheap in hindsight:** the OCC charter, GENIUS Act tailwind, Open Issuance network effect (12+ branded stablecoins now using Bridge), and Visa partnership were all post-acquisition wins. Mastercard's $1.8B BVNK acquisition validates the price floor.

**The single most important strategic insight:** Bridge is now the **stablecoin layer for the entire Stripe agentic-commerce stack** — Privy (wallets) + Bridge (issuance/orchestration) + Tempo (chain) + ACP/MPP (agent commerce protocols) form a coherent end-to-end stack. **No other company has all four pieces.**

---

## 1. Founders & founding story

### Zach Abrams — CEO

**Background path:**
- **Evenly** (2011) — co-founded peer-to-peer payments app with Sean Yu
- **Square** acquired Evenly December 2013 — Abrams became GM of Square Customers
- **Coinbase** (Aug 2017 – Jul 2019) — Head of Consumer Product, **led the launch of USDC**
- **Brex** (May 2019 – April 2022) — Chief Product Officer
- **Bridge** (2022 – present) — co-founder + CEO

Twitter: [@zcabrams](https://x.com/zcabrams) | LinkedIn: [zacharyabrams](https://www.linkedin.com/in/zacharyabrams)

### Sean Yu — CTO

**Background path:**
- Duke (BA, CS/Econ/Math, 2010)
- **Evenly** co-founder with Abrams (2011)
- **Square** (2013-2015) post-acquisition
- **DoorDash** (2015-2018) early engineer / Staff Eng / EM
- **Coinbase** (2018-2019) Staff Engineer
- **Airbnb** (2019-2022) Staff SWE
- **Bridge** (2022) co-founder + CTO

LinkedIn: [seansu4you87](https://www.linkedin.com/in/seansu4you87/)

### The founding insight

Per Sequoia's Series A post and multiple founder interviews: *"Only ~40 cents of every dollar in international aid reaches recipients, and B2B cross-border payments still cost 3–4% and take days."*

Having shipped USDC at Coinbase and watched stablecoins reach scale, Abrams concluded the missing layer was **developer-grade orchestration between fiat and stablecoins across chains, jurisdictions, and currencies** — a "Stripe for stablecoins."

**The pivot:** Bridge initially launched in 2022 as a platform for buying NFTs with stablecoins. After the FTX collapse + USDC depeg shook the market in March 2023, they pivoted to general stablecoin orchestration. **Without the FTX-era trauma forcing the pivot, Bridge wouldn't exist as we know it.**

---

## 2. Funding history (pre-acquisition)

**Total raised before Stripe: $58M across two rounds.**

### Seed round (2022-2023)
- **Lead:** Index Ventures + Haun Ventures
- **Other participants:** Coinbase Ventures, Bedrock, 1confirmation
- **Amount:** ~$18M (inferred: $58M total minus $40M Series A)
- **Post-money valuation:** ~$40M (per angel investor [Zac Townsend's blog](https://blog.zactownsend.com/empathy-on-entrance-price-bridge-dot-xyz-and-astranis))

### Series A — March 2024 (announced August 2024)
- **Amount:** $40M
- **Lead investors:** **Sequoia Capital** (Shaun Maguire took board seat) + **Ribbit Capital**
- **Participating:** Index + Haun
- **Post-money valuation:** ~$200M
- **Other named investors over the company's life:** 1confirmation, Bedrock, Artisanal Ventures

### Cap table inferences
- **Sequoia** was largest VC holder; reportedly took home **>$100M from the Stripe deal** ([Cointelegraph](https://cointelegraph.com/news/sequoia-100-million-stripe-bridge-deal-report))
- Index + Haun (seed leads) earned ~3× from Series A markup, then another ~3× from acquisition = ~9× return on seed
- Founders' equity post-Series A unknown; assuming standard ~30-35% remaining founder ownership at A, **Abrams + Yu likely cleared $200M+ each** in the deal (inferred)
- Pre-acquisition fully diluted valuation was effectively the **$1.1B Stripe price** = 5.5× the Series A mark in 7 months

---

## 3. Team size growth

| Stage | Headcount | Source |
|---|---:|---|
| Founding (2022) | 2 | implied |
| Series A close (Mar-Aug 2024) | ~45 | CNBC |
| Year-end 2024 | ~55 (+324% YoY) | reported |
| Acquisition close (Feb 2025) | ~60 | CNBC |
| Sept 2025 (under Stripe) | **127** | [Latka](https://getlatka.com/companies/bridge.xyz) |

**Notable post-acquisition leadership:** **Neetika Bansal** runs Stablecoin/Money Movement Products on the Stripe side ([Stripe newsroom](https://stripe.com/newsroom/news/stripe-completes-bridge-acquisition)). Bridge has been notably low-profile about exec hires — Abrams is the public face.

---

## 4. The $1.1B Stripe acquisition — the deal

### Headline facts (verified)
- **Deal price:** $1.1B
- **Announced:** October 20, 2024 ([Fortune](https://fortune.com/crypto/2024/10/22/stripe-announces-1-1-billion-acquisition-of-stablecoin-start-up-bridge/))
- **Closed:** February 4, 2025 after regulatory clearance
- **Stripe's largest acquisition ever**
- **Largest stablecoin acquisition in history at the time** — eclipsed by Mastercard/BVNK ($1.8B) March 2026

### Why $1.1B — the math
- **Volume:** ~$5B annualized payment volume as of Aug 2024 (per Sequoia post)
- **Revenue:** estimated **$5M-$15M ARR run rate** at deal time
- Multiple: **~75-110× ARR** (massive)
- **This was strategic, not financial** — Stripe was buying category leadership + founders + regulatory licenses + the position ahead of GENIUS Act passage

### Strategic rationale (Stripe POV — direct quotes)

**Patrick Collison's framing:** Stablecoins are "**room-temperature superconductors for financial services**" ([insights4vc](https://insights4vc.substack.com/p/stripes-stablecoin-strategy)).

**John Collison at Stripe Sessions 2025:** "Stripe basically, broadly in all these things, just wants to support whatever businesses want."

**Patrick at Sessions 2025:** "We're focused on catalyzing stablecoin adoption. And that's really where we're working backwards from."

**The "origin story" detail** ([CNBC](https://www.cnbc.com/2025/02/04/stripe-closes-1point1-billion-bridge-deal-prepares-for-stablecoin-push-.html)): Patrick Collison and Zach Abrams **first met at a Stripe-hosted roundtable with Wally Adeyemo (then Deputy Treasury Secretary) in summer 2024** — months before the deal.

### Was there a competitive process?
No public evidence of a bidding war. Searched for Coinbase, Visa, Mastercard, PayPal counterbids — nothing surfaced. The Sequoia + Stripe relationship (Stripe is a Sequoia portfolio company) and the founders' Coinbase pedigrees suggest a **negotiated deal, not an auction**. Inferred but high confidence.

### Founder retention
Not publicly disclosed. Standard Stripe practice with founder-led acquisitions has been multi-year vesting + retention packages. Abrams remains highly visible as Bridge CEO and Stripe's public face for stablecoins 15 months post-close — strong signal he's locked in.

---

## 5. Post-acquisition trajectory (Feb 2025 → May 2026)

The hit list, in order of strategic significance:

### May 7, 2025 — Stripe Sessions launch: USDB + Stablecoin Financial Accounts

**USDB stablecoin** ([Bridge USDB post](https://www.bridge.xyz/news/usdb)):
- Backed 1:1 by cash + BlackRock money market funds
- **Bridge passes the majority of Treasury yield back to developers as a fee/rebate** — the differentiator vs. USDC
- This monetization model (yield-share with issuer) became Open Issuance's key innovation

**Stablecoin Financial Accounts** ([Stripe blog](https://stripe.com/blog/introducing-stablecoin-financial-accounts)):
- Available in **101 countries** to Stripe business customers
- Lets businesses hold stablecoin balances + accept fiat-and-crypto rails (ACH, SEPA) + send stablecoins globally
- **Powered by Bridge APIs end-to-end**
- Pitched at companies in volatile-currency markets

### June 11, 2025 — Stripe acquires Privy

Privy (server wallets, 75M+ accounts pre-acquisition, $230M valuation March 2025) acquired by Stripe for undisclosed sum ([Privy announcement](https://privy.io/blog/announcing-our-acquisition-by-stripe)).

**This makes the Stripe stack look like:** Stripe Core + Bridge (stablecoin orchestration) + Privy (wallets) — three layers of agentic-commerce infrastructure under one company.

### July 18, 2025 — GENIUS Act signed

President Trump signed the **first US federal stablecoin legislation**. Creates a federal framework: payment stablecoins not securities/commodities; federally-licensed nonbank issuers fall under OCC oversight.

**Direct Bridge benefit:** This is *exactly* the regulatory regime Bridge's OCC trust charter application is built for. **Stripe's $1.1B bet looks dramatically better in light of GENIUS — they bought the leading regulated stablecoin orchestrator 5 months before the law passed.**

### September 2025 — Tempo blockchain announced

Stripe + Paradigm announce **Tempo**, an EVM L1 blockchain for stablecoin payments. Backed by **OpenAI, Anthropic, Deutsche Bank, Visa** as anchor partners.

Bridge is the implied stablecoin issuance/orchestration layer on Tempo. Mainnet launched March 18, 2026; Bridge added full Tempo support 9 days later (March 27, 2026).

### November 12, 2025 — Open Issuance launches

Bridge launches **Open Issuance** — a platform that lets any project launch its own branded stablecoin in days. First marquee customer: **Sui's USDsui**.

Within months, additional Open Issuance customers:
- **Phantom (CASH)** — 15M+ user crypto wallet
- **MetaMask (mUSD)** — first stablecoin from a self-custodial wallet, partnered with M0
- **Hyperliquid (USDH)** — high-velocity DeFi stablecoin
- **Sui Foundation (USDsui)** — L1-native, mainnet March 2026
- **Dakota (DKUSD), Slash, Lava, Takenos** — additional issuers

This is a **flywheel**. Every new issuer brings demand AND adds liquidity for the entire Open Issuance network. Bridge keeps a slice of T-bill yield from reserves on every issued stablecoin.

### February 17, 2026 — OCC conditional approval

Bridge applied October 2025 for a **national trust bank charter**. Conditional approval received Feb 17, 2026 ([CoinDesk](https://www.coindesk.com/business/2026/02/17/stripe-s-stablecoin-firm-bridge-wins-initial-approval-of-national-bank-trust-charter)).

**Will allow Bridge to:** provide custody, issuance, and reserve management under direct federal oversight. Eliminates state-by-state MTL patchwork. **No other stablecoin orchestrator has this** (Anchorage is the closest analog).

Opposed by Independent Community Bankers Association (ICBA) and Bank Policy Institute — predictable but unsuccessful pushback.

### March 3, 2026 — Visa+Bridge cards expand to 100+ countries

Visa announced expansion of Bridge-Visa stablecoin-linked cards from 6 LatAm countries to 100+ globally ([Visa investor release](https://investor.visa.com/news/news-details/2026/Visa-and-Bridge-Expand-Collaboration-with-Plans-to-Bring-Stablecoin-Linked-Cards-to-Over-100-Countries/default.aspx)). Card issuer of record: **Lead Bank**. Stripe Issuing as the processor.

### April 21, 2026 — DoorDash + Coastal Bank

DoorDash and Coastal Bank announced as customers running stablecoin payouts on Bridge + Tempo rails ([CoinDesk](https://www.coindesk.com/business/2026/04/21/doordash-is-bringing-stablecoin-payments-to-masses-with-stripe-backed-blockchain)).

### Brand status today (May 2026)

**Bridge has been kept as a sub-brand inside Stripe**, not absorbed. "Bridge, a Stripe company" continues to issue products, maintain its own website ([bridge.xyz](https://bridge.xyz)), and Abrams is publicly the "Bridge CEO" within Stripe. **Volume quadrupled in 2025** ([CoinDesk Feb 2026](https://www.coindesk.com/business/2026/02/24/stripe-s-bridge-sees-stablecoin-volume-quadruple-as-utility-insulates-from-crypto-winter)).

---

## 6. Product taxonomy — what Bridge actually sells

Four main product lines, each with separate API but shared customer/wallet/compliance core:

### 1. Orchestration (the core API)
- Virtual accounts (USD, EUR, MXN, BRL, GBP, COP — all with native local rails)
- Cross-border transfers (fiat ↔ stablecoin ↔ fiat)
- Liquidation addresses
- The "Stripe for stablecoins" core

### 2. Issuance / Open Issuance (the moat)
- USDB (Bridge's own stablecoin)
- Open Issuance — let any project issue branded stablecoin in days
- Customers: Phantom, MetaMask, Hyperliquid, Sui, Dakota, Slash, Lava, Takenos
- Bridge keeps slice of T-bill yield on every issued stablecoin = **passive recurring revenue at zero marginal cost**

### 3. Wallets
- **Custodial Bridge wallets** (default)
- **Privy non-custodial wallets** (since June 2025 acquisition)
- Bridge smart contracts for direct contract-to-card funding

### 4. Cards
- Visa-branded stablecoin cards
- Lead Bank as issuer of record
- Stripe Issuing as processor
- 18 countries live (Argentina, Colombia, Ecuador, Mexico, Peru, Chile + 12 others) → expanding to 100+

### + Stablecoin Financial Accounts (Stripe product, Bridge backbone)
- Available in 101 countries to Stripe business customers
- Bridge is the custodian of the stablecoin balance underneath

---

## 7. Technical architecture

### Custody model
Bridge runs a **multi-layer custody stack**, not a single MPC-or-bust posture:
- **Custodial Bridge wallets** — Bridge holds keys server-side, abstracts gas
- **Non-custodial via Privy** — server wallets + embedded wallets
- **Bridge smart contracts** — for direct contract → card funding
- **Reserve custody** — bankruptcy-remote at **BlackRock** (cash + short-duration MMFs), **Fidelity**, with **Superstate** as a tokenized-treasury option

**Soon: federally-chartered national trust bank** (Bridge National Trust Bank, OCC-approved Feb 2026) — a regulatory-architectural moat no competitor has.

### Chains supported (15+ in production as of May 2026)

| Chain | Notes |
|---|---|
| Ethereum | USDC, USDT, EURC, USDB, all Open-Issuance coins |
| Solana | USDC, USDT (Mar 2026), USDG, CASH |
| **Tron** | Critical — >50% of circulating USDT lives here. Bridge built **in-house** deposit/withdrawal infra (May 2025) with unlimited deposit addresses |
| Polygon | |
| Base | |
| Arbitrum | |
| Optimism | |
| Avalanche | |
| Stellar | USDC; supports memo + memoless via muxed addresses |
| **Tempo** | Stripe/Paradigm's L1, Bridge added Mar 27 2026 |
| Plasma | |
| Celo | |
| Aptos | |
| Sui | |
| HyperEVM | |

**The Tron support is genuinely deep and is the primary wedge for LatAm/Africa USDT flows.** Most US-built competitors ignore Tron.

### Banking / regulatory entities
- **US:** Bridge Building Inc., FinCEN MSB, NMLS #2450917, state MTLs in 22+ states (soon supplanted by OCC trust charter)
- **EEA:** Bridge Building Sp. Z.o.o. (Polish license, passports across EU)
- **Card issuance:** Lead Bank
- **Reserve custody:** BlackRock + Fidelity + Superstate

### Fiat virtual accounts (six native currencies)
| Currency | Rail | Notes |
|---|---|---|
| USD | ACH + Wire | Same-day ACH if before 4pm ET |
| EUR | SEPA | Polish entity passports across EEA |
| MXN | SPEI | CLABE-format account |
| BRL | Pix | Live since Nov 17, 2025 |
| GBP | Faster Payments | GA Mar 23, 2026 |
| COP | Bre-B | Beta |

### KYC stack
**Persona** as IDV vendor. Auto-approves <60 seconds for individuals; KYB same-day or next-day. Supports 195+ countries' government IDs.

### SDKs (the surprising choice)
**There is no official Bridge SDK in any language.** Bridge ships:
- REST API (`https://api.bridge.xyz/v0/*`)
- OpenAPI spec
- Postman collection
- LLMs.txt for AI-friendly doc consumption

Customers either consume REST directly or use community-built MCP servers. **This is the "Stripe-style API quality" philosophy — REST surface is good enough that SDKs are a thin wrapper.**

### Pricing model

**Two-sided revenue:**
1. **Bridge's take** — FX spread of **up to 1% of fiat value**, plus pass-through gas at cost, plus partner-defined service charges
2. **Developer fees** — partner sets `developer_fee` (USD fixed) or `developer_fee_percent`; collected in source currency, paid out in USD on the 5th of each month

**Effective take rates:**
- **Cross-border orchestration:** ~25-50 bps (vs Wise at 50-100bps, traditional correspondent banking 200-500bps)
- **Stablecoin issuance:** revenue share on T-bill yield (3-4% annual, Bridge keeps minority slice)
- **Cards:** interchange share with Lead Bank + Stripe Issuing

---

## 8. Volume + revenue economics

| Metric | Value | Date | Source |
|---|---:|---|---|
| Annualized payment volume at Series A | ~$5B | Aug 2024 | Sequoia post |
| Revenue at acquisition | $5-15M ARR (estimate) | Oct 2024 | Architect Partners |
| Volume growth 2025 | **4×** (so $20-25B annualized) | end of 2025 | CoinDesk |
| Revenue end of 2025 | ~$28.1M (Latka) — but underdisclosed since blended into Stripe | Sept 2025 | Latka |

**At 4× volume + Open Issuance reserve-yield share, plausibly $50-80M ARR by end of 2025.** Bridge revenue is now subsumed into Stripe's segment reporting.

---

## 9. Named customers (the verified list)

### Tier-1 enterprise
- **SpaceX / Starlink** ✅ — uses Bridge to **collect Starlink revenue in 100+ local currencies** (especially Argentina, Nigeria) and convert to stablecoins for global treasury. **Chamath Palihapitiya publicly said "Starlink was the alert for Stripe to buy Bridge."** Use case: collection + treasury repatriation, not payouts.
- **Coinbase** ✅ — uses Bridge for cross-stablecoin/cross-chain conversions (USDT/Tron ↔ USDC/Base) inside Coinbase's onchain app
- **OpenAI / Google (YouTube Premium)** ✅ — Nigerian consumers pay for ChatGPT and YouTube Premium via stablecoins routed through Bridge ([a16z](https://a16zcrypto.com/posts/article/stripe-bridge-acquisition-stablecoins/))
- **Stellar Development Foundation, Strike** — Bridge as infrastructure for their stablecoin payment features
- **U.S. State Department, U.S. Treasury** — international aid disbursement (per Sequoia)
- **Bitso** (LatAm B2B cross-border)
- **Scale.ai** — global contractor payouts
- **Zulu** (Colombian peso conversions)
- **Dakota** (neobank built on Bridge)

### Stablecoin issuers (Open Issuance)
**Phantom (CASH), MetaMask (mUSD), Hyperliquid (USDH), Sui Foundation (USDsui), Dakota (DKUSD), Slash, Lava, Takenos**

### Distribution-layer fintechs
- **Payoneer** (Q2 2026 launch, ~2M global business customers)
- **Veem** (global B2B payments)
- **Visa** (cards in 18 → 100+ countries)
- **Bitso** (LatAm exchange)

### Notably absent (but adjacent)
- **Anthropic** — referenced as Tempo backer, not direct Bridge customer
- **Ramp, Mercury, Brex** — competing for AI-native treasury wallet share, not adopting Bridge

---

## 10. The competitive landscape (with the BVNK earthquake)

| Company | Focus | Volume / Revenue | Funding / Status | Key Diff vs Bridge |
|---|---|---|---|---|
| **BVNK** | Enterprise stablecoin, EU+UK roots | **$30B annualized TPV** (2.3× YoY), 226 new customers 2025 | **Acquired by Mastercard for up to $1.8B March 2026** | EU/UK-native, 130+ country coverage, deeper enterprise B2B |
| **Conduit** | LatAm + Africa cross-border | **$10B+ annualized**, 16× growth 2024, 5,000+ merchants | $36M Series A May 2025 (Dragonfly + Circle) | Emerging-markets-native, deeper EM than Bridge |
| **Sphere** | Cross-border "Stripe for crypto" | Not disclosed | $5M seed Dec 2024 (Coinbase + Kraken) | Earlier-stage, two orders smaller than Bridge |
| **Brale** | Stablecoin issuance + orchestration | Not disclosed | Lightspeed-backed | Issuance-pure-play, lost Phantom/MetaMask/Hyperliquid to Bridge |
| **Beam** | LatAm stablecoin PSP | $275M+ processed | **Acquired by Modern Treasury for $40M Oct 2025** | Already absorbed |
| **Mansa** | B2B remittance + credit | $11M monthly volume; targeting $1B TPV | $10M seed Tether-backed Feb 2025 | Working-capital lender, not pure infra |
| **Huma Finance** | PayFi / DeFi-native | **$10B+ cumulative**, $1.7B Q3 2025 quarterly | Token-launched | DeFi-native LP model, retail liquidity |
| **Credible Finance** | B2B remittance | $210K/month rev, 15bps | Early-stage | Tiny vs Bridge; SMB EM corridors |
| **Mural Pay** | Contractor payouts | Not disclosed | $5.6M (Firstminute, Galaxy, DCG) | Vertical specialization in global contractor payroll |

### The Mastercard/BVNK deal — the new dynamic

**March 17, 2026:** Mastercard agreed to acquire BVNK for up to **$1.8 billion** ([CNBC](https://www.cnbc.com/2026/03/17/mastercard-acquiring-stablecoin-startup-bvnk-in-crypto-bet.html)).

This **eclipses the Stripe-Bridge deal** and validates the price floor for credible stablecoin infrastructure exits. **The stablecoin infra market has now consolidated around two card-network-backed giants:**
- **Bridge / Stripe** (US-anchored, AI-aligned via Tempo)
- **BVNK / Mastercard** (EU/UK-anchored, enterprise-deep)

**Visa** plays both sides — strategic investor in BVNK (pre-Mastercard) AND anchor validator on Stripe's Tempo blockchain ([CoinDesk](https://www.coindesk.com/business/2026/04/14/visa-throws-its-weight-behind-stripe-s-tempo-blockchain)).

### Consolidation outlook
- **Visa** likely acquires Conduit or Sphere to keep parity
- **PayPal** has PYUSD but no infra play; could acquire Sphere or Mural
- **Coinbase** could roll up Brale (Stellar/XRPL/Algorand multi-chain)
- **Banks (JPMorgan, Citi)** — Citi Ventures invested in BVNK pre-acquisition. Expect a regional bank to acquire Brale or Conduit by end-2026

**The window is closing fast.** By end of 2026, the surviving independents will be Brale, Conduit, Mural, Sphere, Mansa, Huma. Most will be acquired or pivot.

---

## 11. Comparison to Credible Finance — sharpened

Recall Credible's profile (from our earlier research):
- $1.12M on-chain TVL, $210K/month revenue, 15bps take rate
- Single live corridor (US-India)
- Solo/duo founder team (10-25 people)
- ~$1M raised
- Web 2.5 architecture: off-chain orchestrator + Hedera Byzanlink credit pool
- NBFI partners (Loap India, Chorus Africa) for corridor PSP relationships

| Dimension | Credible Finance | Bridge |
|---|---|---|
| **Stage** | Pre-Series A, ~$2.5M ARR | Stripe subsidiary, ~$50-80M ARR |
| **Custody** | Circle Programmable Wallets + Hedera Byzanlink vault | Bridge custodial + Privy non-custodial + (soon) federally-chartered trust bank |
| **Liquidity model** | On-chain LP pool (~16% APY) + NBFI co-lending | Bridge's own balance sheet + Stripe parent. **Pure principal-FX, no LP pool.** |
| **Geographic coverage** | 1 live corridor (US-India), 5+ in pipeline | 101 countries directly, 6 native virtual-account currencies |
| **Take rate** | ~15bps + NIM share | ~25-100bps FX spread + interchange + reserve yield |
| **ICP** | Indian/EM fintechs needing pre-funding elimination ($1k-$10k transfers) | Global enterprises (SpaceX), wallet/card platforms (Phantom, MetaMask) |
| **Regulatory** | Canada MSB + India lending + US partner-MSB + 5 partner jurisdictions | US 22-state MTL + Polish EEA passport + **OCC national trust bank charter (pending)** |
| **Chains** | Hedera + Solana primarily | **15+ chains** including Tron deeply |
| **Lender role** | Credible advances credit | Bridge does NOT extend credit |
| **Stablecoin issuance** | None | Issues USDB + powers 12+ branded stablecoins via Open Issuance |

### The architectural gap
- **Credible's moat:** credit-underwriting + corridor-NBFI relationship
- **Bridge's moat:** regulated entity + balance sheet + Stripe distribution

**They are different businesses inside the same surface area.** Credible takes settlement-risk-as-credit; Bridge takes settlement-risk-as-float (eaten by Stripe's balance sheet). Credible needs the LP pool as fuel; Bridge does not.

### What Credible (or any competitor) can learn from Bridge
1. **Multi-chain from day one is non-negotiable.** Tron is critical for LatAm/Africa USDT — most US-built competitors ignore it
2. **The Open Issuance "interoperable stablecoin network" is a customer-acquisition flywheel** — every issuer brings demand AND adds liquidity for everyone else
3. **The virtual-account primitive IS the actual product** — not "stablecoin transfer," not "off-ramp," but "give me a USD/EUR/MXN/BRL/GBP/COP account number that lands in my chosen wallet on my chosen chain"
4. **Pricing on FX spread, not per-transaction**, scales naturally to enterprise volumes without renegotiating tiers
5. **No SDK, just great REST + OpenAPI + LLMs.txt** is now considered acceptable when DX is Stripe-grade

---

## 12. The "build a better Bridge" angle (for your plan)

Bridge's exposed flanks where a competitor could differentiate:

### 1. **SMB self-serve** — wide open
Bridge requires sales contact, custom pricing, KYB. **A Stripe-style instant-signup stablecoin payment product for $1M-$50M ARR SMBs is wide open.** Mural is closest but under-resourced.

### 2. **Vertical specialization** — Bridge is horizontal
Win with vertical PMF: stablecoin payouts for creators, marketplaces, royalties (Mural's music-royalty wedge), AI-API metering (per-second stablecoin micropayments), B2B trade finance (where Mansa is succeeding).

### 3. **Specific corridor depth** — Bridge thin in:
- **India** (massive remittance market, RBI-regulated, hard) — Indian solo-founder unfair advantage
- **Southeast Asia** (PH, ID, VN)
- **Middle East** (UAE, Egypt)
BVNK/Mastercard will go EMEA hard; **the SE-Asia gap is real**.

### 4. **Emerging-markets working capital** — Bridge doesn't lend
Mansa proved 5,000+ merchants need 1-5 day stablecoin credit lines, not just rails. Credible-style co-lending with NBFI partners could win where Bridge can't.

### 5. **On-chain-native AI agent payments** — both Bridge and BVNK absent here
Stripe is moving via ACP/Tempo but the agent-stablecoin merge is wide-open primitive. **This is the most aligned with our prior research on agent payments.**

### 6. **Below-the-Visa-card consumer wallet**
Phantom Cash captured the wallet-card segment via Bridge. Same model in LatAm/Africa with local-language UX is repeatable.

---

## 13. The strategic bottom line

**Bridge is now the stablecoin layer for the entire Stripe agentic-commerce stack:**

```
┌──────────────────────────────────────────────────────────┐
│  Stripe Agentic Commerce Suite                           │
│  ├─ ACP (with OpenAI)                                    │
│  └─ MPP (on Tempo)                                       │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────┴─────────────────────────────────┐
│  Stripe Core (Payments, Connect, Treasury, Issuing)      │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────┴─────────────────────────────────┐
│  Bridge — stablecoin layer                               │
│  ├─ Orchestration (transfers, virtual accounts)          │
│  ├─ Issuance (USDB, Open Issuance)                       │
│  ├─ Wallets (custodial Bridge + Privy non-custodial)     │
│  └─ Cards (Stripe Issuing + Lead Bank)                   │
└────────────────────────┬─────────────────────────────────┘
                         │
┌────────────────────────┴─────────────────────────────────┐
│  Tempo (Stripe/Paradigm L1) + 14 other chains            │
└──────────────────────────────────────────────────────────┘
```

**No other company has all four pieces.** Coinbase has the chain (Base) and wallets (Coinbase Wallet) but not the orchestration depth. Mastercard now has BVNK but lacks the AI/agent narrative. PayPal has PYUSD but lacks orchestration.

**Stripe paid $1.1B for Bridge + ~$300M for Privy = ~$1.4B total to assemble a stablecoin/wallet stack that Mastercard then paid $1.8B trying to match with BVNK alone.** Stripe's bet aged extremely well.

---

## 14. What surprised me (non-obvious findings)

1. **Bridge originally launched as an NFT-payments platform.** The pivot to stablecoin orchestration only happened after the FTX collapse + USDC depeg in early 2023. Without the FTX-era trauma, Bridge wouldn't exist as we know it.

2. **The Tron support is the unsung hero.** Most US-built competitors ignore Tron. Bridge built **in-house** Tron infrastructure (May 2025). Tron carries >50% of circulating USDT and dominates LatAm/Africa flows. **This is a corridor depth competitors don't appreciate.**

3. **No SDK is a deliberate choice.** Bridge ships REST + OpenAPI + LLMs.txt + Postman. No `@bridge/node`, no `bridge-python`. The bet: REST surface is good enough that SDKs are a thin wrapper, AND in the AI-agent era, LLMs.txt is more useful than language SDKs.

4. **Open Issuance changed Bridge's economics.** Before: per-transaction take rates. After: passive recurring revenue from reserve yield on every issued stablecoin. **Bridge gets paid even when no one transacts** — they earn the spread on T-bill yield held in reserves.

5. **BlackRock + Fidelity + Superstate as reserve custodians** is genuinely unique. No other stablecoin orchestrator has this triumvirate. The legal-structuring work behind it is substantial.

6. **Patrick Collison met Zach Abrams at a Treasury Department roundtable** with Wally Adeyemo months before the deal. The acquisition wasn't a competitive process — it was a relationship.

7. **The OCC trust charter was almost certainly the deal-clincher.** Stripe likely knew (or strongly believed) the GENIUS Act was coming. Bridge's regulatory position + the OCC charter pathway + Bridge's ex-Coinbase-USDC pedigree made it the obvious acquisition target.

8. **The Mastercard/BVNK deal at $1.8B is the more damning data point.** It shows Stripe got Bridge cheap. The BVNK deal happened 18 months after the Bridge deal closed; the market premium for stablecoin infra has gone up, not down.

9. **Bridge's customer mix is stunningly enterprise-heavy.** SpaceX, Coinbase, OpenAI/Google (Nigeria), Stellar Foundation, Strike, US State Department, US Treasury. **Almost no SMB customers** — they don't even market self-serve. This is by design.

10. **Sequoia's $100M+ payout from a $40M Series A check in ~7 months** is one of the highest-velocity returns of the modern fintech era.

---

## 15. YouTube transcripts saved

Three high-signal transcripts in [`./transcripts/`](./transcripts/):

- **[cheeky_pint_collison_abrams_stern.txt](./transcripts/cheeky_pint_collison_abrams_stern.txt)** — Cheeky Pint with John Collison, Nov 4, 2025. **The single most strategic episode** — both Stripe-acquired founders (Zach Abrams of Bridge + Henri Stern of Privy) interviewed by Stripe's co-CEO. Covers M&A, Open Issuance, future of stablecoins. ~84K chars. ([video](https://www.youtube.com/watch?v=4FsGlsfIIkc))
- **[empire_podcast_latam_acquisition.txt](./transcripts/empire_podcast_latam_acquisition.txt)** — Empire podcast video version, "How Latin America Fueled Bridge's $1.1B Stripe Acquisition." ~43K chars. ([video](https://www.youtube.com/watch?v=GRcajzJ8ZWA))
- **[bridge_quadrupled_volume_visa.txt](./transcripts/bridge_quadrupled_volume_visa.txt)** — Most recent (March 11, 2026), Zach Abrams on Bridge volume quadrupling + Visa partnership expanding to 100+ countries. ~50K chars. ([video](https://www.youtube.com/watch?v=BRx_zrPKxf8))

Also worth pulling later if needed:
- [Bankless: Stripe's Trillion-Dollar Bet](https://www.bankless.com/podcast/stripes-trillion-dollar-bet-how-stablecoins-eat-global-payments) (Sept 8, 2025)
- [a16z crypto: Real story of stablecoins with Abrams + Sean Neville (USDC creator)](https://a16zcrypto.com/posts/podcast/stablecoins-bridge-founder-circle-usdc-creator/)

---

## Sources

**Primary (founder transcripts):**
- [Cheeky Pint with John Collison + Zach Abrams + Henri Stern](https://cheekypint.substack.com/p/stablecoin-special-zach-abrams-bridge)
- [Empire podcast: Bridge $1.1B acquisition](https://blockworks.com/podcast/empire/3ab5d822-9b0b-11ef-a966-a3f84f94e3d8)
- [Bridge volume quadrupled + Visa expansion (March 2026)](https://www.youtube.com/watch?v=BRx_zrPKxf8)

**Bridge / Stripe official:**
- [Bridge homepage](https://www.bridge.xyz/)
- [Bridge API documentation](https://apidocs.bridge.xyz/)
- [Bridge company page](https://www.bridge.xyz/company)
- [Bridge USDB launch](https://www.bridge.xyz/news/usdb)
- [Bridge Tron support](https://www.bridge.xyz/news/tron)
- [Bridge OCC trust charter announcement](https://www.bridge.xyz/blog/bridge-receives-occ-conditional-approval-to-organize-a-federally-chartered-national-trust-bank)
- [Stripe blog: Stablecoin Financial Accounts](https://stripe.com/blog/introducing-stablecoin-financial-accounts)
- [Stripe blog: Open Issuance from Bridge](https://stripe.com/blog/introducing-open-issuance-from-bridge)
- [Stripe completes Bridge acquisition](https://stripe.com/newsroom/news/stripe-completes-bridge-acquisition)
- [Privy + Stripe acquisition announcement](https://privy.io/blog/announcing-our-acquisition-by-stripe)
- [Visa investor release: 100-country card expansion](https://investor.visa.com/news/news-details/2026/Visa-and-Bridge-Expand-Collaboration-with-Plans-to-Bring-Stablecoin-Linked-Cards-to-Over-100-Countries/default.aspx)

**Third-party press:**
- [Fortune: Bridge $58M raise (Aug 2024)](https://fortune.com/crypto/2024/08/29/bridge-stablecoins-sequoia-ribbit-index-haun-58-million/)
- [Fortune: Stripe announces $1.1B Bridge acquisition](https://fortune.com/crypto/2024/10/22/stripe-announces-1-1-billion-acquisition-of-stablecoin-start-up-bridge/)
- [Fortune: Mastercard-BVNK $1.8B](https://fortune.com/2026/03/17/mastercard-bvnk-acquisition-stablecoins-1-8-billion/)
- [Sequoia: Partnering with Bridge](https://sequoiacap.com/article/partnering-with-bridge-a-better-way-to-move-money/)
- [CNBC: Stripe closes $1.1B Bridge deal](https://www.cnbc.com/2025/02/04/stripe-closes-1point1-billion-bridge-deal-prepares-for-stablecoin-push-.html)
- [CNBC: Mastercard acquiring BVNK in $1.8B bet](https://www.cnbc.com/2026/03/17/mastercard-acquiring-stablecoin-startup-bvnk-in-crypto-bet.html)
- [CoinDesk: Bridge volume quadruples](https://www.coindesk.com/business/2026/02/24/stripe-s-bridge-sees-stablecoin-volume-quadruple-as-utility-insulates-from-crypto-winter)
- [CoinDesk: Bridge OCC trust charter](https://www.coindesk.com/business/2026/02/17/stripe-s-stablecoin-firm-bridge-wins-initial-approval-of-national-bank-trust-charter)
- [CoinDesk: Sui USDsui via Bridge](https://www.coindesk.com/business/2025/11/12/sui-launches-native-stablecoin-usdsui-using-bridge-s-open-issuance-platform)
- [a16z: Stripe-Bridge acquisition analysis](https://a16zcrypto.com/posts/article/stripe-bridge-acquisition-stablecoins/)
- [Architect Partners: Stripe-Bridge $1.1B analysis](https://architectpartners.com/stripe-is-acquiring-bridge-for-1-1-billion-the-most-strategically-important-transaction-since-the-emergence-of-crypto/)

**Founder backgrounds:**
- [LinkedIn: Zach Abrams](https://www.linkedin.com/in/zacharyabrams)
- [LinkedIn: Sean Yu](https://www.linkedin.com/in/seansu4you87/)
- [X: @zcabrams](https://x.com/zcabrams)
- [Crunchbase: Square acquires Evenly (2013)](https://www.crunchbase.com/acquisition/square-acquires-evenly--50699deb)

**Adjacent / context:**
- [Latham & Watkins: GENIUS Act analysis](https://www.lw.com/en/insights/the-genius-act-of-2025-stablecoin-legislation-adopted-in-the-us)
- [insights4vc: Stripe's stablecoin strategy](https://insights4vc.substack.com/p/stripes-stablecoin-strategy)
- [Conviction Finance: The Incredible Story of Bridge.xyz](https://conviction.finance/2024/bridge-xyz-the-stripe-of-crypto/)
- [The Asian Banker: Bridge invisible payments](https://www.theasianbanker.com/updates-and-articles/bridge-and-the-rise-of-invisible-stablecoin-payments)
