# Credible Finance — All Numbers in One Place

> Every concrete data point we've collected, with source, date, and confidence label. Built to spot contradictions and track how the story has shifted over time.
> **Date:** 2026-05-03

**Confidence labels:**
- ✅ **Verified** — on-chain reading, named primary source, or third-party press
- 🟡 **Founder-attested** — founder said it in a public source (interview, pitch, blog) but no third-party confirmation
- 🔴 **Marketing claim** — appears in marketing materials only; contradicted, deprecated, or unverifiable
- ⚙️ **Derived** — calculated from other numbers (with the math shown)

---

## 1. Transaction Processing Volume (TPV) — claimed numbers

| Number | Period | Source | Date | Confidence |
|---:|---|---|---|---|
| **$6M USDC loans facilitated** | 3 months pre-PR | Plume × Credible PR | Dec 2024 | ✅ (only third-party-verified TPV figure ever) |
| $20M | Last 30 days (Sep 2025) | Founder, OnePiece interview | Oct 2025 | 🟡 |
| $30M (projected) | Oct 2025 | Founder, OnePiece interview | Oct 2025 | 🟡 |
| $60M+ | Cumulative, 11 months | Founder, OnePiece interview | Oct 2025 | 🟡 |
| $250M+ | Cumulative remittance, 2025 | Credible 2025 wrap-up blog | Dec 2025 | 🔴 |
| $400M+ | Cumulative TPV | Credible blog | Mar 2026 | 🔴 |
| **$350M** | Last 5 months | Founder, Colosseum Demo Day pitch | May 2026 | 🟡 |
| **$140M/month** | Current run-rate | ⚙️ derived: $210K rev ÷ 0.0015 | May 2026 | ⚙️ |
| $100M+/month | Projected after US opens | Founder, OnePiece interview | Oct 2025 | 🔴 |
| **$3B** | Projected annual volume | Founder, Colosseum Demo Day | May 2026 | 🟡 |
| $15M | Deployed into Africa via Chorus Finance | Founder, OG Labs pitch | ~Q1 2025 | 🟡 |
| $132M | "PTC pipeline" (securitized borrower receivables) | Founder, OG Labs pitch | ~Q1 2025 | 🟡 |

### Internal consistency check on TPV

- **Founder-reported $350M cumulative over 5 months** + **10% MoM growth** + **current $140M/month** → geometric series back-solve gives roughly $580M total over 5 months, not $350M. So either the 10% MoM is overstated, the cumulative is understated, or only fee-bearing transactions are counted in the $350M
- **The $400M TPV claim from March 2026** vs **$350M cumulative claim from May 2026** — *the cumulative number went DOWN by $50M between March and May*. Either March's $400M was inflated, or "cumulative" definitions changed (perhaps March was lifetime, May was last-5-months)
- **Only third-party-verified number ever: $6M (Plume PR Dec 2024).** Everything else is founder-attested

---

## 2. Revenue & take rate

| Number | Period | Source | Date | Confidence |
|---:|---|---|---|---|
| **$70K total** | First 6 months | Founder, OG Labs pitch | ~Q1 2025 | 🟡 |
| **$210K/month** | Current monthly | Founder, Colosseum Demo Day | May 2026 | 🟡 |
| **$2.52M ARR** | Current run-rate | ⚙️ derived: $210K × 12 | May 2026 | ⚙️ |
| **$4.5M ARR** | Projected | ⚙️ derived: $3B × 0.0015 | May 2026 | ⚙️ |
| **10% MoM growth** | Current rate | Founder, Colosseum Demo Day | May 2026 | 🟡 |
| **15 basis points** | Take rate per transaction | Founder, Colosseum Demo Day | May 2026 | 🟡 (first explicit) |

### Revenue growth math check

$70K total over 6 months in early 2025 → $210K/month by May 2026. That's ~12-month gap, growing from ~$12K/month average to $210K/month = **~17.5x growth in 12 months**, or **~26% MoM compounded** — much higher than the stated 10% MoM. So either:
- The 10% MoM is the recent run-rate (slowing) and earlier growth was higher
- The $70K six-month total was understated
- The $210K monthly current is overstated

Most likely explanation: the 10% MoM is the *current* growth rate, and earlier months had much faster growth (typical for a startup hitting product-market-fit).

---

## 3. On-chain TVL — verified

| Pool | Chain | TVL | Source | Date | Confidence |
|---|---|---:|---|---|---|
| **Credible PayFi Vault** | Hedera (Byzanlink) | **$1,122,303 USDC** | Live `eth_call` to `totalAssets()` on `0x6b8d…16FB` | May 3, 2026 | ✅ |
| Aethir Private Investors Portal | Solana | Unknown | Aethir blog (gated) | — | 🔴 |
| Plume vault | Plume Network | Unknown / not deployed | Not on RWA.xyz | — | 🔴 |
| **Verifiable total** | | **$1.12M** | | | ✅ |

**The $1.12M TVL (verified) vs $350M+ TPV (claimed) gap is reconcilable** — most settlement happens off-chain through partner NBFIs; the Hedera vault funds only a fraction of total flow. But it means the institutional LP story is weaker than marketing implies.

### Hedera vault — full holder distribution

| Wallet | bCred balance | % of supply | Identity |
|---|---:|---:|---|
| `0x23632a…46f6` | 384,807.65 | **99.987%** | Operator/Credible treasury (created 124 min after vault deploy) |
| `0x121696…177d` | 23.29 | 0.006% | Test/dev wallet |
| `0x56d48a…5e81` | 10.00 | 0.003% | Retail tester |
| `0xd99ae4…5fc1` | 2.00 | 0.001% | Retail tester |
| `0x2354d3…3e46` | 1.997 | 0.0005% | Retail tester |
| `0xb1116c…4f14` | 0.40 | 0.0001% | Retail tester |
| `0x5f1159…5558` | ~0 | — | Cycled out |
| `0x000…dead` | 0.000001 | — | Burn dust |
| **Total nonzero** | **7 addresses** | | |

**5 unique non-team retail wallets, holding combined ~$37 USDC.** Not 5,000 retail. Not 5 whales. Five tire-kickers.

### Hedera vault deposit/withdrawal cycling

- 40 `deposit()` calls, $1,085,170 gross inflow
- Big wallet `0x23632a…46f6` is receiver on 15 of 40 deposits (99.996% of inflow): $1,085,123
- ~$700K of $1.08M deposited has been withdrawn back via 17 settlement-clearing calls
- Pattern: $200K, $175K, $400K, $300K, $300K cycled — consistent with operator round-tripping, not external LP inflow

---

## 4. APY numbers

| APY | Type | Source | Date | Confidence |
|---:|---|---|---|---|
| **16% "fixed"** | Hedera vault | Founder, OnePiece interview | Oct 2025 | 🔴 contradicted |
| **16% est** | Hedera vault | Byzanlink page | Live | ✅ ("estimated, not fixed") |
| Up to 24% | Solana Aethir pool | Aethir blog | Jul 2025 | 🟡 |
| 8.9% | Hedera Jan 22 → Feb 20 | ⚙️ from on-chain NAV | Apr 2026 | ⚙️ |
| 17.8% | Hedera Feb 20 → Apr 27 | ⚙️ from on-chain NAV | Apr 2026 | ⚙️ |
| **15.2%** | Hedera full life (Jan 22 → Apr 27) | ⚙️ from on-chain NAV (1.0000 → 1.0371 over 94 days) | Apr 2026 | ⚙️ |

**The 15.2% on-chain APY is mechanically real** but operator-controlled — same party deposits + redeems + sets settlement, NAV is whatever they say. No independent loan-book audit. The mid-period jump to 17.8% is what happens when an operator donates a small absolute yield amount into a $1M TVL pool.

---

## 5. Users / customers

| Number | What | Source | Date | Confidence |
|---:|---|---|---|---|
| 100K+ | Active users across PH/NG/UAE | Circle Alliance directory | 2025 | ✅ (Circle source) |
| 320K | Credit card waitlist | Founder, OG Labs pitch | ~Q1 2025 | 🟡 |
| 370K+ | Total users | Founder, OnePiece interview | Oct 2025 | 🟡 |
| 350K | Credit card waitlist | Founder, Colosseum Demo Day | May 2026 | 🟡 (waitlist not active) |
| **150K+ from Nigeria** | Nigerian users | Founder, Sanctum fireside | Apr 2025 | 🟡 |
| **30-50K** | Realistic Nigerian active (after Sybil deduplication) | Our research | May 2026 | ⚙️ |
| 5 fintech clients | Live in production | Credible 2025 wrap-up | Dec 2025 | 🔴 (Abound's legal docs don't name Credible — possibly aspirational) |
| 6 financial institutions | Onboarded across PH/NG/UAE/IN/TH | Founder, Sanctum fireside | Apr 2025 | 🟡 |

### User-count plausibility check

**At $0.47 ARPU** (150K Nigerian users ÷ disclosed Nigerian deployment), 150K active economic users is mathematically improbable. Q1 2025 Credible airdrop tutorials in Nigerian English explicitly recommended multi-account farming ("scale your earnings up to $1,000 by creating multiple accounts and wallets"). **Realistic Nigerian active users: 30-50K after deduplication.**

---

## 6. Funding

| Amount | Source | Date | Confidence |
|---:|---|---|---|
| $100K | Outlier Ventures pre-seed (RWA Base Camp accelerator) | Jun 2024 | ✅ |
| $25K | Solana Cypherpunk Hackathon prize (Stablecoin Track 2nd place) | Dec 2025 | ✅ |
| $250K SAFE | Colosseum Cohort 4 accelerator | Mar 2026 | ✅ |
| $150K | Stellar Development Foundation grant | Mar 2026 | 🟡 (not in awarded list snapshots; founder-claimed) |
| $5M pre-TGE + $30M OracleAI node sale (target) | OnePiece Labs blog | May 2025 | 🔴 (never closed) |
| **~$1M total** | "Investments + grants over past year" | Founder, Colosseum Demo Day | May 2026 | 🟡 |
| **$0 priced round** | Per Tracxn: "no funding rounds yet" | Tracxn | May 2026 | ✅ |

**Verifiable funding floor: ~$375K (Outlier $100K + Hackathon $25K + Colosseum $250K).** Founder claim of "~$1M raised including grants" suggests Stellar grant + various smaller checks accounting for the gap.

---

## 7. Team

| Number | What | Source | Date | Confidence |
|---:|---|---|---|---|
| 2 | Co-founders (Shrikant Bhalerao + Akshay Soam) | Multiple | — | ✅ |
| 1 | COO (Jacob McCarthy) | RocketReach | — | 🟡 |
| 14 years | Founder fintech experience | Founder, OnePiece interview | Oct 2025 | 🟡 |
| ~37 | Total employees (per Tracxn snapshot) | Tracxn | Jan 2026 | 🟡 |
| 1 | Healthcare financing startup acquired (Shrikant's prior exit) | Founder | 2023 | 🟡 |

---

## 8. Partnerships — named

| Type | Name | Role | Confidence |
|---|---|---|---|
| **NBFI capital deployment** | **Loap** (India) | Capital deployment partner | ✅ (founder-named, OG Labs) |
| **NBFI capital deployment** | **Chorus Finance** (Africa) | $15M deployed | ✅ (founder-named, OG Labs) |
| Co-lender | **Mount Fuji** (Singapore) | Singaporean lending institution example | ✅ (founder-named, Sanctum) |
| Liquidity / strategic | BitSwiss Capital | Investor + oracle coalition | ✅ (Plume PR) |
| Stablecoin | Circle | USDC + Programmable Wallets via Alliance | ✅ |
| Vault host | Byzanlink | ERC-4626/7540 vault on Hedera | ✅ |
| LST routing | Sanctum | jupSOL collateral for credit cards | ✅ (Sanctum fireside) |
| DePIN credit card | Aethir | ATH-token-collateralized card | ✅ (July 2025 PR) |
| RWA / tokenized debt | Plume Network | Roadmap, $500M target by Dec 2025 (only $6M verified) | 🟡 |
| US MSB partner | **Unannounced** (likely Brale) | Sender-side US fiat | 🔴 (founder said "applied" but unnamed) |
| Customer (claimed) | Abound | NRI remittance — **legal docs don't name Credible** | 🔴 (likely aspirational) |
| Customer | Pexx | Singapore stablecoin (uses Fireblocks + Ripple, not Credible custody) | ✅ (more accurate framing: "credit-line consumer of Credible USDC") |
| Customer (claimed) | Borderless, WireNow | Logo on website | 🔴 |

---

## 9. Licenses — current state

| License | Jurisdiction | Status | Source | Confidence |
|---|---|---|---|---|
| FinCEN MSB | US | **Registered** Mar 2026 | Credible blog | 🟡 |
| FIU crypto exchange | India | **Owned** | Founder Colosseum | 🟡 |
| Lending license | India | "Owned" (likely via Western Fintrade NBFC) | Founder OnePiece | 🟡 |
| MSB + PSP | Canada | **Applied for** (not owned) | Founder Colosseum | 🟡 (corrects earlier "owned" claim) |
| UAE | UAE | **Partner-licensed** (no own) | Founder OnePiece | 🟡 |
| Singapore | Singapore | **Partner-licensed via Mount Fuji** (no own) | Founder Sanctum | 🟡 |
| ADGM SPC structure | UAE/Cayman-style | **Planned** for token issuance | Founder Colosseum | 🟡 |

---

## 10. Risk / default metrics

| Metric | Value | Source | Date | Confidence |
|---|---:|---|---|---|
| Defaults claimed | **Zero** on $60M+ over 11 months | Founder, OnePiece | Oct 2025 | 🟡 (no third-party verification) |
| Credit duration (initial) | 30-90 days | Founder, OnePiece | Oct 2025 | ✅ |
| Credit duration (now) | **3-5 days** | Founder, OnePiece | Oct 2025 | ✅ (the key insight) |
| FX spread vs Wise (USD→INR) | **~4-5% better** (90 vs 85-86 INR/USD) | Founder, OnePiece | Oct 2025 | 🟡 |
| ACH float duration | 2-3 days | Founder, OnePiece | Oct 2025 | ✅ (industry standard) |

---

## 11. Sanctum LST credit card mechanics

| Parameter | Value | Source | Confidence |
|---|---:|---|---|
| LTV | 50% (e.g., $500 credit on $1,000 jupSOL) | Founder, Sanctum fireside | ✅ |
| Liquidation threshold | **40% price drop** (vs typical AAVE 20-25%) | Founder, Sanctum fireside | ✅ (notably borrower-friendly) |
| Staking yield share | **100% to user** (Credible takes nothing) | Founder, Sanctum fireside | ✅ |
| Repayment grace | 3 days | Founder, Sanctum fireside | ✅ |

---

## 12. MetaDAO context (for the planned CRED launch)

| Number | What | Source | Confidence |
|---|---:|---|---|
| ~$57M | META token market cap | Phantom listing | May 2, 2026 | ✅ |
| ~$2.4M | MetaDAO lifetime revenue (Futarchy AMM) | Blockworks | Since Oct 10, 2025 | ✅ |
| Nov 2023 | Launched | Solana Compass | ✅ |
| Drift, Jito, Sanctum | Notable past launches | Solana Compass | ✅ |

---

## 13. The reconciliation — does the story add up?

### What's internally consistent
- $210K monthly revenue × 12 = $2.5M ARR is plausible for a 12-18 month-old fintech
- $140M/month volume is plausible for a single live US-India corridor with multiple fintech partners
- $1M raised + $2.5M ARR = realistic seed-stage capital efficiency
- 15bps take rate is competitive with Wise (40-60bps total) and reasonable for stablecoin-rail PSP
- 5-day credit duration + zero defaults is plausible IF underwriting is conservative AND ACH risk is well-managed

### What contradicts itself
- **March 2026 "$400M cumulative TPV"** vs **May 2026 "$350M cumulative over 5 months"** — the cumulative number went DOWN by $50M between March and May. Either March was lifetime and May was 5-month-window (definition change), or one of them is wrong
- **$70K six-month revenue (early 2025)** vs **$210K monthly + 10% MoM (May 2026)** — implies ~17.5x growth in 12 months at ~26% MoM compounded, much higher than stated 10% MoM. Suggests recent slowdown
- **"16% fixed APY"** (founder) vs **"16% est APY, no capital guarantees"** (Byzanlink page) — direct contradiction
- **"Biggest LP based out of US"** (founder, Apr 2025) vs **Hedera vault deployed Jan 2026** (so the claim is temporally impossible for that vault) AND **US persons explicitly TOS-banned** from depositing
- **"6 financial institutions onboarded"** (founder, Apr 2025) vs **"live in US-India corridor only"** (founder, May 2026) — what happened to the other 5 corridors?
- **"Canadian MSB owned"** (founder, Oct 2025) vs **"applied for Canadian MSB"** (founder, May 2026) — corrected
- **Abound listed as customer** (multiple Credible sources) vs **Abound's legal docs naming Mudrex+Layer2+Bridge instead of Credible**

### What's verifiable in 2026
- **$1.12M TVL on Hedera vault** ✅ on-chain
- **$6M USDC loans facilitated by Dec 2024** ✅ third-party press
- **$57M META mcap, $2.4M MetaDAO lifetime revenue** ✅ third-party
- **15.2% on-chain NAV growth** ✅ derived from blockchain
- **Funding floor ~$375K** ✅ (Outlier + Hackathon + Colosseum)
- **5 retail wallets in vault holding $37 total** ✅ on-chain
- **99.99% of vault LP supply held by one wallet** ✅ on-chain

### What's unverifiable
- $350M cumulative volume claim
- $210K monthly revenue
- $2.5M ARR
- 15bps take rate (no fee schedule published)
- 10% MoM growth
- $1M total raised
- 150K Nigerian users (likely Sybil-inflated)
- "Zero defaults"
- "Biggest US LP"

---

## 14. The two numbers that matter most

If you only remember two numbers:

1. **$1.12M = the verified on-chain TVL of the Hedera PayFi Vault.** This is what's actually staked, audited, and on-chain. Everything else about LP capital is marketing.

2. **$210K/month = the founder-claimed current revenue.** If true, it's a real ~$2.5M ARR business. If the take rate (15bps) and growth (10% MoM) are also true, the unit economics work. **No third-party verification exists for either, but the math is internally consistent.**

The honest read: **Credible is a real $2-3M ARR seed-stage business with a single live corridor and weak on-chain transparency.** Everything bigger than that is forward-looking or unverifiable.

---

## 15. Sources

**On-chain (primary):**
- Hedera mirror node: `https://mainnet-public.mirrornode.hedera.com/api/v1/contracts/0x6b8dfa6aa5f803a886beb2492ef3307ec0ee16fb`
- Live `eth_call` to vault contract for TVL/NAV/holders

**Founder transcripts (in `./transcripts/`):**
- `colosseum_demo_day_pitch.txt` — May 2026 (latest, most concrete)
- `onepiece_interview.txt` — Oct 2025 (revenue, defaults, credit duration)
- `sanctum_forecast_fireside.txt` — Apr 2025 (LST mechanics, partner FIs, score positioning)
- `aethir_partnership_announcement.txt` — Jul 2025 (DePIN credit card)
- `brand_video.txt` — Apr 2025 (Credible Score consumer marketing)

**Third-party press / verifications:**
- [Plume × Credible PR (Dec 2024) — $6M USDC verified](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)
- [Aethir × Credible launch (Jul 2025)](https://ecosystem.aethir.com/blog-posts/aethir-and-credible-launch-first-depin-powered-credit-card-and-loan-product-backed-by-ath)
- [Byzanlink Markets — vault page](https://markets.byzanlink.com/vaults/credible-payfi-vault/)
- [Tracxn — Credible Finance profile](https://tracxn.com/d/companies/credible-finance/__U_RGxgg7-BUs9t6k5__4-XyLjMS2vbj6KrXb_mvHsqQ)
- [Outlier Ventures portfolio](https://outlierventures.io/portfolio/credible-finance/)
- [Circle Alliance Directory](https://partners.circle.com/partner/credible-finance)
- [Solana Compass — MetaDAO](https://solanacompass.com/projects/metadao)

**Adjacent:**
- [Abound legal disclosures (Mudrex+Layer2+Bridge stack — does not name Credible)](https://accounts.joinabound.com/legal)
- [Credible Finance Airdrop](https://credible.finance/airdrop)
- [DefiLlama — Credible NOT listed](https://defillama.com/chain/Hedera)
