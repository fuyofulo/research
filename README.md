# AI × Crypto Research

just researching so that I understand the ai and crypto space deeper.

---

## Folder structure

```
research/
├── markets/                                  → Market & category research
│   ├── ai_crypto_landscape.md
│   ├── agent_payments/
│   │   ├── solutions.md
│   │   └── compliance.md
│   └── payfi/
│       └── liquidity_models.md
├── companies/                                → Per-company deep dives
│   ├── credible-finance/
│   │   ├── deep_dive.md
│   │   ├── how_to_build.md
│   │   ├── liquidity_architecture.md
│   │   ├── architecture.md
│   │   ├── happypath.png                     (user's hand-drawn flow)
│   │   └── transcripts/                      → Founder interview transcripts
│   ├── blockworks/
│   │   ├── deep_dive.md
│   │   └── transcripts/
│   ├── frames-ag/
│   │   ├── how_it_works.md
│   │   └── deep_dive.md
│   └── bridge/
│       ├── deep_dive.md
│       ├── architecture.md
│       ├── use_cases_and_examples.md
│       ├── developer_experience.md
│       ├── product_evolution.md
│       └── transcripts/
```

**Conventions:**
- `markets/` for cross-cutting research on a category, vertical, or problem space
- `companies/` for deep dives on individual companies; transcripts kept inside the company folder
- New verticals get their own subfolder under `markets/` (e.g., `markets/decentralized_training/`)
- New companies get a kebab-case subfolder under `companies/`

---

## Index

### Markets

| File | Topic | Date |
|------|-------|------|
| [markets/ai_crypto_landscape.md](./markets/ai_crypto_landscape.md) | Top-down landscape: 15 categories, money flows, real vs. narrative, emerging themes | 2026-04-26 |
| [markets/agent_payments/solutions.md](./markets/agent_payments/solutions.md) | x402, AP2, Stripe, Skyfire, Crossmint, Privy, Catena, Visa/MC and more — tech, teams, funding, traction. Includes "what surprised me" + dominant stack patterns. | 2026-04-26 |
| [markets/agent_payments/compliance.md](./markets/agent_payments/compliance.md) | US (FinCEN, MSB, OFAC, GENIUS Act), EU (MiCA, PSD2/3, AI Act, GDPR), other jurisdictions. The 5 sharpest unsolved compliance problems where startups can build. | 2026-04-26 |
| [markets/payfi/liquidity_models.md](./markets/payfi/liquidity_models.md) | **Liquidity design space for cross-border payment orchestrators.** 9 capital-sourcing mechanisms (bank warehouses, CeFi prime brokers, DeFi over-coll, open pools, RWA treasury, tranching, etc.) + 5 capital-efficiency levers (cross-corridor netting, RTP/FedNow, multi-rail) + 5 risk-transfer mechanisms. 3 alternative architectures that could outperform Credible. | 2026-05-01 |
| [markets/payfi/us_payout_rails.md](./markets/payfi/us_payout_rails.md) | **The honest mechanics of T+0 to US bank accounts.** Five US payment rails (ACH, Same-Day ACH, Wire, RTP, FedNow, Visa Direct) — speed, cost, coverage. Off-ramp partners (Bridge, Brale, Circle Mint). Why "T+0" claims hide bank-coverage gating (RTP/FedNow at ~67% in 2026). End-to-end flow diagrams for forward + reverse corridors. The reverse corridor (INR→USD) is structurally CHEAPER to build because the pain is rail-routing, not funding. | 2026-05-03 |

### Companies

| File | Topic | Date |
|------|-------|------|
| [companies/credible-finance/deep_dive.md](./companies/credible-finance/deep_dive.md) | B2B stablecoin payment-orchestrator. Founders, funding, customers, tech stack, business model, compliance. Includes 3 founder transcripts. **They're cash-flow positive.** *(Note: see `liquidity_architecture.md` for major architecture corrections.)* | 2026-04-27 |
| [companies/credible-finance/how_to_build.md](./companies/credible-finance/how_to_build.md) | Linear playbook to build Credible from scratch — phases, dependencies, vendors, costs, hiring, marketing. Year-1 cash needed: ~$1–3.2M. *(Note: see `liquidity_architecture.md` for phase-level corrections.)* | 2026-04-29 |
| [companies/credible-finance/liquidity_architecture.md](./companies/credible-finance/liquidity_architecture.md) | **Liquidity & tech deep dive.** PayFi Vault is on **Hedera via Byzanlink** (not Solana), ERC-4626/7540, ~16% est APY, ~7-day notice redemption. Multi-chain: Hedera (live), Solana (Aethir), Plume (roadmap). Co-lending model with named TradFi partners (Mount Fuji, etc.). Sanctum LST-backed credit card. Founder's **real product is Credible Score, not payments**. Includes 5th transcript (Sanctum fireside). | 2026-04-30 |
| [companies/credible-finance/architecture.md](./companies/credible-finance/architecture.md) | **Complete architecture in Mermaid diagrams.** All 6 product flows mapped: B2B remittance, LP capital lifecycle, co-lending credit, Sanctum LST cards, Aethir DePIN cards, Credible Score pipeline. Plus cross-chain split, compliance stack, end-to-end transaction trace, and "the company in one frame" diagram. Confidence-labeled (✅/🟡/🔴). | 2026-05-01 |
| [companies/credible-finance/operational_partnerships.md](./companies/credible-finance/operational_partnerships.md) | **The on-chain ground truth.** Direct Hedera mirror-node pull: real TVL is **$1.12M** (not multi-million); 99.99% of LP supply is one wallet created 124 min after deploy (Credible-controlled, not external LP); only 5 retail wallets total. **Named NBFI partners: Loap (India), Chorus Finance (Africa, $15M deployed)** — Credible is a credit-orchestration layer ON TOP of partner NBFIs, not a direct PSP. Six-month revenue: **$70K**. 150K Nigerian users mostly airdrop-farmed (true active 30-50K). Abound legal disclosures don't name Credible. Updates many prior files. | 2026-05-03 |
| [companies/credible-finance/may_2026_update.md](./companies/credible-finance/may_2026_update.md) | **Colosseum Demo Day pitch (May 2026) update.** Founder-stated: **$350M cumulative volume in 5 months**, **$210K monthly revenue (10% MoM growth)**, **15bps take rate**, **$3B projected annual volume**, **$2.5M ARR run-rate**. Currently live in **US-India corridor ONLY** (correcting our prior multi-corridor framing). Canadian MSB is **applied-for, not owned**. **CRED token launching on MetaDAO** (Solana-native futarchy platform — NOT an Ethereum L2) as permissioned project. New positioning: "first payment gateway built on stablecoins" (Stripe/Adyen comp, $20T TAM). ~$1M raised in investments+grants over past year. Includes founder transcript. | 2026-05-03 |
| [companies/credible-finance/numbers.md](./companies/credible-finance/numbers.md) | **Every number we've collected, in one place.** TPV, revenue, on-chain TVL, APY, users, funding, team, partnerships, licenses, defaults, FX spread, Sanctum/Aethir card mechanics, MetaDAO context. Each number tagged ✅ verified / 🟡 founder-attested / 🔴 marketing claim / ⚙️ derived. Includes contradiction analysis ("the cumulative volume claim went DOWN $50M between March and May") and "the two numbers that matter most" verdict. | 2026-05-03 |
| [companies/credible-finance/website_faq_analysis.md](./companies/credible-finance/website_faq_analysis.md) | **Analysis of credible.finance FAQ.** Three new findings: (1) **Merchant of Record (MoR) model** claim — most likely "partner-MoR" with FI as legal counterparty, exploitable as a competitor wedge; (2) **EUR collection accounts** first mentioned — bidirectional flows confirmed (collect + pay, not just outbound remittance); (3) **Solana/blockchain branding stripped from website** — deliberate enterprise dual-positioning vs the crypto-audience pitches. Recommends Indian SaaS exporters using EUR/USD collection accounts as the better wedge for a competitor (vs NRI remittance). | 2026-05-03 |
| [companies/blockworks/deep_dive.md](./companies/blockworks/deep_dive.md) | Crypto media/research/events. Founders Yanowitz + Ippolito. Bootstrapped 6yr → $12M Series A 2023 → ~$30M revenue 2025. **Killed news division Oct 2025**, pivoted to data + Lightspeed IR. Includes 3 founder transcripts. | 2026-04-29 |
| [companies/frames-ag/how_it_works.md](./companies/frames-ag/how_it_works.md) | **Server wallets for AI agents** with x402 + MPP payment signing, email-OTP onboarding, multi-chain (EVM 9 networks + Solana + Tempo), policy engine, referral/airdrop tier system. Distribution via "skill files" agents read at runtime. Mermaid architecture diagrams. | 2026-05-02 |
| [companies/frames-ag/deep_dive.md](./companies/frames-ag/deep_dive.md) | **Company deep dive.** Founder: Luís Freitas (ex-Bitte CTO, Lisbon). 4-month-old, ~2-person team. **Custody is actually Privy underneath** (confirmed via API). **2,160 wallets, $0 real 24h volume** (all internal promo). No funding announced. Not in x402 ecosystem. Moltbook is Meta-owned — frames.ag is a skill in their registry. **Distribution wedge real, infra is borrowed.** | 2026-05-02 |
| [companies/bridge/deep_dive.md](./companies/bridge/deep_dive.md) | **Bridge — acquired by Stripe for $1.1B (Oct 2024).** Founders Zach Abrams + Sean Yu (ex-Square Evenly, ex-Coinbase USDC). $58M raised pre-acquisition. **Volume 4×ed in 2025 → ~$20-25B annualized.** Post-acquisition: USDB stablecoin + Stablecoin Financial Accounts (101 countries) + Open Issuance (Phantom CASH, MetaMask mUSD, Hyperliquid USDH, Sui USDsui) + **OCC national trust bank charter (Feb 2026)** + Visa cards expanding to 100+ countries. **NEW: Mastercard acquired BVNK for $1.8B March 2026** — eclipses Bridge deal but validates the floor. Bridge is now the stablecoin layer for the entire Stripe agentic-commerce stack (Privy + Bridge + Tempo + ACP/MPP). Includes 3 founder transcripts. | 2026-05-03 |
| [companies/bridge/architecture.md](./companies/bridge/architecture.md) | **Bridge complete technical architecture.** How Bridge actually moves money — full transaction flows (US→Nigeria, MX→EU) with API mechanics, Mermaid diagrams, every endpoint. **Critical insight: Bridge has NO LP pool** (unlike Credible). Liquidity = operational float per chain + JIT USDB mint/burn + Stripe balance-sheet backstop. **Bridge ends at "USDC to wallet" for emerging markets** — local exchanges (Yellow Card, Bitso, etc.) handle the actual fiat conversion. Lead Bank + Modulr named partners; everyone else opaque. 15-chain architecture, Tron is the unsung hero. Open Issuance + card mechanics + Stablecoin Financial Accounts + OCC trust charter implications. Sharpened "build a better Bridge" angles. | 2026-05-03 |
| [companies/bridge/use_cases_and_examples.md](./companies/bridge/use_cases_and_examples.md) | **Concrete customer walkthroughs (16 named).** End-user flow for each, with money path, Bridge products used, costs. Tier 1: DolarApp/ARQ ($3 flat US→MX), Felix Pago (**$2.99/tx, 40% reduction**), Phantom CASH (Visa swipe burns CASH on-chain), SpaceX Starlink emerging-market collect, Airtm Stellar payouts ($1.2B 2024 vol), Cenoa (**0.99% total** Turkey freelancer fee), Coinbase (USDT-Tron↔USDC-Base routing), MetaMask mUSD (M0 protocol), Hyperliquid USDH, Sui USDsui. Tier 2: DoorDash on Tempo, Payoneer Q2'26, Slash USDSL ($1B annualized vol), Dakota DKUSD (**shipped in <1 day**, 55% AUM migrated). Tier 3 inferred: Nigerian YouTube/ChatGPT subscription via Stripe-Bridge stablecoin checkout. **Open Issuance interop = 1:1 atomic swap** between CASH↔mUSD↔USDsui↔USDH↔DKUSD. Strike–Bridge integration debunked. | 2026-05-03 |
| [companies/bridge/developer_experience.md](./companies/bridge/developer_experience.md) | **Bridge DX, pricing, and the API surface.** KYB same-business-day. Sandbox is hobbled: webhooks don't fire, Wallets/Issuance only work in production, Plaid disabled. **No official SDKs** in any language; only one community MCP server. **Pricing has no public rate card** — only Bridge's legal Fee Disclosure mentions "≤1% FX spread." Stripe Stablecoin Financial Accounts charges flat **1.5% per stablecoin payment**. Slash built MVP in **2 weeks**, hit $1B annualized; Cenoa under 1 month. 10 documented gotchas (memo-required Stellar/Tron, minimums-after-dev-fees, idempotency 24h window with 422 after expiry, Prefunded Accounts deprecated Mar 24 2026). Verbatim Transfer curl + endpoint inventory. **Verdict: Bridge is the least price-transparent stablecoin-infra vendor — Brale/Crossmint/Routefusion all publish more.** | 2026-05-03 |
| [companies/bridge/product_evolution.md](./companies/bridge/product_evolution.md) | **Quarter-by-quarter changelog 2022→May 2026.** Founded March 2022, **first idea was bank-to-NFT acquisition** (pivoted in May 2022). Two-pillar Orchestration+Issuance pitch crystallized by March 2023 (Wayback). $40M Series A March 2024 at ~$200M (5.5× to Stripe price). Stripe deal Feb 4 2025. Then in 13 months: USDB May 2025, Tron in-house infra May 2025, Visa cards Apr 2025, Privy June 2025 (kept independent), Open Issuance Sept 2025 with Phantom CASH headline, OCC charter applied Oct 2025, Tempo announced Sept 2025, **OCC conditional approval Feb 12, 2026**, Tempo GA on Bridge Mar 27 2026. Sessions 2026: Machine Payments Protocol + Universal Commerce Protocol w/ Google. **Chain order**: ETH → Polygon → Solana → Stellar → Base → Arbitrum → OP → Avalanche → Tron → Plasma → Celo → Tempo → HyperEVM → Sui → Aptos. **Fiat rail order**: USD ACH/Wire → SEPA → MXN SPEI (Apr 25) → BRL Pix (Nov 25) → GBP FPS (Mar 26). Strategic-decision analysis (why USDB before Open Issuance, why OCC charter when, why Privy stays independent). | 2026-05-03 |

---

## Key takeaways so far

**AI × crypto landscape (markets/ai_crypto_landscape.md):**
- ~919 tracked AI-crypto projects, ~$22-26B combined mcap
- ~40% of crypto VC went to AI-adjacent in 2025 (vs 18% in 2024)
- Real plumbing: DePIN GPU, agent payments, prediction markets, decentralized training
- Mostly narrative: AI agent launchpads (Virtuals, ai16z deflated), tokenized AI agents, most ZKML
- Defensible thesis: "crypto as the rails for autonomous agent commerce" (x402 + ERC-8004 + DePIN compute + verifiable inference)

**Agent payments reality check (markets/agent_payments/):**
- x402 has $50M cumulative volume but **real organic daily volume is ~$14K** — ~50% of activity is gamed; daily txns down 92% from Dec '25 peak
- **Stripe quietly owns the entire stack** post-Privy acquisition: identity (Privy) + spend (SPT/ACP/MPP) + settlement (Stripe + Bridge) + reporting
- **Card networks are positioned to win consumer agentic commerce** — they own dispute/chargeback infra that crypto natively lacks
- **Subscription delegation is the boring winner** — virtual cards + spending limits, less hyped than x402 but far more real value movement
- **Compliance is the wall:** banks can't open accounts for AI agents (KYC is for humans), PSD2 SCA breaks autonomous payments in EU, no FinCEN guidance exists for agent-specific SAR typologies, no chargeback rail for stablecoin agent payments
- **Catena Labs is the dark horse** — Sean Neville (USDC inventor) building a regulated AI-native FI with $18M from a16z crypto + Tom Brady + Balaji + Sam Palmisano

**Credible Finance — quick read (companies/credible-finance/):**
- Real B2B stablecoin payment-orchestrator, NOT a Solana protocol despite branding ("Web 2.5" — DeFi for credit pool only, off-chain for settlements)
- Founder Shrikant Bhalerao: 14 years fintech, healthcare-financing exit in 2023, RBI NBFC director — senior operator
- **Cash-flow positive** at ~$20M/month volume; $60M+ processed in 11 months with **zero defaults**
- 370K users (150K+ from Nigeria), 5+ B2B fintech clients (Abound, Pexx, Borderless, WireNow)
- Licenses: own MSB Canada + own lending+exchange India + FinCEN-registered US + UAE/SG partners
- **Real moat = ~4–5% better FX vs Wise/Remitly** (85 rupees vs 90 rupees per USD), enabled by USDC credit pool eliminating ACH pre-funding
- 16% fixed APY for USDC/USDT depositors funding the credit pool — rare "real-yield" stablecoin source
- Biggest gap: no public GitHub / Solana program IDs; OracleAI 100K-node narrative is fundraising scaffolding

**Blockworks — quick read (companies/blockworks/):**
- Crypto media + research + events business; founded 2017–18 by Yanowitz + Ippolito
- **Bootstrapped 6 years** before single $12M Series A at $135M post (10T + Framework + Santiago Santos, May 2023)
- 2025 revenue projected **>$30M**, profitable every year but one, **$0 marketing spend** ("reverse CAC")
- **Shut down news division Oct 29, 2025** — pivoted hard to data + distribution
- Yanowitz pre-Blockworks at **Sisense** ($300M data analytics) — the data pivot is *founder going home*
- Permissionless 2023 alone did >$10M revenue
- New flagship product: **Lightspeed IR** (Dec 2025, with Solana Foundation) — institutional investor relations B2B SaaS
- Origin curiosity: Yanowitz had a 4,600-person multi-level-marketing energy-drink downline at age 19. That's where his distribution muscles came from.

---

## Open threads / next steps

### Already-identified problem areas worth deeper dives
- [ ] **Off-chain dispute / chargeback rail for stablecoin agent payments** (compliance gap #3 — biggest enterprise blocker)
- [ ] **Agent-aware AML / SAR tooling** (compliance gap #4 — first mover with FinCEN-blessed typology wins)
- [ ] **Tax / reporting layer for machine-to-machine flows** ("Stripe Tax for agent payments")
- [ ] **Programmable spending controls as regulator-blessed standard** (PCI-equivalent for agent payments)
- [ ] **Agent-identity-to-regulated-entity attestation** (KYA-as-a-service, MSB+CASP licensed)

### Other AI × crypto threads from market map
- [ ] Bottom-up developer pain mining (Reddit r/LocalLLaMA, r/AI_Agents, HN, GitHub issues on agent frameworks)
- [ ] Decentralized training economics — does it work without subsidies? (Pluralis, Prime Intellect, Nous, Gensyn)
- [ ] TEE-based confidential AI as the practical alternative to ZKML (Phala, Marlin, Nillion)
- [ ] AI-settled markets / information finance (Gensyn Delphi)
- [ ] Rights-cleared training data rails (Story + OpenLedger; regulatory tailwind)
- [ ] DePIN GPU enterprise overflow inflection (Aethir, Render, Akash, io.net)

### Companies to research (queue)
- _add as encountered_

### Tools / setup
- [x] Feynman skills installed (`/feynman-deepresearch`, `/feynman-lit`, `/feynman-compare`, etc.)
- [x] last30days configured (SCRAPECREATORS_API_KEY, 100 free credits — conserve)
- [ ] Optional: install `alpha` CLI for full alphaXiv paper search via Feynman

---

## File conventions

- Filenames are content-descriptive, kebab- or snake-case, no numeric prefixes (folder structure replaces chronology)
- Each `.md` is dated and self-contained — can be read standalone
- Sources linked inline; full source list at bottom of each file
- Key takeaways from each file rolled up in this README so the index gives a fast intuition refresh
- Founder/insider video transcripts saved as `.txt` next to the deep dive that uses them
