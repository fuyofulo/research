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
│   └── credible-finance/
│       ├── deep_dive.md
│       └── transcripts/
└── plans/                                    → Strategic plans (separate from research)
```

**Conventions:**
- `markets/` for cross-cutting research on a category, vertical, or problem space
- `companies/` for deep dives on individual companies; transcripts kept inside the company folder
- New verticals get their own subfolder under `markets/`
- New companies get a kebab-case subfolder under `companies/`

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
| [companies/credible-finance/deep_dive.md](./companies/credible-finance/deep_dive.md) | B2B stablecoin payment-orchestrator. Founders, funding, customers, tech stack, business model, compliance. **Cash-flow positive.** | 2026-04-27 |

---

## Key takeaways so far

**AI × crypto landscape:**
- ~919 tracked AI-crypto projects, ~\$22-26B combined mcap
- ~40% of crypto VC went to AI-adjacent in 2025 (vs 18% in 2024)
- Real plumbing: DePIN GPU, agent payments, prediction markets, decentralized training
- Mostly narrative: AI agent launchpads (Virtuals, ai16z deflated), tokenized AI agents, most ZKML

**Agent payments reality check:**
- x402 has \$50M cumulative volume but real organic daily volume is ~\$14K
- Stripe quietly owns the entire stack post-Privy acquisition
- Card networks positioned to win consumer agentic commerce — they own dispute/chargeback infra
- Compliance is the wall: banks can't open accounts for AI agents
- Catena Labs is the dark horse — Sean Neville (USDC inventor) building a regulated AI-native FI

---

## File conventions

- Filenames are content-descriptive, kebab- or snake-case, no numeric prefixes
- Each `.md` is dated and self-contained — can be read standalone
- Sources linked inline; full source list at bottom of each file
- Founder/insider video transcripts saved as `.txt` next to the deep dive that uses them
