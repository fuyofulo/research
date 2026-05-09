# Ramp Network (rampnetwork.com) — Research Folder

Compiled May 2026 by deep-dive playbook (5 parallel research streams).

> **Disambiguation:** This folder is exclusively about **Ramp Network** (ramp.network / rampnetwork.com), the Warsaw/London-founded fiat ↔ crypto on/off-ramp company. It is **not** Ramp Business (ramp.com), the NYC corporate-card / spend-management company — see `../ramp-business/` for that one. The two companies have actually litigated over the "Ramp" trademark (USPTO TTAB, June 2022).

---

## Headline finding

Ramp Network is a **mid-tier, EU/UK-anchored, MiCAR-licensed fiat-to-crypto on/off-ramp** founded in 2017 by Polish entrepreneurs Szymon Sypniewicz (CEO until ~mid-2025; now Chairman) and Przemek Kowalczyk (current CEO). Total funding ~$134M across 4 rounds (last priced round Nov 2022 at ~$300M post). Genuine regulatory moat: **8th UK FCA cryptoasset registration ever (Aug 2021), MiCAR CASP authorisation via Central Bank of Ireland Dec 2025, FinCEN MSB + 9 US state MTLs, SOC 2 Type II (Jun 2024)**. ~150 wallet/dApp partners (MetaMask, Trust Wallet, Brave, Ledger, Argent, Sorare, Axie, 1inch, Coco Wallet) — but partnerships have all become non-exclusive aggregator slots; Phantom (the dominant Solana wallet) has never integrated. April 2026 strategic pivot: launched its own consumer self-custodial multichain wallet, putting it in partial competition with the wallet partners that drive its volume. Most likely 18–24 month outcome: takeover candidate by a Tier-2 acquirer wanting EU regulatory rails.

The "honest one-liner": *Ramp Network is a top-3 European fiat-to-crypto on/off-ramp widget. It sits inside about a hundred wallets and dApps; it's MiCAR-licensed in Ireland and FCA-registered in the UK; it ships crypto non-custodially to your address; its all-in card cost is around 5–6% (a 3.9% disclosed fee plus an undisclosed FX/asset spread); and it works in roughly 130 countries for cash-out and 150 for buying with caveats. It's competent, reasonably trusted, mid-priced, and fighting Stripe-Bridge above it and Onramper-aggregated commodity providers below it.*

---

## Folder structure

```
companies/ramp-network/
├── README.md                   ← you are here
├── deep_dive.md                ← founders, funding, legal entities, regulatory licenses by jurisdiction
├── architecture.md             ← product SKUs, banking partners, PSP, chains, KYC tiers, REST API, SDKs, custody
├── use_cases_and_examples.md   ← named wallet/dApp customers, end-user money paths, customer losses
├── marketing_vs_reality.md     ← 25-claim audit, dual positioning, moat analysis, red/green flags
├── developer_experience.md     ← widget DX, sandbox, webhooks (ECDSA secp256k1), peer comparison vs MoonPay/Coinbase/Stripe
└── transcripts/                ← (empty; founder podcast .txt files would go here)
```

---

## File index

- **[deep_dive.md](deep_dive.md)** — Polish founders Szymon Sypniewicz (ex-Norton Rose Fulbright lawyer) and Przemek Kowalczyk (BCG, Warsaw blockchain hub). UK Companies House #11850124 (Ramp Swaps Limited, 27 Feb 2019); EU entity Ramp Swaps (Ireland) Limited (CBI ref C515693); US entity Ramp Swaps LLC (Miami FL, EIN 87-2664742); Polish Ramp Link sp. z o.o. (KNF AISP3/2020). Funding: €1M pre-seed 2018 → $10.1M Seed (NfX + Galaxy Digital, Jun 2021) → $52.7M Series A (Balderton, Dec 2021, ~$300M post) → $70M Series B (Mubadala + Korelya, Nov 2022) — total $134M. **Quiet CEO transition between mid-2024 and mid-2025** (Szymon → Przemek), no formal press release. Self-claimed: 8M+ customers, 150+ countries, 100+ assets, 160+ employees. No public layoffs disclosed despite 2022-2024 crypto winter. 2025-2026 pivot to consumer multichain wallet (April 2026).

- **[architecture.md](architecture.md)** — Three-layer stack: hosted/overlay/embedded widget + native mobile SDKs (iOS/Android/RN/Flutter) + REST API v3 (`api.ramp.network/api/host-api/v3`). Banking partners + PSPs **not publicly disclosed** — most likely Checkout.com card acquirer (rumoured), TrueLayer/Yapily Open Banking provider (unconfirmed). **Solana on-ramp + off-ramp both first-class** (SOL, USDC-SPL, USDT-SPL, JUP, BONK). 16 chains for delivery, 38+ assets for off-ramp, 40+ fiat currencies. **0.99% off-ramp fee** (best in class, vs MoonPay ~1%+). Card 2.9–4.9%, bank transfer from 0.49% (with €2.49 SEPA minimum that's a 10% floor on small buys). KYC handled in-house (Onfido-class vendor + Sumsub interop). No Token-2022, no x402/AP2 commitment, no published custody architecture.

- **[use_cases_and_examples.md](use_cases_and_examples.md)** — Anchor wallet partners: MetaMask, Trust Wallet, Brave, Ledger, Argent (now Ready), Opera, 1inch, Zerion, Coco Wallet, SWEAT. Web3 games: Sorare (case study, Premier League fans), Axie Infinity (60→19 onboarding steps), Loopring (20K txns / 90 days at $300 avg). L1 partners: Solana Foundation (listed on solana.com/solanaramp), Avalanche, Polygon, Polkadot Asset Hub via Velocity Labs (Apr 2024), zkSync Era (Ramp was first onramp), LUKSO, Telos, NEAR, Plasma. Six end-user money-path walkthroughs: Argent/Léa (Lyon EUR→ETH StarkNet), Trust Wallet/Diego (Madrid SEPA→BNB), Brave/Aiko (Tokyo JCB→BTC), Loopring/Tomek (Warsaw PLN→USDC L2), Sorare/James (Manchester GBP→ETH StarkEx), Axie/Maria (Manila USD→AXS Ronin). **Phantom never integrated** — biggest single Solana-dev gap. ~10K Trustpilot reviews ~3.5–4.0 stars. No documented public competitor migration stories either way.

- **[marketing_vs_reality.md](marketing_vs_reality.md)** — 25-claim adversarial audit. Survives: SOC 2 Type II Jun 2024 ✅, MiCAR CASP Dec 2025 ✅, UK FCA registration since Aug 2021 ✅, non-custodial architecture ✅, real wallet partnerships ✅. Doesn't survive: "8 million customers" (no MAU breakdown, possibly cumulative), "150+ countries" (mixes reachability with full functionality), "first/pioneer" claims (multiple unverifiable), "all 50 US states" (only 9 confirmed MTLs), "lowest fees" (Onramper aggregator data routinely shows competitors beating Ramp on net-received). **Brand-confusion problem with Ramp Inc. (ramp.com)** is real and not Ramp Network's fault. Hidden FX spread brings effective card cost to 5–6% all-in (vs 3.9% headline). Most plausible 2027 outcome: **acquisition by Tier-2 player** (Robinhood, Kraken, Coinbase non-US, payments processor) leveraging the FCA + MiCAR + SOC 2 stack.

- **[developer_experience.md](developer_experience.md)** — Widget SDK (`@ramp-network/ramp-instant-sdk` v6.2.0, ~4-8K weekly DL) is solid. **Biggest DX friction: API key requires email + form, no self-serve dashboard** (24-72h wait). Sandbox at `app.demo.ramp.network` is real but weakest of the major five (no test cards, KYC still required, no programmatic webhook simulator). REST API v3 has 5 endpoints, no OpenAPI spec, no Postman collection, no idempotency keys, no published numeric rate limits. Webhooks use **ECDSA secp256k1** (unusual vs HMAC-SHA256 industry standard) — pros: no shared secret to leak, cons: harder one-line verification. Comparison matrix vs MoonPay / Transak / Onramper / Stripe Crypto / Coinbase On-Ramp shows Ramp losing on self-serve onboarding, OpenAPI, sandbox, idempotency, rate limits — winning on mobile SDK breadth (4 languages including Flutter) and 0-fee USDT/USD on Solana. Weekend integration feasible only if partner email submitted Friday morning.

---

## Solana-developer specific findings

If you came hunting AI × crypto opportunities (per the user's research thesis):

1. **No Solana-native wallet has a deep Ramp integration.** Phantom uses MoonPay+Coinbase+Stripe+Robinhood; Backpack and Solflare have their own provider stacks. The embedded-onramp slot in Solana wallets is **contested and provider-replaceable** — meaning routing/quote-aggregation logic on Solana is itself a product surface worth building.
2. **0-fee USDT↔USD on Solana via Ramp + Privy + Plasma launched 2025** is genuinely competitive for stablecoin-heavy products. ([The Defiant](https://thedefiant.io/news/defi/usdt-live-solana-plasma-ethereum-ramp-privy-rt2zgt))
3. **Ramp's emerging-markets lean (Coco Wallet LATAM, Pix, SPEI)** suggests the high-margin volume is shifting from "DeFi degens in London" to "remittance corridors via stablecoins" — different end-user persona than the MetaMask/Argent original wedge.
4. **For agent-payments / x402 / AP2**: Ramp Network has **not** publicly committed to any agent-payments protocol. There is space here for an x402 facilitator that pulls fiat onramp via Ramp under the hood, but Ramp itself is not building this surface.

---

## Sources used (top-tier)

Primary docs: `rampnetwork.com`, `docs.rampnetwork.com`, `support.rampnetwork.com`. Regulatory: UK FCA register (FRN 928783), Central Bank of Ireland (C515693), FinCEN MSB (#31000287566749), Companies House (#11850124).

Press: TechCrunch, CoinDesk, The Block, Sifted, Decrypt, Cointelegraph, Bitcoin.com News, Coinspeaker, Globenewswire, Benzinga, RTÉ.

Founder voice: DL News long-form Przemek interview (2025), DailyCoin/Bitget interview, EUVC Pod E322 (Sypniewicz), Solfate-style Polish podcasts.

Code: GitHub `RampNetwork/*` org (38 stars on instant-sdk), npm `@ramp-network/ramp-instant-sdk`, pub.dev `ramp_flutter`, Bundlephobia, Socket security profile.

Comparisons: Onramper, Paybis, Crossmint, Bitget Academy.

Sentiment: Trustpilot (~10K reviews), Reddit r/cryptocurrency.

---

## How to use this folder

If you have **30 seconds**, read the headline above and the file index. If you have **5 minutes**, read this README + `marketing_vs_reality.md`. If you're **integrating Ramp into a Solana dApp/wallet**, read `developer_experience.md` + `architecture.md` first. If you're **evaluating Ramp as a competitor or potential acquirer target**, read `marketing_vs_reality.md` + `deep_dive.md`. If you're **researching AI × crypto / agent payments**, read `developer_experience.md` §19 ("AI x crypto angle") and consider what Ramp's silence on x402/AP2 means.
