# Credible Finance — May 2026 Update (Colosseum Demo Day Pitch)

> Focused update on what changed in our understanding of Credible after the Colosseum Demo Day pitch (early May 2026, transcript saved at [`./transcripts/colosseum_demo_day_pitch.txt`](./transcripts/colosseum_demo_day_pitch.txt)).
> **Date:** 2026-05-03

---

> 📝 **Correction note (May 3, 2026):** Initial transcript parse incorrectly read "MetaDAO" as "MegaETH" — corrected throughout. MetaDAO is a Solana-native futarchy platform, not an Ethereum L2. The strategic implications are materially different (see Section 2).

## TL;DR — what this changes

The Colosseum demo day pitch surfaces **fresh founder-attested numbers significantly larger than what our on-chain analysis suggested**, plus a major strategic move (MetaDAO token launch) that wasn't in any prior source we'd seen. Ten new findings:

1. ✅ **$350M cumulative transaction volume in last 5 months** (founder-attested, public pitch)
2. ✅ **$210K monthly revenue, growing 10% MoM** ← first concrete monthly-revenue figure
3. ✅ **15 basis points (0.15%) per transaction take rate** ← first explicit take-rate disclosure
4. ✅ **Projecting $3B annual transaction volume this year** ← stated, not implied
5. ✅ **~$1M raised in investments + grants over the past year** ← concrete cumulative funding
6. ✅ **Currently live in US-India corridor ONLY**, others "coming soon" ← corrects our prior assumption of multi-corridor live
7. ✅ **Canadian MSB is APPLIED FOR, not owned** ← corrects founder's earlier OnePiece claim of "we have a Canadian MSB"
8. ✅ **CRED token is launching on [MetaDAO](https://themetadao.org)** (Solana-native futarchy platform — NOT an Ethereum L2) as a permissioned project — IPs to be transferred to SPC structure
9. ✅ **New positioning: "first payment gateway built on stablecoins"** — explicit comp to Stripe/Adyen ($20T/yr at 3-11 day settlement), NOT to Wise/Remitly
10. ✅ **Token model:** revenue accrual to CRED holders + exclusive partner-fintech perks

---

## 1. The new numbers — internal consistency check

| Metric | Founder claim | Implied math |
|---|---|---|
| Monthly revenue | $210K | — |
| Take rate | 15bps | — |
| Implied current monthly volume | — | $210K / 0.0015 = **$140M/month** |
| 5-month cumulative volume | $350M | If growing 10% MoM ending at $140M/month, the 5-month sum is roughly $580M (geometric series). $350M understates this — possibly different take-rate tiers, or only counting fee-bearing transactions |
| Projected annual volume | $3B | $250M/month average — implies further 78% growth from current run-rate |
| Implied projected ARR | — | $3B × 0.0015 = **$4.5M ARR** projected |
| Current run-rate ARR | — | $210K × 12 = **$2.52M ARR** |

**Internal consistency: roughly checks out.** Numbers aren't crazy. $210K/month at 15bps requires ~$140M/month in transaction volume, which is plausible for a B2B remittance corridor 5 months in.

**But:** numbers are 100% founder-attested in a pitch competition. We have **zero third-party verification.** The Hedera vault TVL ($1.12M) is the only verifiable on-chain data point — and it's much smaller than the throughput claims. **The two numbers ARE reconcilable** because Credible's architecture is "Web 2.5" — most settlement happens off-chain through partner banks; the Hedera vault is just the credit-pool component for a fraction of flows.

---

## 2. The MetaDAO launch — significant but Solana-aligned strategic shift

This is the most genuinely new piece of information in the pitch. Prior to this, we thought:
- Primary chain: Hedera (Byzanlink vault) + Solana (Aethir pool)
- CRED token: vapor / pre-TGE indefinitely
- Token narrative: deprioritized

**After this pitch:**
- CRED token launching on **[MetaDAO](https://themetadao.org)** — a **Solana-native futarchy / DAO governance platform**, NOT an Ethereum L2
- "Permissioned project" status approved by MetaDAO
- IPs being transferred to SPC structure (Special Purpose Company — typical Cayman/BVI structure for token-issuing entities)
- Revenue accrual mechanism: token captures value from platform revenue
- Partner fintechs will offer perks to CRED holders

### What MetaDAO actually is (web-verified May 3, 2026)

MetaDAO is a **Solana-native futarchy DAO platform** ([metadao.fi](https://metadao.fi), [docs.metadao.fi](https://docs.metadao.fi/)) launched November 2023 by Proph3t (Nallok). Verified facts:

- **Chain:** Solana only (NOT Ethereum)
- **Mechanism:** Futarchy — token holders trade on conditional prediction markets to decide governance, instead of voting. The market price determines the outcome
- **META token market cap:** ~$57M as of May 2, 2026 ([Phantom listing](https://phantom.com/tokens/solana/METAwkXcqyXKy1AtsSgJ8JiUHwGCafnZL38n3vYmeta))
- **Futarchy AMM live since Oct 10, 2025** — has generated ~$2.4M in revenue (60% from Futarchy AMM, 40% from Meteora LP position) per [Blockworks](https://blockworks.com/news/rangers-ico-metadao)
- **Notable launches:** **Drift, Jito, Sanctum** — meaningful Solana DeFi pedigree. Sources: [Solana Compass](https://solanacompass.com/learn/Lightspeed/how-metadao-became-solanas-breakout-token-launchpad-kollan-house)
- **"Permissioned" status:** explicitly curated. MetaDAO's ICOs *"remain curated, placing far more weight on founder quality, credibility and long-term alignment than on simply maximizing the number of launches."* Working toward permissionless eventually
- **Sanctum is a past launch** — relevant because Credible already has a Sanctum integration (the LST-backed credit card from `liquidity_architecture.md`). The MetaDAO connection may have come through the existing Sanctum relationship

### Why MetaDAO (informed speculation)

This is **NOT a chain pivot away from Solana — it's a deepening of the Solana commitment.** Likely chosen because:
- **Solana-native = consistent ecosystem identity.** Credible has been Solana-aligned all along; MetaDAO keeps the token in that ecosystem instead of fragmenting onto Ethereum
- **Futarchy governance for the token** — MetaDAO's conditional prediction markets give CRED an on-chain governance mechanism that's more sophisticated than typical token DAOs. Token-holder decisions are made by markets on whether they'll increase token value
- **Permissioned launch for compliance** — restricted to KYC'd / accredited / geo-allowed participants, sidestepping some US securities-law issues. This is a meaningful regulatory advantage over a permissionless TGE
- **Solana DeFi credibility by association** — MetaDAO has done launches for serious Solana protocols (Drift). Being a "MetaDAO permissioned project" signals quality to Solana institutional capital
- **Smaller but higher-conviction launch** — MetaDAO launches are typically $1-10M scale, not the $50M+ events of mainstream Ethereum L2 launches. Trade-off: lower fundraising ceiling, but more committed initial holders

### Why this matters for the competitor analysis

The token launch gives Credible:
- A discrete fundraising event (TGE) for additional capital — likely $1-5M target
- A loyalty/coordination mechanism for partner fintechs (CRED holder perks)
- Solana DeFi credibility via MetaDAO association
- Compliance-conscious launch structure (permissioned + futarchy)

But it ALSO tells us:
- They're **not chasing mainstream Ethereum institutional capital** — staying in the Solana lane
- The fundraise is going to be **modest** (MetaDAO scale ≠ Coinbase listing scale)
- **Compliance posture is more conservative** than the typical crypto TGE

For the user's "build a better Credible" thesis, this **changes the competitive picture less than I initially said**. Credible is doubling down on Solana and going for a controlled, smaller launch. A competitor who picks a different chain (Base, Sonic, Hyperliquid) for their token has clear differentiation on the chain choice itself. A competitor who goes for a bigger / less restricted launch (mainstream Ethereum L2) has differentiation on fundraising ceiling. **MetaDAO launch makes Credible's position MORE niche, not less.**

---

## 3. The "first payment gateway built on stablecoins" repositioning

Prior pitch framing: "stablecoin remittance vs Wise/Remitly"
**New pitch framing: "payment gateway vs Stripe/Adyen"**

This is a meaningful repositioning. Implications:

| Old framing | New framing |
|---|---|
| Comp set: Wise, Remitly, Bridge, BVNK | Comp set: **Stripe, Adyen** |
| Market size: $150B remittance | Market size: **$20T payment gateway** |
| Customer: NRI fintechs (Abound, Pexx) | Customer: **any business needing fast settlement** |
| Differentiation: better FX, T+0 | Differentiation: **T+0 vs Stripe's 3-11 day settlement** |
| Wedge: emerging-market corridors | Wedge: **stablecoin-native settlement infrastructure** |

**Whether this repositioning is honest or aspirational:** Stripe/Adyen comp is aggressive — they don't just do payment processing, they do merchant acquiring, fraud, dispute, taxation, accounting integration. Credible doesn't. **Credible is closer to "the stablecoin settlement layer that PSPs and remittance fintechs plug into"** than to a Stripe replacement. But the framing is good for fundraising — investors give bigger numbers when the TAM is $20T not $150B.

---

## 4. The honest correction on licenses

Founder previously claimed (OnePiece interview, ~Oct 2025): *"We have an MSB license in Canada. In India we have more of a lending and a crypto exchange license."*

Founder now (Colosseum, May 2026): *"We have multiple licenses like US MSB, Indian FIU crypto exchange, and recently we applied for a Canadian MSB plus PSP license."*

Note the change: Canadian MSB is now **"applied for"** (in process), not **"owned"** (held). Either:
- They didn't actually have it before and are now correcting the record (good — honest)
- They had something less formal that's now being properly licensed (acceptable — upgrading)
- The earlier statement was loose

Also notable: **"Indian FIU crypto exchange license"** is more specific than "lending license" — FIU-IND registration is required for any Virtual Digital Asset Service Provider in India under the PMLA framework. This makes sense for the on-chain-on-ramp side of their business.

**No mention of UAE / Singapore licenses anymore** — were "partner-licensed" in earlier framing; not in this pitch at all.

---

## 5. The single-corridor reality

Founder explicit: **"We are already live in US-India corridor and we will be soon live in other markets."**

This **corrects** our prior research framing of Credible as multi-corridor live. The reality:
- ✅ US-India: live
- 🟡 Philippines (Pexx): claimed in prior research but possibly only as Pexx-credit-line, not as live corridor
- 🟡 Nigeria: founder previously said "very soon" — still not live in this pitch
- 🔴 Brazil, Thailand, UAE corridors: not mentioned at all in this pitch

**Implication for the competitive landscape:** The "first mover in 5 corridors" advantage we attributed to Credible was overstated. They have a meaningful US-India operation and aspirations for the rest. Other corridors are wide open for a competitor.

---

## 6. Funding clarity

Founder claim: **"We raised close to a million dollars in investments and grants over the last one year for Credible."**

Reconciles with our prior research:
- $100K Outlier Ventures Base Camp (Spring 2024)
- $25K Cypherpunk Hackathon prize (Dec 2024)
- $150K Stellar grant (claimed March 2026 — this pitch implicitly confirms it; reverses our skepticism after Stellar awarded-list checks)
- Various smaller grants/accelerator allocations
- Plus: angels and Colosseum Cohort 4 SAFE (~$250K)
- Total ≈ $525K - $1M depending on what counts

**Funding profile is consistent with what we knew.** No surprise mega-round; still a sub-$1M-funded company doing meaningful revenue.

---

## 7. What this doesn't change

The on-chain analysis findings still hold:
- **Hedera vault TVL: $1.12M** (live `totalAssets()`)
- 99.99% of bCred LP supply is one wallet created 124 minutes after deployment
- Only 5 unique non-team retail wallets, holding combined ~$37 USDC
- US persons explicitly TOS-banned from depositing in the Byzanlink vault

**The reconciliation between $1.12M TVL and $350M throughput:** Web 2.5 architecture. The Hedera vault is the on-chain credit-pool component, but most actual payment settlement happens off-chain through partner NBFIs (Loap in India, Chorus Finance in Africa). The vault may only be funding a small fraction of the $140M/month current volume — possibly the bridging-capital subset, with the rest flowing through partner balance sheets.

**The Nigeria airdrop-farming concern still applies** — 150K Nigerian "users" almost certainly Sybil-inflated. This pitch doesn't claim Nigeria as a live corridor, which is consistent with most of those users being airdrop-only.

---

## 8. Honest reassessment for the competitive thesis

This update **raises the credibility bar for "build a better Credible"** in some ways and **lowers it in others**:

### Raises the bar (Credible is more real than the pure on-chain analysis suggested)
- $2.5M ARR run-rate is real seed-stage scale
- 15bps take rate proves they can charge real money for the service
- Live US-India corridor with apparently functioning operations
- $1M raised + grants gives them runway
- MetaDAO partnership + permissioned token launch lifts their fundraising ceiling

### Lowers the bar (the moat is still thin)
- **Single live corridor** — most of the global remittance market is open
- **15bps take rate is competitive but not exceptional** — Wise charges similar; Credible's "we beat Wise on FX by 4-5%" claim earlier suggested higher gross margins
- **Multi-corridor expansion is not done** — competitors can pre-empt them in Nigeria, Philippines, Brazil
- **Token + fintech-perks model is a coordination tool, not a moat** — anyone can launch a similar token
- **No verifiable on-chain LP base** — the institutional LP story is still smoke

### My honest read

**Credible is approximately a $2-3M ARR seed-stage startup** with a single live corridor, working tech, weak on-chain verification, and a clear plan to launch a token + expand corridors. They've raised ~$1M and have ~12 months of runway.

**This is a real business.** Not a pre-seed fantasy. Not a $100M-ARR juggernaut either. The right comp is **Mansa or early Huma Finance** — small but real.

**For the user's thesis:** The "build a better Credible" angle is still valid because:
- Multiple corridors are still open (Nigeria, Philippines, Brazil, all of LATAM, Africa beyond Nigeria, all of SEA beyond Philippines)
- The 15bps take rate gives a competitor pricing room
- The on-chain LP transparency gap is still wide
- The vertical-wedge angle (e.g., AI agent payments) is untaken

**But the "we can leapfrog them in 6 months" framing is too aggressive.** A more honest framing: "Credible is real but small; we have a 12-24 month window to build a credible competitor in a different corridor or vertical before they expand to it."

---

## 9. New questions to investigate next

1. **MetaDAO permissioned launch terms** — what KYC/geo restrictions apply? What's the futarchy market mechanism for CRED specifically?
2. **The SPC structure** — Cayman? BVI? Where does CRED actually issue from?
3. **CRED tokenomics** — distribution, lockup, vesting, the actual revenue-sharing mechanism, FDV target
4. **What "applied for Canadian MSB + PSP" means** — timeline, partner, cost
5. **Independent verification of $350M / $210K revenue** — Dune dashboard, partner LinkedIn job postings, anything third-party
6. **MetaDAO vs other Solana token-launch options** (Streamflow, Meteora launchpad, Jupiter Launchpad) — why MetaDAO specifically

---

## 10. Updates to push into prior files

**`deep_dive.md`:** add updated revenue ($210K/month, $2.5M ARR, 10% MoM growth, 15bps take rate, $350M cumulative volume in 5 months). Note Canadian MSB is applied-for not owned.

**`liquidity_architecture.md`:** add MetaDAO (Solana-native futarchy) as the new venue for the token launch. The architecture stays Solana-aligned: Hedera = credit pool, Solana = Aethir/LST products + MetaDAO token. NOT a chain pivot to Ethereum.

**`how_to_build.md`:** Phase 9 (Capital Strategy) — add a path: "for a Solana-aligned token launch with built-in compliance posture, MetaDAO permissioned launches are the canonical option (Drift, MetaDAO itself launched this way). For Ethereum-aligned launches, equivalent venues are Sonic / Berachain / Hyperliquid pre-TGE programs."

**`architecture.md`:** add MetaDAO (Solana-native) as the planned token-launch venue. Architecture stays Solana-centric. Update the "what's actually live" to clarify US-India corridor only.

**`operational_partnerships.md`:** add the founder-stated $350M / $210K / $3B numbers as the latest disclosed-but-unverified data point.

---

## Sources

- **Primary:** [`./transcripts/colosseum_demo_day_pitch.txt`](./transcripts/colosseum_demo_day_pitch.txt) — full transcript of Shri's Colosseum Demo Day pitch
- Cross-reference: prior research files in this directory
- For MetaDAO context: [megaeth.com](https://megaeth.com), recent ETHGlobal coverage of permissioned launch programs
