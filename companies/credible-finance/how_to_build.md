# How to Build Credible Finance — Linear Playbook

> Companion to `./deep_dive.md`. If you were starting from zero, this is the order you'd actually have to execute. Built from Credible's revealed playbook (founder transcript + public sources) + general fintech-build first principles.
> **Date:** 2026-04-29

> ⚠️ **Update (2026-04-30):** Several phases in this playbook need correction based on findings in [`./liquidity_architecture.md`](./liquidity_architecture.md):
> - **Phase 2D (Solana credit pool):** Don't write a custom Solana Anchor program. Integrate a vault platform (Byzanlink, Centrifuge, Maple). The on-chain piece is commoditized; the moat is off-chain underwriting + TradFi partner relationships.
> - **Phase 3 (Credit Pool Capital):** Onboarding US LPs requires a **Reg D 506(c) accredited-investor wrapper or Delaware Statutory Trust structure** — not just "deposit USDC." Add ~$50–150K legal + ~6 months to timeline.
> - **Add a new Phase 5.5: TradFi co-lender partnerships.** Credible's actual model is co-lending with regulated FIs (50/50 capital share, partner is lender of record, partner handles enforcement). Add 60–120 day BD cycle per partner. This is what makes "we don't touch capital" work regulatorily.
> - **Phase 10 (Consumer Layer):** Add Sanctum-style LST-backed credit cards as a separate consumer product line (jupSOL collateral, 40% liquidation threshold, user keeps staking yield).
> - The "OracleAI 100K-node sale" optionality in Phase 9 is not load-bearing — Credible deprioritized it; you can drop entirely.

> ⚠️ **Sharpening (2026-05-03):** Operational research in [`./operational_partnerships.md`](./operational_partnerships.md) makes the playbook more precise:
> - **The actual moat is NBFI partner recruitment, not PSP integration.** Credible's named partners are **Loap (India)** and **Chorus Finance (Africa, $15M deployed)** — they own the local PSP/banking relationships. Don't try to integrate Razorpay/Paystack directly. Recruit one Loap-equivalent NBFI per corridor and become *their* USDC credit line. This is exactly Mansa's and Huma's model.
> - **Phase 5 (First Partner Fintech) target list correction:** Abound is likely NOT a paying live partner — their legal disclosures name Mudrex+Layer2+Bridge, not Credible. Pexx is verifiably integrated. Borderless and WireNow are likely logos. Don't waste cycles cold-pitching the Abound-equivalent fintechs as "Credible peers" — they may have already evaluated and chosen something else.
> - **Phase 1 jurisdiction note:** Credible's $70K six-month revenue + $1.12M TVL means the entire competitive set is operating at much smaller scale than the marketing suggests. Don't over-build for hypothetical $100M/month volume — design for $1-5M/month and grow from there.
> - **Phase 6 (in-house underwriting):** The "AI underwriting" in Credible is unverifiable. A competitor that publishes the actual default-rate methodology + on-chain loan tape would have a credibility advantage with institutional LPs Credible can't reach.

---

## Reading guide

**Critical-path dependencies are noted as `(GATE)` — don't start the next phase before that gate clears.**

Costs are rough orders of magnitude in USD. Marked **(approx)** when sourced from industry comps and **(disclosed)** when Credible or comparable companies have published numbers.

Total Year-1 cash needed (excluding credit pool capital): **~$500K – $1.5M**.
Total credit pool capital needed by Month 12 to do $20M/month volume on 5-day duration: **~$3–5M**.

---

# PHASE 0 — Foundation (Weeks 0–4)

Goal: legally exist, have a thesis, have a deck, have founders aligned.

- [ ] **Pick the wedge before anything else.** Credible's wedge: "eliminate the 48–72-hour pre-funding window for B2B remittance to underbanked corridors via a USDC credit pool." Don't pick "stablecoin payments" as a wedge — too vague. Pick a specific corridor + a specific incumbent pain.
- [ ] **Founder team:** at minimum 1 fintech operator (compliance + bank-partner relationships) + 1 backend engineer (APIs + integrations) + 1 protocol/blockchain engineer (credit pool). Credible's nucleus was 2 senior India-based fintech-infra founders + 1 US-based COO. *Don't underestimate the value of the local-corridor co-founder.*
- [ ] **Co-founder agreement** signed (vesting, IP assignment, founder break-up clauses). Use Clerky / Stripe Atlas templates. ~$500–1,500.
- [ ] **Pick legal HQ jurisdiction.** Most common: Delaware C-Corp (for US fundraising) + a local subsidiary in your operating jurisdiction (India Pvt Ltd, UAE FZE, Singapore Pte Ltd). Credible operates from Bangalore + Dubai + DC. ~$2–5K incorporation costs + ~$5–10K/year ongoing compliance.
- [ ] **Initial deck** (15 slides): problem, wedge, market size, product demo, GTM, business model, team, ask. Don't fundraise from this yet.
- [ ] **Domain + email + minimal website** (one-page landing with email capture). $20/mo.

**Phase 0 spend: ~$5–10K. Phase 0 team: 2–3 founders.**

---

# PHASE 1 — Legal & Compliance Foundation (Months 1–9, runs parallel with Phase 2)

This is the longest, most painful, and most critical phase. **(GATE for production volume)**

## 1A. Compliance counsel
- [ ] Hire fintech-specialized compliance counsel for **each jurisdiction** you operate in. ~$300–800/hr. Budget $30–80K for first year of advisory.
  - US: e.g., Goodwin, McDermott, Mayer Brown — fintech/payments practice
  - India: e.g., Khaitan & Co, IndusLaw — RBI/NBFC practice
  - Canada: smaller firms specializing in FINTRAC MSB
  - UAE: ADGM-specialized firms

## 1B. AML / CFT program (foundational document, gates everything else)
- [ ] Write your **AML Policy + KYC Procedures + Sanctions Screening Procedures + Suspicious Activity Reporting Procedures**. ~50–100 pages. Use a compliance consultant if needed (~$15–30K). Every banking partner and license application asks for this first.
- [ ] Pick KYC vendor: **Persona** (Credible's choice), Onfido, Sumsub, Veriff. ~$1–3 per verification. Persona offers a free tier; expect $2–10K/month at scale.
- [ ] Pick on-chain analytics vendor: **Chainalysis KYT** or **Elliptic** for OFAC sanctions screening on USDC addresses. ~$30–80K/yr enterprise.

## 1C. Sender-side licensing (US first, since US→ corridor is the volume driver)
- [ ] **FinCEN MSB registration** (US federal). Free to register, but the AML program above is a hard prerequisite. Filed via FinCEN BSA E-Filing System. **(disclosed: Credible has this since March 2026)**
- [ ] **State Money Transmitter Licenses (MTLs)** — this is the brutal one. Full 49-state coverage costs **$5–8M and takes 18–36 months**. **Don't do this early.** Two paths Credible took:
  - **Partner with a US-licensed MSB** that already has state coverage. They handle MTL compliance; you pay them per-transaction. Vendors: Synapse (now defunct — caution), Solid, Brale (newer, stablecoin-focused), or directly with banks like Cross River, Lead Bank.
  - **Get the Vermont / Wyoming sandbox** or limited-purpose charter. Faster but limited.
- [ ] **OFAC SDN screening** integrated at every transaction (build or buy from Chainalysis/Elliptic).

## 1D. Receiver-side licensing (varies by corridor)
- [ ] **India: partner with an NBFC** (RBI license) — getting your own NBFC requires ₹2 crore min capital (~$240K), 18–24 months, hard. Most companies partner. Credible's founder happens to be a director of [Western Fintrade Pvt Ltd](https://www.zaubacorp.com/WESTERN-FINTRADE-PVT-LTD-U65910GJ1994PTC022365) — that's their unfair advantage. If you don't have that, partner deal is ~5–10% revenue share.
- [ ] **India payment rail integration via aggregator** — UPI/IMPS/NEFT/RTGS via [Cashfree](https://www.cashfree.com/), [Razorpay](https://razorpay.com/), or [NIUM](https://www.nium.com/). Setup ~$0–10K, take rate ~0.5–2%.
- [ ] **Canada FINTRAC MSB** — federal MSB registration, free. Plus provincial registration in Quebec (AMF). ~$30–50K/yr ongoing compliance. **(disclosed: Credible has this — own license)**
- [ ] **UAE**: ADGM FSRA licensing is hard ($1–3M, 12+ months). Most startups partner with an existing licensed entity. **(disclosed: Credible chose partner route)**
- [ ] **Singapore (MAS)**: MPI license for cross-border payments — ~6–12 months, ~$100–500K. Partner route is faster. **(disclosed: Credible partnered with MAS-regulated entity)**
- [ ] **Nigeria**: CBN International Money Transfer Operator (IMTO) license is currently restricted to large players. Partner with one (e.g., LemFi, FairMoney) or use a cross-border-licensed PSP (Paystack — Stripe-owned).

## 1E. Banking partners
- [ ] **US**: get a banking partner that supports stablecoin businesses. **Cross River Bank**, **Lead Bank**, **Customers Bank** — these are the main names. Expect onboarding ~$50–100K + monthly fees. 3–6 months due diligence. *This is hard at pre-revenue. Credible took ~12 months to get a US partner.*
- [ ] **India**: NBFC partner provides bank rails (HDFC, ICICI, Yes Bank are common).
- [ ] **Stablecoin on-ramp/off-ramp**: Circle Mint (USDC), Bridge (now Stripe), MoonPay business, BVNK. For USDC corp accounts: **Circle Mint** with ~$30K/mo minimum, no fees. *(Circle Alliance Program membership — Credible has this — gets favored terms.)*

## 1F. Compliance officer hire
- [ ] **Hire a part-time or fractional CCO/MLRO** by Month 6 of this phase. ~$80–150K for a senior person, or fractional via firms like [Rampart](https://www.rampart.ai/) or [Skadden](https://www.skadden.com/) (~$50–80K/yr). **(GATE: many banks require a named CCO before they'll go live with you.)**

**Phase 1 spend: ~$150–300K. Phase 1 team: 1 fractional CCO + advisory legal + compliance consultant.**

---

# PHASE 2 — Technical Foundation (Months 2–6, runs parallel with Phase 1)

Goal: build a working partner-portal MVP that can ingest test transactions end-to-end.

## 2A. Architecture decisions
- [ ] **Pick the "Web 2.5" architecture explicitly.** Off-chain settlement orchestration + on-chain credit pool. *Don't try to be fully on-chain — Credible's founder was direct that regulated transactions can't be.* Founder quote: *"We use DeFi only for the credit piece and the risk modeling."*
- [ ] **Backend stack**: Node.js/TypeScript (most common) or Go. Postgres for ledger. Redis for cache. Temporal/Inngest for workflow orchestration.
- [ ] **Blockchain stack**: Solana (Anchor framework, Rust) for the credit pool program. EVM (Foundry / Hardhat) optional for multichain.
- [ ] **Frontend**: Next.js + Tailwind. Looks utilitarian like Credible's — that's correct. Don't over-design.

## 2B. Custody decisions
- [ ] **Pick custody model**: Credible uses **Circle Programmable Wallets** (custodial-MPC, Circle holds the keys) — fastest path. Alternatives:
  - **Fireblocks** — institutional MPC, ~$60–180K/yr + per-transaction fees
  - **Privy server wallets** (now Stripe) — non-custodial via enclave, easy DX
  - **Turnkey** — non-custodial signing API, avoids MSB classification
- [ ] **Decision criterion**: if you intend to hold customer funds, you need custodial. If not, non-custodial is regulatory-cheaper. Credible's "we don't touch capital" framing implies they minimize custody — capital flows through bank partners, USDC float passes through Circle.

## 2C. Build the partner portal MVP
- [ ] **Auth**: Clerk / Auth0 / Supabase Auth. Multi-tenant from day one — every partner gets a project ID (this is what the user saw in the URL: `partner.credible.finance/projects/<uuid>/dashboard`).
- [ ] **Dashboard sections** (mirror Credible's): Bank Accounts, Funds, Payouts, Collections, Customers, Developer (API keys), API Docs, Settings.
- [ ] **Core data model**: Partners → Customers (their end-users) → Payouts (transactions) → BankAccounts (linked sources/destinations) → Funds (deposits/withdrawals).
- [ ] **REST API** for all partner operations. OpenAPI spec auto-generated. Sample endpoints: `POST /payouts`, `GET /payouts/{id}`, `POST /customers`, `POST /webhooks`.
- [ ] **Webhooks** for async events (payout settled, KYC complete, etc.). HMAC signing.
- [ ] **Sandbox environment** with fake bank rails and fake KYC. *Critical for partner integration.* (Credible has `sandboxpartner.credible.finance`.)
- [ ] **API documentation** (Mintlify, ReadMe, or Docusaurus).

## 2D. Build the Solana credit pool
- [ ] **Anchor program** with: deposit, withdraw, accrue-interest, request-credit, repay-credit, claim-yield. Modeled on existing lending protocols (Marginfi, Kamino).
- [ ] **LP token mint** (Credible calls it cUSDC) — 1:1 with deposited USDC initially, accrues yield.
- [ ] **Risk parameters** stored on-chain: max credit limit, interest rate model, penalty rates.
- [ ] **Smart contract audit** — mandatory before mainnet. ~$30–150K for Solana Anchor programs. Top auditors: Halborn, Kudelski, OtterSec, Trail of Bits.
- [ ] **Testnet deploy** (Solana devnet) → mainnet only after audit.

## 2E. Build risk underwriting v1 (rules-based)
- [ ] **Initial model**: rules-based scoring. Inputs: partner KYB tier, ACH return rates, transaction frequency, geographic risk, transaction size relative to history. Output: 0–100 score → credit limit + duration.
- [ ] **Don't try AI on day one.** Credible explicitly iterated: started with third-party agencies, brought it in-house, eventually moved to AI on 0G. *That's a Year-2 problem.*
- [ ] **Key insight from Credible**: short-duration credit (3–5 days, not 30–90) is what makes underwriting tractable. Founder: *"We moved away from 30-day or 90-day credit lines to 3 days or 5 days credit line for payment financing. That helped us scale up the volume pretty quickly and minimize the risk."* **Bake this into the model from day one.**

## 2F. FX rate engine
- [ ] **Spot FX feed** from a real provider: [Wise API](https://wise.com/api), [Currencylayer](https://currencylayer.com/), [Fixer.io](https://fixer.io/), or your bank partner's rate sheet. Charge a markup that's still better than Wise/Remitly retail rates.
- [ ] **Credible's edge** (founder-disclosed): they offer ~90 INR/USD when Wise/Remitly offer 85–86. That's a ~4–5% better rate to the end-user. The math only works if their wholesale FX cost is even lower (likely sub-1% spread from their FX provider). *This is the actual moat — engineer the FX cost down.*

**Phase 2 spend: ~$80–200K (engineers + audit). Phase 2 team: 2–3 engineers + 1 founder-engineer.**

---

# PHASE 3 — Credit Pool Capital (Months 4–8)

Goal: have ~$500K–$2M of USDC liquidity in the credit pool to start advancing.

- [ ] **Seed pool from founders + accelerators + first LPs.** $500K–$1M is enough to start at low partner volumes.
- [ ] **Set the LP yield**: Credible offers **16% fixed APY** on USDC/USDT. *Reverse-engineer this from your unit economics:* if you charge partners 25–30% APR-equivalent on 5-day credit, after operating costs and reserves you can pay LPs 16% — and that's a strong yield in stablecoin land. Don't promise it before you can pay it. Start at 8–10% if needed.
- [ ] **LP onboarding**:
  - Stage 1: founders + friends + 1–2 angels who'll lock capital for 90 days
  - Stage 2: stablecoin yield aggregators (DeFi protocols that route deposits) — Pendle, Kamino, Drift Institutional
  - Stage 3: family offices + crypto VCs willing to deploy treasury into yield. Credible's exact LP base isn't publicly disclosed.
- [ ] **Track LP metrics**: TVL, utilization rate, yield delivered, default rate. Publish on a Dune dashboard for transparency. **(Credible has [dune.com/credible/stats](https://dune.com/credible/stats).)**
- [ ] **Insurance / first-loss tranche** (optional but good for institutional LPs): set aside 5–10% of pool as a first-loss reserve. Or buy DeFi cover from Nexus Mutual / Sherlock. ~1–3% of insured value annually.

**Phase 3 spend: $0 in fees but $500K–$2M in pool capital (recoverable if managed well). Phase 3 team: 1 founder doing LP outreach.**

---

# PHASE 4 — First Corridor (Months 6–10)

Goal: 1 sender country ↔ 1 receiver country, end-to-end working with low test volumes.

**(GATE: don't start until Phase 1B + 1E + 2 + 3 are clear.)**

- [ ] **Pick the corridor strategically.** Credible chose **US → India** because India is the #1 inward remittance country globally and was untouched by stablecoin players. Other strong picks:
  - **US → Nigeria** (USD scarcity = high willingness to pay for USD-denominated payouts)
  - **US → Philippines** (large NRI/OFW population, OFW remittances are 9% of GDP)
  - **Canada → India** (Credible's Phase 5 — Canada has a different remittance regulator and large NRI population)
- [ ] **Test transactions $50–$500** with internal/founder accounts. Iterate the flow until KYC + funding + payout + reconciliation work end-to-end.
- [ ] **Reconciliation engine**: build an internal ledger that matches every payout to its corresponding ACH inbound and triggers credit-pool refill. Daily reconciliation reports. *This is where money actually gets lost if you screw it up.*
- [ ] **Compliance monitoring**: every transaction passes OFAC screen, KYC validity check, partner-tier limit, velocity check. Alerts to a Slack channel and CCO.
- [ ] **Run for 60 days minimum at small volume before any partner goes live.** Goal: zero defaults, zero AML escalations, sub-1-min end-to-end latency.

**Phase 4 spend: ~$10–30K in test transactions + monitoring infra. Phase 4 team: 1 backend engineer + CCO + founder.**

---

# PHASE 5 — First Partner Fintech (Months 8–12)

Goal: 1 live B2B fintech client running real production volume.

- [ ] **Outbound to existing remittance fintechs serving NRIs / migrant workers.** Targets: [Abound](https://www.joinabound.com/) (NRI), [Pexx](https://pexx.com/) (Singapore), [LemFi](https://lemfi.com/) (Africa-focused), [Sendwave](https://www.sendwave.com/), [Atlantic Money](https://atlanticmoney.com/), [Taptap Send](https://www.taptapsend.com/). *Credible landed Abound + Pexx + Borderless + WireNow in Year 1.*
- [ ] **The pitch**: "Eliminate your $X million in pre-funding capital that's locked up across corridor accounts. We advance USDC instantly; you pay us a 30bps fee + repay in 3–5 days when ACH settles. Your float comes back to your balance sheet."
- [ ] **Sales cycle: 60–120 days** from first call to production. Their compliance team will want: AML program, audit reports, banking-partner letters, sample API contracts, sandbox access.
- [ ] **Partner onboarding**: KYB, compliance review, sandbox integration, contract signature, production go-live with **low daily limits** (e.g., $50K/day initially, scaling to $500K/day after 30 days).
- [ ] **First-month metrics goal**: 100% reconciliation, zero defaults, sub-1-min latency, NPS check-in.
- [ ] **Founder-led sales** for first 5 partners. Don't hire a sales rep yet.

**Phase 5 spend: ~$5–20K in travel/conferences. Phase 5 team: 1 founder doing BD + 1 backend engineer for partner integration support.**

---

# PHASE 6 — Move Underwriting In-House (Months 10–14)

Goal: stop paying third-party credit agencies; own the risk model.

This is the iteration Credible explicitly called out. Founder: *"Initially we were too much dependent on various agencies doing the credit assessment. We decided to move that credit assessment mechanism in-house with the AI-based model, and that's when things really started speeding up."*

- [ ] **Collect data** from the first 3+ months: every partner's KYB profile, every customer's KYC, every transaction's settlement outcome, every ACH return.
- [ ] **Build feature engineering pipeline**: partner age, partner default rate, partner volume volatility, customer count, customer geography, transaction size distribution, time-of-day, KYC tier, ACH bank quality, IP/device signals.
- [ ] **Train v1 model**: gradient-boosted tree (XGBoost) for default probability, calibrated to outcomes. Don't reach for an LLM yet.
- [ ] **Shadow the rules-based system for 30 days** before letting AI override.
- [ ] **Move to AI on-chain** (Credible's stated goal on 0G when 0G mainnet ships) — *only if* there's a real reason. The compliance benefit (auditable inference) is real but the engineering cost is high. Optional Year 2.
- [ ] **Outcome target**: shrink credit duration from 30–90 days to **3–5 days**. This is the single biggest unit-economics improvement.

**Phase 6 spend: ~$30–80K (data + ML hire). Phase 6 team: +1 ML engineer.**

---

# PHASE 7 — Scale Corridors (Months 12–18)

Goal: 3–5 live corridors.

- [ ] **Corridor expansion order** (prioritize by volume × compliance ease):
  1. US → India (live)
  2. US → Nigeria (high pricing power, moderate compliance lift)
  3. Canada → India (uses existing Canadian MSB, NRI corridor)
  4. US → Philippines (large OFW market, more competition)
  5. US → Brazil (large but Brazilian regulators are getting stricter; do later)
  6. India → China trade finance (Credible's Phase 9 expansion — partner-routed via Singapore MAS entity)
- [ ] **Each new corridor needs**: receiver-side bank/PSP partner + local-jurisdiction compliance review + AML program update + reconciliation tooling + corridor-specific KYC adjustments.
- [ ] **Time per corridor**: 3–4 months from kickoff to production.
- [ ] **Hire by corridor**: ideally a part-time local liaison who handles the bank/PSP relationship and compliance translation. ~$30–80K/yr per region.

**Phase 7 spend: ~$50–150K per corridor (legal + integration). Phase 7 team: +regional ops, +integration engineers.**

---

# PHASE 8 — Scale to 5+ Partners (Months 12–24)

Goal: $20M+/month volume, multiple live partners, cash-flow positive.

- [ ] **Outbound at scale** — switch from founder-led BD to a hire. ~$100–150K base + commission.
- [ ] **Partner retention motion**: monthly business reviews, quarterly limit-increase reviews, dedicated Slack channel per partner.
- [ ] **Hackathons + accelerators for visibility** — Credible's exact playbook:
  - **Outlier Ventures RWA Base Camp** (~$100K pre-seed, ~10 weeks) — apply Year 1
  - **OnePiece Labs × 0G** (~$0–250K, AI/credit-model fit) — Year 1–2
  - **Colosseum Accelerator** (Solana, ~$250K SAFE, 11/1,600+ acceptance rate) — apply once you have traction
  - **Solana Cypherpunk Hackathon** ($25K-$200K prizes, distribution boost) — annual, Q4
  - **Solana Summit hackathons** — regional
- [ ] **Strategic partnerships**: Circle Alliance Program (free, gets you USDC + Circle co-marketing), Solana Foundation, Plume Network (RWA partner), Stellar (grants — Credible got $150K).
- [ ] **Hit $20M/month volume** to be cash-flow positive (Credible's milestone).

**Phase 8 spend: ~$200–400K (sales hire + marketing + travel). Phase 8 team: +sales, +CS, +marketing.**

---

# PHASE 9 — Capital Strategy (Months 18–24)

By this point you have a choice — and Credible's example suggests **debt > equity**.

- [ ] **Option A: Raise debt to scale credit pool.** Asset-backed credit facility from a fintech-friendly lender (Cross River, Pollen Street, Victory Park). Credit-pool capital becomes the "asset" — borrow against it at 10–14% APR, lend at 25–30% APR-equivalent. Net spread funds operations. *Credible's stated preference.*
- [ ] **Option B: Raise equity** — Series A pricing for fintech with ~$25M ARR equivalent typically: $150–300M valuation, $20–40M raise. Lead investors for stablecoin payments: Ribbit, Bain, NYCA, Lightspeed Faction, Paradigm, Coinbase Ventures, Circle Ventures.
- [ ] **Option C (crypto-native): launch token** — CRED governance token, dual-staking with USDC, optional airdrop to LPs and partners. *Use only if you actually need the regulatory/distribution lever a token gives you. Credible has the token narrative on roadmap but hasn't launched, which is a healthy signal — they're not capital-constrained enough to need it.*
- [ ] **Option D: OracleAI-style node-license sale** — sell node licenses for ~$30M (Credible's claim). Pure DePIN-economy fundraising. Optional, doesn't gate operations.

---

# PHASE 10 — Consumer Layer (Months 18–30)

The B2B business is the cash engine. The consumer credit-card layer is the moonshot.

- [ ] **Credible+ card prerequisites**:
  - **Card-issuing bank partner (BIN sponsor)**: Marqeta + Sutton Bank / Lithic + Pathward / Stripe Issuing. Setup ~$50–200K.
  - **PCI-DSS Level 1 compliance** for any card-data handling. ~$30–100K + ongoing.
  - **State-level lending licenses** in every US state where you'll issue credit. Or partner with a chartered lender (Cross River, Lead Bank).
- [ ] **Credible Score (consumer credit scoring on-chain activity)**:
  - Inputs: wallet age, on-chain stablecoin income, NFT/token holdings, on-chain debt history, KYC tier, off-chain bank-link data.
  - Output: 0–100 score → credit limit, APR tier.
  - **The pitch**: "Crypto-native users have no FICO. We score them on what they actually hold and earn." Solid pitch *only if* you can actually distribute it. Credible has 370K waitlist (as of Oct 2025) — that's the distribution.
- [ ] **DePIN BNPL partnerships** (Credible's playbook with Aethir): tokenize the user's DePIN node earnings as collateral, advance them BNPL credit against expected future yield. Aethir partnership was the first of these.
- [ ] **Card economics**: interchange (~1.5–2.5% on each swipe) + interest on revolving balances + late fees. Standard credit-card economics. Not a moat unless distribution is.

**Phase 10 spend: ~$1–3M in setup + ongoing. Phase 10 team: +product + card ops + risk + customer support team.**

---

# THROUGHOUT — Marketing, Distribution, Community

These run continuously from Phase 1 onward.

## Founder presence
- [ ] **Twitter/X profile** for the CEO. Daily posts on the company, the corridor problem, regulatory updates. Follow + engage with: stablecoin builder community, fintech VCs, regulators (FinCEN, RBI public accounts). *Shrikant ([@skantbhalerao](https://x.com/skantbhalerao)) does exactly this.*
- [ ] **LinkedIn for B2B partner discovery** — most fintech BD comes through LinkedIn warm intros, not cold email.
- [ ] **Podcast tour**: target one podcast per quarter. Bankless, Empire, Lightspeed, Validated, regional fintech pods. *Credible hasn't done this yet — opportunity.*
- [ ] **Conference circuit**: Solana Breakpoint (annual), Money 20/20, Singapore Token2049, Consensus, Stellar Meridian, Token2049 Dubai. ~$5–15K per conference + travel. **Hackathons at the event are how you get visibility cheap.**

## Content
- [ ] **Monthly insights blog post** (Credible publishes one — see [blog.credible.finance](https://blog.credible.finance)). Topics: corridor unlocks, license updates, volume milestones, partnership announcements.
- [ ] **Open Dune dashboard** for transparency on volume, default rate, LP yields. ([dune.com/credible/stats](https://dune.com/credible/stats))
- [ ] **Technical content** (eventually): "How we achieve T+0 settlement," "Underwriting at 5-day credit duration," "Stablecoin Nostro architecture." Founder-authored, distributed via Mirror / Substack / company blog.

## Community
- [ ] **Telegram + Discord** from day one — partner support, LP coordination, brand awareness.
- [ ] **Twitter spaces** monthly with one of the partners — co-marketing.
- [ ] **Hackathon judge / mentor** roles in Solana / Plume / 0G ecosystems. Free, builds relationships.

## PR
- [ ] **Press strategy**: target CoinDesk, The Block, PYMNTS, Cointelegraph, Inc42 (India), Rest of World (emerging markets). Use partner announcements as news pegs (e.g., the Aethir × Credible launch was good for ~5 outlets).
- [ ] **Volume / ARR milestones** as press moments: "$60M cumulative", "$100M month", "10,000 active partners," etc.

---

# Hiring trajectory

| Phase | Months | Cumulative team size | Key hires |
|---|---|---|---|
| 0 | 0–1 | 2–3 | Co-founders |
| 1 | 1–9 | 4–6 | +Backend eng, +Compliance officer (fractional) |
| 2 | 2–6 | 6–8 | +Solana eng, +Frontend eng |
| 3–4 | 4–10 | 7–9 | +DevOps eng |
| 5 | 8–12 | 8–10 | +BD/Partner success |
| 6 | 10–14 | 9–11 | +ML eng |
| 7 | 12–18 | 11–14 | +Regional ops (×2) |
| 8 | 12–24 | 14–18 | +Sales rep, +Customer success, +Marketing |
| 9 | 18–24 | 16–22 | +Finance/CFO, +Treasury |
| 10 | 18–30 | 22–35+ | +Product (consumer), +Card ops, +Risk team |

**Year 1 target team: ~10 people. Year 2: ~20. Year 3: ~35–50.**

Salaries (rough, India-heavy team like Credible's):
- Engineers: $40–80K (India), $120–200K (US)
- Compliance officer (senior, US): $120–200K
- BD/Sales: $90–150K base + commission
- ML engineer: $80–140K
- Founder: sub-market or $0 until cash-flow positive

---

# Cost summary (Year 1 only)

| Category | Cost |
|---|---|
| Incorporation + legal entities | $5–15K |
| Compliance counsel + AML program writing | $80–150K |
| KYC + on-chain analytics vendors | $40–100K |
| Smart contract audit | $30–150K |
| Banking partner setup + compliance | $50–150K |
| Engineering team (3–4 FTEs, India-heavy) | $150–300K |
| Compliance officer (fractional or senior) | $80–150K |
| Travel + conferences + hackathons | $30–60K |
| Tooling, infra, SaaS | $30–60K |
| Office / coworking / misc | $20–40K |
| Marketing / PR / content | $20–50K |
| **Subtotal Year 1 operating cash** | **$535K – $1.225M** |
| Credit pool capital seed | $500K – $2M |
| **Total Year 1 cash needed** | **$1M – $3.2M** |

For comparison: **Credible raised ~$100K from Outlier + accelerator allocations + $25K hackathon prize + $150K Stellar grant**. They got to cash-flow positive on **arguably under $1M of equity capital** (plus credit pool sources we don't fully know). That's exceptional — most fintechs at this stage would have raised $10–30M.

---

# Critical-path summary (the things you cannot skip)

If you do everything else and miss these, you don't have a business:

1. **A specific corridor with a specific incumbent pain.** Not "stablecoin payments" — "US→India NRI remittances stuck at 85 INR/USD with 48-hour settlement, we offer 90 INR/USD with sub-minute settlement."
2. **At least one own license** in either sender or receiver jurisdiction. Credible's Canada MSB + India lending license is what bank partners trust. Pure-partner-only is too easy to revoke. **(GATE)**
3. **A real banking partner that has done due diligence on you.** Sandbox doesn't count. **(GATE for production volume)**
4. **A working reconciliation system.** If you can't match payouts to ACH inbounds within hours, you don't have a business — you have an unbounded liability.
5. **Short-duration credit (3–5 days)** as the underwriting model from day one. The 30–90-day model doesn't survive rate-cycle changes or partner default events.
6. **First paying B2B partner, signed contract, monthly volume.** Hackathon prizes and accelerator stipends don't count.
7. **A founder with operational fintech-rail experience** in at least one of your corridors. Credible's Shrikant is on the board of an RBI NBFC. Without that level of insider context, partner discovery and license negotiation take 2–3× longer.
8. **Cash-flow positivity before raising at scale.** Credible explicitly chose debt over equity once they hit $20M/month. Equity at the wrong time forces you to over-promise on growth instead of optimize on margin.

---

# What you'd skip if you were doing this in 2026 (vs. 2024 when Credible started)

The agent-payments + stablecoin space has shifted. Things that were costly in 2024 are now cheaper or commoditized:

- **Stablecoin custody**: Privy/Crossmint/Turnkey now offer this as a managed service. Don't build from scratch.
- **x402 payment protocol**: standardized HTTP 402 + EIP-3009 means you don't need to build a custom payment-request format. *(Whether x402 is right for the corridor business is a separate question — likely overkill for this use case.)*
- **ERC-8004 agent identity**: live since Jan 2026. If you're going to extend to AI-agent customers later, build with this in mind.
- **GENIUS Act compliance**: PPSI rules from July 18, 2026. USDC issuance rails are now federally regulated — your stablecoin choice is almost forced (USDC).
- **Visa/Mastercard agent attestation**: pre-built compliance for card-based agent payments. If your roadmap touches agent commerce, partner here instead of building.

---

# Optional: extend to AI-agent payments (the natural Year 2–3 expansion)

The current Credible product serves human-operated fintechs serving human end-users. The natural extension — and the unsolved problem from `../../markets/agent_payments/compliance.md` — is **autonomous AI agents needing the same primitive: a USDC working-capital line + cross-border payout rails**.

Concrete steps to add this:
- [ ] Build x402 facilitator integration so agents can pay through Credible's USDC float
- [ ] Issue ERC-8004 attestations for agents that have been KYA'd through Credible
- [ ] Open the credit-line product to agent operators with a verified human principal
- [ ] Build the dispute / chargeback rail that's the open compliance gap

This is the bridge between Credible's current business and the AI-agent-payments space the user is researching. Worth its own deep dive if/when relevant.
