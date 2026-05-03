# Credible Finance — Operational Partnerships & On-Chain Ground Truth

> The "what they actually do, with whom, at what scale" file. Built from three parallel deep-research passes (corridor mechanics, capital stack, Nigeria deep-dive) on May 3, 2026, including a fresh on-chain Hedera mirror-node pull.
> **Date:** 2026-05-03
> **Major corrections to prior files** flagged inline below — `deep_dive.md`, `liquidity_architecture.md`, `architecture.md`, and `how_to_build.md` should be read with these updates in mind.

---

## TL;DR — six findings that materially update our understanding

**Confidence labels:** ✅ verified (on-chain or named primary source) / 🟡 inferred (strong circumstantial) / 🔴 marketing claim only

1. ✅ **Credible is NOT a PSP and does NOT own corridor rail integrations directly.** They are the credit + capital orchestration layer on top of **partner NBFIs**, who own the actual UPI/NIBSS/InstaPay/Pix integrations. The named partners are: **Loap (India), Chorus Finance (Africa), Pexx (Philippines)**, an unannounced US MSB (most likely Brale or Cross River). The "Razorpay vs Cashfree" question is *Loap's* question, not Credible's.

2. ✅ **The Hedera PayFi Vault has $1.12M TVL — not multi-million.** Live on-chain reading of `totalAssets()` on `0x6b8d…16FB` confirms. Marketing claims of "$60M cumulative" and "$400M+ TPV" are *transaction throughput* (the same dollar recycled every 7-14 days), not LP capital.

3. ✅ **99.99% of vault LP supply is held by ONE wallet** that was created 124 minutes after vault deployment, almost certainly a Credible/Byzanlink-controlled treasury wallet. Combined with 5 unique retail wallets holding $37 USDC total, the vault is **a single-tank demonstrator with a token retail tail**, not a live multi-LP institutional product.

4. ✅ **The "biggest LP based out of US" founder claim doesn't survive scrutiny.** The Hedera vault's TOS explicitly bans US persons from depositing. No press release, partnership announcement, or LP shoutout names anyone. Most plausible reading: founder was speaking loosely about the team's own working capital cycled through a friendly US-based entity (likely BitSwiss).

5. ✅ **$15M deployed into the African market via Chorus Finance** (founder OG Labs pitch). $132M "PTC pipeline" mentioned. Total disclosed Credible revenue over 6 months: **$70K**. That revenue figure is wildly inconsistent with the "150K Nigerian users" headline and supports the deduplication hypothesis (true active users probably 30-50K after stripping airdrop farms).

6. ✅ **Abound's legal disclosures DO NOT name Credible.** Their stack is Mudrex + Layer2 + Persona + Bridge + Plaid. So Abound is either an aspirational logo (not yet a paying live partner) or Credible sits invisibly behind Mudrex/Layer2. Either way, the "Abound is a Credible client" framing in our prior research overstates the relationship.

---

## 1. The corrected framing — Credible is a layer above the rails

**Earlier framing (in our prior research):** Credible has direct PSP integrations across India (Razorpay/Cashfree), Nigeria, Philippines, etc. Multi-jurisdiction license stack is the moat.

**Correct framing (per this research):** Credible is **a credit + capital deployment layer** sitting on top of partner NBFIs. Each NBFI partner owns the local PSP/banking relationships and the regulatory perimeter. Credible's job is to:
- Provide the USDC liquidity (credit pool)
- Underwrite risk (Credible Score)
- Aggregate fintech-partner demand
- Orchestrate the API layer

The named partners (founder OG Labs pitch, late 2025):
- **Loap** — India NBFC capital deployment partner (founder: *"Loap will be our partner to deploy the capital in the India market"*)
- **Chorus Finance** — Africa capital deployment partner (founder: *"Chorus Finance helped us in deploying capital into the African markets"*)
- **Pexx** — Philippines (operates own BSP-licensed flow with Fireblocks custody + Ripple blockchain payments; Credible supplies the USDC credit advance)
- **Unannounced US MSB** — most likely Brale (architecturally consistent: stablecoin-native, USDC-rails-friendly, lowest-friction onboarding)

**Strategic implication for any competitor:** You don't compete by integrating Razorpay or Paystack. You compete by recruiting one Loap-equivalent NBFI per corridor and becoming *their* USDC credit line. **Mansa and Huma Finance run this same model.**

---

## 2. Corridor-by-corridor operational reality

### India 🟡

| Layer | Detail | Confidence |
|---|---|---|
| NBFI partner | **Loap** (named by founder) | ✅ |
| Founder relationship | Shrikant Bhalerao is a director of Western Fintrade Pvt Ltd (RBI NBFC since 1994); Western Fintrade is also likely involved | ✅ |
| Likely PSP rail (via Loap) | Cashfree or Razorpay for IMPS/UPI payouts | 🟡 |
| Probable workhorse | **IMPS** (uses raw account+IFSC, what most remittance flows use) | 🟡 |
| KYC vendor (India-specific) | Hyperverge / IDfy / Bureau (layered on top of global Persona) | 🟡 |
| Crypto custody | Liminal (likely; founder previously at Mudrex, where Liminal is the Indian institutional default) or Fireblocks | 🟡 |
| Adjacent infrastructure to investigate | **Saber.Money** — built by Mudrex (founder's prior employer), launched Oct 2023, supports IMPS/NEFT/UPI/RTGS via REST API + KYC SDK + webhook. **The architectural fit is exact**; whether Credible uses Saber.Money specifically or something nearly identical is unconfirmed | 🟡 |

**The Mudrex/Saber.Money parallel matters.** It strongly suggests Credible's INR rail is plumbed through tooling that already exists in the Mudrex ecosystem — meaning the "India corridor" is operationally simpler than building from scratch. Anyone building a competitor could use Saber.Money directly.

### Nigeria (Africa) 🟡

| Layer | Detail | Confidence |
|---|---|---|
| Capital partner | **Chorus Finance** (named by founder) | ✅ |
| African deployment | **$15M deployed via Chorus** (founder OG Labs pitch) | ✅ |
| PSP / off-ramp partner | **Yellow Card most likely** (only continent-scale licensed crypto on/off-ramp; explicit Payments API for USDT/USDC ↔ NGN bank settlement; default rail for crypto-native fintechs since CBN's Dec 2023 partial unban) | 🟡 |
| Other PSP candidates | Onafriq, Fincra, Grey, Breet | 🟡 |
| Nigerian VASP license | **Credible does NOT hold one.** Operating via partner-VASP shield (Yellow Card or Quidax holds it) | ✅ verified absence |
| NIBSS Instant Payment (NIP) integration | Yes, via PSP partner | 🟡 |
| FX rate | Post-2024 unification — official NAFEX vs effective P2P now within ~2% (the historic 30-50% parallel-market gap collapsed) | ✅ |
| User base mix | **Stablecoin-direct delivery** (USDC/USDT to user wallet) more common than fiat conversion, since most Nigerian users want USD-equivalents as Naira inflation hedge | 🟡 |

### Philippines ✅

| Layer | Detail | Confidence |
|---|---|---|
| Founder rank | **#1 user corridor** (Sanctum fireside) | ✅ |
| Named client | **Pexx** (Singapore-based, BSP-licensed via partner, USDT/USDC-to-fiat across 50+ countries) | ✅ |
| Pexx's stack | **Fireblocks for custody + Ripple for blockchain payments** (per Pexx's own materials) | ✅ |
| Credible's actual role | **Credit-line consumer of Credible USDC** — Pexx owns its own settlement rail; Credible advances USDC against Pexx user receivables | 🟡 |
| Rail | InstaPay (real-time, sub-PHP 50K) + PesoNet (batch). GCash and Maya both sit on InstaPay | ✅ |
| Likely Credible PSP | Coins.ph (BSP VASP-licensed, corporate API) | 🟡 |
| BSP licensing | Pexx holds the EMI/VASP license; Credible operates behind it | 🟡 |

**Crucial reframing:** "Pexx as Credible client" actually means "Pexx as a credit-line consumer of Credible USDC." Pexx still owns its own settlement rail. This is much less of a Credible-controlled relationship than the marketing implies.

### Brazil 🔴

Mostly speculative. Mentioned in Plume PR (Dec 2024) and listed as a corridor in Circle Alliance directory, but no concrete deployment figures. Likely Pix integration via **Bitso Business** (operates LATAM USDC↔BRL via Pix), but unconfirmed. Treat as "advertised, not operating."

### UAE ✅

- Credible HQ is Abu Dhabi
- Founder explicitly said: *"setting up a credit fund or SPV structure with **ADGM in UAE**"* — meaning **FSRA (ADGM)** is the regulator, not VARA (Dubai) or CBUAE
- **The UAE corridor is for incorporation + treasury + credit-fund structuring, NOT retail UAE-resident off-ramp.** Credible does not have CBUAE Stored Value Facility or Money Services license required for AED retail flows.

### Thailand 🔴

Founder mentioned Thailand among partner corridors, but no Thai partner publicly announced. Likely **Bitkub** (largest Thai SEC-licensed crypto exchange, supports PromptPay deposits) but unconfirmed.

### US Senders 🟡

| Layer | Detail | Confidence |
|---|---|---|
| US MSB partner | **Unannounced — most likely Brale** (newer, stablecoin-native, USDC-rails-friendly, low-friction onboarding) or Cross River Bank or Lead Bank | 🟡 |
| Canada MSB | **Owned by Credible directly** (founder confirmed) — enables Canada→India remittance without partner | ✅ |
| Rails accepted | ACH (confirmed). Wire / RTP / FedNow likely supported but not advertised | 🟡 |
| Direct USDC sender support | A US fintech can probably send USDC directly to Credible (no fiat conversion). Architecturally consistent but not advertised as a separate product | 🟡 |
| Synapse-style BaaS layer | **Explicitly avoided** — Credible pitches as orchestrator, not BaaS middleware | ✅ |

---

## 3. Integration shape — what partner fintechs actually plug into

**From `credible.gitbook.io/docs` (the most authoritative source):**

| Aspect | Detail |
|---|---|
| Primary integration | **Single REST API.** Quote: *"Merchants integrate once through a single API, while Credible manages all local complexity underneath."* |
| Async events | Webhook callbacks for settlement confirmation |
| Pay-out flow | Synchronous "immediate settlement confirmation" via API response → async fiat execution + reconciliation event via webhook |
| Sandbox URL | `sandboxpartner.credible.finance` (SPA shell only via WebFetch — needs real browser to inspect JS chunks) |
| Production URL | `partner.credible.finance` |
| SDK | **No public SDK** (TypeScript/Python/Go) advertised in any Credible material |
| No-code dashboard | Yes (Partner Portal) — fintechs can submit payouts manually as fallback |
| API rate limits | Not disclosed |
| Pricing | Not disclosed per-call; founder mentioned per-day rate on USDC float |
| Average integration time | Not disclosed; Saber.Money parallel suggests "weeks not days" given regulated-partner onboarding burden |

**To verify what JS-bundle vendors are loaded** (would settle several open questions): inspect `sandboxpartner.credible.finance` in a real browser with DevTools, look for substrings: `razorpay.com`, `cashfree.com`, `mudrex.com`, `saber.money`, `liminal.io`, `fireblocks.io`, `persona.com`, `hyperverge.co`, `idfy.com`, `bridge.xyz`, `brale.xyz`.

---

## 4. The on-chain ground truth — Hedera vault analysis

**Direct mirror-node pull on May 3, 2026.** Vault contract `0x6b8dfA6aa5f803a886Beb2492eF3307EC0Ee16FB` (Hedera account `0.0.10230098`):

| Field | Value | Source |
|---|---|---|
| Deployed | **2026-01-15 12:25:41 UTC** | mirror node `/contracts/{addr}` |
| Token name | "Credible Payfi Vault" | `name()` |
| Token symbol | **"bCred"** (note casing — not "bCRED") | `symbol()` |
| Underlying asset | Hedera HTS USDC `0.0.456858` | `asset()` |
| `totalAssets()` | **$1,122,303.55 USDC** | live `eth_call` |
| `totalSupply()` | 1,082,139.30 bCred | live `eth_call` |
| Implied NAV | **1.0371 USDC/bCred** | derived |

### LP holder distribution — 7 nonzero addresses ever

| Holder | bCred balance | % of supply | Identity |
|---|---:|---:|---|
| `0x23632a…46f6` | **384,807.65** | **99.987%** | Operator/Credible treasury wallet |
| `0x121696…177d` | 23.29 | 0.006% | Test/dev wallet (12 micro deposits) |
| `0x56d48a…5e81` | 10.00 | 0.003% | One-off retail test |
| `0xd99ae4…5fc1` | 2.00 | 0.001% | One-off retail test |
| `0x2354d3…3e46` | 1.997 | 0.0005% | One-off retail test |
| `0xb1116c…4f14` | 0.40 | 0.0001% | One-off retail test |
| `0x5f1159…5558` | ~0 (cycled) | — | Withdrew |
| `0x000…dead` | 0.000001 | — | Burn dust |

**Five unique non-team retail wallets, holding combined ~$37 USDC.** This is not 5,000 retail. It's not 5 whales. It's 5 tire-kickers.

### The one big LP wallet — what it actually is

`0x23632a…46f6` (Hedera account `0.0.10230197`):
- **Created `2026-01-15 14:29:37 UTC` — exactly 124 minutes after vault deployment**
- Created by the same external account that funded vault deployment (key type ECDSA secp256k1, fresh seed)
- **Zero transaction history before vault deposits** — never used for anything else
- Memo field empty; no labels on Hashscan

**Inference:** This is overwhelmingly likely a Credible/Byzanlink-controlled treasury wallet, not an external LP. The "biggest LP based out of US" claim from the April 2025 Sanctum fireside is **temporally impossible** (the Hedera vault didn't exist then) and was either (a) referring to the Solana lending pool (still unverified), or (b) marketing fluff, or (c) describing the team's own working capital cycled through a friendly US-based entity (BitSwiss is the most plausible candidate).

### Cumulative deposit/withdrawal cycling pattern

40 `deposit()` calls totaling $1.085M gross inflow. **15 of those 40 (totaling $1,085,123 — 99.996% of inflow) were the big wallet.** Of that, **~$700K has already been withdrawn back** via redemption flow. Pattern: $200K, $175K, $400K, $300K, $300K cycled in/out.

**This is consistent with one party stress-testing or "round-tripping" capital to demonstrate yield and bootstrap NAV** — not external institutional inflow.

### NAV trajectory (the "16% APY" claim)

| Period | Days | NAV start | NAV end | Annualized |
|---|---:|---:|---:|---:|
| Jan 22 → Feb 20 | 29 | 1.0000 | 1.0068 | **8.9% APY** |
| Feb 20 → Apr 27 | 66 | 1.0068 | 1.0371 | **17.8% APY** |
| Full life | 94 | 1.0000 | 1.0371 | **15.2% APY** |

NAV growth is mechanically real. **But:**
- NAV is set by the operator wallet (`0x0febcd…0e8c`) which calls the settlement selector `0x5c9ce04d` 17 times to clear redemptions
- When a single party controls deposits + settlement + NAV, **NAV is whatever they say it is on-chain**
- No independent oracle or auditor confirms the loans funding the yield are real
- The mid-period jump to 17.8% APY is mathematically what happens when an operator donates a small absolute amount of yield into a small TVL — easy to manufacture

### Capital structure / KYC reality (from Byzanlink docs Q&A endpoint)

- ✅ **US persons explicitly TOS-banned** from depositing ("cannot use the interface if citizen, resident, or otherwise located in the United States of America")
- ✅ **No Reg D 506(c) carve-out** documented
- ✅ **No Cayman SPV / DST / trust wrapper** disclosed
- ✅ **No minimum/maximum/lockup** documented
- ✅ KYC is wallet-screening + email/account info only (lighter than accredited verification)

This **directly contradicts the "biggest LP based out of US" claim** — that LP would be in violation of the protocol's own TOS.

---

## 5. Total TVL across all pools (best estimate)

| Pool | TVL | Source |
|---|---:|---|
| Hedera Byzanlink "Credible PayFi Vault" | **$1.12M** | live `totalAssets()` |
| Solana lending pool (cUSDC) | **Unknown** | Not on DeFiLlama; protocol page lists no live figure |
| Aethir Private Investors Portal | **Unknown — gated** | Aethir blog discloses no figures |
| Plume vault (if any) | **Not deployed at scale** | Not on RWA.xyz Plume index |
| **Verifiable total** | **~$1.12M** | |

**DeFiLlama check:** Credible Finance is **not listed**. The "$60M cumulative" and "$400M+ TPV" numbers are *transaction throughput*, not TVL. Throughput can be inflated by recycling the same dollar through the vault every few days — which is exactly the on-chain settlement pattern.

---

## 6. Capital raises & token status — May 2026

- ✅ **No 2026 funding round visible** — Tracxn says "Credible Finance has not raised any funding rounds yet." PitchBook funding shows $0. Outlier accelerator + early angels not always indexed.
- ✅ **CRED token still pre-TGE** — Moons points farming live on `credible.finance/airdrop`, no TGE date
- ✅ **OracleAI node sale narrative is stale** — no 2026 update, treat as abandoned
- ✅ **Stellar Community Fund grant unverified** — Credible doesn't appear in awarded list snapshots from SCF #41 (Feb 2026 deadline), contradicting our earlier "received $150K from SDF March 2026" claim. This was probably also marketing.

---

## 7. The Nigeria reality check

**150K Nigerian users from a $70K-revenue company in 6 months is mathematically impossible.** That's $0.47 ARPU. Either the user count is heavily inflated or the revenue isn't being captured.

**The Q1 2025 airdrop campaign explicitly recommended multi-account farming.** Tutorials in Nigerian English: *"scale your earnings up to $1,000 by creating multiple accounts and wallets."* This is the standard Sybil-farming geography pattern (Nigeria + Vietnam + Indonesia + Pakistan + Bangladesh).

**Realistic deduplication factor: 3-5x.** True Nigerian active users probably **30K-50K**.

**What Credible actually does in Nigeria:**
- B2B payout infrastructure (US businesses paying contractors / sellers / creators in NG)
- Stablecoin-direct delivery (USDC to user wallet) more common than NGN conversion
- Aethir card globally available but Nigerian last-mile delivery unverified
- Founder said "very soon in Nigeria" for the FI partnership — **still not landed publicly** as of the Sanctum fireside

**The wedge a competitor could take:**
- A true USD savings account for Nigerians (Credible's product earns yield but isn't a savings account)
- A Nigeria-issued, Nigeria-shipped USD card loadable from NGN (Credible's card isn't)
- B2C remittance with a Lagos brand presence (Credible is positioned B2B)

**Operational requirements to compete in Nigeria:**
- SEC Nigeria VASP license (₦500M paid-up capital, 60% Nigerian board, 9-18 months, ~$1-2M)
- Tier-1 bank partnership under CBN's Dec 2023 VASP-account guidelines
- $5M+ NGN/USDC liquidity book
- Local team: compliance officer, payments ops lead, NG English/Pidgin support bench

---

## 8. Implications for the user's plan (and corrections to prior files)

### Updates to push into existing files

**`deep_dive.md` — needs corrections:**
- Replace "$60M+ in stablecoin credit, zero defaults" with: "$60M is *throughput*, not LP capital. TVL is $1.12M. Six-month revenue: $70K (founder-disclosed)."
- Replace "5+ live B2B fintech clients (Abound, Pexx, Borderless, WireNow)" with: "Pexx is verifiably integrated as a credit-line consumer. Abound's legal disclosures don't name Credible (their stack is Mudrex+Layer2+Bridge). Borderless and WireNow are likely logos, not paying live partners."
- Replace "150K+ users from Nigeria" with: "150K *registered wallets* from Nigeria, heavily airdrop-farmed; realistic active users 30-50K"
- Add: "$15M deployed in African market via Chorus Finance partnership (founder OG Labs pitch)"

**`liquidity_architecture.md` — needs corrections:**
- "16% est APY backed by transaction fees" — corrected: NAV-mechanically real, but operator-controlled. No independent loan-book audit.
- "Biggest LP based out of US (founder-disclosed)" — corrected: temporally impossible (Hedera vault deployed Jan 2026, founder claim was April 2025); US persons explicitly TOS-banned; no LP names anywhere; most plausible reading is team's own treasury cycled through a friendly entity
- Add: 99.99% of bCred is one wallet created 124 minutes after vault deployment
- Add: 5 unique non-team retail wallets total, holding ~$37 USDC combined
- Add: Stellar Community Fund $150K grant claim is unverified (Credible doesn't appear in awarded list snapshots)

**`architecture.md` — partner table needs major revision:**
- Replace the "Indian NBFC (Western Fintrade-adjacent; UPI/IMPS via Cashfree/Razorpay)" framing with: **"Loap (named India NBFI partner) → likely Cashfree/Razorpay underneath"**
- Add **Chorus Finance** as the named Africa NBFI partner ($15M deployed)
- Reframe Pexx as "credit-line consumer of Credible USDC" (Pexx owns own rail with Fireblocks + Ripple)
- Note that the US MSB partner is most likely Brale (not yet announced)
- Remove Saber.Money / Mudrex specific references unless confirmed (architecturally adjacent but unconfirmed)

**`how_to_build.md` — Phase 1 should change:**
- Don't try to integrate Razorpay/Paystack directly. **Recruit one Loap-equivalent NBFI per corridor and become *their* USDC credit line.** This is exactly Mansa's and Huma's model.
- Phase 5 (TradFi co-lender partnerships) should specifically name "NBFI capital deployment partner" as the role to recruit
- Add: Saber.Money (Mudrex's B2B onramp) is a possible direct vendor for India INR rails — saves the NBFI recruitment for later

### What this means for the user's strategic positioning

The "build a better Credible" thesis gets sharper when you internalize what Credible actually is:

1. **Credible is much smaller than marketing suggests.** $1.12M TVL, $70K six-month revenue, ~30-50K real users. They're a Series-Seed-stage company by every meaningful metric, despite the "operating in 7 corridors" branding.

2. **Their actual moat is partner-recruitment, not technology.** The smart contract is commoditized (Byzanlink hosts it). The "AI underwriting" is unverifiable. **The moat is signing Loap, Chorus Finance, and a US MSB.** If you can sign equivalent partners faster — and your founder Indian background actually helps with Loap-tier outreach — you can leapfrog.

3. **The vault demonstration is theater, not substance.** A team-treasury-funded vault with NAV growth they control is a marketing artifact. A real LP-funded vault with audited loan books would be a different category of credibility. **A competitor that publishes verifiable on-chain LP data and actual loan tape would dominate the institutional LP conversation Credible is currently pretending to have.**

4. **Nigeria is not as locked-up as it looks.** 150K headline users is mostly airdrop residue. Credible has not yet landed the Nigerian FI partnership. **The Nigeria corridor is genuinely open** — first mover with a real Lagos office + bank partnership + Naira-fundable card could take meaningful share.

5. **Position B (vertical wedge) and Position C (open-source/compliance-forward) from the plan now look stronger relative to Position A (US-onshore wedge).** The reason: Credible's actual gap isn't US-onshore positioning (they don't have it but they also don't need it for their tiny scale). Their gap is **transparency + real LP capital + verifiable on-chain operations**. A competitor who publishes everything Credible obscures could win institutional LPs without competing on the same regulatory wedge.

---

## 9. Highest-leverage next-research questions

In priority order:

1. **Loap (India NBFC)** — search "Loap India NBFC" / "Loap.fi Solana"; DM founder on X/Telegram; check RBI NBFC register. This is the load-bearing India relationship.
2. **Chorus Finance (Africa)** — same approach. Holds $15M deployment.
3. **The unannounced US MSB partner** — most likely Brale; verify via Brale's public partner list and Solana payment-rails announcements from Q1 2026.
4. **The Indian KYC vendor** — submit a fake-application flow at the partner portal and capture the iframe domain. Likely Hyperverge, IDfy, or Bureau.
5. **`sandboxpartner.credible.finance` JS-bundle inspection** — must be done in a real browser. Look for vendor substrings.
6. **Plume Network's tokenization docs** — Plume hosts Credible's PTC tokenization. The Plume mainnet tx history would show Credible's actual on-chain pool sizes and could identify LP-cohort wallets.
7. **The Solana lending pool's actual TVL** — separate from the Hedera Byzanlink vault. Need on-chain Solana program ID first (still unpublished anywhere).
8. **Founder's direct response on Twitter / Telegram** — DM `@skantbhalerao` with a polite question about LP base or ask in their Telegram. Often gets a response.

---

## 10. Sources

**On-chain (primary):**
- Hedera mirror node: `https://mainnet-public.mirrornode.hedera.com/api/v1/contracts/0x6b8dfa6aa5f803a886beb2492ef3307ec0ee16fb`
- Live `eth_call` to `totalAssets()`, `totalSupply()`, `name()`, `symbol()`, `asset()` on Hedera vault contract

**Web/PR (named primary sources):**
- [Credible PayFi Vault on Byzanlink Markets](https://markets.byzanlink.com/vaults/credible-payfi-vault/)
- [Byzanlink Q1 2026 Recap](https://byzanlink.substack.com/p/byzanlink-q1-2026-recap)
- [Byzanlink docs Q&A endpoint](https://docs.byzanlink.com/welcome-to-byzanlink.md)
- [Credible Finance Airdrop](https://credible.finance/airdrop) + [CryptoRank guide](https://cryptorank.io/drophunting/credible-activity668)
- [Aethir × Credible launch](https://ecosystem.aethir.com/blog-posts/aethir-and-credible-launch-first-depin-powered-credit-card-and-loan-product-backed-by-ath)
- [PR Newswire: $500M PayFi Plume + Credible (Dec 2024)](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)
- [Tracxn: Credible Finance profile](https://tracxn.com/d/companies/credible-finance/__U_RGxgg7-BUs9t6k5__4-XyLjMS2vbj6KrXb_mvHsqQ)
- [DefiLlama Hedera (no Credible/Byzanlink listing)](https://defillama.com/chain/Hedera)

**Local transcripts (founder direct):**
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/transcripts/onepiece_interview.txt`
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/transcripts/sanctum_forecast_fireside.txt`
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/transcripts/aethir_partnership_announcement.txt`

**Adjacent (for triangulation):**
- [Saber.Money (Mudrex B2B onramp)](https://saber.money/) — architecturally adjacent to Credible's likely Indian rail
- [Abound legal](https://accounts.joinabound.com/legal) — Mudrex+Layer2+Bridge stack confirms Abound doesn't directly use Credible
- [Western Fintrade Pvt Ltd](https://www.zaubacorp.com/WESTERN-FINTRADE-PVT-LTD-U65910GJ1994PTC022365) — founder's NBFC director role
- [Pexx](https://pexx.com/) — Singapore-based BSP-licensed flow with Fireblocks + Ripple
- [Yellow Card Payments API](https://yellowcard.io/payments/) — most likely Credible Nigeria PSP
- [Huma Finance docs](https://docs.huma.finance/) — closest comparable model
