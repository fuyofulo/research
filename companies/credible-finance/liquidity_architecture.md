# Credible Finance — Liquidity & Tech Architecture

> Companion to [`./deep_dive.md`](./deep_dive.md) and [`./how_to_build.md`](./how_to_build.md). How the on-chain liquidity actually works — vault contract, LP yield mechanics, KYC gates, co-lending structure, comparable protocols. **Contains corrections to prior files.**
> **Date:** 2026-04-30
> **Sources:** Web research agent + Sanctum Forecast fireside transcript (Apr 9, 2025) + Byzanlink launch video (Feb 13, 2026 — transcript unavailable, music-only)

> ⚠️ **On-chain ground truth (2026-05-03):** A direct Hedera mirror-node pull in [`./operational_partnerships.md`](./operational_partnerships.md) substantially corrects this file's framing:
> - **Real TVL is $1.12M** (live `totalAssets()` on `0x6b8d…16FB`), not multi-million as the marketing implies
> - **99.99% of bCred LP supply is held by ONE wallet** (`0x23632a…46f6`) that was created 124 minutes after vault deployment — almost certainly a Credible/Byzanlink-controlled treasury wallet, not an external LP
> - **Only 5 unique non-team retail wallets ever**, holding combined ~$37 USDC. Not 5,000 retail. Not 5 whales. Five tire-kickers.
> - The big wallet's deposit pattern ($200K, $175K, $400K, $300K, $300K cycled in/out — ~$700K of $1.08M deposited has been withdrawn back) is consistent with **operator round-tripping capital to demonstrate yield + bootstrap NAV**, not external institutional inflow
> - The **"biggest LP based out of US" founder claim is temporally impossible** for the Hedera vault (it didn't exist in April 2025) and US persons are explicitly TOS-banned from depositing per Byzanlink docs
> - The **16% APY is mechanically real but operator-controlled** — same party deposits + redeems + sets settlement, NAV is whatever they say it is on-chain. No independent loan-book audit
> - **Stellar $150K grant is unverified** — Credible doesn't appear in awarded list snapshots
> - **No Reg D 506(c) wrapper, no DST trust, no SPV** disclosed in Byzanlink docs. Pure on-chain ERC-4626/7540 with sanctions screening only
> Read this file for the architectural overview; read `operational_partnerships.md` for the on-chain ground truth.

---

## TL;DR — the biggest correction to our prior understanding

**The PayFi Vault is not on Solana.** It's on **Hedera mainnet**, hosted by **Byzanlink Markets** as an ERC-4626/7540 vault. Vault contract: `0x6b8dfA6aa5f803a886Beb2492eF3307EC0Ee16FB`. LP token: `bCRED`. Audited by Sherlock (Nov 2025 + Jan 2026 — reports private, not public contests). Deployed Feb 13, 2026.

Credible's actual on-chain footprint is **multi-chain and split**:

| Chain | What's there | Status |
|---|---|---|
| **Hedera** (via Byzanlink) | Main PayFi Vault — ERC-4626/7540, ~16% est. APY on USDC, NAV-priced, ~7-day notice redemption, audited | **Live since Feb 13, 2026** |
| **Solana** (via Aethir partnership) | Separate "Private Investors Portal" lending pool — up to 24% APY for ATH/Aethir holders, + Sanctum LST-backed credit card | **Live but undisclosed scale** |
| **Plume** (RWAfi L1) | Tokenized debt issuance + oracle coalition (Credora, Brickken, DeFactor, BitSwiss) | **Announcement only ($500M target Dec 2024 PR; only $6M verified since)** |

**Three things the agent + Sanctum transcript surfaced that change how we should think about Credible:**

1. **No public Solana program ID exists.** The Credible GitHub org has only `brand-kit`, `sdk-examples` (JS), and `switch` (a fork of Hyperswitch). **Zero on-chain code published.** "Web 2.5" was understatement — they don't even open-source the credit-pool program.
2. **The Credible gitbook has been sanitized.** Every reference to CRED token, cUSDC, OracleAI nodes, dual-staking has been removed since Jan 2026. The OracleAI page now returns 404. The litepaper is gone. Score one for "marketing scaffolding has been deprioritized."
3. **The 16% APY isn't fixed.** Byzanlink's vault page explicitly labels it **"Est. APY"** with **"no capital guarantees."** This contradicts the founder's "we provide 16% which is fixed" claim from the OnePiece Labs interview. *Treat 16% as a marketing target, not a contractual rate.*

**The most important insight from the Sanctum fireside (April 2025):**

> *"The financial services that we are providing — they're actually just a way for us to prove that this credit score works. Credit score is our main product. The whole point of this product is to compete with FICO."* — Shrikant Bhalerao

Credible isn't trying to be a payment company. It's trying to be the **FICO-for-Web3**. The PayFi vault, the credit card, the partner orchestration — those are demonstrations. The product is **Credible Score**, distributed through 6+ regulated financial institutions across PH / NG / UAE / IN / TH (named example: **Mount Fuji** in Singapore).

---

## 1. The actual deployed architecture (multi-chain, split)

Once you stop treating "Credible Finance" as a single product, the architecture makes sense:

```
                   ┌──────────────────────────────────────┐
                   │  Credible Finance (off-chain orchestrator) │
                   │   - Partner APIs                          │
                   │   - KYC/KYB (Persona)                     │
                   │   - Reconciliation                        │
                   │   - AI underwriting model                 │
                   │   - Credit Score generation               │
                   └──────────────┬───────────────────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────────────┐
        │                         │                                 │
   ┌────▼─────┐         ┌─────────▼──────────┐         ┌────────────▼────────┐
   │ Hedera   │         │ Solana             │         │ Plume Network       │
   │ Byzanlink│         │ - Aethir lending pool        │ - Tokenized debt    │
   │ PayFi    │         │   (24% APY ATH/USDC/USDT)    │ - Oracle coalition  │
   │ Vault    │         │ - Sanctum LST-backed         │   (announcement only)│
   │ (~16%    │         │   credit card                │                     │
   │  est APY)│         │   (jupSOL collateral)        │                     │
   │ bCRED LP │         │                              │                     │
   │ ERC-4626 │         │                              │                     │
   └──────────┘         └──────────────────────────────┘                     │
                                                                              │
        ┌─────────────────────────────────────────────────────────────────────┘
        │
   ┌────▼─────────────────────────────────────────────────────────────┐
   │  Co-lending TradFi partners (the actual credit-issuance layer)   │
   │  - Mount Fuji (Singapore)                                         │
   │  - Named partners across Philippines / Nigeria / UAE / India / TH │
   │  - US partner FI for fintech onboarding (announced)               │
   │  - Credible: liquidity-only or 50/50 co-lending                   │
   └───────────────────────────────────────────────────────────────────┘
```

**Why three chains:** Each serves a different LP cohort.
- **Hedera/Byzanlink** = institutional / RWA-platform LPs comfortable with ERC-4626 and Byzanlink's KYC layer
- **Solana** = crypto-native LPs (Aethir DePIN holders, jupSOL stakers, retail Solana users)
- **Plume** = future RWA tokenization rail (announced; not live in production volume)

**Why split execution from settlement:** Off-chain APIs handle the actual ACH/UPI/Pix/etc. movement (regulated rails). On-chain vaults are pure liquidity providers + audit trail.

---

## 2. Smart contract — Byzanlink vault details

| Item | Value | Source |
|---|---|---|
| Vault contract | `0x6b8dfA6aa5f803a886Beb2492eF3307EC0Ee16FB` | [Byzanlink page](https://markets.byzanlink.com/vaults/credible-payfi-vault/) |
| Chain | Hedera mainnet | Byzanlink + PR Newswire (Byzanlink-Hedera, July 2025) |
| LP token | **bCRED** | Byzanlink page |
| Standard | ERC-4626 (sync) / ERC-7540 (async) | [Byzanlink docs](https://docs.byzanlink.com) |
| Pricing model | NAV-based with periodic NAV updates (frequency undisclosed) | Byzanlink |
| Audits | Sherlock — Nov 19, 2025 + Jan 13, 2026 | Byzanlink (logo only, **reports not public**) |
| Protocol fee | "Free for a limited time" | Byzanlink |
| Capital guarantees | **None** ("There are no capital guarantees") | Byzanlink |
| Strategy manager | **Credible Finance** (off-chain) | Byzanlink |

**Byzanlink's framing:** *"The vault itself is non-custodial and does not directly originate loans … Strategy execution, credit exposure, and repayment obligations are managed by Credible Finance through its PayFi platform."*

So the vault is a **passive liquidity wrapper** — Byzanlink owns the smart contract, ERC-4626 standardization, and KYC plumbing; Credible owns the off-chain underwriting + relationship with TradFi co-lenders.

**Why this matters for the playbook:** Cloning Credible doesn't mean writing a Solana Anchor program. It means **integrating a vault platform like Byzanlink + Centrifuge + Maple + Sky**, off-chain underwriting, and TradFi co-lender relationships. The on-chain piece is **commoditized infrastructure**, not the moat.

---

## 3. Economic model — disclosed vs undisclosed

### What's disclosed (gitbook + Byzanlink):
- LP yield comes from **transaction-level settlement fees**: instant-settlement fee, liquidity-advancement fee, orchestration/routing fee, FX execution fee
- Receivable financing duration: **1–7 days** (a key risk-management choice; Credible founder iterated *down* from 30–90 days specifically)
- Conservative utilization thresholds and buffers (no numbers given)
- Dynamic liquidity allocation; ability to throttle settlement speed by corridor or partner if defaults rise
- 16% **estimated** APY on Byzanlink (not fixed); up to 24% on the Solana Aethir/Private Investors Portal pool

### What's undisclosed (asked the docs' built-in agent endpoint and got null):
- Numeric APY for LPs in the gitbook itself — only Byzanlink and Aethir surfaces have numbers
- **Rate charged to fintech partners** (the upstream half of the NIM)
- Net interest margin breakdown
- Loan-to-deposit ratio / target utilization
- **Insurance fund or first-loss tranche — explicitly NOT mentioned anywhere in the docs**
- Default-loss waterfall: who absorbs the loss if a partner defaults

### How 16% might actually back (back-of-envelope)

Founder claim: charge fintech partners on 5-day average duration. If receivable rate is ~25–30% APR-equivalent (matches typical EM payment financing), then on $100M annualized volume:
- Gross interest revenue: ~$1–1.5M (5-day duration × 25% APR × $100M turnover = ~$340K, but turnover is higher — actual gross margin pool is in the $1–3M range)
- Plus FX spread (~1–2% per transaction at $100M = $1–2M)
- Plus settlement-fee take (~30–50bps × $100M = $300–500K)

Total gross revenue pool maybe $2–5M annualized at $100M/yr volume. If LPs are $5M of capital earning 16% = $800K/yr in interest.

That's mathematically plausible if and only if (a) volume hits $100M+/yr and (b) LP capital stays small relative to volume (high turnover). **It does NOT pencil out without high turnover** — sub-1-week receivable duration is essential, exactly as the founder iterated.

### The hidden risk: the 16% is a forward target, not a yield curve

Byzanlink labels it "Est. APY." If volume drops or partner defaults occur, LP yield drops mechanically. There's no committed-rate structure. **For a US playbook this would need to be marketed as variable-rate.**

---

## 4. Deposit / withdrawal mechanics

| Parameter | Value | Source |
|---|---|---|
| Lockup period | None disclosed | Byzanlink |
| Withdrawal | **Notice-based, ~7-day settlement** | Byzanlink |
| Minimum deposit | Not disclosed | — |
| NAV update frequency | "Periodic" — not specified | Byzanlink |
| Slippage on partial withdrawals | Not disclosed | — |
| Institutional vs retail vault | No distinction on Byzanlink. **Separate Solana "Private Investors Portal" exists for ATH holders @ up to 24% APY** | Aethir blog |

The 7-day redemption is structurally the same as a 7-day receivable cycle — withdrawals wait for the next batch of advances to wind down. This is closer to a **Maple Finance withdrawal queue** than a continuously-redeemable money-market token.

**For the playbook:** the 7-day notice is what makes the model work — it lets Credible refuse to break a 5-day advance because they liquidated an LP. If you build this, **don't promise instant LP withdrawals**.

---

## 5. KYC and legal — the biggest gap for US persons

This is the part most opaque, most important for replicability, and most regulator-relevant.

### What's disclosed
- Byzanlink uses **ERC-3643** standards for permissioned RWA tokens — **gating is supported infrastructurally**
- The Credible **airdrop product** (separate from the vault) requires KYC to earn Moons points
- Multiple airdrop guides instruct users to "use a VPN if blocked" — circumstantial evidence of geo-fencing

### What's NOT disclosed
- KYC requirements for vault deposits (can a US person deposit?)
- Geographic restrictions (likely US-restricted via offshore entity terms, not stated)
- bCRED LP token's legal status under US securities law
- No Reg D / Reg S / Reg A+ filing has been published
- **Credible operates from Abu Dhabi** — likely VARA/ADGM perimeter (UAE), not US-registered

### Founder direct on this (Sanctum fireside, April 2025)
> *"Frankly we have our biggest LP based out of US. Our [bank we work with] is based out of US, and they also work with three to four fintechs in the US market. So we will be onboarding US fintechs to adopt Credible Score as well."*

**This is a critical signal:** the biggest US LP is *one regulated bank/institution*, not a retail user base. They're operating an institutional B2B funnel for capital, not a public retail vault. The Byzanlink retail-looking interface is either (a) for non-US retail or (b) a marketing surface for institutional onboarding.

### Verdict for the US playbook

**Credible's LP product is NOT legally onboardable for a US retail person via any documented compliant path as of April 2026.** Replicating in the US requires one of:
- **Reg D 506(c)** accredited-investor wrapper around the vault (most likely path — what Credible's US LP probably uses)
- **Reg A+ Tier 2** offering (longer, more public, ~$5–10M in legal/audit fees)
- **Centrifuge-style trust structure** (Delaware Statutory Trust, common for tokenized RWA pools)

This needs to be added to the Phase 3 (Credit Pool Capital) section of [`./how_to_build.md`](./how_to_build.md) — *current playbook understates the legal lift.*

---

## 6. The Sanctum LST integration — a separate product line we missed

**This is new from the April 2025 Sanctum Forecast fireside.** Credible has a Solana-side product that's distinct from the Byzanlink Hedera vault.

### Mechanic (founder direct):
1. User stakes SOL with Credible
2. Credible buys **jupSOL from Sanctum** in the backend (single LST integration point — Sanctum routes to Jupiter, etc.)
3. The LST sits as collateral with Credible
4. User keeps the staking yield (Credible takes nothing from the staking yield)
5. User gets a **credit limit** of ~50% LTV (e.g., $500 against $1,000 of jupSOL)
6. Credit limit can be spent on the credit card or withdrawn as fiat
7. Monthly invoicing + 3-day grace period before liquidation
8. **Liquidation threshold: 40% price drop** (vs typical 20–25% on AAVE-style platforms)

> *"Whatever you stake — if you pick Jupiter, we purchase jupSOL from Sanctum in the backend instead of going and staking directly. So Sanctum acts as a single point for us for acquiring any LST."* — Shrikant

### Why this matters
- **It's NOT the same product as the Byzanlink vault.** Byzanlink LPs supply USDC; Sanctum users stake SOL.
- Two distinct revenue streams:
  - Byzanlink USDC LPs → fund stablecoin payment advances → ~16% est APY
  - Sanctum LST stakers → get credit card / fiat credit line backed by LST → keep their staking yield + use credit
- It's the consumer-side answer to over-collateralized DeFi credit. Founder framing: *"Current collateralization rates are suited for memecoin trading. We're bringing Web3 credit to the normal world."*
- The 40% liquidation threshold (vs AAVE's 20–25%) is borrower-friendly **at the cost of LP risk** — meaning the LP side has to be priced higher to compensate.

### What we still don't know about the Sanctum integration
- Solana program ID (still no public address)
- LST collateral pool size
- Default rates on the LST product
- Whether Sanctum gets any economic share or it's a pure infra integration

---

## 7. The co-lending model — TradFi institutions are the actual credit issuers

**Critical from the Sanctum fireside:** Credible doesn't issue no-collateral credit directly. They orchestrate it through regulated TradFi co-lenders.

### Named partners (founder direct)
- **Mount Fuji** — Singapore lending institution (cited as example)
- 6 financial institutions onboarded across **Philippines (#1), Nigeria (#2), UAE, India, Thailand**
- US: "biggest LP based out of US, they also work with 3–4 US fintechs"

### Two structures
1. **Credible-as-liquidity-only:** Credible provides USDC, partner FI provides credit underwriting + legal-recourse infrastructure
2. **50/50 co-lending:** Credible provides 50% of capital, partner provides 50% + handles enforcement

### Why this matters
- The TradFi partner has **legal recourse on default** (seize local assets, contact employer in jurisdictions like Singapore, etc.)
- Credible's "zero defaults in 11 months on $60M" is partially because they're *not* taking the credit risk alone — partners share it
- This is **CeDeFi by design**, not by accident. DeFi liquidity + DeFi scoring → TradFi enforcement framework

### Founder's framing
> *"This is the CeDeFi architecture where the DeFi liquidity, DeFi scoring — everything is being used by the TradFi framework to provide you no-collateral credit. This way we also protect ourselves and also meet the requirement for the borrower."*

**For the playbook:** This is the actual structural insight — *don't try to be the lender of record.* Be the liquidity provider + credit-scoring layer; partner with regulated FIs for the actual credit issuance. This is also why "we don't touch capital" works regulatorily: capital flows through the TradFi partner's legal entity.

---

## 8. Plume Network integration — announcement-only

Status: **not yet verifiable in production volume**.

The Dec 2024 PR Newswire release ([link](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)) committed to:
- $500M in PayFi transactions on Plume by **December 2025**
- Credible products embedded across Plume's **Nest** vault and lending protocol
- Stack: stablecoins + **debt tokenization** + AI credit scoring
- **Oracle coalition** governing Credible's oracle stack: **Credora** (now part of RedStone), **Brickken**, **DeFactor**, **BitSwiss Capital**
- $6M USDC loans facilitated in the 3 months before announcement (**only third-party verified dollar number**)

### What's actually live as of April 2026
- Plume mainnet launched mid-2025 with ~$150M RWAs deployed (per The Block)
- Plumeberg News Oct/Nov 2025 mentions "PayFi Vault Launch" — but the vault that actually went live (Feb 13, 2026) is on **Hedera, not Plume**
- **No public Q4 2025 / Q1 2026 update on whether the $500M target was hit**
- The oracle coalition has produced **no public artifacts** that I could find — no oracle node software, no slashing economics, no operator set
- **Debt tokenization mechanic is undescribed** — what's tokenized, who buys it, how it bridges Plume↔Solana/Hedera

### Verdict
The Plume partnership is **roadmap, not production**. The split — Hedera live, Solana semi-live, Plume announced — is the most important architectural finding of this entire investigation. **One brand, three chains, three different LP/product configurations.**

---

## 9. OracleAI / credit-scoring oracle — marketing scaffolding confirmed

The OracleAI gitbook page **now returns 404**. The `llms-full.txt` (their docs' machine-readable bundle) contains **zero references** to "Oracle", "OracleAI", "node", "stake", or "slash". Removed entirely.

### What lives on third-party sources
- "AI-driven credit scoring akin to FICO, aggregating wallet and transactional data across DeFi platforms" (Plume PR)
- Aethir credit-card AI scoring uses *"users' ATH portfolio, activity in the Credible lending pool, and card transactions"* — only concrete description of feature inputs
- "Credible is actively seeking node sale partnerships" — i.e., **node sale is roadmap, not closed**
- **The $30M node-license sale we saw in the original deep dive is not corroborated** by any current source

### Verdict
OracleAI is **pure marketing scaffolding** as of April 2026. No mechanism for how oracle nodes pipe risk parameters into the vault. No staking/slashing economics. No published model card. Removing the docs page is a deliberate de-prioritization signal.

For the playbook: **don't bother with the OracleAI node narrative.** It was fundraising scaffolding that the company itself has stopped repeating.

---

## 10. On-chain stats — verifying the $60M+ claim

| Source | Number | Verifiability |
|---|---|---|
| Founder OnePiece interview (Oct 2025) | $60M+ stablecoin credit processed, zero defaults | **Self-attested only** |
| Credible 2025 wrap-up blog | $250M+ T+0 remittance + $60M+ PayFi Vault | **Self-attested only** |
| March 2026 Credible blog | $400M+ TPV, $100M April target | **Self-attested only** |
| Plume PR (Dec 2024) | $6M USDC loans facilitated in 3 months pre-announcement | **Third-party PR (only verified number)** |
| dune.com/credible/stats | Dashboard exists | **Renders client-side, not scrape-able** |
| DefiLlama | **No protocol page for Credible Finance** | Negative confirmation |
| Hashscan/Hedera explorer for `0x6b8dfA…16FB` | Did not return 404; data not extracted in time-budget | Inconclusive |

**Bottom line:** The $60M figure is a **founder self-attestation** at this point. Until DeFiLlama indexes them or Dune visuals are captured, treat as marketing claim. The only third-party-confirmed dollar amount remains $6M from Dec 2024.

---

## 11. Comparable protocols (lateral context)

| Protocol | Chain(s) | TVL / Volume | LP yield | Lockup / withdrawal | Default record |
|---|---|---|---|---|---|
| **Credible PayFi Vault** | Hedera (live), Solana (Aethir pool), Plume (announced) | Not disclosed (claim: $60M cum.) | **16% est.** (Byzanlink), up to 24% (Solana Aethir pool) | ~7-day notice redemption | "Zero defaults" self-attested |
| **Huma Finance** | Solana, Stellar, BNB, Polygon, Celo | **$10B+ cumulative volume by Feb 2026** | ~9% USDC (Classic), 19–31.5% (leveraged Maxi) | Permissionless, daily redemption | **Zero credit defaults** (self-attested, $2B+ in 2025) |
| **Maple Finance** | Ethereum, Solana | ~$2B (2026) | ~10–13% USDC | 30–90 day cycles | **Multiple historical defaults** (Orthogonal/M11 2022, ~$36M; recovered) |
| **Goldfinch** | Ethereum | ~$60M mkt cap; TVL ~$10–20M | 8–13% (Senior Pool) | 14-day epochs | Defaults on multiple deals 2023–24 (publicly disclosed) |
| **Centrifuge** | Ethereum, Centrifuge chain | ~$160M mkt cap; ~$400M+ RWA TVL | 4–10% (varies by pool) | Pool-specific epochs | Some defaults on early Tinlake pools |
| **Jia** | Celo / Ethereum | Small / private | Not public | Closed product cycles | No public default data |

### Closest comp: Huma Finance

Same "PayFi" branding, same Solana commitment, **much larger verified volume** ($10B vs Credible's $60M self-attested), **lower headline APY** (9% vs 16%), broader chain footprint, **publicly traded HUMA token**.

If Credible's narrative scales, Huma is the obvious benchmark. **Huma's model demonstrates that 16% fixed on a self-managed LP vault is unusually rich for the asset class** — 9% is more sustainable. The 16% Credible markets either (a) reflects very high target utilization, (b) is variable-rate dressed up as fixed, or (c) is a temporary subsidy to seed liquidity.

**For the playbook:** if you're building a clone, target a sustainable ~9% (Huma-tier), not 16%. Underpromise, overdeliver.

---

## 12. CRED token — vapor as of April 2026

| Claim | Status |
|---|---|
| Native governance token | Cited consistently across third-party sources (Solana Compass, airdrops.io, cryptorank.io) |
| Minted via dual-staking cUSDC + SOL | Cited on third parties; **completely absent from current gitbook** |
| Boost yields, NFT/RWA access, governance | Same — third-party only |
| Moons points (KYC + referrals + platform usage) → CRED | Live on `credible.finance/airdrop`; conversion ratio undisclosed |
| **Token launched on a chain?** | **No.** No contract address; "Estimated value: n/a" on airdrop trackers |
| Tokenomics / litepaper | **Not published anywhere I could find.** |

**Verdict:** CRED is vapor. Points are accruing but the token is not on-chain. The new gitbook (last reorg Jan 2026) deletes every reference to CRED, cUSDC, and dual-staking — likely a deliberate sanitization ahead of either (a) regulatory review, (b) re-launch under a different structure, or (c) a complete pivot away from the token narrative.

For the playbook: **don't model CRED into your replica's revenue or LP-acquisition strategy.** It hasn't worked for Credible in 2+ years and doesn't appear to be the path forward.

---

## 13. Corrections to prior research files

These findings update specific sections of [`./deep_dive.md`](./deep_dive.md) and [`./how_to_build.md`](./how_to_build.md):

**In `deep_dive.md`:**
- The "Solana program code is the biggest verification gap" framing is half right — they have *no* on-chain code public on any chain. The PayFi Vault is on Byzanlink/Hedera, not custom Credible code.
- Architecture is **multi-chain**, not Solana-primary. Hedera (live), Solana (Aethir), Plume (roadmap).
- The 16% "fixed" APY founder claim is contradicted by the deployed vault marking it "Est. APY"
- OracleAI is no longer in the docs at all — confirmed marketing scaffolding

**In `how_to_build.md`:**
- **Phase 2D (Build the Solana credit pool)** is wrong-framed. Replace with: "Integrate a vault platform (Byzanlink, Centrifuge, Maple) — *don't write a custom Solana program*. Off-chain underwriting + TradFi co-lender relationships are the moat."
- **Phase 3 (Credit Pool Capital)** understates the US legal lift. To onboard US LPs you need Reg D 506(c) wrapper or DST trust structure — not just "deposit USDC."
- Add a new **Phase 5.5: Co-lender partnerships** between "First Corridor" and "First Partner Fintech." Credit issuance to end-borrowers should flow through regulated partner FIs (Mount Fuji-style), with Credible as liquidity-only or 50/50 co-lender. This was missing from the original playbook.
- The Sanctum LST integration is a separate consumer product worth mentioning in Phase 10 (Consumer Layer) — staking-backed credit cards.

I'll add explicit correction notes at the top of those files pointing here.

---

## 14. Key takeaways for the AI × crypto research thesis

1. **The "Credible Score as the real product" framing is the most lateral-useful insight.** Founder explicitly: *"The financial services are just a way to prove that this credit score works."* If you're thinking about AI-agent-credit-scoring (Compliance Gap #1 from `markets/agent_payments/compliance.md`), Credible's positioning is the template — build credit-scoring infrastructure first, distribute through regulated FIs second.

2. **CeDeFi co-lending is the regulatorily-tractable model, not pure DeFi.** Credible's design — DeFi liquidity + DeFi scoring + TradFi enforcement — is what works in 2026. Pure-DeFi credit doesn't have legal recourse. Pure-TradFi can't onboard crypto-native borrowers. **The AI-agent-credit version is structurally identical: agent reputation + on-chain underwriting + regulated FI as lender of record.**

3. **The vault platform is commoditized.** Byzanlink, Centrifuge, Maple, Sky — these are infrastructure layers, not moats. The moat is the underwriting model + the partner relationships.

4. **Multi-chain isn't strategic confusion — it's LP-cohort matching.** Hedera = institutional/RWA. Solana = crypto-native. Plume = future RWA tokenization. Different chains for different capital sources.

5. **Founder's actual exit path is FICO-for-Web3, not "Bloomberg of crypto."** Different company than first-glance read suggests. Closer to a credit bureau than a payment company.

---

## 15. YouTube content

Saved in [`./transcripts/`](./transcripts/):

- **[sanctum_forecast_fireside.txt](./transcripts/sanctum_forecast_fireside.txt)** — Sanctum Forecast #12, Apr 9, 2025. ~40K chars. **This is the highest-signal LP-side founder interview** outside the OnePiece one. Covers: co-lending model with named partners (Mount Fuji), Sanctum LST integration mechanic, 40% liquidation threshold, the Credible-Score-as-main-product framing. ([video](https://www.youtube.com/watch?v=NOzUlNMQX2o))
- **[byzanlink_vault_launch.txt](./transcripts/byzanlink_vault_launch.txt)** — Byzanlink Feb 13, 2026 product launch. **Transcript unavailable** (music-only / no spoken content). Video metadata only confirms the Hedera vault deployment date. ([video](https://www.youtube.com/watch?v=0IBfg_UjMl4))

Already pulled (from prior research):
- [onepiece_interview.txt](./transcripts/onepiece_interview.txt) — covers the partner-side mechanics
- [aethir_partnership_announcement.txt](./transcripts/aethir_partnership_announcement.txt) — DePIN credit card framing
- [brand_video.txt](./transcripts/brand_video.txt) — Credible Score consumer marketing

---

## 16. Sources

**Verifiable, primary:**
- [Byzanlink Markets — Credible PayFi Vault page](https://markets.byzanlink.com/vaults/credible-payfi-vault/) — the only fully verifiable on-chain reference
- [Credible gitbook (current, sanitized)](https://credible.gitbook.io/docs/)
- [Sanctum Forecast #12 transcript](./transcripts/sanctum_forecast_fireside.txt) — Apr 9, 2025 founder fireside
- [Credible GitHub org](https://github.com/crediblefinance) — confirms no on-chain code public

**Third-party / news:**
- [Plume × Credible PR ($500M target, oracle coalition, Dec 2024)](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)
- [Aethir × Credible DePIN credit card launch (July 2025)](https://ecosystem.aethir.com/blog-posts/aethir-and-credible-launch-first-depin-powered-credit-card-and-loan-product-backed-by-ath)
- [Solana Compass profile (older Solana cUSDC architecture, now removed from official docs)](https://solanacompass.com/projects/credible-finance)
- [airdrops.io — Credible airdrop page (Moons points)](https://airdrops.io/credible/)
- [Byzanlink-Hedera launch PR (July 2025)](https://www.prnewswire.com/news-releases/byzanlink-launches-on-hedera-bringing-rwa-vaults-to-the-network-302207340.html)

**Comparable protocol references:**
- [Huma Finance docs](https://docs.huma.finance/)
- [Maple Finance protocol page](https://maple.finance/)
- [Goldfinch protocol page](https://goldfinch.finance/)
- [Centrifuge protocol page](https://centrifuge.io/)
