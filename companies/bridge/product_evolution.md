# Bridge Product Evolution: 2022 → May 2026

A focused research pass on Bridge (bridge.xyz), the stablecoin payments infrastructure company acquired by Stripe in October 2024, tracing its evolution from a failed NFT-payments product to the operating system for Stripe's stablecoin strategy.

---

## 1. Executive Snapshot — What Bridge Is Today vs Then

| Year | What Bridge Was | Headcount/Stage | Key Product Surface |
|---|---|---|---|
| **2022** | Bank-account → NFT acquisition product (Abrams, in *Cheeky Pint*: *"the first idea we had was using your bank account to acquire NFTs"*) | Founded March 2022 by Zach Abrams + Sean Yu (ex-Square, ex-Coinbase), seed funded ~April 2022 | Pre-product; pivoted by May 2022 |
| **2023** | "Stablecoin APIs for developers" — Orchestration + Issuance positioning live by March 2023 (Wayback Machine) | Quietly building; private beta with select customers (Airtm, Coinbase, SpaceX) | Two-pillar pitch: *Orchestration* (convert any dollar form) + *Issuance* (whitelabel a stablecoin) |
| **2024** | $40M Series A (March, Sequoia/Ribbit/Index/Haun, ~$200M valuation); public launch August 29; $1.1B Stripe acquisition announced Oct 21 | ~$5B annualized payment volume by Aug 2024; 10× growth in 2024 per Stripe | Orchestration (USD/EUR fiat ↔ USDC/USDT/PYUSD/EURC), Issuance (whitelabel), Cards (early) |
| **2025** | Acquisition closed Feb 4; Stablecoin Financial Accounts in 101 countries (May 7); USDB launched (May 7); Tron in-house infra (May 13); Visa partnership (Apr 30); Privy joined Stripe (June 11); Open Issuance (Sept 30); OCC charter applied (Oct 14) | $10B+ annualized volume; "Bridge, a Stripe company" branding | Five-pillar product: Orchestration, Issuance (now Open Issuance), Cards, Wallets, Cross-Border Payments |
| **2026 (May)** | OCC conditional approval (Feb 12-17); Visa expansion to 100+ countries (March 3); Tempo full support (March 27); chains added at speed (Plasma, Aptos, Sui, HyperEVM, Celo); Payoneer partnership (Feb 17) | "Bridge National Trust Bank" application pending final OCC approval; 18 countries live for cards, scaling to 100+ | Bank-grade infra: trust charter pending; expanding into agentic-payments rails via Tempo |

Sources: [Cheeky Pint episode](https://cheekypint.substack.com/p/stablecoin-special-zach-abrams-bridge), [Wayback Mar 2023](http://web.archive.org/web/20230321181446/https://www.bridge.xyz/), [Fortune Aug 2024](https://fortune.com/crypto/2024/08/29/bridge-stablecoins-sequoia-ribbit-index-haun-58-million/), [Stripe newsroom](https://stripe.com/newsroom/news/stripe-completes-bridge-acquisition).

---

## 2. Quarter-by-Quarter Changelog (Q1 2022 → Q2 2026)

### Q1–Q2 2022: Founding and the NFT-Payments Idea
- **March 2022:** Zach Abrams (ex-Brex, ex-Coinbase product lead behind USDC) and Sean Yu (ex-Square, ex-Coinbase) leave their jobs to start the company.
- **April 2022:** Pre-seed funding raised (Index, Haun Ventures' Chris Ahn's first check, others).
- **First idea:** Use your bank account to acquire NFTs — "deduct money from the bank → convert to stablecoin → buy NFT." Abrams in *Cheeky Pint*: *"the first idea we had was using your bank account to acquire NFTs."*
- **May 2022:** Pivot away from NFTs. Briefly considered wallets-as-a-service (which Privy was building) but Abrams called it a "tar pit" and moved to stablecoins.
- **Mid-2022:** [bridge.xyz domain purchased for $120K](https://gen.xyz/blog/bridgexyz) (the 6th-largest .xyz sale ever at the time).
- **Sept 6, 2022:** Wayback shows the website tagline *"Stablecoin APIs for developers — APIs that enable developers to build exciting money movement experiences."* Already off NFTs. ([Wayback Sept 2022](http://web.archive.org/web/20220906213505/https://www.bridge.xyz/))

### Q3–Q4 2022: Macro Shock and Mode Shift
- **Q3 2022 (Terra/Luna fallout) → Nov 2022 (FTX) → March 2023 (Silvergate/Signature/USDC depeg):** Abrams in *a16z* and *Cheeky Pint* describes "the first year of the company being awful." Conviction grows that stablecoins will be the rail; nobody wants to do the unsexy compliance/banking glue work.

### Q1 2023: The Two-Pillar Pitch Crystallizes
- **March 21, 2023 (Wayback):** Bridge.xyz now explicitly markets the two pillars:
  - *Orchestration* — "easily convert between any two dollar formats"
  - *Issuance* — "convert any of these dollars into a stablecoin you fully control"
- Tagline: *"Move any form of a dollar."*
- Site lists supported stablecoins, "join our waitlist," "Not our first rodeo" team section.

### Q2–Q3 2023: Quiet Build, Early Customers
- Bridge operating in stealth-ish; pre-Series A; building integrations to USDC, USDT, PYUSD, and core fiat rails (USD ACH/Wire, EUR SEPA).
- Fireblocks customer story published this period; first paying customers include Airtm (Latin America cross-border), Coinbase (USDT-Tron ↔ USDC-Base routing), and a small set of fintechs.

### Q4 2023: Foundations Laid
- Solidified compliance posture (KYC/KYB, US licenses), virtual accounts product in private beta.

### Q1 2024: Series A
- **March 2024:** $40M Series A co-led by Sequoia, Ribbit, Index, Haun Ventures at ~$200M post-money valuation (per [Architect Partners](https://architectpartners.com/stripe-is-acquiring-bridge-for-1-1-billion-the-most-strategically-important-transaction-since-the-emergence-of-crypto/), 5.5× of which was the Stripe acquisition price).
- **March 2024:** Airtm × Bridge cross-border payouts via Stellar go live; nearly half of Airtm's enterprise payout volume runs through it.

### Q2 2024: Scaling, SpaceX
- SpaceX/Starlink begins using Bridge for Starlink revenue collection in Argentina, Nigeria, and other emerging markets, converting local fiat into stablecoins for global treasury (per [Chamath disclosure](https://www.thestreet.com/crypto/innovation/spacex-uses-stablecoins-to-collect-payments-from-starlink-customers-says-chamath-palihapitiya)).
- **June 2024:** Coinbase using Bridge to route USDT-on-Tron ↔ USDC-on-Base for users.

### Q3 2024: Public Launch + Stripe Talks
- **August 29, 2024:** [*"Introducing Bridge"*](https://www.bridge.xyz/news/introducing-bridge) blog post — the formal coming-out. Funding total disclosed: $58M. Customers public: SpaceX, Coinbase, Airtm. Annual run-rate: $5B.
- **Sept 2024:** Stripe acquisition negotiations underway (per Architect Partners timeline).

### Q4 2024: The Stripe Deal
- **Oct 20–22, 2024:** [Stripe announces $1.1B acquisition of Bridge](https://fortune.com/crypto/2024/10/22/stripe-announces-1-1-billion-acquisition-of-stablecoin-start-up-bridge/) — largest crypto M&A ever.
- **Oct 22, 2024:** [*"Building a Bigger, Better Bridge"*](https://www.bridge.xyz/news/building-a-bigger-better-bridge) — Bridge's response post.
- 2024 full year: 10× business growth (per Stripe disclosure on close).

### Q1 2025: Closing + First Stripe-Era Move
- **February 4, 2025:** [Stripe completes Bridge acquisition](https://stripe.com/newsroom/news/stripe-completes-bridge-acquisition). Bridge now operates as a Stripe subsidiary with Abrams as CEO of Bridge.
- **Feb 27, 2025:** Wirex × Bridge — Wirex Pay launches stablecoin payment platform in the US powered by Bridge.

### Q2 2025: Stripe Sessions Blowout
- **April 28, 2025:** [*"Stablecoin-enabled FX, Now Live in Mexico"*](https://www.bridge.xyz/news/mxn-fx) — local on/offramps for MXN via SPEI go live.
- **April 30, 2025:** [Visa × Bridge partnership announced](https://stripe.com/newsroom/news/bridge-partners-with-visa) — first global stablecoin-linked card-issuing product. Initial markets: Argentina, Colombia, Ecuador, Mexico, Peru, Chile.
- **May 7, 2025 (Stripe Sessions):**
  - [Stablecoin Financial Accounts launched in 101 countries](https://stripe.com/blog/introducing-stablecoin-financial-accounts) — powered entirely by Bridge.
  - [USDB stablecoin launched](https://www.bridge.xyz/news/usdb) — Bridge's own programmable, reward-bearing stablecoin, 1:1 backed by cash + BlackRock short-duration money market funds. Free conversion to USDC.
- **May 13, 2025:** [*"Tron Support on Bridge"*](https://www.bridge.xyz/news/tron) — Tron becomes the *first* chain on Bridge's in-house deposit + withdrawal infrastructure. Unlimited deposit addresses, full USDT.trx interoperability, memoless onramps.
- **June 11, 2025:** [Stripe acquires Privy](https://www.bloomberg.com/news/articles/2025-06-11/payment-company-stripe-to-acquire-crypto-wallet-provider-privy) — but Privy stays independent (Bridge for custody/orchestration; Privy for non-custodial wallets; deliberate split).

### Q3 2025: Open Issuance & Tempo
- **July 15, 2025 (changelog):** Bridge Wallet can now fund fiat returns automatically; new fields added to `LiquidationAddress`, `VirtualAccount`, `StaticMemo`.
- **July 20, 2025 (changelog):** Tighter proof-of-address handling in KYC/KYB; new `documents.purpose=proof_of_address` flow.
- **August 18, 2025 (changelog):** Dashboard overhaul — admin permissions self-serve, billing tab, beta payments module.
- **September 4, 2025:** [Tempo announced](https://www.paradigm.xyz/2025/09/tempo-payments-first-blockchain) — payments-first L1 backed by Stripe + Paradigm (Matt Huang leading), with launch partners Anthropic, OpenAI, Coupang, Deutsche Bank, DoorDash, Lead Bank, Mercury, Nubank, Revolut, Shopify, Standard Chartered, Visa.
- **September 17, 2025 (changelog):** Reverse exchange rates (EUR/MXN/BRL → USD); new `missing_return_policy` payment state.
- **September 30, 2025:** [*"Introducing Open Issuance"*](https://www.bridge.xyz/news/introducing-open-issuance). Phantom's CASH stablecoin is the launch partner; existing Bridge-issued coins migrate over: USDH (Hyperliquid, via Native Markets), MetaMask USD (mUSD, with M0), Dakota, Slash, Lava, Takenos. Reserves managed by BlackRock, Fidelity, Superstate; cash held by Lead Bank.
- **September 30, 2025:** Coordinated with OpenAI/Stripe Agentic Commerce Protocol launch — ChatGPT Instant Checkout uses Stripe-Bridge plumbing.

### Q4 2025: Charter and Expansion
- **October 14, 2025:** [Bridge files OCC application for a national bank trust charter](https://www.coindesk.com/business/2025/10/14/stripe-s-bridge-applies-for-national-bank-trust-charter-to-expand-stablecoin-business). Entity name: **Bridge National Trust Bank, NA**. Parent: Bridge Ventures LLC (BVL), wholly owned by Stripe.
- **October 2025:** Sendwave Wallet launches — stablecoin-backed P2P money in 100+ countries, powered by Bridge.
- **November 12, 2025:** [Sui launches USDsui](https://www.coindesk.com/business/2025/11/12/sui-launches-native-stablecoin-usdsui-using-bridge-s-open-issuance-platform) — native Sui stablecoin issued via Open Issuance.
- **November 17, 2025 (changelog):** BRL on/offramps via **Pix** go live (Brazil).
- **December 2, 2025:** Bridge expands stablecoin card issuing to Africa and LATAM; Open Issuance customer pipeline grows.
- **December 10, 2025:** [Stripe acqui-hires Valora](https://www.coindesk.com/business/2025/12/10/stripe-acqui-hires-crypto-payments-startup-valora-venturing-further-into-stablecoins) — adds mobile-first stablecoin team.

### Q1 2026: Charter Win
- **January 20, 2026 (changelog):** USDG (Global Dollar) on Solana support added.
- **January 23, 2026 (changelog):** GBP on/offramps via UK Faster Payments (FPS) — beta launch.
- **January 29, 2026 (changelog):** EURC on Ethereum + USDT on Plasma added.
- **February 9, 2026 (changelog):** Celo on/offramp; enhanced crypto returns; Fixed Outputs (specify destination amount, Bridge solves the source-side math).
- **February 12, 2026:** OCC issues Corporate Decision #1365/#1367 — **conditional approval** for Bridge National Trust Bank.
- **February 17, 2026:** [Bridge announces OCC conditional approval](https://www.bridge.xyz/blog/bridge-receives-occ-conditional-approval-to-organize-a-federally-chartered-national-trust-bank). Same day: [Payoneer announces Bridge-powered stablecoin capabilities](https://investor.payoneer.com/news-releases/news-release-details/payoneer-launch-stablecoin-capabilities-powered-bridge-bringing) launching Q2 2026.
- **February 23, 2026 (changelog):** USDT on Ethereum supported in Bridge custodial wallets.
- **February 25, 2026:** Decibel (Aptos perpetuals DEX) launches with **usDCBL** issued by Bridge — protocol-native stablecoin, USDC on/off ramp.
- **February 26–27, 2026 (changelog):** External Account API improvements (deactivation reason, webhook events).
- **March 3, 2026:** [Visa × Bridge expansion](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22206.html) — from 18 to 100+ countries planned across Europe, APAC, Africa, Middle East by year-end.
- **March 9, 2026 (changelog):** USDT on Solana; USDT MXN/BRL on/offramps via SPEI/Pix; Tron in custodial wallets.
- **March 17, 2026:** Mastercard announces $1.8B BVNK acquisition — direct competitor consolidation, validating the space.
- **March 23, 2026 (changelog):** Scoped API keys (granular permissions); GBP via FPS goes GA.
- **March 24, 2026 (changelog):** Prefunded Account API deprecated in favor of Bridge Wallets.
- **March 27, 2026 (changelog):** **Tempo Mainnet GA on Bridge** — full suite (onramps, offramps, wallets, virtual accounts, issuance, cards). Refund states (`refund_in_flight`, `refund_failed`).

### Q2 2026: Sessions 2026 + Multichain Sprint
- **April 1, 2026 (changelog):** Fixed-fee monetization for Virtual Account onramps (beta).
- **April 3, 2026 (changelog):** USDC on **HyperEVM** added.
- **April 20, 2026 (changelog):** USDC on **Sui** + Memoless Stellar deposits (muxed addresses).
- **April 22, 2026 (changelog):** Transfers now reflect actual rail received (`payment_received_rail` ≠ `payment_rail` if ACH covers a wire-intent transfer).
- **April 27, 2026 (changelog):** USDC and **usDCBL on Aptos** added; Deactivate endpoint for external accounts.
- **April–May 2026: Stripe Sessions 2026** — [Stripe announces 288 launches](https://stripe.com/newsroom/news/sessions-2026):
  - Bridge supports Tempo, Plasma, Celo, Sui as supported blockchains
  - Open Issuance expanded with new business types (treasury, banks)
  - Stablecoin-backed cards GA for spend
  - Stripe accepts stablecoin payments in **32 additional markets**
  - Privy "digital asset accounts" — hold/move/grow stablecoin balances anywhere
  - Privy → Morpho integration: idle balances earn yield via curated DeFi vaults
  - Machine Payments Protocol (MPP) — co-authored Stripe + Tempo, agentic micropayments / recurring payments
  - Universal Commerce Protocol with Google (Gemini app + AI Mode checkout)

---

## 3. The Roadmap (Stated and Inferred)

| Item | Status (May 2026) | Source |
|---|---|---|
| Bridge National Trust Bank operational | OCC conditional approval Feb 12; awaiting final approval. Erebor precedent ≈4 months → likely **mid-to-late 2026 opening** | [OCC CD #1365](https://www.occ.gov/topics/charters-and-licensing/interpretations-and-decisions/2026/cd1365.pdf) |
| Visa × Bridge 100+ countries | Live in 18, target end of 2026 for 100+ across Europe, APAC, Africa, ME | [Visa PR Mar 2026](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22206.html) |
| Tempo migration plan | GA on Bridge Mar 27, 2026; flagged as preferred chain for agentic payments and predictable-fee global payouts | Bridge changelog |
| Payoneer launch | Q2 2026 select markets; broader rollout through year | [Payoneer PR Feb 2026](https://investor.payoneer.com/news-releases/news-release-details/payoneer-launch-stablecoin-capabilities-powered-bridge-bringing) |
| Open Issuance pipeline | Decibel (usDCBL on Aptos) live Feb 2026; treasury-issuer + bank-issuer customers in beta per Sessions 2026 | Sessions 2026 |
| New product categories revealed | Machine Payments Protocol (agentic micro/recurring payments); stablecoin "digital asset accounts" via Privy + Morpho yield; Universal Commerce Protocol with Google | Sessions 2026 announcements |
| New fiat rails likely next | Strong signals around COP (Bre-B), additional APAC rails, more LATAM (CLP, ARS) given Visa card geography | Inferred from Visa expansion + Bre-B Sept 2025 launch |

---

## 4. Pivots and Walked-Back Decisions

| Decision | Date | What Happened |
|---|---|---|
| **The NFT pivot** | May 2022 | Pivoted away from "buy NFTs with your bank account" idea after a few weeks. Per Abrams in *Cheeky Pint*: "terrible idea" — but during the build they discovered building products with stablecoins is "very difficult," which seeded the eventual focus. |
| **Wallets-as-a-Service rejected** | Mid-2022 | Bridge briefly considered building Privy's eventual product. Abrams called WaaS a "tar pit" and walked away. Stripe later acquired Privy separately (June 2025) and kept it independent. |
| **Prefunded Accounts deprecated** | March 24, 2026 | Bridge officially deprecated Prefunded Accounts API; future investment goes to Bridge Wallets. Existing API supported indefinitely but no new features. |
| **DELETE-as-deactivate documentation correction** | April 27, 2026 | DELETE on `external_accounts` was historically labeled "Deactivate" but actually soft-deletes. New explicit `/deactivate` endpoint introduced; docs corrected. (Minor but a real "we got this wrong" cleanup.) |
| **Memo-only Stellar deposits → muxed addresses** | April 20, 2026 | Original Stellar integration required memos; added memoless `memoless_to_address` to handle wallets that don't support muxed addresses. Memo path retained. |
| **Bitcoin not pursued** | Ongoing | Despite Stripe earlier pulling out of Bitcoin payments in 2018 and "stablecoin volume in week 1 exceeded all-time BTC volume" per Patrick Collison, Bridge has never added BTC support. Pure stablecoin focus. |

---

## 5. Strategic Decisions Visible in the Timeline

**Why USDB before Open Issuance? Why May 2025?**
USDB at Sessions 2025 (May 7) was the proof-of-concept stablecoin: it demonstrated Bridge's reserve-management + reward-sharing model with a Bridge-branded coin before opening the platform to outside issuers. The launch was intentionally aligned with Stablecoin Financial Accounts (also May 7) — Stripe needed *its own* stablecoin in those accounts to share economics with customers. Open Issuance came 5 months later (Sept 30, 2025), *after* USDB had operational miles, and *with* Phantom's CASH as the headline launch partner — so Bridge could point to "real customer, working at scale" rather than "we built it for ourselves." The May timing also locked in 101-country distribution before competitors (Circle, Paxos, BVNK) caught up.

**Why apply for OCC charter in October 2025?**
Bridge filed October 14, 2025 — eight months after Stripe completed the acquisition, ~6 weeks after Open Issuance launched, and shortly after the OCC began conditionally approving stablecoin trust charters in December 2024–early 2025 (Circle, Ripple, Paxos, BitGo, Fidelity Digital Assets all got nods around that window). Bridge's filing was timed to (a) ride the regulatory window opened by the GENIUS Act discussions, (b) get bank-grade reserve custody internalized so it doesn't depend on Lead Bank for the long term, and (c) match the trust-charter posture of competitors before they could differentiate on regulation. Conditional approval came Feb 12, 2026 — about four months later, consistent with peer timelines.

**Why launch Tempo with Paradigm + OpenAI/Anthropic instead of going alone?**
Tempo was announced Sept 4, 2025 — *before* Open Issuance (Sept 30). The decision to bring in Paradigm (Matt Huang co-leading) plus Anthropic, OpenAI, Coupang, DoorDash, Mercury, Nubank, Revolut, Shopify, Standard Chartered, and Visa as launch partners served three purposes: (1) credibility — a Stripe-only chain would look like a captive walled garden; (2) demand-side commitments before mainnet — agentic payments from OpenAI/Anthropic need a chain optimized for sub-second microtransactions, and these partners co-design rather than just adopt; (3) regulatory cover — having Deutsche Bank and Standard Chartered in the founder set diffuses any "Stripe is becoming a bank" narrative. Bridge subsequently became Tempo's day-one orchestration layer (GA March 27, 2026).

**Why let Privy stay independent under Stripe?**
Privy was acquired June 11, 2025 but explicitly kept independent. The split: Bridge owns custody, fiat onramps, compliance, and stablecoin issuance; Privy owns non-custodial wallet UX. Forcing a merge would have collapsed Privy's positioning to neutral wallet infra (it serves OpenSea, Coinbase Ventures portfolio companies, and 75M+ wallets). By keeping Privy independent, Stripe gets to (a) sell to Bridge's competitors via Privy, (b) maintain Privy's ecosystem trust, and (c) get the "wallet + stablecoin + fiat" stack via API integration rather than legal entity merger. The Sessions 2026 announcement confirmed this: Privy now offers "digital asset accounts" (custody-light) with Morpho yield — a product Bridge would never offer directly because of its trust-charter posture.

---

## 6. Chain Integration Order (Best-Reconstructed)

Bridge's full chain history isn't all in the public changelog (which only goes back to July 2025), but combining the changelog, blog posts, sitemap, and press, the order is roughly:

| # | Chain | First Supported | Stablecoins | Strategic Reason |
|---|---|---|---|---|
| 1 | **Ethereum** | 2023 (private beta) | USDC, USDT, PYUSD, EURC | Default Day-1 chain; required for institutional credibility |
| 2 | **Polygon** | 2023 | USDC | Low-fee EVM for early developer demand |
| 3 | **Solana** | 2023 | USDC | Coinbase + Phantom routing |
| 4 | **Stellar** | Late 2023 / Q1 2024 | USDC | Airtm partnership for LATAM payouts (March 2024 launch) |
| 5 | **Base** | 2024 | USDC | Coinbase use case (USDT-Tron ↔ USDC-Base) |
| 6 | **Arbitrum** | 2024 | USDC, USDT | EVM coverage |
| 7 | **Optimism** | 2024 | USDC | EVM coverage |
| 8 | **Avalanche** | 2024 | USDC, USDT | EVM coverage |
| 9 | **Tron** | 2024 (orchestration); **May 13, 2025** in-house infra | USDT.trx | Tron hosts >$77B USDT — over half the total supply; SpaceX/Starlink emerging-market routing required it |
| 10 | **HyperEVM** | April 3, 2026 | USDC | Hyperliquid customer (USDH issuer) needed it |
| 11 | **Sui** | April 20, 2026 | USDC, USDsui | USDsui Open Issuance launch (Nov 2025) needed native USDC orchestration |
| 12 | **Aptos** | April 27, 2026 | USDC, usDCBL | Decibel mainnet launch with usDCBL Open Issuance customer |
| 13 | **Plasma** | January 29, 2026 | USDT | USDT-optimized chain; zero-fee transfers |
| 14 | **Celo** | February 9, 2026 | USDC.Celo | Mobile-first emerging-market story |
| 15 | **Tempo** | March 27, 2026 | (full Bridge stack) | Stripe's own chain; agentic payments |
| 16 | **Linea** | Roadmap (Sessions 2026 implied) | TBD | EVM L2 coverage for enterprise customers |

**USDG (Global Dollar) on Solana** added Jan 20, 2026 was a stablecoin addition, not a new chain.

---

## 7. Fiat Rail Integration Order

| # | Rail | Date Added | Banking Partner | Strategic Reason |
|---|---|---|---|---|
| 1 | **USD ACH** | 2023 | Lead Bank (eventual) | Foundation US rail |
| 2 | **USD Wire** | 2023 | Lead Bank | Higher-value transfers |
| 3 | **EUR SEPA** | 2024 | Bridge Building Sp. z o.o. (EU entity) | Required for EU customers, virtual IBANs |
| 4 | **MXN SPEI** | April 28, 2025 | Local Mexico partner | Latam corridor; Visa card LATAM rollout demanded it |
| 5 | **BRL Pix** | November 17, 2025 | Local Brazil partner | LATAM-2 corridor; cards expansion |
| 6 | **GBP Faster Payments (FPS)** | January 23, 2026 (beta) → March 23, 2026 (GA) | UK partner | EU-adjacent expansion; Visa cards Europe rollout |
| 7 | **USDT × MXN/BRL on/offramps** | March 9, 2026 | Same as above | Tron-native flows for LATAM remittances |

**Implied next:** COP via Bre-B (Colombia, launched Sept 2025), additional APAC rails (Visa expansion implies it), Argentine/Chilean rails.

---

## 8. Stablecoin Issuance Customers (Open Issuance)

| Customer | Stablecoin | Launch Date | Chain(s) | Reserve Structure | Notable |
|---|---|---|---|---|---|
| **Bridge (self)** | USDB | May 7, 2025 | All Bridge-supported chains | Cash + BlackRock short-duration MMFs | First of its kind — proved the model; rewards shared with developers |
| **Hyperliquid** (built by Native Markets) | USDH | Mid-2025 (pre-Open Issuance), migrated Sept 30 | HyperCore, HyperEVM | 1:1 backed | Native chain stablecoin |
| **Dakota** | (Dakota stablecoin) | 2025 (pre-Open Issuance) | Multi | Standard Bridge reserves | Stablecoin dollar-bank product |
| **Slash** | (Slash stablecoin) | 2025 | Multi | Standard | Fintech stablecoin |
| **Lava** | (Lava stablecoin) | 2025 | Multi | Standard | Fintech use |
| **Takenos** | (Takenos stablecoin) | 2025 | Multi | Standard | LATAM payments |
| **Phantom** | CASH | September 30, 2025 (Open Issuance launch) | Solana + EVM | Bridge-managed | Headline launch partner; 15M+ wallet users |
| **MetaMask** (with M0) | mUSD | 2025 (post-Open Issuance) | Linea-first, multi | M0-architected | First self-custodial wallet native stablecoin |
| **Sui** | USDsui | November 12, 2025 | Sui native | Bridge reserves | Native chain stablecoin, U.S.-compliant, reward-bearing |
| **Decibel (Aptos)** | usDCBL | February 25, 2026 | Aptos | Cash + short-term US Treasurys, yield retained by protocol | Pre-mainnet stablecoin for perpetuals collateral |

Reserves overall: BlackRock (treasuries), Fidelity (treasuries), Superstate (tokenized treasuries), Lead Bank (cash for liquidity).

---

## 9. Bridge Blog: Categorized Read

From the [bridge.xyz sitemap](https://www.bridge.xyz/sitemap.xml) (33 posts across blog + news as of May 2026):

### Product Announcements (15)
- *Introducing Bridge* (Aug 29, 2024) — public launch, $58M funding
- *Building a Bigger, Better Bridge* (Oct 22, 2024) — Stripe acquisition response
- *MXN FX, Now Live in Mexico* (Apr 28, 2025)
- *USDB* (May 7, 2025)
- *Tron Support on Bridge* (May 13, 2025)
- *Stablecoin-backed Cards Integrated with Stripe Issuing*
- *Bridge Joins Solana Developer Platform*
- *Introducing Open Issuance* (Sept 30, 2025)
- *Why a World with Multiple Stablecoins Makes Sense*
- *Powering the Next Wave of Digital Asset Utility with Cards*
- *Everything You Can Now Do in the Bridge Dashboard*
- *Stablecoin-Backed Cards Are Now Integrated with Stripe Issuing*
- *Bridge Receives OCC Conditional Approval to Organize a Federally Chartered National Trust Bank* (Feb 17, 2026)
- *The Last Mile: How Card Programs Are Turning Stablecoins into a Real Utility*
- *5 Benefits of Launching Your Own Stablecoin and 5 Things to Consider*

### Customer Stories / Case Studies (8)
- *Airtm Case Study* — LATAM payouts on Stellar
- *Cenoa Case Study* — emerging markets dollar bank
- *Dakota Case Study* — stablecoin business banking
- *Meow Case Study* — treasury management
- *Slash Case Study* — fintech card program
- *Unlocking Global Spending: Chipper Cash* — Africa cards
- *Turning Global Payments into Everyday Spending: Morse* — unified financial experience
- *How Airtm Helps Users Spend Digital Earnings with Cards*

### Strategic / Thought Leadership (10)
- *The Real Reason People Are Using Stablecoins*
- *Why Enterprises Are Exploring Their Own Stablecoin*
- *Tokenized: State of Play in 2024 Stablecoin Payments*
- *Circle Executive Insights: State of the USDC Economy 2025*
- *Cambrian Fintech with Rex Salisbury — Zach Abrams Interview*
- *On the Brink: Moving Money with Zach Abrams*
- *Unchained Podcast with Zach Abrams*
- *Bridge on Fortune*

Plus a deep "Learn" library (~17 educational posts on stablecoin payments, infra, regulations, wallets) — content marketing aimed at enterprise prospects.

---

## 10. Stripe Sessions 2025 + 2026 — What Was Announced About Bridge

### Stripe Sessions 2025 (May 6-8, 2025, San Francisco)
Per [Stripe newsroom](https://stripe.com/newsroom/news/sessions-2025):
1. **Stablecoin Financial Accounts in 101 countries** — businesses hold balances in USDC + USDB, receive funds on crypto and fiat rails (ACH, SEPA), send stablecoins globally. *Powered entirely by Bridge.*
2. **USDB launch** — Bridge's own stablecoin debuts.
3. **Expanded acceptance** — Stripe accepts USDC stablecoin payments in ~70 markets.
4. Bridge-Visa partnership previewed (announced 1 week earlier, Apr 30).
5. AI Foundation Model for Payments — adjacent but interrelated since agentic flows would later use Bridge.

### Stripe Sessions 2026 (April 28 – May 1, 2026)
Per [Stripe blog: Everything we announced at Sessions 2026](https://stripe.com/blog/everything-we-announced-at-sessions-2026) and [288 launches newsroom](https://stripe.com/newsroom/news/sessions-2026):
1. **Bridge multichain expansion**: Tempo, Plasma, Celo, Sui all supported.
2. **Open Issuance expansion** — businesses (not just crypto-native) can launch own stablecoins; treasury-management and bank issuer use cases revealed.
3. **Stablecoin-backed cards GA** — recipients spend funds locally or globally.
4. **32 additional markets** for stablecoin acceptance.
5. **Privy "digital asset accounts"** — hold/move/grow stablecoin balances anywhere.
6. **Privy + Morpho** — earn yield on idle balances via curated DeFi vaults.
7. **Machine Payments Protocol (MPP)** — co-authored by Stripe + Tempo. Microtransactions, recurring payments, agentic use cases.
8. **Universal Commerce Protocol (UCP)** with Google — checkout via Gemini app and AI Mode (the agentic-commerce extension of OpenAI's ACP from Sept 2025).
9. **Self-serve card programs in minutes** — for humans and AI agents, prebuilt templates.

Net read: Sessions 2025 was *"Bridge is now Stripe's stablecoin OS for businesses."* Sessions 2026 was *"Bridge is now Stripe's stablecoin OS for businesses **and AI agents**, on Stripe's own chain."*

---

## Sources (Primary)
- [Bridge changelog](https://apidocs.bridge.xyz/changelog/changelog) — primary source for July 2025–April 2026 entries (older entries not publicly indexed)
- [Bridge sitemap](https://www.bridge.xyz/sitemap.xml) — full blog/news inventory
- [Wayback Machine — bridge.xyz Sept 2022](http://web.archive.org/web/20220906213505/https://www.bridge.xyz/) and [March 2023](http://web.archive.org/web/20230321181446/https://www.bridge.xyz/) — confirmed product positioning timeline
- [Stripe newsroom: Bridge acquisition completion (Feb 4, 2025)](https://stripe.com/newsroom/news/stripe-completes-bridge-acquisition)
- [Stripe newsroom: Sessions 2025](https://stripe.com/newsroom/news/sessions-2025) and [Sessions 2026](https://stripe.com/newsroom/news/sessions-2026)
- [Bridge blog: Introducing Open Issuance](https://www.bridge.xyz/news/introducing-open-issuance), [USDB](https://www.bridge.xyz/news/usdb), [Tron](https://www.bridge.xyz/news/tron), [MXN FX](https://www.bridge.xyz/news/mxn-fx), [Building a Bigger Better Bridge](https://www.bridge.xyz/news/building-a-bigger-better-bridge), [Introducing Bridge](https://www.bridge.xyz/news/introducing-bridge)
- [Cheeky Pint episode — Abrams + Stern](https://cheekypint.substack.com/p/stablecoin-special-zach-abrams-bridge) — NFT pivot story
- [Fortune — $1.1B Stripe acquisition](https://fortune.com/crypto/2024/10/22/stripe-announces-1-1-billion-acquisition-of-stablecoin-start-up-bridge/)
- [Architect Partners — Stripe-Bridge MA Alert](https://architectpartners.com/wp-content/uploads/2024/10/MA-Alert_Stripe_Bridge.pdf)
- [Visa × Bridge initial partnership (Apr 30, 2025)](https://stripe.com/newsroom/news/bridge-partners-with-visa) and [expansion (Mar 3, 2026)](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.22206.html)
- [OCC Corporate Decision #1365 (Feb 2026)](https://www.occ.gov/topics/charters-and-licensing/interpretations-and-decisions/2026/cd1365.pdf)
- [TechCrunch — Tempo launch with Anthropic/OpenAI/Paradigm (Sept 4, 2025)](https://techcrunch.com/2025/09/04/stripe-enlists-a-whos-who-including-anthropic-openai-and-paradigm-to-build-a-new-blockchain/)
- [CoinDesk — Sui USDsui (Nov 12, 2025)](https://www.coindesk.com/business/2025/11/12/sui-launches-native-stablecoin-usdsui-using-bridge-s-open-issuance-platform)
- [Payoneer × Bridge (Feb 17, 2026)](https://investor.payoneer.com/news-releases/news-release-details/payoneer-launch-stablecoin-capabilities-powered-bridge-bringing)
- [Stripe acquires Privy (June 11, 2025)](https://www.bloomberg.com/news/articles/2025-06-11/payment-company-stripe-to-acquire-crypto-wallet-provider-privy)
- [Wirex × Bridge US expansion (Feb 27, 2025)](https://www.prnewswire.com/news-releases/wirex-announces-the-expansion-of-its-stablecoin-payment-platform-to-the-us-in-partnership-with-bridgexyz-302387674.html)
- [Decibel × Bridge usDCBL (Feb 25, 2026)](https://www.coindesk.com/business/2026/02/25/perpetuals-exchange-decibel-goes-live-on-aptos-following-usd50-million-in-pre-deposits)
- [Tron × Bridge integration (May 2025)](https://trondao.medium.com/tron-network-strengthens-global-payment-infrastructure-as-bridge-a-stripe-company-expands-e22e986c8a46)
- [Sequoia: Partnering with Bridge](https://sequoiacap.com/article/partnering-with-bridge-a-better-way-to-move-money/)

---

**Key finding:** Bridge's product evolution has three distinct chapters — (1) **2022–2023 quiet build** after a fast NFT pivot, where the Orchestration + Issuance two-pillar pitch was already locked in by March 2023; (2) **2024 commercial breakout** culminating in the $1.1B Stripe deal driven by SpaceX/Coinbase scale; (3) **2025–present Stripe-era expansion** at almost stunning velocity — USDB, Stablecoin Financial Accounts, Tron in-house infra, Visa, Open Issuance, OCC charter, Tempo, all in 13 months. The roadmap signal is clear: Bridge is becoming a **federally-chartered, multi-chain, agentic-payments-ready stablecoin bank** that sits underneath all of Stripe's stablecoin and AI-commerce surface area, with explicit positioning as the issuance + settlement layer for Tempo and the agentic Machine Payments Protocol.
