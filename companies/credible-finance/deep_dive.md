# Credible Finance — Deep Dive (April 2026)

> Companion to the agent-payments research files. Goal: understand what Credible actually does, who's behind it, what works, and whether the Solana branding is real or marketing.
> **Date:** 2026-04-27
> **Sources:** Web research agent pass + 3 YouTube transcripts (founder interview, Aethir announcement, brand video) saved in `transcripts/`

> ⚠️ **Update (2026-04-30):** Architecture findings in [`./liquidity_architecture.md`](./liquidity_architecture.md) materially update this file. Specifically:
> - The PayFi Vault is on **Hedera (via Byzanlink)**, NOT Solana. Solana hosts a separate Aethir-related lending pool. Plume is roadmap-only.
> - **Zero on-chain code is public on any chain** (no Solana program ID, no GitHub vault repo).
> - Founder's "16% fixed APY" claim is contradicted by the deployed vault marking it "Est. APY" with no capital guarantees.
> - OracleAI page now returns 404 — confirmed marketing scaffolding.
> - The credit issuance is via TradFi co-lenders (e.g., Mount Fuji in Singapore), not Credible directly.
> Read this file for company background and founder narrative; read `liquidity_architecture.md` for the actual deployed mechanism.

> ⚠️ **Major update (2026-05-03):** On-chain Hedera mirror-node analysis + targeted partner research in [`./operational_partnerships.md`](./operational_partnerships.md) materially correct several claims in this file:
> - **TVL is $1.12M, not multi-million.** The "$60M cumulative" / "$400M+ TPV" numbers are *transaction throughput* (same dollar recycled every 7-14 days), not LP capital
> - **Six-month founder-disclosed revenue: $70K** (OG Labs pitch) — wildly inconsistent with "150K Nigerian users" headline
> - **99.99% of vault LP supply is held by ONE wallet created 124 minutes after vault deployment** — almost certainly a Credible/Byzanlink-controlled treasury, not external institutional LPs
> - **The "biggest LP from US" claim is unverifiable** and US persons are explicitly TOS-banned from depositing
> - **Abound's legal disclosures don't name Credible** — their stack is Mudrex+Layer2+Bridge+Plaid+Persona. Abound is likely an aspirational logo
> - **Named NBFI partners** (founder OG Labs pitch): **Loap (India)**, **Chorus Finance (Africa, $15M deployed)**. Credible doesn't own corridor PSP relationships — partner NBFIs do
> - **150K Nigerian users is heavily airdrop-farmed** (multi-account farming was explicitly recommended in tutorials); realistic active users probably 30-50K
> - **Stellar $150K grant claim is unverified** — Credible doesn't appear in awarded list snapshots from SCF #41 (Feb 2026 deadline)
> - **No 2026 funding round visible** (Tracxn confirms)

---

## TL;DR

**What it is:** A B2B stablecoin payment-orchestrator with an embedded working-capital credit line, run from Bangalore/Dubai by senior Indian fintech-infra founders. They sit between US/Canadian/European neobanks (sender side) and emerging-market payout corridors — primarily **India, Nigeria, Philippines** — and use a USDC credit pool on Solana to eliminate the 48–72-hour pre-funding window that incumbents like Wise, Remitly, Bridge, OpenFX all need.

**The user's UI hunch is correct but the framing is wrong in one important way.** The "boring on-chain payments infrastructure" guess is right *and* there's more to it than the bland UI implies. Critically: **they're cash-flow positive, processed $60M+ in stablecoin credit over 11 months with zero defaults, and just printed $20M of volume in the last 30 days.** This is not a hackathon-stage protocol — it's a real business.

**One correction on the user's memory:** They likely saw Credible at the **Solana Cypherpunk Hackathon awards at Breakpoint Berlin in December 2025** (where they took 2nd place in the Stablecoin Track, $25K USDC). The Colosseum **Cohort 4 Accelerator demo day hasn't happened yet** — that program runs through May 11, 2026. Credible is one of 11 selected from 1,600+ submissions.

**The single most important architectural fact** (from the founder's mouth, not from marketing):
> *"We technically are a Web 2.5 platform. We use DeFi only for the credit piece and the risk modeling, but when it comes to transactions, because of the regulated nature of the product and since other fintechs are built on top of Credible, we have to give API-based access."*

Credible is not a Solana protocol. It's a **traditional payments-orchestrator that uses a USDC liquidity pool as its Nostro account**. The "Solana protocol" framing is more about LP yield (16% APY on USDC/USDT for credit-pool depositors) than about settlement. The user's instinct that the UI doesn't look "sophisticated" is correct because **they're not pretending to be a smart-contract platform** — they're a fintech-as-a-service play with a stablecoin treasury layer.

---

## 1. What they actually do

From the [OnePiece Labs founder interview](./transcripts/onepiece_interview.txt) — Shrikant in his own words:

> "Credible enables remittance rails from developed markets like US, Canada, Europe to developing markets like Nigeria, India, Philippines... We are essentially having a credit pool in between that enables the realtime transfer experience."

The mechanics, exactly as he describes them:

1. A US neobank (the partner / "fintech built on top of Credible") submits a payout request through Credible's API
2. Credible **immediately pays out on the receiver side** (India/Nigeria/Philippines) using USDC liquidity from its credit pool
3. Credible **underwrites the risk** that the partner's ACH transfer will settle on the sender side
4. 2–3 days later, the ACH settles, USD lands at Credible's regulated US partner, and the credit pool is refilled

> "This is how the prefunding or the Nostro setup works in traditional finance, and that's what we are mimicking with Credible — for B2B as well as personal remittances for neobanks."

**The product, in plain English:** *"Stripe's API + a USDC working-capital line, so neobanks can offer real-time international payouts to underserved corridors without locking up pre-funded float in 50 different countries."*

There's a separate consumer-facing layer ("Credible+", "Credible Score", a stablecoin/staking-backed credit card) that the [brand video](./transcripts/brand_video.txt) markets — but the partner dashboard the user registered on is the B2B side.

---

## 2. Founders / team

**Shrikant Bhalerao — Founder / CEO** ([@skantbhalerao](https://x.com/skantbhalerao), [LinkedIn](https://www.linkedin.com/in/shrikantbhalerao/))

Founder's own words on his background ([transcript](./transcripts/onepiece_interview.txt)):
> "I come from a fintech background where I've worked nearly 14 years, mainly towards traditional finance. Prior to Credible, I had a healthcare financing company that got acquired in 2023, and before that I did quite some consulting in the Web3 space — worked with a few exchanges, worked with DeFi protocols primarily in Singapore, Thailand, and the Southeast Asia region."

This is meaningfully more senior than the third-party agent research surfaced. Two material additions from the transcript that *aren't* in his public LinkedIn or news coverage:

- **14 years in fintech** (not 9), pre-Web3 work in EMV / mobile payments / banking
- **A healthcare-financing company acquired in 2023** (specific company name not disclosed in transcript)

Other public roles: co-founded **Seracle** (Web3 infra, 2018) with Akshay Soam; director of **Western Fintrade** (RBI-regulated NBFC) since Feb 2021; ex-Outlier Ventures, Mudrex, DeCharge.

**Akshay Soam — Co-founder & CTO** ([Pune, India](https://www.analyticsinsight.net/interview/exclusive-interview-with-akshay-soam-chief-technology-officer-seracle))
- Co-founded Seracle with Shrikant
- Ex-HSBC engineer, ML specialist
- Background: CipherHut / Cipher Venture Capital / Carabiner Technologies

**Jacob McCarthy — COO** (Washington, DC)
- Ex-Sharky, UGS Labs (crypto-adjacent)
- Thinner public footprint than the Indian co-founders; the US-facing operator

**Notable absences from public team listings:** No named head of compliance, head of credit risk, or head of underwriting — odd for a company doing licensed credit issuance across multiple jurisdictions. Either they're roles Shrikant covers personally given his NBFC board role, or they're unfilled.

**Team size:** Unverified publicly. Pre-seed + accelerator-cohort signals suggest ~10–25 people.

> Sloppy detail to be aware of: An older [Solana Compass profile](https://solanacompass.com/projects/credible-finance) lists "John Doe / Jane Smith / Michael Brown" as CEO/CTO/CFO — that page is either an autogenerated stale clone or never finished. Don't rely on it.

---

## 3. Funding & accelerator history

| Date | Event | Amount | Source |
|---|---|---|---|
| 2024 (Spring) | Outlier Ventures **RWA Base Camp** accelerator | $100K pre-seed | [Outlier portfolio page](https://outlierventures.io/portfolio/credible-finance/) |
| 2024 (Summer) | Solana Summit hackathon — winner | (in-kind) | per Outlier portfolio page |
| 2025 (Spring) | OnePiece Labs × 0G Cohort 2 / Batch #7 | (accelerator) | [0G blog](https://0g.ai/blog/ai-accelerator-cohort-2) |
| 2025 (May) | Active raise announced (claim only) | $5M pre-TGE + $30M OracleAI node sale target | [OnePiece Labs blog](https://www.onepiecelabs.xyz/blog/announcing-the-progress-of-0g-x-onepiece-labs-second-ai-accelerator-cohort) |
| 2025 (Dec) | **Solana Cypherpunk Hackathon — 2nd in Stablecoin Track** | $25K USDC | [Colosseum announcement](https://blog.colosseum.com/announcing-the-winners-of-the-solana-cypherpunk-hackathon/) |
| 2026 (Mar) | **Colosseum Accelerator Cohort 4** (1 of 11 from 1,600+ apps) | ~$250K SAFE | [Colosseum blog](https://blog.colosseum.com/announcing-colosseums-accelerator-cohort-4/) |
| 2026 (Mar) | **Stellar Development Foundation grant** | $150K | [Credible blog](https://blog.credible.finance) |

**Headline backers** on credible.finance: Outlier Ventures, BitSwiss Capital, Circle, Solana, 0G, OnePiece Labs, Colosseum, Superteam, Polygon. Some are equity investors, others are ecosystem/strategic partnerships (Circle is via the Alliance Program; Stellar via grant).

**Crucial founder quote on fundraising posture** (transcript):
> "Right now, frankly, we are in a position where like 4 months ago we were running door-to-door to find investment, and in today's date we are cash-flow positive. We are even thinking if we really need to raise — probably we'll raise some debt but not a proper VC round."

Translated: as of October 2025 (interview recording date), Credible was **cash-flow positive and not actively fundraising equity**. This is unusual at this stage and is the strongest signal that the business is real. The OracleAI node-license sale narrative is best understood as optionality / longer-term upside, not load-bearing fundraising.

**Pre-existing CRED token narrative** (governance + dual-staking + airdrop) survives in docs but **no public CRED contract is listed on CoinGecko or DexScreener**. ~20 retail-influencer YouTube videos from Q1 2025 walk through KYC + lending tasks for the *expected* CRED airdrop. Treat the token roadmap as live but unrealized.

---

## 4. Customers / partners

**Stated customers** (homepage marquee logos, all stablecoin-adjacent fintechs):
- **[Abound](https://www.joinabound.com/)** — Times of India–backed US→India remittance app for NRIs (~800K users, $14M+ raised in 2023)
- **[Pexx](https://pexx.com/)** — Singapore-based stablecoin neobank, also a Circle Alliance member
- **[Borderless.xyz](https://borderless.xyz/)** — global stablecoin orchestration network
- **WireNow** — smaller cross-border payments platform

Per Credible's [2025 wrap-up](https://blog.credible.finance/blog/credible-2025-wrap-up-real-time-stablecoin-settlement-with-payfi): **5 fintech clients live in production by end of 2025**, plus 100K+ end-users (up to **370K+ users by Oct 2025** per founder transcript). Of those 370K, **150K+ are from Nigeria** — Nigeria is the largest single market.

**Strategic partners:** Circle (Alliance Program), Solana, Polygon, Plume Network (RWAfi L1), 0G (AI-on-chain), Stellar (grant). Plus an **oracle coalition** with Credora, Brickken, DeFactor, BitSwiss for the OracleAI credit-scoring stack ([Plume PR Dec 2024](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)).

**Earlier-era partnerships (RWA pivot, status unclear):**
- **Aethir** — DePIN-powered credit card backed by ATH tokens ([crypto.news](https://crypto.news/aethir-and-credible-join-forces-to-launch-the-first-depin-powered-credit-card/), [transcript](./transcripts/aethir_partnership_announcement.txt))
- **DeCharge** — 35 EVs / 70 chargers tokenized RWA pool

**New pipeline (founder transcript):**
- **India ↔ China trade finance** — partnership with "Trinity" group in Shenzhen, ~5,000 merchants ready to offer 0% interest BNPL to Indian importers; Credible underwrites, merchants pay Credible commissions. Routes through an MAS-regulated Singaporean entity since China doesn't support stablecoins directly. Founder: "It's a pure trade finance use case but with short-term credit... that will be the next big milestone for us."
- **Canada → India corridor** opening next (large NRI population, no existing stablecoin remittance options)

**Geography summary:** APAC + Middle East + selected LatAm/Africa corridors, USD-inbound from US businesses paying out locally. Nigeria + India are the volume drivers.

---

## 5. Tech stack — the "Web 2.5" reveal

This is the most important architectural insight from the founder transcript and one that completely reframes how to evaluate Credible:

> "We technically are a Web 2.5 platform. We use DeFi only for the credit piece and the risk modeling, but when it comes to transactions, because of the regulated nature of the product and since other fintechs are built on top of Credible, we have to give API-based access. We have to give them an abstracted experience to move money from fiat to crypto, crypto to fiat."

**What this means:**

| Layer | Implementation |
|---|---|
| **Settlement currency** | USDC primary; USDT also supported. Stellar grant suggests USDC-on-Stellar integration in flight. |
| **Credit pool / Nostro** | On-chain on Solana (the "DeFi piece") — depositor LPs supply USDC/USDT, earn 16% fixed APY |
| **Risk modeling** | On-chain on 0G Network (their stated reason for picking 0G: "the only chain that allows direct integration with OpenAI models"). Migration from off-chain to on-chain pending 0G mainnet. |
| **Settlement transactions** | **Off-chain. API-based. Web2 fiat rails.** Partners call REST APIs; Credible orchestrates regulated bank partners on each side. |
| **KYC** | Persona (string match in JS bundle); 1–2 business day workflow consistent with off-chain handoff |
| **Custody** | Inferred MPC-style via Circle programmable wallets; **Credible explicitly does not touch the capital** — it flows through licensed partners |
| **Multichain footprint** | Solana (primary) + Plume (RWAfi tokenized debt) + Stellar (grant-funded corridor) + Polygon (logo presence). 0G integration pending. |
| **GitHub** | **No public Credible org on GitHub.** Founder's [personal account](https://github.com/shrikantbhalerao) only has stale Bitcoin-exchange forks. **No Solana program IDs disclosed anywhere in docs or JS bundle.** This is the single biggest verification gap. |
| **Public stats** | [dune.com/credible/stats](https://dune.com/credible/stats) referenced but didn't load cleanly — its existence is itself a positive signal |
| **Sandbox + production environments** | `partner.credible.finance` (live), `sandboxpartner.credible.finance` (dev), `app.credible.finance` (consumer), `legacy.credible.finance` (v1 RWA-era still alive) |

**What "Solana-native" actually means here:** the credit pool LP product (where you deposit USDC and earn 16% APY) is on Solana. The actual payment flow that matters to the partner (the user's dashboard) is regulated fiat rails with USDC as a settlement asset. **The Solana piece is the treasury, not the rails.**

This is actually a *correct* architecture for a regulated payment business. But it means:
- Anyone evaluating Credible as a "Solana protocol" is mismodeling
- The competitive comp is **Bridge / BVNK / Mansa**, not Helio / Squads / Drift
- The "OracleAI 100K-node" narrative is largely scaffolding around a fundamentally Web2 payment business

---

## 6. Business model — actual unit economics

Multiple revenue layers. The founder transcript reveals which are real today:

### 1. FX spread on remittance — the actual moat
Founder example, verbatim:
> "If you're sending a dollar from US to India, the FX rate that you get [from Wise/OFX/Remitly] is 85 rupees or 86 rupees per dollar. But if you send it to Credible, you get 90 rupees. So it's massive difference."

That's a **~4–5% better FX rate** than incumbents. On $100M/month projected volume, even capturing 1% of that as net spread = **~$1M/month gross margin**. This is the actual core revenue today.

### 2. Net interest margin on advanced credit
- Credit pool LPs earn **16% fixed APY** (USDC/USDT)
- Credible advances credit to fintech partners at a higher rate
- 11 months in: **$60M+ processed, zero defaults** (founder's words)
- Average credit duration shrunk from 30–90 days to **3–5 days** as they moved underwriting in-house — this is a major de-risking move

### 3. Trade-finance commissions (new, India-China pipeline)
- 0% interest to Indian importers
- Chinese merchants pay Credible commissions to enable BNPL
- "Cost of capital covered by merchant commissions" — pure asset-light revenue if it scales

### 4. Future: Credible+ consumer credit card
- 370K user waitlist (300K cited in some sources, 370K in latest founder interview)
- Staking-backed, scored by AI ([brand video](./transcripts/brand_video.txt))
- DePIN integration for BNPL tiers
- Revenue: interchange + interest

### 5. Future: OracleAI node-license sale
- $30M target (claim only, no third-party verification)
- Standard DePIN-economy fundraising mechanism

**Plausibility check:** If Credible truly does $100M/month in payment volume after the US opens, and captures ~1–2% blended take (FX spread + credit margin), that's **$12–24M annualized gross revenue at full ramp**. They were cash-flow positive at the $20M/month level, so unit economics work without subsidies.

---

## 7. Compliance / licensing — direct from founder

The agent's report flagged compliance claims as "unverified" — the transcript clarifies them precisely:

> "We have an MSB license in Canada. In India we have more of a lending and a crypto exchange license. And in UAE we don't have our own license, but we have partnered with a licensed institution. Same thing in US — we recently partnered with another institution which can do the on-ramping and everything."

| Jurisdiction | Posture | Notes |
|---|---|---|
| **Canada** | **Own MSB license** (likely FINTRAC) | Confirmed by founder |
| **India** | **Own lending license + crypto exchange license** | Likely via Western Fintrade NBFC where Shrikant is a director |
| **UAE** | Partnered with licensed institution (no own license) | Founder explicit. Don't conflate with the unrelated [CredibleX](https://www.adgm.com/media/announcements/crediblex-unleashes-next-generation-lending-solutions-with-new-adgm-licences) (ADGM-licensed) — different entity |
| **US** | **FinCEN MSB-registered** ([blog Mar 2026](https://blog.credible.finance)) + newly partnered with US-licensed MSB for on-ramping (going live "by end of next month" per Oct 2025 transcript) | State-by-state MTL coverage *not* claimed and is a separate lift |
| **Singapore** | Partnership with MAS-regulated entity (for the China corridor) | Founder explicit |

**Founder's framing on regulatory architecture** is sophisticated:
> "We had to build a flow in which we do not touch the capital because we are not regulated, and we had to convince these regulated partners to believe in us. Some of them believed, and having our own MSB and having our own lending license and exchange license in India gave them the confidence that we can do the settlements in India."

This is a **deliberate regulatory arbitrage**: Credible orchestrates, regulated partners hold capital. As regulators evolve their stance on crypto-rail orchestration, this design either becomes the dominant model or attracts MSB-classification scrutiny — currently a gray zone.

---

## 8. The growth trajectory

From the founder transcript (recorded ~Oct 2025):

| Metric | Value |
|---|---|
| Cumulative stablecoin credit processed (11 months) | **$60M+** |
| Defaults to date | **Zero** |
| Volume in last 30 days (as of Oct 2025) | **$20M** |
| Projected volume this month (Oct 2025) | **$30M** |
| Projected volume after US corridor opens | **$100M+/month** |
| Total users | **370K** |
| Users from Nigeria | **150K+** |
| Live B2B clients | **5+** |
| Position 4 months prior | "Running door-to-door to find investment" |
| Position today | **Cash-flow positive** |

Their March 2026 blog post claims **$400M+ TPV cumulative** with a $100M April target. That implies the volume ramp continued — $400M cumulative by March 2026 is consistent with the trajectory of $20M → $30M → $100M+/month described in October.

**Volume claims are self-disclosed and not yet third-party-corroborated** (Dune dashboard exists but didn't load cleanly). But the trajectory is internally consistent across multiple founder statements months apart.

---

## 9. Strategic thesis & what's next

Founder's own words on strategy:
> "Our entire objective is: how do we dollarize the world? How do we make US markets, US assets, US tools of finance accessible to all these developing markets?"

Concrete near-term roadmap (all from transcript, October 2025):
1. **US ↔ India corridor opening** — partnered US MSB goes live, end-to-end on-ramp without third-party dependency. Unlocks $100M+/month volume target.
2. **Canada ↔ India corridor** — existing Canadian MSB license, large NRI population, no stablecoin remittance competitors.
3. **India ↔ China trade finance** — Trinity group, 5,000 merchants, MAS-regulated Singapore entity for routing.
4. **Credible+ consumer credit card** — 370K waitlist, AI-scored, DePIN BNPL tiers.
5. **Migration of risk-modeling to 0G mainnet** when 0G ships.

**PMF framing** (founder candor):
> "First we were trying to build what is trending, then we were trying to build what the VCs want, then we were like 'okay chuck it, let's just build what the demand is, where we have the customer.' Don't build what is trending. Don't build what is the hype or what the VCs want to listen to right now. If you have good numbers, the VCs will come to you."

This explains the pivot history (RWA → DePIN credit card → stablecoin remittance). The current iteration is the one that found PMF.

---

## 10. Red flags / concerns (refined)

After incorporating the founder transcript, the original concerns weight differently:

| Concern (from agent) | Updated weighting |
|---|---|
| **Pivot whiplash** | Confirmed by founder — but now framed as PMF discovery. Less concerning given current cash-flow-positive status. |
| **Solana Compass placeholder team page** | Still sloppy. Minor red flag. |
| **No public GitHub / Solana program IDs** | **Most material verification gap**, unchanged. For a "Solana-native protocol" at this volume there should be public program code. The "Web 2.5" framing partially explains it (settlement is off-chain) but the credit pool itself should be on-chain Solana code. |
| **OracleAI 100K-node sale narrative** | Still reads as fundraising scaffolding. Not load-bearing now that they're cash-flow positive — easier to discount entirely. |
| **Self-disclosed volume claims** | Transcript-confirmed by founder, multiple times across months, with internally consistent trajectory. Lower risk than initially flagged. |
| **Airdrop-farming long tail** | Mostly Q1 2025 cohort. The B2B business serves real fintechs (Abound, Pexx) who wouldn't tolerate fake activity. Less relevant. |
| **Compliance claims outpace disclosure** | Resolved by founder transcript: Canada = own MSB, India = own lending + exchange, UAE = partnered, US = newly partnered + FinCEN-MSB. Specific jurisdictions and structures now clear. |
| **UI looks unsophisticated** | Reframed: deliberate "Web 2.5" choice — they're a regulated fintech orchestrator, not a Solana smart-contract platform. UI matching infrastructure tools (Stripe Connect, Bridge), not consumer DeFi. |

**Net:** The biggest remaining concern is the absence of public Solana program code. Everything else clarifies favorably under transcript review.

---

## 11. What surprised me (post-transcript)

1. **The founder is significantly more senior than third-party sources suggest.** "14 years in fintech" + "healthcare-financing company acquired in 2023" is not in any public bio I found, but Shrikant says it directly. This isn't a hackathon-tourist founder.

2. **They're cash-flow positive at hackathon stage.** Almost no Cypherpunk-or-Cohort-4 cohort company is. This single fact reorders the whole evaluation.

3. **Zero defaults on $60M in 11 months.** If true (founder claim), that's elite credit underwriting. The move from 30–90-day to 3–5-day credit lines is the underrated mechanical insight — short-duration credit on highly observable ACH-settlement risk is structurally low-risk.

4. **The actual moat is FX, not credit.** "85 rupees from Wise vs 90 rupees from Credible" is a 4–5% FX edge at the consumer level. In a $100B+/yr US-India remittance market, even 1% capture = enormous TAM. The credit pool is the *enabler* (eliminates pre-funding); FX edge is what users actually choose them for.

5. **Nigeria is bigger than India for them today.** 150K+ of 370K users from Nigeria, despite India being the strategic focus. There's a story here — likely USD-collateralized payouts to Nigerian recipients in a USD-scarce, naira-devaluing market.

6. **The "Web 2.5" architectural honesty is rare.** Most stablecoin-payment startups pretend to be more on-chain than they are. Shrikant is direct: settlements are off-chain API calls, the credit pool is on-chain, that's it. This is correct architecture but bad marketing — and the founder owns it.

7. **The India-China trade finance pipeline is potentially huge.** 5,000 Chinese merchants offering 0% BNPL to Indian importers, with merchants paying Credible commissions = pure asset-light fee revenue. India imported **$117B from China in 2024** ([Times of India](https://timesofindia.indiatimes.com/business/india-business/indias-trade-deficit-with-china-widens-to-99-2-billion-in-2024-25/articleshow/120308379.cms)). Even capturing 0.1% of that flow = $117M/yr.

8. **The founder explicitly named competitors and dismissed them in detail.** Bridge, OpenFX, Wise, Remitly, OFX — all called out as "still pre-funding-dependent, 48–72-hour settlement." This is not someone who's confused about what their wedge is.

9. **0G chain choice is technically motivated, not just opportunistic.** Founder: "0G is the only chain which allows you to do direct integration with OpenAI models and there's no other chain... For our risk modeling purpose we need to have data access for both off-chain and on-chain, and that's where 0G's compute helps us."

10. **Recommendation rating from a brutally honest accelerator:** Founder on KJ (OnePiece Labs mentor): *"He's so blunt and so straightforward... he helped us getting the right PMF mindset... brutally good."* Companies that survive blunt mentorship and emerge cash-flow positive 12 months later are a different cohort than companies that get told what they want to hear.

---

## 12. Verdict — should you keep watching?

**Yes.** The user's hunch is right and somewhat conservative. Credible is:

✅ **A real B2B stablecoin payment-orchestrator** — not a token-narrative project
✅ **Run by a senior founder** — 14 years in fintech, prior exit
✅ **Cash-flow positive** at $20M/month volume, with a clear path to $100M/month
✅ **Genuinely differentiated** — pre-funding-elimination + AI-underwriting + 16% LP yield + emerging-market corridor coverage
✅ **Multi-jurisdictional licensed** — Canada own MSB, India own lending + exchange, US FinCEN + partner, UAE partner, Singapore partner
✅ **Solving a real problem** — incumbent stablecoin-rail companies (Bridge, BVNK, Iron) all still have the 48–72-hour pre-funding issue Credible eliminates

⚠️ **The marketing is louder than the substance** in a few specific places — OracleAI 100K-node narrative, "Solana protocol" framing, CRED token expectations
⚠️ **Verification gaps remain** — no public GitHub, no published Solana program IDs, Dune dashboard didn't load, volume numbers are self-attested
⚠️ **The Web 2.5 architecture is correct but underrated** — they look like a Solana protocol but are operationally a Web2 fintech with stablecoin treasury

**For the user's research thesis (AI × crypto problems worth solving):** Credible isn't *itself* a problem-finding target — it's an example of a working solution that hides several still-open problems underneath:

- **Cross-border AI-agent payouts to underbanked corridors** — Credible solves this for fintech partners but not for AI agents directly. An agent-native version of Credible's primitive (autonomous agent gets a USDC working-capital line with on-chain underwriting) doesn't exist yet.
- **On-chain credit underwriting for autonomous economic actors** — Credible's underwriting today is for human/corporate fintech partners. Underwriting an autonomous agent's spending behavior is an entirely separate problem (touches the SAR-typology gap from `../../markets/agent_payments/compliance.md`).
- **The 16% APY stablecoin yield from real payment financing** — this is one of the very few stablecoin yield sources that isn't recycling DeFi token emissions. It's actual short-duration trade-finance interest. Worth understanding more deeply as a *yield primitive* for AI agent treasuries.

---

## YouTube transcripts

Saved in `research/transcripts/`:

- **[onepiece_interview.txt](./transcripts/onepiece_interview.txt)** — 18-min OnePiece Labs founder interview, Oct 1, 2025. Single highest-signal source on the company. ([video](https://www.youtube.com/watch?v=lDN7cum06c0))
- **[aethir_partnership_announcement.txt](./transcripts/aethir_partnership_announcement.txt)** — Coindesk-style Aethir × Credible DePIN credit-card announcement (turned out to be an Aethir partnership clip, not a Seracle backstory; still useful for the DePIN credit-card framing). ([video](https://www.youtube.com/watch?v=HjHgDrDgriE))
- **[brand_video.txt](./transcripts/brand_video.txt)** — 87-second Credible brand video, April 2025. ([video](https://www.youtube.com/watch?v=9lSEiBHb2Sk))

**Not yet pulled (lower priority but available):**
- [OnePiece Labs × 0G Cohort 2 Demo Day](https://www.youtube.com/watch?v=Lmw7gcg2Heo) — 55-min full demo day, May 29, 2025
- [Cypherpunk Hackathon Winners short](https://www.youtube.com/shorts/ICiMcuJQBuU) — Solana official, Dec 28, 2025

**Not available (confirmed missing):**
- Standalone Credible pitch from Cypherpunk Hackathon final
- Solana Breakpoint / Hacker House / Bankless / Empire / Lightspeed / Validated podcast appearances
- Colosseum Cohort 4 Demo Day (hasn't happened yet — May 11, 2026)

---

## Sources

**Primary (founder, direct):**
- [OnePiece Labs founder interview transcript](./transcripts/onepiece_interview.txt)
- [Aethir × Credible announcement transcript](./transcripts/aethir_partnership_announcement.txt)
- [Credible brand video transcript](./transcripts/brand_video.txt)

**Company-published:**
- [credible.finance](https://credible.finance) homepage
- [docs.credible.finance / gitbook](https://credible.gitbook.io/docs/) — OracleAI architecture
- [blog.credible.finance](https://blog.credible.finance) — March 2026 roundup, 2025 wrap-up

**Third-party / news:**
- [Outlier Ventures portfolio page](https://outlierventures.io/portfolio/credible-finance/) — pre-seed details
- [Colosseum Cypherpunk Hackathon winners](https://blog.colosseum.com/announcing-the-winners-of-the-solana-cypherpunk-hackathon/)
- [Colosseum Cohort 4 announcement](https://blog.colosseum.com/announcing-colosseums-accelerator-cohort-4/)
- [Plume Network / Credible PR (Dec 2024)](https://www.prnewswire.com/news-releases/500m-of-global-payfi-transaction-scales-with-credible-and-plume-302325118.html)
- [crypto.news — Aethir / Credible DePIN credit card](https://crypto.news/aethir-and-credible-join-forces-to-launch-the-first-depin-powered-credit-card/)
- [Circle Alliance Directory](https://partners.circle.com/partner/credible-finance)
- [0G AI Accelerator Cohort 2 announcement](https://0g.ai/blog/ai-accelerator-cohort-2)
- [OnePiece Labs Cohort 2 progress](https://www.onepiecelabs.xyz/blog/announcing-the-progress-of-0g-x-onepiece-labs-second-ai-accelerator-cohort)
- [token-relations.xyz — DeCharge × Credible RWA tokenization](https://www.token-relations.xyz/p/decharge-partners-with-credible-finance)
- [RocketReach org chart](https://rocketreach.co/credible-finance-management_b6f2e6adc69e177e)

**Founder background:**
- [Shrikant Bhalerao LinkedIn](https://www.linkedin.com/in/shrikantbhalerao/)
- [Shrikant Web3 Cafe op-ed (2023)](https://www.web3cafe.in/opinion/story/opinion-piece-by-seracles-shrikant-bhalerao-on-indias-web3-evolution-know-the-opportunities-and-challenges-605589-2023-07-04)
- [Akshay Soam Analytics Insight interview](https://www.analyticsinsight.net/interview/exclusive-interview-with-akshay-soam-chief-technology-officer-seracle)
- [Western Fintrade Pvt Ltd (RBI NBFC)](https://www.zaubacorp.com/WESTERN-FINTRADE-PVT-LTD-U65910GJ1994PTC022365)

**Pre-pivot RWA / token-narrative pages (use with caution):**
- [Solana Compass profile](https://solanacompass.com/projects/credible-finance) — has placeholder team
- [Plume RWAfi spotlight](https://plume.org/blog/rwafi-ecosystem-spotlight-october-25-november-1)
