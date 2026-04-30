# AI × Crypto Research

Ongoing research into problems in the AI space that crypto/blockchain can solve. Bias toward niche, under-explored problems over rehashed top-down theses.

---

## Folder structure

```
research/
├── markets/                                  → Market & category research
│   ├── ai_crypto_landscape.md
│   └── agent_payments/
│       ├── solutions.md
│       └── compliance.md
├── companies/                                → Per-company deep dives
│   ├── credible-finance/
│   │   ├── deep_dive.md
│   │   ├── how_to_build.md
│   │   ├── liquidity_architecture.md
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
| [markets/agent_payments/compliance.md](./markets/agent_payments/compliance.md) | US (FinCEN, MSB, OFAC, GENIUS Act), EU (MiCA, PSD2/3, AI Act, GDPR), other jurisdictions. The 5 sharpest unsolved compliance problems where startups can build. | 2026-04-26 |

### Companies

| File | Topic | Date |
|------|-------|------|
| [companies/credible-finance/deep_dive.md](./companies/credible-finance/deep_dive.md) | B2B stablecoin payment-orchestrator. Founders, funding, customers, tech stack, business model, compliance. **Cash-flow positive.** *(See `liquidity_architecture.md` for major architecture corrections.)* | 2026-04-27 |
| [companies/credible-finance/how_to_build.md](./companies/credible-finance/how_to_build.md) | Linear playbook to build Credible from scratch — phases, dependencies, vendors, costs, hiring, marketing. Year-1 cash needed: ~\$1–3.2M. | 2026-04-29 |
| [companies/credible-finance/liquidity_architecture.md](./companies/credible-finance/liquidity_architecture.md) | **Liquidity & tech deep dive.** PayFi Vault is on Hedera via Byzanlink (not Solana), ERC-4626/7540, ~16% est APY. Multi-chain: Hedera (live), Solana (Aethir), Plume (roadmap). Co-lending model with named TradFi partners. Founder's real product is Credible Score, not payments. | 2026-04-30 |
| [companies/blockworks/deep_dive.md](./companies/blockworks/deep_dive.md) | Crypto media/research/events. Founders Yanowitz + Ippolito. Bootstrapped 6yr → \$12M Series A 2023 → ~\$30M revenue 2025. Killed news division Oct 2025, pivoted to data + Lightspeed IR. | 2026-04-29 |

---

## Key takeaways so far

**Credible Finance — quick read:**
- Real B2B stablecoin payment-orchestrator, NOT a Solana protocol despite branding ("Web 2.5" — DeFi for credit pool only, off-chain for settlements)
- Founder Shrikant Bhalerao: 14 years fintech, healthcare-financing exit in 2023, RBI NBFC director — senior operator
- **Cash-flow positive** at ~\$20M/month volume; \$60M+ processed in 11 months with **zero defaults**
- Real moat = ~4–5% better FX vs Wise/Remitly, enabled by USDC credit pool eliminating ACH pre-funding
- 16% fixed APY for USDC/USDT depositors funding the credit pool — rare "real-yield" stablecoin source
