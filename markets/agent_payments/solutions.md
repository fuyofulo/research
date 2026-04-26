# Agent Payments — Solutions Deep Dive (April 2026)

> Companion to `../ai_crypto_landscape.md`. Goes one level below the market map: actual mechanics of every major solution, who the teams and money are, what's working, what's broken, who is making real money.
> **Date:** 2026-04-26
> **Source:** Deep-research agent pass with WebSearch + WebFetch

---

## Comparison table — the full agent-payments matrix

| Solution | Controller | Primitive | Settlement rail | Identity model | Wallet model | Live $ scale (Apr 2026) | Backers / funding |
|---|---|---|---|---|---|---|---|
| **x402** | x402 Foundation (Linux Foundation), incubated by Coinbase + Cloudflare | HTTP 402 + signed payment header (EIP-3009) | USDC on Base (~85%), Polygon, Solana, Arbitrum, Stellar, World | None native; pairs with ERC-8004 / KYA / World ID | Bring-your-own (Privy, Crossmint, CDP, Circle, smart wallets) | ~$50M cumulative, ~$28K/day in Feb '26 (Artemis), ~50–60% "gamed" | Coinbase, Cloudflare, Stripe, AWS, Google, Visa, Mastercard, Circle, Solana Foundation |
| **Google AP2** | Google + 60+ partners | Cryptographically-signed Intent & Cart "Mandates" (VDCs) | Card networks first (V0.1), bank/wallet later, x402 as crypto extension | Mandate signature = user device key | Wallet-agnostic; ties to Google Pay first | No public TPV | Google, Amex, Mastercard, PayPal, Adyen, Etsy, Salesforce, Coinbase, Mysten, Worldpay |
| **Stripe ACP** ("Agentic Commerce Suite") | Stripe + OpenAI | Shared Payment Tokens (SPT) — agent uses buyer's tokenized credentials | Card / Stripe-supported rails (incl. SPT bridge to Visa/MC, BNPL) | None native; merchant-side | Buyer's existing payment method, vaulted | Live in ChatGPT (Etsy, Shopify, URBN, Coach, etc.); merchant-funnel scale unclear | Stripe (private), OpenAI partnership |
| **Stripe MPP** ("Machine Payments Protocol") | Stripe (March '26) | Session-based pre-authorized streaming micropayments across rails | Tempo chain (stablecoin), Stripe fiat, Visa cards, Bitcoin via Lightspark | Session token | Stripe-managed | Brand-new (March 18, 2026 launch) | Stripe |
| **Skyfire (KYAPay)** | Skyfire (corp) | Closed network — agents prefund USDC wallets, "Know-Your-Agent" credentials | USDC, custodial deposits/withdrawals fiat | KYA = agent identity layer (~70% of internet anti-bot coverage) | Custodial Skyfire wallet per agent | Not disclosed; "thousands" beta agents | $9.5M (Neuberger Berman, Arrington, Coinbase Ventures, a16z CSX) |
| **Nevermined** | Nevermined Foundation (Switzerland) | Per-request billing + payment multiplexer; bridges agents → Stripe/Braintree/Cybersource and x402 | Crypto + fiat via existing PSPs; integrates Visa Intelligent Commerce | Wallet/agent-keyed | Their own + plug into others | Not disclosed; $7M total raised | $4M Jan '25 led by Generative Ventures (Polymorphic, NEAR, Halo, Arca, founders of Olas/Naptha/Gensyn) |
| **Coinbase AgentKit + Agentic Wallets** | Coinbase | TEE-backed non-custodial agent wallet + onchain action library | USDC on Base primarily | Pairs with x402 / World ID | TEE-protected, key-policied | Embedded in CDP usage; not separately reported | Coinbase corporate |
| **Privy (now Stripe)** | Stripe (acquired June 2025) | Server wallets w/ enclave-signed transactions and policy guardrails | Any EVM/Solana, paired with x402 → Stripe merchant balance | None — relies on Stripe identity / agent dev | Embedded MPC/enclave non-custodial | 75M+ accounts, billions in cumulative volume across all uses | Acquired by Stripe at >$230M valuation; ex-investors Sequoia, Paradigm, Founders Fund |
| **Crossmint** | Crossmint Inc. (Miami) | Wallets + virtual cards + onramps as a unified "agent financial identity" API; multi-protocol (x402, ACP, AP2, MPP) | Stablecoins + cards (Wirex integration) | Delegation from human user | MPC + smart wallet, plus virtual cards | 40K+ companies; subscription rev +1,100% YoY; GOAT SDK 150K npm dl in 2 months | $23.6M Series A March 2025 (Ribbit, Franklin Templeton, NYCA, First Round, Lightspeed Faction) |
| **Lightspark + Spark** | Lightspark (David Marcus, ex-Meta/Libra) | UMA addresses + Bitcoin Lightning settlement; Spark = L2 for stablecoin-on-Bitcoin | BTC, USDT on Spark, fiat via Cross River | UMA usernames | SDKs for wallets; non-custodial via Spark | Powers Tether WDK / QVAC AI agents; specific TPV not public | Paradigm, a16z, others; acquired by/partnered Solana Dev Platform March '26 |
| **Catena Labs (Agent Commerce Kit)** | Catena Labs / Sean Neville (ex-Circle, USDC inventor) | ACK-ID (W3C DIDs/VCs) + ACK-Pay (cryptographic receipts across rails) | Multi-rail (cards, banks, blockchain) | DID-based, with org ownership chain | Their own AI-native FI (planned regulated) | No public usage; pre-launch FI | $18M seed (a16z crypto, Breyer, Circle Ventures, Coinbase Ventures, CoinFund, Pillar, Balaji, Tom Brady, Sam Palmisano) |
| **Visa Intelligent Commerce / "Connect"** | Visa | Card-rail tokenization + spend controls + agent attestation; supports TAP, MPP, ACP, UCP | Visa rails | Trusted Agent Protocol (TAP) | None — uses card-on-file | Hundreds of pilot txns; full launch April 8, 2026 | Visa corporate |
| **Mastercard Agent Pay / Agent Suite** | Mastercard | "Agentic Tokens" (network-issued per-agent tokens), with Microsoft Copilot, PayPal wallet integration | Mastercard rails | Network-issued agent token | None | First live txns in LAC, Australia (CBA + Event Cinemas), early '26 | Mastercard corporate |
| **PayOS** | PayOS | Card-native agentic checkout + payment tokens + bill pay | Card networks via Mastercard Agentic Token | Network-issued | None | Live commercial onboarding from Sept 2025; specific TPV unknown | Funded private |
| **OpenAI Instant Checkout (ACP)** | OpenAI + Stripe | Agentic Commerce Protocol; SPT delegation | Stripe rails | None | Buyer's stored Stripe method | Pivoted away March '26 — moved to merchant-app model | OpenAI corp |
| **Halliday** | Halliday | "Agentic workflow protocol" — onchain immutable guardrails for delegated agent tasks | Cross-chain | Workflow signature | n/a | Limited public usage | Andreessen Horowitz crypto |
| **Kite (KITE)** | Kite Foundation | Purpose-built Agent L1 — "Proof of AI" consensus + Agent Passport identity | Native chain stablecoin | Agent Passport (KITE AIR) | Built-in | Mainnet roadmap announced Jan 27 '26; testnet hackathon Mar '26 | $18M Sep 2025 (General Catalyst, Plug & Play) |
| **PayAI Network** | PayAI | x402 facilitator + multi-chain + token | Base, Solana, Polygon, Avalanche, Sei, SKALE, X Layer | n/a | n/a | #2 x402 facilitator after Coinbase: 13.78% of all x402 txns | Token-funded |
| **Cloudflare (x402 + EmDash + "deferred scheme")** | Cloudflare | x402 in Workers, MCP server payments, deferred-settlement scheme for batched billing, EmDash CMS | x402 rails | Cloudflare's Trusted Agent Protocol | n/a | "Pay per crawl" live; specific TPV not reported | Co-founder x402 Foundation |

---

## 1. x402 — the deepest dive

### What it actually does (technical primitive)
x402 revives HTTP status code 402 to enable a precise dance: client requests a resource → server returns `402 Payment Required` with a JSON `paymentRequirements` body (price, asset, network, payTo, scheme) → client constructs an `X-PAYMENT` header containing a signed authorization → server (or its facilitator) calls `/verify` and `/settle` → on success, returns `200 OK` plus an `X-PAYMENT-RESPONSE` header with the settlement receipt. ([x402 spec](https://github.com/coinbase/x402))

The dominant scheme is **`exact`**, which on EVM uses **EIP-3009 `transferWithAuthorization`** — a typed EIP-712 message (`from`, `to`, `value`, `validAfter`, `validBefore`, `nonce`) that the facilitator submits onchain. Critically, this is **gasless for the buyer**: the facilitator pays gas. Tokens must support EIP-3009 (USDC, EURC) or be supported via the new ERC-20 generic flow added in v2 ([scheme spec](https://github.com/coinbase/x402/blob/main/specs/schemes/exact/scheme_exact_evm.md)). On Solana, `exact-v2` uses native SPL transfers; on Stellar, SEP-41 assets ([Stellar x402](https://developers.stellar.org/docs/build/agentic-payments/x402)).

**v2 (December 2025)** introduced: CAIP-2 chain identifiers (e.g., `eip155:84532`), wallet-based agent identity, dynamic recipients, modular SDKs, automatic API discovery, and an "upto" scheme for variable-cost calls. **Cloudflare's "deferred scheme"** lets agents accumulate hundreds of micro-debts and settle in batches, addressing the absurdity of paying gas-and-finality on every sub-cent call ([Cloudflare](https://blog.cloudflare.com/x402/)).

### Tech stack
- **Chains:** Base (~85% of volume), Polygon, Arbitrum, Solana, Stellar, World, Algorand, Optimism, HyperEVM
- **Token:** USDC dominant; also EURC; Stellar uses SEP-41 assets
- **Wallet:** wallet-agnostic — any EOA, smart account, or server wallet that can sign EIP-712
- **Settlement:** facilitator pattern (verify + settle); over **30 facilitators** now exist ([ecosystem page](https://www.x402.org/ecosystem)) including CDP (Coinbase), PayAI, Cloudflare, Heurist, Stellar's, Primer, Mogami, Polygon's, Treasure, OpenFacilitator, Algorand's GoPlausible, and Rust facilitators (`x402.rs`)
- **Identity:** none native — pairs with ERC-8004, World ID (via World's "agentkit"), KYA, OOBE Protocol, OMATrust (EAS attestations)

### Team / governance
- Originally Coinbase (Erik Reppel and team at CDP). **x402 Foundation** spun out in 2026 under the **Linux Foundation** with Cloudflare as co-founder, plus 20+ institutional backers (Stripe, AWS, Google, Visa, Mastercard, Circle, Solana Foundation, Anthropic, Hyperbolic) ([Cloudflare blog](https://blog.cloudflare.com/x402/), [CryptoNews](https://cryptonews.com/news/coinbase-x402-ai-agent-app-store-crypto-payments/))

### Funding
No "x402 raise" — it's standards work. Money flows are around it: Coinbase invests via CDP product line; Cloudflare via infra; Stripe via SPT/ACP integration. Coinbase moved the canonical repo from `coinbase/x402` to `x402-foundation/x402` in 2026.

### Traction — be candid
- **Headline numbers:** ~69K agents, 165M+ transactions, ~$50M cumulative volume since launch (May 2025). Aggressively quoted by Coinbase/Pollak ([CoinDesk Apr 25 '26](https://www.coindesk.com/tech/2026/04/25/coinbase-s-jesse-pollak-says-ai-agents-are-the-next-big-wave-for-crypto-payments))
- **The Artemis reality check:** daily volume ~**$28K**, average txn ~**$0.20**. December '25 hit ~731K txns/day, then **collapsed to ~57K txns/day by February 2026 — a 92% drawdown** ([CoinDesk](https://www.coindesk.com/markets/2026/03/11/coinbase-backed-ai-payments-protocol-wants-to-fix-micropayment-but-demand-is-just-not-there-yet), [BeInCrypto](https://beincrypto.com/x402-transactions-drop-in-feb/))
- **Wash / self-dealing:** Artemis estimates ~**50% of txns** are "gamed" — same wallet as buyer & seller, or seller funds buyer who immediately sends it back. **86% of all-time Solana x402 activity is gamed**; Base is "most consistent legitimate," Polygon shows real growth ([startuphub.ai](https://www.startuphub.ai/ai-news/startup-news/2026/x402-payments-the-real-numbers))
- **Net of gaming, x402 is processing on the order of ~$14K/day in real activity** — about a Berkeley coffee shop. The narrative is enormous; the substance is small.

### Revenue model
- Coinbase facilitator: **free tier** of 1,000 settled payments/month, then **$0.001 per settled payment** since Jan 1, 2026 ([Coinbase Dev](https://x.com/CoinbaseDev/status/1995564027951665551)). Negligible direct revenue today; the play is platform lock-in (CDP wallets, USDC, Base sequencer revenue, KYT compliance)
- Other facilitators (PayAI, Heurist) are token-funded or free; OpenFacilitator charges $5/month self-host
- **Core business model is still "monetize the surrounding stack" — not the protocol itself.**

### Open questions / known issues
1. **No native refunds or disputes.** Forced workaround: `x402r` (refund extension protocol with escrow) was created precisely because builders complained about API failures after payment ([x402r.org](https://www.x402r.org/))
2. **Replay/retry handling:** the same payment proof can be submitted twice if a client retries — every facilitator has to dedupe
3. **Mostly-test-traffic problem:** Coinbase admits in March 2026 that it's still a "future not yet here" — the "agent demand" thesis hasn't materialized
4. **No identity:** without ERC-8004 / KYA / World ID, persistent agent reputation is impossible
5. **Facilitator centralization risk:** despite 30+ facilitators, Coinbase CDP processes the majority. PayAI is #2 at 13.8%

### Builder ecosystem (what surprised me about scale)
The x402 ecosystem page lists **150+ named projects** in 14 categories: ~30 facilitators, ~30 services/endpoints, ~15 wallets, ~10 agent frameworks, ~15 monetization gateways, plus discovery tools (x402scan, x402list.fun, x402station, EntRoute) and many MCP-bridge plays (Foldset, MCPay, Tollbooth, Latinum, Locus, Fluora). For better or worse, **the protocol's biggest win to date is being the Schelling point that everyone is building infra against**, not actual transaction volume.

---

## 2. Google AP2 (Agent Payments Protocol)

### What it does
Defined as **verifiable digital credentials (VDCs)** called *Mandates*. Two flavors:
- **Cart Mandate** (human-present): user signs the exact cart with payer/payee/method/risk payload. Their hardware-keyed signature is non-repudiable proof.
- **Intent Mandate** (human-not-present): user signs natural-language conditions giving agent autonomous spend authority within bounded constraints.

Both are JSON, signed via EIP-712-like typed messages with hardware-backed keys; algorithms permitted include RS256 and ES256K but the spec is intentionally non-prescriptive ([AP2 spec](https://github.com/google-agentic-commerce/AP2/blob/main/docs/specification.md)).

### Tech stack
- V0.1 (current): **pull payments** — credit/debit cards
- V1.x roadmap: **push payments** — A2A bank, e-wallets, real-time
- **Stablecoin/x402 explicitly supported** as a complementary execution rail (the "AP2-x402" doc explicitly states they're complementary: AP2 = authorization, x402 = settlement)
- Identity: starts with curated allowlists; long-term decentralized via DIDs / DNS / mTLS
- Settlement: AP2 does not define one — relies on existing PSPs

### Team / funding / traction
- Google Cloud product team (announced Sept 16, 2025)
- 60+ launch partners: Amex, Ant International, Mastercard, PayPal, Revolut, Salesforce, Adyen, Etsy, Forter, Intuit, JCB, Mysten Labs, Coinbase, ServiceNow, UnionPay, Worldpay
- **No public TPV.** It's an authorization spec, not a payment processor — by design it has no settlement throughput to report.

### Revenue model
None. Google gets ecosystem control + Google Cloud / Google Pay distribution.

### Open issues
- "Defines permissions, not payment execution" — Crossmint flags this as the big practical gap
- Card-based reference implementations are still maturing
- Walled-garden tendency (GCP-favored)

---

## 3. Skyfire

### What it does
**Closed network** with two products: (1) **KYAPay** ("Know Your Agent") — an open identity protocol where agents authenticate themselves to anti-bot systems; Skyfire claims **~70% coverage of the internet** today via security-provider partnerships, pushing toward 90%; (2) the **payment network** — businesses deposit fiat which Skyfire converts to USDC and holds in agent-tied custodial wallets; agents pay services with these.

### Tech stack
- USDC-backed custodial wallets
- KYA identity layer is the differentiator
- Chain-agnostic-ish (USDC on multiple)

### Team
- Founders: **Amir Sarhangi** (CEO; ex-Ripple, founder of Jibe Mobile and Messaging Plus) and **Craig DeWitt** (CPO; ex-Ripple). Built Ripple's cross-border network that processed >$50B during their tenure.
- ~37 employees as of Jan 2026 ([Tracxn](https://tracxn.com/d/companies/skyfire/__-gSNwLdAbLR2EH3jQO5ja24BZ2dqjmKWC_BS3-4pf1s))
- Senior engineering hires from Google and Ripple

### Funding
- **$9.5M total** ($8.5M seed Aug 2024 led by Neuberger Berman with Inception Capital, Arrington Capital; +$1M from a16z's CSX accelerator Fall 2024 + Coinbase Ventures)
- 18 investors total ([The Block](https://www.theblock.co/post/322742/coinbase-ventures-and-a16zs-csx-bring-skyfires-total-funding-raised-to-9-5-million))

### Revenue model
**Take rate of 2–3% per transaction** plus flexible API monetization for service providers ([Skyfire docs](https://docs.skyfire.xyz/docs/monetization-features)). This is one of the **few agent-payment companies with a clear, traditional take-rate model**.

### Traction
- "Thousands" of agent signups in beta; LLM-aggregator and large financial-services customers cited but not named publicly
- No disclosed TPV

### Open issues
- Closed/custodial — counter to the open-protocol thesis of x402
- Smaller volume than x402 ecosystem
- KYA depends on B2B partner buy-in which has progressed quietly

---

## 4. Nevermined

### What it does
**Payment multiplexer for agent commerce.** Per-request billing with cost/usage/outcome-based pricing, working with any agent framework (OpenAI, LangChain, CrewAI, OpenClaw) and any transport (HTTP, A2A, MCP, x402). On the fiat side, Nevermined plugs into **Stripe, PayPal Braintree, Cybersource**; on crypto into x402 facilitators. April 2026 announced **Visa Intelligent Commerce integration** giving agents persistent delegated card spend authority, settling via x402 ([CryptoBriefing](https://cryptobriefing.com/ai-payment-integration-visa-nevermined/)).

### Team
- Founders: **Don Gossen** (CEO), **Aitor Argomaniz** (CTO), **Dimitri De Jonghe** (CIO) — all formerly **Ocean Protocol** ([SiliconAngle](https://siliconangle.com/2025/01/09/decentralized-payments-startup-nevermined-raises-4m-unlock-ai-ai-agent-commerce/))
- Switzerland-based (regulatory positioning)

### Funding
- **$7M total** raised; **$4M Series A Jan 9, 2025** led by Generative Ventures with Polymorphic Capital, NEAR, Halo Capital, Factor Capital, Lyrik Ventures, Arca, plus angel checks from David Minarsch / Oak (Olas/Valory), Richard Blythman / Mark Schmidt (Naptha), Ben Fielding (Gensyn) — a "who's who of agent infra"

### Traction
- Partnerships with Olas, Naptha, peaq, FLock, Combinder
- Live operating x402 facilitator
- TPV not publicly disclosed

### Revenue model
SaaS/usage fees on top of payment processing.

### Open issues
- Same micro-payment demand problem as x402
- Multi-rail complexity hard to differentiate from Crossmint and Catena Labs

---

## 5. Crossmint

### What it does
**Single-API agent financial identity:** stablecoin wallets + virtual cards + onramp. The wallets are MPC-style smart accounts; agents get programmable guardrails (per-domain caps, spend limits, approvals). The differentiator is multi-protocol — Crossmint speaks **x402, ACP, AP2, and MPP simultaneously** so builders pick the rail later.

### Tech stack
- Chains: Solana, Base, EVM broadly
- Smart wallet model with MPC + delegation
- **GOAT SDK** ("Great Onchain Agent Toolkit") — open-source agent-finance library; Crossmint claims **150K npm downloads in two months** (Q1 2026); npm `@goat-sdk/core` shows 112 dependent projects
- Wirex card integration brings real-world spend
- Compatible with Eliza, LangChain, AI SDK, ZerePy, GAME, ElevenLabs, OpenAI, Anthropic, Aptos

### Team
- Founders: **Rodri Fernandez** (Co-founder), **Alfonso Touza** (Co-founder), **Alfonso Gómez-Jordana Mañas** (Co-founder) — Spanish engineers, Miami-based, founded 2022

### Funding
- **$23.6M Series A March 18, 2025** led by **Ribbit Capital**, with Franklin Templeton, NYCA, First Round, Lightspeed Faction, HF0, others ([Crossmint blog](https://blog.crossmint.com/crossmint-raises-23-6m-led-by-ribbit-capital/))
- Total raised: $23.6M across 2 rounds, 14 investors
- Customers include Adidas, Red Bull, MoneyGram, Wirex, Toku — these are real enterprise logos

### Traction (real numbers)
- **40,000+ companies/developers** on platform
- **Subscription revenue +1,100% YoY** (March 2024 → March 2025)
- GOAT SDK 150K npm dl

### Revenue model
SaaS subscriptions (the 1,100% number suggests this works) + likely interchange on virtual cards via Wirex.

### Open issues
- Differentiation from Privy + ATXP + Catena Labs
- Crypto-first identity in a card-dominant world

---

## 6. Privy (acquired by Stripe, June 2025)

### What it does
**Server wallets for agents.** Non-custodial via secure-enclave key reconstitution. Agents call Privy to sign; Privy enforces policies (per-tx cap, per-domain limit, agent permissions, workflow approval) before signing. Pairs with x402 → USDC settles on Base → lands in merchant Stripe balance. **Gas abstraction is key** — agents see USD, not gwei.

### Tech stack
- Embedded MPC/enclave wallets
- All EVM chains + Solana
- OpenClaw skill (Peter Steinberger's framework) integrates Privy directly

### Team / funding
- Founded 2021 as Horkos Inc.; Henri Stern (CEO), Asta Li (CTO)
- **Acquired by Stripe June 11, 2025** for undisclosed sum — last private valuation **$230M (March 2025)**, likely sold at meaningful premium
- Pre-acquisition investors: Sequoia, Paradigm, Founders Fund, BlueYard, Ribbit (some via Privy seed)

### Traction
- **75M+ accounts**, billions in cumulative volume across all uses (most non-agent)
- 1,000+ developer teams
- Customers: OpenSea, Hyperliquid, Toku, Farcaster

### Revenue model
SaaS pricing; now bundled into Stripe's broader stack.

### Strategic positioning (post-acquisition)
Privy is the **fast path for any consumer-agent product in the Stripe ecosystem.** Combined with Stripe's Bridge acquisition (stablecoin orchestration) and the Agentic Commerce Suite, Stripe now has end-to-end: identity / wallets (Privy) → spend authorization (SPT/ACP/MPP) → fiat or stablecoin settlement (Stripe + Bridge) → reporting/payouts (Stripe). **This is the most coherent stack any single company owns.**

---

## 7. Stripe — Agentic Commerce Suite, ACP, MPP, Agent Toolkit

Stripe is now a mega-player across four overlapping products:

1. **Agent Toolkit** (`@stripe/agent-toolkit`): function-calling library for LangChain, Vercel AI SDK; exposes Stripe via MCP at `https://mcp.stripe.com` over OAuth. Lets agents create payment links, manage subscriptions, etc.
2. **Agentic Commerce Protocol (ACP)** with OpenAI: open spec for shopping-agent → merchant. Live in ChatGPT (Etsy, Shopify, URBN, Coach, Kate Spade, Ashley Furniture, Revolve, Halara). Powered by **Shared Payment Tokens (SPT)** — agent uses buyer's stored credentials without seeing them. SPT supports cards (incl. Visa Intelligent Commerce + Mastercard Agent Pay tokens) and BNPL (Affirm, Klarna).
3. **Machine Payments Protocol (MPP)** — March 18, 2026 launch. **Session-based** pre-authorized spending across stablecoins (Tempo chain), Stripe fiat, Visa cards, Bitcoin via Lightspark. Differentiator: streaming micropayments with no per-tx overhead.
4. **x402 integration** — Feb 2026: merchants enable x402 via middleware; USDC settles on Base; **funds land in Stripe merchant balance**. Stripe absorbs the settlement-rail headache. ([Privy blog on this flow](https://privy.io/blog/when-agentic-wallets-meet-real-merchants))

**Take/business model:** standard Stripe interchange (2.9% + 30¢ for cards, lower for ACH/SPT), plus subscription Stripe Billing for usage-based models, plus the Bridge stablecoin take.

**Stripe is the company most aggressively monetizing the agent-payments wave today.** It already has revenue infrastructure — agents are an extension, not a new business.

---

## 8. Visa Intelligent Commerce + Mastercard Agent Pay

### Visa
- **Visa Intelligent Commerce Connect** launched April 8, 2026 — single integration via Visa Acceptance Platform for tokenization, spend controls, agent attestation, payment initiation
- Supports **multiple agent protocols**: Trusted Agent Protocol (Visa's own), MPP (Stripe), ACP (OpenAI/Stripe), UCP (Google/Shopify)
- Hundreds of pilot transactions completed in 2025; full enterprise rollout 2026
- Asia-Pacific and Europe pilots early '26; LAC and Caribbean throughout 2026

### Mastercard
- **Agent Pay** launched April 2025 + **Agent Suite** (Q2 2026) of services
- Live transactions: Australia (CBA debit + Event Cinemas), Latin America/Caribbean (March '26), Santander pilot (March '26)
- **Microsoft Copilot Checkout** integration: Agent Pay is the rail
- **PayPal wallet integration** announced October 2025
- Network-issued **Agentic Tokens** = the per-agent token mechanism

**Reality:** The card networks are doing exactly what they did with NFC — wait, let standards form, then bolt on tokenization + spend controls + dispute infrastructure they already own. They will likely capture significant value because (a) they own dispute/chargeback infra, which crypto natively lacks, and (b) merchants don't want a second integration.

---

## 9. OpenAI Instant Checkout — the cautionary tale

OpenAI launched **Instant Checkout** Feb 16, 2026, powered by Stripe + ACP. Etsy first, Shopify-million-merchant rollout planned. **By March 2026, OpenAI pivoted away** to a "merchant-app within ChatGPT" model:
- Onboarding merchants was harder than expected
- Errors high (described as "prone to errors")
- **Users research products in ChatGPT but don't complete purchases there**
- OpenAI hadn't built sales-tax remit/collect infrastructure

This is the highest-profile failure-to-date of the agent-checkout thesis. The diagnosis is generic: **discovery + payment + post-sale (returns, taxes, customer service) is a much bigger product than just "let the agent click pay."** ([CNBC](https://www.cnbc.com/2026/03/24/openai-revamps-shopping-experience-in-chatgpt-after-instant-checkout.html))

---

## 10. Catena Labs — Agent Commerce Kit + AI-native FI

### What it does
**ACK-ID** (W3C DIDs + Verifiable Credentials for agents-with-verifiable-ownership-chains) and **ACK-Pay** (cryptographic receipts across rails: cards, banks, blockchain). The longer play: **the first regulated AI-native financial institution.**

### Team / funding
- Founder: **Sean Neville** — co-founder of Circle, inventor of USDC. (This is heavy.)
- **$18M seed** led by **a16z crypto**, with Breyer Capital, Circle Ventures, Coinbase Ventures, CoinFund, Pillar VC, plus angels: **Tom Brady, Bradley Horowitz, Hamel Husain, Kevin Lin, Peter Mattoon, Sam Palmisano, Balaji Srinivasan** ([Catena](https://catenalabs.com/blog/announcing-catena-labs/))

### Status
Pre-launch. ACK is open source. The FI is being built.

### Why it matters
This is the first credible attempt at **a chartered/regulated financial institution natively for agents.** If they pull a banking license + ACK adoption, they leapfrog every protocol player.

---

## 11. Lightspark + Spark (Bitcoin Lightning rail)

### What it does
**Lightspark** = Bitcoin Lightning + UMA (Universal Money Address) global payments. **Spark** = a new open protocol/L2 for Bitcoin & Lightning, specifically for self-custody scaling and stablecoins-on-Bitcoin.

### Agent angle
- **Tether's WDK / QVAC** (Tether's decentralized AI agent platform) integrates Spark to let agents transact in USDT and BTC
- Lightning's sub-cent settlement makes it actually viable for real micropayments — unlike most "micropayment" stories
- David Marcus (CEO) was head of Meta's Diem/Libra — political and credibility heft

### 2026 events
- Joined Solana Developer Platform as infra partner (March 24, 2026)
- Cross River partnership for 24/7 fiat (Feb 18, 2026)
- Breez partnership for native Lightning payments

### Reality
**The most underrated agent-rail.** Lightning is the only existing rail with truly economic sub-cent payments. The reason it isn't dominant in agent-payments today is (a) most agents are EVM-native, (b) Lightning DX still rough, (c) cultural — agent builders default to Coinbase/Stripe stack.

---

## 12. Coinbase AgentKit + Agentic Wallets

### What it does
- **AgentKit:** TypeScript/Python framework for AI agents to do onchain actions (send, trade, earn, fund); supports OpenAI Agents SDK
- **Agentic Wallets** (2026): TEE-backed non-custodial wallets specifically for agents — keys live in secure enclaves, agent never holds them; built on CDP SDK
- Integrates with x402 by default

### Tech stack
- Base USDC primary
- TEE = "true self-custody with enterprise security"
- OnchainKit conversational UI

### Why it matters
This + x402 + Privy (now Stripe) is the **default starting stack** for an EVM-side agent payment build. Coinbase is positioning to be the **AWS of agent finance**.

---

## 13. Halliday, Kite, PayOS, PayAI, Cloudflare's "deferred"

- **Halliday** — onchain workflow protocol for delegated agents; immutable guardrails enforced onchain; a16z crypto–backed; less about payments, more about *what an agent is allowed to do*. Adjacent.
- **Kite (KITE)** — a **Layer-1 blockchain purpose-built for agents.** "Proof of AI" consensus, native Agent Passport identity, stablecoin payments. **$18M raised Sep 2025 (General Catalyst, Plug & Play)**. Mainnet roadmap Jan 2026; testnet hackathon March 2026 with Encode Club. Risky but interesting if even part of it works.
- **PayOS** — card-native agentic checkout. First Mastercard Agentic Token transaction Sept 29, 2025. Now selling to merchants. Token-based revenue model.
- **PayAI** — the #2 x402 facilitator after Coinbase, **13.78% of all x402 txns**. Has a token (PAYAI). Multi-chain coverage.
- **Cloudflare's deferred-scheme** — quietly the most pragmatic addition: batch sub-cent calls, settle later via fiat or USDC. Enables their "pay per crawl" program.

---

## 14. What works (categorically)

| Category | Status | Why |
|---|---|---|
| **Agent → API (x402-style pay-per-call)** | Works technically; demand thin | EIP-3009 + USDC + Base settles in 2 sec for ~$0.0001 gas. ~150 services live on x402. The plumbing is real. |
| **Agent → human service (Skyfire model)** | Works for narrow B2B | Skyfire's KYA + custodial USDC is operational; partners onboarding LLM aggregators and FS firms. |
| **Agent → agent** | Mostly demo | Olas reports 10M+ agent-to-agent txns on Gnosis (per market map), but in production, A2A payment use cases are still rare outside Polystrat-style trading bots. |
| **Subscription delegation** | Works — actually adopted | This is the "boring winner": Crossmint virtual cards, MPP sessions, Visa/MC tokenization. Sets a cap and lets the agent draw from it like an employee credit card. **Less hyped than x402 but powering far more real value movement today.** |
| **Shopping-agent checkout (ACP)** | Mixed | OpenAI pivoted; Stripe stack working with major brand catalog; Visa/MC pilots live. The technology works; the consumer behavior of "buy in-chat" is still uncertain. |

---

## 15. What doesn't work

### Real micropayments (sub-cent)
The CoinDesk March 2026 piece ([here](https://www.coindesk.com/markets/2026/03/11/coinbase-backed-ai-payments-protocol-wants-to-fix-micropayment-but-demand-is-just-not-there-yet)) was explicit: $28K daily volume against a >$7B ecosystem valuation, ~50% of activity gamed. Why?

1. **There's no business model for sub-cent.** API providers prefer subscription pricing because forecasting and CAC math both require it. A $0.001 call rate produces zero clarity for either side.
2. **Most "AI agents" today aren't autonomous economic actors.** They're orchestrated workflows with API keys. The supplier doesn't need a payment rail; they need an API key + invoice.
3. **Settlement still costs gas.** Even on Base, batching matters — hence Cloudflare's deferred scheme.
4. **The wash-trading numbers** show a narrative-led market — protocols pay grants/airdrops to bootstrap usage, builders self-deal to qualify.

### Cross-protocol agent identity
Five competing identity layers: AP2 mandates, ACK-ID DIDs/VCs, Skyfire KYA, Visa TAP, Mastercard agent tokens, ERC-8004, Kite Passport, OOMA Trust. **None interoperate today.** A merchant accepting agents will need to handle 3-5 attestation formats by the end of 2026.

### Refunds and disputes
x402's irreversible settlement broke this so badly it spawned `x402r` as a separate refund protocol. Card networks (Visa, MC, Stripe ACP) don't have this problem, which is precisely why agentic shopping will likely default to card rails for high-value items and only use crypto for sub-dollar API calls.

### Spending caps / parental controls
Privy and Crossmint have policy-engine SDKs (per-tx cap, per-domain, per-workflow). But cross-app caps (the agent shouldn't spend more than $X this week across all services) require an identity layer that doesn't exist yet. **The IRL parallel is "credit card with a $500 monthly limit" — easy on a single rail, impossible across rails.**

### Tax / accounting
Stunningly underbuilt. OpenAI specifically cited not having "set up systems to collect and remit state sales taxes" as a reason to pull Instant Checkout. There's no AP2 or x402 spec for tax. **This is the first bottleneck enterprises will scream about** when they try to scale this in 2026-27.

---

## 16. Who is actually making money?

The honest answer: **almost nobody, at agent-payment-specific volume.** But the infrastructure layers serving builders are doing fine:

| Layer | Money-making example | Why it works |
|---|---|---|
| **Card networks** | Visa, Mastercard | Interchange continues regardless. Adding agent flows = pure upside, no cannibalization. |
| **PSPs** | **Stripe** (probably the single biggest beneficiary) | Bridge + Privy + ACP + MPP + x402 integration. Every agent-payment that touches fiat passes through Stripe-owned infrastructure now. |
| **Wallet infra** | **Crossmint** | Subscription revenue +1,100% YoY. Real enterprise logos (Adidas, Red Bull, MoneyGram). |
| **Wallet infra** | **Privy** | Acquired at >$230M; now Stripe revenue line |
| **Stablecoin issuers** | **Circle (USDC)** | Float on every USDC sitting in agent wallets = direct revenue. They are arguably the largest passive beneficiary of x402's growth. |
| **L2 sequencer** | **Base** (Coinbase) | 85% of x402 settles on Base. Sequencer revenue + ecosystem flywheel. |
| **Closed networks** | **Skyfire** | 2-3% take rate. Small but real. |
| **DePIN compute facilitating agents** | Aethir, Render, Akash (per market map) | $147M ARR (Aethir) — agents are a customer segment, not the only customer |
| **Agent frameworks** | Eliza (open source, no rev), Mastra (YC), Crossmint GOAT SDK | Hard to monetize directly; lead-gen for paid wallet/agent infra |
| **Protocol-only plays** | x402 Foundation, AP2 | Zero direct revenue. Standards work. |
| **Token plays** | Kite, PayAI, Virtuals | Token treasuries fund operations; real revenue minimal |

**Punchline: The card networks and Stripe + Coinbase/Circle are the structural winners regardless of which protocol "wins." Specialist startups (Crossmint, Skyfire, Catena, Kite, Nevermined) have to find a defensible niche before the platforms eat them.**

---

## 17. Builder ecosystem — what frameworks integrate

| Framework | Agent-payment integration |
|---|---|
| **LangChain** (Python/JS) | Stripe Agent Toolkit, GOAT SDK, Crossmint, openlibx402, Coinbase AgentKit, Nevermined |
| **CrewAI** | Stripe, Nevermined, Crossmint |
| **AutoGen** | Stripe MCP, Coinbase AgentKit |
| **Mastra** (TypeScript, YC) | x402 via Olostep + Pay-per-use; community plugins |
| **Vercel AI SDK** | Stripe Agent Toolkit, GOAT SDK, native x402 monetization for tools |
| **OpenAI Agents SDK** | Coinbase AgentKit explicitly supports it |
| **Eliza** (ELIZA framework, ~10K stars) | GOAT SDK, Coinbase AgentKit, Nevermined |
| **OpenClaw** (Peter Steinberger) | Privy agentic-wallets-skill (purpose-built), Nevermined |
| **MCP servers** | Stripe MCP, MCPay, Tollbooth, Latinum, Locus, Foldset, Cloudflare's MCP-via-x402, ClawPay |

GitHub stars (notable):
- **coinbase/x402** repo: 5.4K stars, 1K forks (canonical now at `x402-foundation/x402`)
- **GOAT SDK** (`goat-sdk/goat`): the #1 agentic finance toolkit by stated downloads (150K npm in 2 months)
- **Stripe agent toolkit** (`stripe/ai`): bundled in Stripe's docs as default, scaling with Stripe AI volume
- **catena-labs/ack** repo: open source, modest stars (early)

npm package metrics:
- `@coinbase/x402`: 32 dependent packages
- `@goat-sdk/core`: 112 dependent packages

---

## 18. Dominant stack pattern

Based on what's actually shipped and works as of April 2026:

**The "EVM-native agent payments" canonical stack:**

```
Agent Logic         → LangChain / Vercel AI SDK / Mastra / OpenClaw
   ↓
Agent Wallet        → Privy server wallet OR Crossmint smart wallet OR Coinbase Agentic Wallet (TEE)
   ↓
Spend Policies      → Privy/Crossmint policy engine (per-tx cap, per-domain limit)
   ↓
Payment Protocol    → x402 (HTTP 402 + EIP-3009 signed authorization)
   ↓
Settlement          → USDC on Base via CDP / PayAI / Cloudflare facilitator
   ↓
Merchant Receivable → Stripe balance (when via ACP/x402-Stripe), OR direct merchant wallet
   ↓
Identity (optional) → ERC-8004 + World ID + (eventually) AP2 mandate VDC
```

**The "card-rail agent payments" canonical stack:**

```
Agent              → ChatGPT / Copilot / Gemini / consumer agent
   ↓
Authorization      → AP2 Cart/Intent Mandate signed with user device key
   ↓
Token              → Visa Intelligent Commerce token OR Mastercard Agentic Token OR Stripe SPT
   ↓
Settlement         → Existing card rails (Visa/MC) → existing PSP (Stripe/Adyen)
   ↓
Merchant           → Existing checkout, agent-tagged for fraud / dispute routing
```

These two stacks are **not** in zero-sum competition — they likely converge: AP2 for authorization, ACP/MPP for high-value commerce, x402 for sub-dollar machine-to-machine. Crossmint, Catena Labs, and Stripe are each positioning to abstract this multi-protocol mess.

---

## 19. What surprised me (non-obvious findings)

1. **The 92% February 2026 transaction collapse.** The headline narrative ("69K agents, 165M txns") obscures that x402 has been *bleeding usage* since Dec 2025. Daily txns went from ~731K to ~57K. The "$50M cumulative volume" number is dominated by the late-2025 wash-trading boom. Real organic daily volume is closer to **$14K** — the price of a lightly-trafficked SaaS startup. The market cap of the x402 ecosystem is roughly **500,000× annualized real volume**. That's a definitional bubble.

2. **Stripe quietly owns the entire stack now.** Privy (June 2025 acquisition) + Bridge (stablecoin orchestration, late 2024) + ACP (with OpenAI) + MPP (March 2026) + x402 integration (Feb 2026) + Stripe Agent Toolkit. **Every other agent-payment startup has to either compete with Stripe-owned infrastructure or sit on top of it.** The Privy acquisition price was likely ~$300M+ — possibly the most valuable agent-infra exit so far, and the agent angle was a footnote in coverage.

3. **The Coinbase facilitator started charging fees Jan 1, 2026** — $0.001 per settled call after 1K free. This is the first actual *take rate* in the x402 ecosystem from its dominant facilitator. Tiny but signals that "free protocol" was a launch pattern, not a permanent state.

4. **Cloudflare's deferred scheme is the under-appreciated breakthrough.** The original x402 promise of "every HTTP call gets a USDC payment" is economically incoherent. Cloudflare's batched/deferred settlement scheme is what makes "pay per crawl" actually work. Expect this to become the dominant pattern for sub-cent flows.

5. **Catena Labs is the dark horse.** A $18M seed led by a16z crypto with Sean Neville (USDC inventor) building a *regulated AI-native FI*, with Tom Brady, Sam Palmisano, and Balaji on the cap table — and almost no industry chatter. If they get a banking charter + ACK adoption, they have a moat no protocol can match.

6. **Agent-to-agent payments at scale exist — on Gnosis Chain through Olas, not on x402.** Olas reports 10M+ A2A txns; this is the actual production A2A workload today. The "agent → API" use case dominates x402, but agent-to-agent commerce is happening in a quieter ecosystem.

7. **Skyfire's KYA covers ~70% of the internet's anti-bot infrastructure.** This stat is barely cited. If true, Skyfire has quietly become a critical agent-identity gatekeeper without much fanfare.

8. **The 2-3% Skyfire take rate is the only clean monetization in the entire field.** Everyone else is either subsidizing volume, monetizing surrounding infrastructure (CDP, Stripe interchange, Circle float), or hoping a token will work. Skyfire's model is the most boring and the most analogous to PayPal — and the small team quietly builds.

9. **Crossmint's GOAT SDK has 150K npm downloads in 2 months** — for an agent-finance library, that is a striking signal of bottom-up developer adoption, more so than any single protocol's hype.

10. **OpenAI's pivot away from Instant Checkout is the under-told story of 2026.** The biggest consumer surface in AI ($3T+ valuation, hundreds of millions of users) tried agentic checkout — and rolled it back to "merchant apps within ChatGPT" within a month. **Reality is winning over narrative.**

11. **The card networks added agent attestations almost effortlessly.** Visa Intelligent Commerce + Mastercard Agent Pay + PayOS + Microsoft Copilot Checkout all came online while x402 wash-traded. **Once real merchant volume materializes, it will probably default to card rails first** — because chargebacks, dispute, KYC, and tax reporting are already solved there and unsolved on chain.

12. **The biggest strategic move of the period was the x402 Foundation under Linux Foundation.** It moves x402 from "Coinbase product" to "neutral standard," letting Visa, Mastercard, Stripe, AWS, Google, Cloudflare all back it without competitive worry. This was a sophisticated piece of standards politics that let the ecosystem grow much faster than if it had stayed under Coinbase.

---

## Sources

- [x402 main repo (Coinbase)](https://github.com/coinbase/x402)
- [x402 specification](https://github.com/coinbase/x402/blob/main/specs/x402-specification.md)
- [x402 exact-EVM scheme spec](https://github.com/coinbase/x402/blob/main/specs/schemes/exact/scheme_exact_evm.md)
- [x402.org ecosystem page (150+ projects)](https://www.x402.org/ecosystem)
- [Cloudflare x402 Foundation announcement + deferred scheme](https://blog.cloudflare.com/x402/)
- [CoinDesk: Coinbase-backed protocol — demand isn't there (March 2026)](https://www.coindesk.com/markets/2026/03/11/coinbase-backed-ai-payments-protocol-wants-to-fix-micropayment-but-demand-is-just-not-there-yet)
- [BeInCrypto: x402 transactions drop in Feb 2026](https://beincrypto.com/x402-transactions-drop-in-feb/)
- [Coinbase x402 fee structure tweet (Jan 1, 2026)](https://x.com/CoinbaseDev/status/1995564027951665551)
- [Coinbase Jesse Pollak on AI agents (April 25, 2026)](https://www.coindesk.com/tech/2026/04/25/coinbase-s-jesse-pollak-says-ai-agents-are-the-next-big-wave-for-crypto-payments)
- [Coinbase x402 marketplace launch](https://cryptonews.com/news/coinbase-x402-ai-agent-app-store-crypto-payments/)
- [x402 v2 launch announcement](https://www.x402.org/writing/x402-v2-launch)
- [x402 v2 InfoQ summary](https://www.infoq.com/news/2026/01/x402-agentic-http-payments/)
- [Stellar x402 implementation](https://developers.stellar.org/docs/build/agentic-payments/x402)
- [PayAI as #2 facilitator](https://blog.payai.network/x402-payment-protocol/)
- [x402scan ecosystem explorer](https://www.x402scan.com/)
- [x402r refund extension protocol](https://www.x402r.org/)
- [Google AP2 announcement](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol)
- [AP2 specification](https://github.com/google-agentic-commerce/AP2/blob/main/docs/specification.md)
- [AP2-x402 complementary doc](https://ap2-protocol.org/topics/ap2-and-x402/)
- [Skyfire raises $8.5M seed (TechCrunch)](https://techcrunch.com/2024/08/21/skyfire-lets-ai-agents-spend-your-money/)
- [Skyfire $9.5M total / a16z CSX (The Block)](https://www.theblock.co/post/322742/coinbase-ventures-and-a16zs-csx-bring-skyfires-total-funding-raised-to-9-5-million)
- [Skyfire monetization docs](https://docs.skyfire.xyz/docs/monetization-features)
- [Skyfire Tracxn profile](https://tracxn.com/d/companies/skyfire/__-gSNwLdAbLR2EH3jQO5ja24BZ2dqjmKWC_BS3-4pf1s)
- [Nevermined $4M Series A (SiliconAngle)](https://siliconangle.com/2025/01/09/decentralized-payments-startup-nevermined-raises-4m-unlock-ai-ai-agent-commerce/)
- [Nevermined-Visa Intelligent Commerce integration (CryptoBriefing)](https://cryptobriefing.com/ai-payment-integration-visa-nevermined/)
- [Crossmint $23.6M Series A (CoinDesk)](https://www.coindesk.com/business/2025/03/18/blockchain-firm-crossmint-used-by-adidas-red-bull-raises-usd23-6m-in-funding)
- [Crossmint funding announcement](https://blog.crossmint.com/crossmint-raises-23-6m-led-by-ribbit-capital/)
- [Crossmint protocol comparison](https://www.crossmint.com/learn/agentic-payments-protocols-compared)
- [GOAT SDK (Crossmint open source)](https://github.com/goat-sdk/goat)
- [Privy acquired by Stripe (PYMNTS)](https://www.pymnts.com/acquisitions/2025/stripe-acquires-privy-to-bolster-its-cryptocurrency-game/)
- [Privy + Stripe announcement](https://privy.io/blog/announcing-our-acquisition-by-stripe)
- [Privy server-wallets meet merchants (with x402)](https://privy.io/blog/when-agentic-wallets-meet-real-merchants)
- [Stripe agent toolkit docs](https://docs.stripe.com/agents)
- [Stripe Agentic Commerce Suite](https://stripe.com/blog/agentic-commerce-suite)
- [Stripe SPT + Agentic Commerce launch](https://stripe.com/blog/introducing-our-agentic-commerce-solutions)
- [OpenAI Instant Checkout / ACP launch](https://openai.com/index/buy-it-in-chatgpt/)
- [OpenAI pivot — CNBC](https://www.cnbc.com/2026/03/24/openai-revamps-shopping-experience-in-chatgpt-after-instant-checkout.html)
- [Visa Intelligent Commerce Connect launch April 8, 2026](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22276.html)
- [Mastercard Agent Pay (April 2025)](https://www.mastercard.com/us/en/news-and-trends/press/2025/april/mastercard-unveils-agent-pay-pioneering-agentic-payments-technology-to-power-commerce-in-the-age-of-ai.html)
- [Mastercard Agent Pay Australia (CBA + Event Cinemas)](https://www.mastercard.com/news/ap/en/newsroom/press-releases/en/2026/mastercard-accelerates-ai-powered-commerce-with-australia-s-first-authenticated-agentic-transactions-using-agent-pay/)
- [Mastercard + PayPal partnership](https://newsroom.paypal-corp.com/2025-10-27-Mastercard-and-PayPal-Join-Forces-To-Accelerate-Secure-Global-Agentic-Commerce)
- [Catena Labs $18M seed announcement](https://catenalabs.com/blog/announcing-catena-labs/)
- [Catena Labs on ACK technical](https://catenalabs.com/blog/agent-commerce-kit)
- [ACK GitHub](https://github.com/catena-labs/ack)
- [Lightspark / Spark intro](https://www.lightspark.com/news/spark/introducing-spark)
- [Tether WDK + Spark for AI agents](https://www.lightspark.com/news/spark/tether-integrates-spark-into-wdk-ushering-in-a-new)
- [Coinbase AgentKit GitHub](https://github.com/coinbase/agentkit)
- [Coinbase Agentic Wallets launch (PYMNTS)](https://www.pymnts.com/cryptocurrency/2026/coinbase-debuts-crypto-wallet-infrastructure-for-ai-agents/)
- [Kite $18M raise (CoinDesk)](https://www.coindesk.com/business/2025/09/02/kite-raises-usd18m-to-bridge-stablecoin-payments-and-autonomous-agents)
- [Kite docs](https://docs.gokite.ai/)
- [Halliday agentic workflow protocol](https://medium.com/@HallidayHQ/halliday-the-first-agentic-workflow-protocol-2f7f56a661c4)
- [PayOS + Mastercard live agentic transaction](https://finance.yahoo.com/news/one-small-step-payos-one-052600633.html)
- [PayAI Network](https://payai.network/)
- [EIP-3009 review (Extropy)](https://academy.extropy.io/pages/articles/review-eip-3009.html)
- [ATXP protocol comparison (X402, ACP, UCP, AP2)](https://atxp.ai/blog/agent-payment-protocols-compared/)
- [Insignia VC: Infrastructure behind agentic commerce (April 24, 2026)](https://review.insignia.vc/2026/04/24/when-agents-go-shopping-the-infrastructure-behind-agentic-commerce/)
- [Fenwick: Is 2026 the year of agentic payments](https://www.fenwick.com/insights/publications/is-2026-the-year-of-agentic-payments)
