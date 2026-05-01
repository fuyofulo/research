# AI × Crypto Research

Ongoing research into problems in the AI space that crypto/blockchain can solve. Bias toward niche, under-explored problems over rehashed top-down theses.

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
│   │   └── transcripts/
│   └── blockworks/
│       ├── deep_dive.md
│       └── transcripts/
└── plans/                                    → Strategic plans (separate from research)
```

---

## Index

### Markets

| File | Topic | Date |
|------|-------|------|
| [markets/ai_crypto_landscape.md](./markets/ai_crypto_landscape.md) | Top-down landscape: 15 categories, money flows, real vs. narrative, emerging themes | 2026-04-26 |
| [markets/agent_payments/solutions.md](./markets/agent_payments/solutions.md) | x402, AP2, Stripe, Skyfire, Crossmint, Privy, Catena, Visa/MC and more — tech, teams, funding, traction. | 2026-04-26 |
| [markets/agent_payments/compliance.md](./markets/agent_payments/compliance.md) | US, EU, other jurisdictions. The 5 sharpest unsolved compliance problems where startups can build. | 2026-04-26 |
| [markets/payfi/liquidity_models.md](./markets/payfi/liquidity_models.md) | **Liquidity design space for cross-border payment orchestrators.** 9 capital-sourcing mechanisms + 5 capital-efficiency levers + 5 risk-transfer mechanisms. 3 alternative architectures that could outperform Credible. | 2026-05-01 |

### Companies

| File | Topic | Date |
|------|-------|------|
| [companies/credible-finance/deep_dive.md](./companies/credible-finance/deep_dive.md) | B2B stablecoin payment-orchestrator. Founders, funding, customers, tech stack, business model, compliance. **Cash-flow positive.** *(See `liquidity_architecture.md` for major architecture corrections.)* | 2026-04-27 |
| [companies/credible-finance/how_to_build.md](./companies/credible-finance/how_to_build.md) | Linear playbook to build Credible from scratch — phases, dependencies, vendors, costs, hiring, marketing. Year-1 cash needed: ~\$1–3.2M. | 2026-04-29 |
| [companies/credible-finance/liquidity_architecture.md](./companies/credible-finance/liquidity_architecture.md) | **Liquidity & tech deep dive.** PayFi Vault is on Hedera via Byzanlink (not Solana), ERC-4626/7540, ~16% est APY. Multi-chain: Hedera (live), Solana (Aethir), Plume (roadmap). | 2026-04-30 |
| [companies/credible-finance/architecture.md](./companies/credible-finance/architecture.md) | **Complete architecture in Mermaid diagrams.** All 6 product flows mapped. Plus cross-chain split, compliance stack, end-to-end transaction trace. Confidence-labeled. | 2026-05-01 |
| [companies/blockworks/deep_dive.md](./companies/blockworks/deep_dive.md) | Crypto media/research/events. Founders Yanowitz + Ippolito. Bootstrapped 6yr → \$12M Series A 2023 → ~\$30M revenue 2025. Killed news division Oct 2025, pivoted to data + Lightspeed IR. | 2026-04-29 |
