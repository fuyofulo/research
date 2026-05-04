# Altitude (altitude.xyz) — Research Folder

Compiled May 2026 by deep-dive playbook (5 parallel research streams + 2 follow-ups).

---

## Headline finding

**Altitude is not its own company.** It is the flagship product of **Squads Labs** — the team behind Squads Protocol, Solana's dominant multisig / smart-account standard ($10B+ secured across 500+ orgs as of 2026). Altitude is a stablecoin-native USD/EUR business banking product (multi-currency accounts, ACH/Wire/SEPA + USDC/EURC, ~5% APY, batch payments, Bill Pay, corporate cards "coming soon"), self-custodial via Squads' formally verified Solana programs, with regulated banking rails plumbed through licensed PSP partners (Bridge/Stripe, MoonPay, Infinite, Due). Public launch Dec 2025; $200M+ processed by April 2026; total funding $42.9M with the latest $18M strategic round (Apr 2026) led by Solana Ventures.

The "honest one-liner": *Altitude is a slick, self-custodial business-account UX on top of partner stablecoin rails, built by the same team that runs Solana's leading multisig — currently doing ~$200M of self-reported throughput, paying ~5% USDC rewards funded by tokenized T-bill exposure, advertised as "your bank replacement" while explicitly disclosing it's an unregulated service that doesn't custody, issue, or redeem anything.*

---

## Folder structure

```
companies/altitude/
├── README.md                   ← you are here
├── deep_dive.md                ← company history, founders, funding, regulatory/legal
├── architecture.md             ← Solana programs, IDLs, PDAs, CPI graph, SDKs
├── use_cases_and_examples.md   ← named customers (Jupiter), persona walkthroughs, money paths
├── marketing_vs_reality.md     ← claim-by-claim audit, dual-positioning, moat analysis
├── on_chain_truth.md           ← program IDs, vault check, holder concentration, anomalies
├── developer_experience.md     ← Grid API quality, sandbox, KYB, SDK, pricing, gotchas
├── product_evolution.md        ← Q3-2021 hackathon → Dec-2025 Altitude launch (changelog)
└── transcripts/                ← (empty; founder podcast .txt files would go here)
```

---

## File index

- **[deep_dive.md](deep_dive.md)** — Squads Labs is the company; Altitude is the product. Founders Stepan Simkin (ex-Clifford Chance M&A lawyer, no prior Solana), Deni Ershtukaev, Sean Ganser. BVI-incorporated. $42.9M raised across 5 rounds (Oct 2021 → Apr 2026); cap table includes Solana Ventures, Multicoin, Coinbase Ventures, Haun Ventures, Electric Capital, Placeholder, Jump Crypto, Anatoly Yakovenko / Mert Mumtaz / Lucas Bruder as angels. **Holds zero financial licenses anywhere** — operates as "unregulated service" per its own ToS, with compliance delegated to PSP partners.

- **[architecture.md](architecture.md)** — Three-layer stack: Altitude (consumer app) → Grid (REST API) → Squads Smart Account Program on Solana (`SMRTzfY6DfH5ik3TKiyLFfXexV8uSG3d2UksSCYdunG`). No Altitude-branded program ID. The custody program is **Squads V4** (`SQDS4ep65T869zMMBKyuUq6aD6EgTu8psMjkvj52pCf`) — immutable since Nov 2024, audited 4× (OtterSec, Neodyme, Trail of Bits, Certora formal verification). Co-custodial "settings authority" model: user holds threshold-of-N approval, but Altitude is settings_authority for recovery / signer rotation. Includes full IDL parse, PDA seed schema, Mermaid CPI graph.

- **[use_cases_and_examples.md](use_cases_and_examples.md)** — Only **one** publicly named customer (Jupiter, via Kash Dhanda). Yield/integration partners: Kamino, Gauntlet, Plume, BlackRock-via-BUIDL. PSPs: Bridge, MoonPay, Infinite, Due. Four marketed personas (exporters, agencies, crypto-native co's, remote teams) — none with public testimonials beyond Jupiter. The data void itself is a finding: $200M throughput likely concentrated in <50 Solana-native protocols, not the long tail Squads markets.

- **[marketing_vs_reality.md](marketing_vs_reality.md)** — 25-claim audit table. Survives audit: Squads' formally-verified custody, real cap table, real self-custody architecture. Doesn't survive: "Banking" framing (it's not a bank), "CFO stack" (cards/bill-pay/accounting are roadmap), "trusted by leading companies" (no logo wall), "BlackRock-backed" (actual yield issuer never named), "Trade Any Asset" pitch (quietly removed between May 2025 and Dec 2025). Heavy Bridge/Stripe counterparty risk. Selimor Investments Limited as opaque operating entity.

- **[on_chain_truth.md](on_chain_truth.md)** — Standard rug-check playbook returns mostly N/A: no Altitude token, no airdrop, no vault PDAs to inspect, no DefiLlama listing (the "Altitude" on DefiLlama is a different EVM bridge). On-chain footprint = Squads V4 + SAP PDAs deployed by Altitude's backend keypair. The $200M throughput claim is plausible but not on-chain-verifiable without enumerating Altitude's deployer keypair. Squads V4 immutable + 4-firm audited; SAP audited but upgrade authority not yet burned. Five-minute verification recipe included.

- **[developer_experience.md](developer_experience.md)** — Grid is the developer API powering Altitude. Public OpenAPI 3.1 spec at `grid.squads.xyz/api-docs/openapi.json` — 51 paths, 211 schemas. Self-serve dashboard, sandbox/devnet/mainnet envs, idempotency keys, structured errors. **Embedded-wallet aggregation over Privy + Turnkey + Dynamic + passkey** (this resolves the open question from architecture.md). Sumsub-backed KYB. Pricing: Basic $0, Pro $499/mo, Enterprise custom — but **fiat rails, KYB, fee sponsorship, and multisig proposals are all enterprise-only**. Two genuine gaps: **no public webhooks**, **no documented rate limits**. SDKs: `@sqds/grid` 3.1.2 (~2.5k weekly DL), `@sqds/multisig` 2.1.4 (~26k weekly DL — load-bearing infra in Helium / Hyperlane / LayerZero / Solana Foundation explorer / sendai-fun). Verdict: strong yes for Solana-native B2B treasury / agent-payment products, no for self-serve fintech-with-fiat.

- **[product_evolution.md](product_evolution.md)** — Quarter-by-quarter changelog from the Q3-2021 Solana Season hackathon (unfinished DAO governance MVP) → V1 Feb 2022 → V3 late 2022 → V4 Oct 2023 → Fuse smart wallet Jun 2024 → Smart Account Program Q1 2025 → Grid API May→Sept 2025 → Altitude public launch Dec 2025 → $18M round Apr 2026. Includes killed/dropped features table ("Trade Any Asset" pitch dropped between May/Dec 2025; mobile DAO governance origin completely buried; Fuse demoted to plumbing under Altitude). Three rewrites of the on-chain program (V2→V3→V4→SAP), V4 immutable since Nov 22 2024.

---

## Sources used (top-tier)

Primary docs: `altitude.xyz`, `squads.xyz`, `developers.squads.so`, `grid.squads.xyz/api-docs/openapi.json`, `support-altitude.squads.xyz`, `squads.xyz/legal/altitude`.

Code: [Squads-Protocol GitHub org](https://github.com/Squads-Protocol) (V4, smart-account-program, squads-mpl, public-v4-client), [Squads-Grid GitHub org](https://github.com/Squads-Grid) (neobank-example-app), npm `@sqds/grid` + `@sqds/multisig`, crates.io `squads-multisig`.

Press: The Block, Blockworks, CoinDesk, Decrypt, PR Newswire, Crowdfund Insider, TechStartups (Apr 2026 funding round); Solfate Pod #33 (Sep 2023 founder long-form); Multicoin / Placeholder / Electric / Solana Ventures investment memos; Wayback Machine snapshots of altitude.xyz across 2025-2026.

On-chain: Solscan, SolanaFM, DefiLlama, Dune, Helius docs.

---

## How to use this folder

If you have **30 seconds**, read the headline above and the file index. If you have **5 minutes**, read this README + `marketing_vs_reality.md`. If you're **building on it**, read `developer_experience.md` first then `architecture.md`. If you're **evaluating it as a competitor or partner**, read `deep_dive.md` + `marketing_vs_reality.md` + `product_evolution.md`. If you're **a Solana developer wanting the technical truth**, read `architecture.md` + `on_chain_truth.md` + `developer_experience.md`.
