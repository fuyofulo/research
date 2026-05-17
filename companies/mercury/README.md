# Mercury (mercury.com) — Research Folder

Compiled May 2026 by deep-dive playbook (6 parallel research streams).

> **Disambiguation:** This folder is exclusively about **Mercury (mercury.com)**, the San Francisco-headquartered US startup banking platform founded by Immad Akhund. It is **not** Mercury Layer (Bitcoin statechain), Mercury Insurance, Mercury Systems (defense contractor), Mercury Marine, or Mercury Retirement. Cross-references to other research in this workspace: `../ramp-business/` (NYC corporate cards / spend management — same buyer persona, different surface), `../brex/` (acquired by Capital One April 2026 — Mercury's adjacent competitor for the corporate-card seat).

---

## Headline finding

Mercury is the **fastest-growing US business-banking platform that is actively transitioning from BaaS-on-partner-banks to its own OCC-chartered bank**. Founded 2017 by Immad Akhund (ex-Heyzap, YC), Max Tagher, and Jason Zhang; public launch May 2019. Total raised: ~$520M+ across Seed → Series A (Andreessen Horowitz, Sept 2019) → Series B (Coatue, 2021, $120M @ $1.6B post) → **Series C $300M March 26 2025 @ $3.5B post (Sequoia-led, first-ever Sequoia check on Mercury, includes secondary tranche)**. As of Q3 2025: **$650M annualized revenue, $248B 2025 transaction volume, ~$20B in deposits, 300K+ customers, four straight years of GAAP profitability** (per CEO Immad on Fortune 2025-11-07). **Mercury Bank N.A. received OCC conditional approval on April 27 2026** (HQ Utah; Jon Auxier ex-SoFi as proposed Bank CEO; FDIC + Fed sign-off pending). The charter ends the partner-bank dependency arc that defined the company's first seven years and is the dominant strategic event in Mercury's recent history.

Banking-rails stack today: **Choice Financial Group (Fargo ND)** + **Column N.A. (William Hockey, SF)** + **Patriot Bank N.A. (Stamford CT)** as active partners, with **Evolve Bank & Trust (Memphis TN)** winding down through end of 2025 post-Synapse. **Lithic (not Marqeta)** is the issuer-processor for both Mercury Debit and Mercury IO (Mastercard, exclusively). **Mercury Lending LLC (NMLS 2606284)** is Mercury's own balance-sheet subsidiary for Working Capital — unusual for the BaaS cohort. **Treasury** runs through **Apex Clearing** custody into **JPMorgan US Treasury Plus MMF + Morgan Stanley Ultra-Short Income (MULSX)**, $250K min, ~4.35% target net APY. **Mercury Vault** sweeps deposits across up to ~20 partner banks for $5M FDIC pass-through.

The "honest one-liner": *Mercury is a fast-growing US business-banking platform that started as the YC-default checking account and is becoming an actual chartered bank in 2026. It runs a no-fees, free-domestic-wires, software-first product on top of three FDIC partner banks (Choice, Column, Patriot), uses Lithic to issue Mastercards, custodies treasury cash at Apex into Vanguard/JPMorgan/Morgan Stanley MMFs, and runs its own lending balance sheet via Mercury Lending LLC. At Q3 2025 it's $650M annualized revenue, $248B annual transaction volume, ~$20B in deposits, 300K+ customers, and four straight years of GAAP profitability. The two real overhangs: (1) compliance debt from the Jan 2024 Choice FDIC consent order and the July 2024 mass closure of accounts across 13+ countries (Nigeria/Ukraine/Pakistan/Venezuela/Croatia/Philippines/Haiti), and (2) the agent-and-stablecoin gap — Mercury shipped a hosted first-party MCP server and a CLI, but Immad has publicly said "I don't think Claude is going to go build a bank," so the official rail is locked read-only, and Mercury has no x402, no Visa Intelligent Commerce / Mastercard Agent Pay participation, and no USDC/PYUSD custody.*

---

## Folder structure

```
companies/mercury/
├── README.md                   ← you are here
├── deep_dive.md                ← founders, funding, legal entities, OCC charter path, Choice consent order
├── architecture.md             ← banking partners, Lithic processor, Mercury Lending LLC, Apex treasury, API
├── use_cases_and_examples.md   ← Phantom, Linear, Supabase, ElevenLabs, Lovable, Hathora, CAPNOS, sentiment
├── marketing_vs_reality.md     ← 30-claim audit, "not-a-bank" disclaimer scrutiny, sweep arithmetic, Synapse blast radius
├── developer_experience.md     ← Mercury MCP (mcp.mercury.com), CLI (May 2026), API + sandbox, peer comparison
├── product_evolution.md        ← Q-by-Q changelog 2017→2026; killed features; SVB inflow; Synapse migration
└── transcripts/                ← (empty; founder podcast .txt files would go here)
```

---

## File index

- **[deep_dive.md](deep_dive.md)** — Founders Immad Akhund (Heyzap exit; YC), Max Tagher (CTO), Jason Zhang. Delaware C-corp Mercury Technologies, Inc. Funding arc: Seed → Andreessen Horowitz Series A $20M (Sept 2019) → Coatue Series B (2021, $1.6B post) → **Sequoia $300M Series C March 26 2025 at $3.5B** (Sequoia's first check on Mercury, partial secondary). **The widely-cited "NYT investigation" does not exist — the actual piece was The Information / Michael Roddan, March 28 2024**: "Inside Mercury's Stumble From Fintech Hero to Target of the Feds," which documented PO-box addresses, affiliate commissions to LLC University and Firstbase.io, a missed SAR on an attempted Cuba ATM transaction, and a Mercury-built compliance system that Choice never independently vetted. The **Choice Financial Group FDIC consent order (Jan 26 2024)** is directly traceable to Mercury onboarding practices — 4-year CIP lookback, AML/CFT committee, CDD overhaul. **Mercury Bank N.A. OCC conditional approval April 27 2026** (HQ Utah; Jon Auxier ex-SoFi as proposed Bank CEO). $650M annualized revenue Q3 2025; $248B 2025 volume; ~$20B deposits; 300K+ customers; 4 years GAAP profitable. **No CapitalG-led secondary exists in public reporting** — the $3.5B mark is the Sequoia round.

- **[architecture.md](architecture.md)** — **Lithic (NOT Marqeta)** is the issuer-processor for both Mercury Debit and Mercury IO (charge card). Mastercard-exclusive — no Visa SKU. **IO** issued by **Patriot Bank N.A. (Stamford CT)**; debit issued by **Choice + Column**. **Mercury Lending, LLC (NMLS 2606284)** originates Working Capital from Mercury's own balance sheet — distinct from deposit partners. **Treasury** stack: Apex Clearing custody → JPMorgan US Treasury Plus MMF + Morgan Stanley Ultra-Short Income (MULSX), $250K min, ~4.35% target net APY. **Mercury MCP is live** at `https://mcp.mercury.com/mcp` (34 tools, OAuth 2.0 + RFC 7591 Dynamic Client Registration, **read-only at launch by design**, HMAC-SHA256 webhook signing via `x-mercury-signature`). API at `api.mercury.com/api/v1`. **Glaring enterprise gap**: Mercury does NOT publicly document SAML/OIDC SSO at any plan tier — vs. Brex (Premium) and Ramp (all paid plans). No named Visa Intelligent Commerce or Mastercard Agent Pay participation. Mercury is technically ahead on MCP, behind on the network-level agentic-payments rails Ramp has locked in.

- **[use_cases_and_examples.md](use_cases_and_examples.md)** — Verifiable named customers with primary-source evidence: **Phantom** (Solana wallet, "perfect for web3 founders looking for a crypto-friendly and streamlined experience" — direct mercury.com/web3 quote), **Hathora** (Mercury Treasury case study with CEO Siddharth Dhulipalla; >90% funds parked in Treasury; runway extended 3 months), **CAPNOS** (Working Capital case study, third financing term), **Forage** (Mercury blog "Memory Bank" feature with CEO Ofek Lavian), **Lithic** (case study showing $248B transaction volume + 40% fraud reduction), and the marketing-confirmed quartet **Linear / ElevenLabs / Supabase / Phantom** from Mercury's Nov 2025 reference roster. Plus **Tempo, Decagon, Tennr, DeepScribe, Lovable**. **SVB inflow March 2023**: $2B in 5 days, 26K+ accounts in 4 months, 92% retention at 6 months. **Synapse fallout (May 2024)**: Mercury proactively migrated $3B off Synapse before the collapse — spared most customers but spawned a $50M dispute. **The single most damaging customer-sentiment finding**: the **July 2024 mass purge of non-US-founder accounts across 13+ countries** (Ukraine, Nigeria, Pakistan, Venezuela, Croatia, Philippines, Haiti, etc.) — driven by the Jan-2024 Choice consent order citing Mercury's role in opening "thousands of accounts using questionable methods to prove US presence" — covered as a brand-trust event by Sifted, TechCrunch, Kyiv Independent, Tech in Africa.

- **[marketing_vs_reality.md](marketing_vs_reality.md)** — 30-claim adversarial audit. Survives: free domestic wires ✅, $0 monthly fees ✅, four years GAAP profitable ✅, real Sequoia round ✅, MCP server live ✅. Doesn't survive: "the bank account for ambitious companies" 🔴 (Mercury is not a bank — yet — and customers were exposed to BaaS-middleware risk that 200K+ Yotta/Juno/Copper users discovered during Synapse), "open from anywhere in the world" 🔴 (17+ excluded jurisdictions + the 2024-2025 mass closures), "up to $5M FDIC insurance" 🟡 (20-bank sweep capacity, not single-bank insurance; pass-through conditioned on partner-bank FBO record integrity — exactly the failure mode Synapse demonstrated), "apply in 10 minutes" 🟡 (keystroke time, not approval; 1-2 business days for clean US, 7+ days for non-US with material rejection risk). **Most underrated risk**: the Jan 2024 Choice consent order and the chain of evidence in The Information's Mar 2024 piece (PO-boxes, paid affiliate commissions to LLC-formation services, sought "whitelisting" of higher-risk users, declined-SAR on attempted Cuba ATM). A second compliance event before Mercury Bank N.A. activates would crack the IPO narrative — structural exposure persists for another 12-18 months until charter migration completes.

- **[developer_experience.md](developer_experience.md)** — **Mercury MCP at `https://mcp.mercury.com/mcp`** with 34 tools, OAuth 2.0 + RFC 7591 Dynamic Client Registration. Immad's framing: "I don't think Claude is going to go build a bank" — so the official endpoint is **read-only by design**. **Mercury CLI** launched May 2026 at `cli.mercury.com/install.sh` (agent-shell-able from Claude Code / Cursor). Auth: bearer token (or HTTP Basic) for first-party, OAuth 2.0 PKCE for third-party but approval-gated. Token scoping is fine-grained (Read / Write / Custom). **Excellent self-serve sandbox** at `api-sandbox.mercury.com` — pre-populated, swap-token-to-prod, webhooks triggerable. Webhooks: HMAC-SHA256 in `x-mercury-signature` (hex-encoded, raw-body), exponential-backoff retries. **No official SDKs, no public OpenAPI download, no documented rate limits**. **AI × crypto gap**: Mercury holds **fiat only** — no USDC/PYUSD/USDT custody, no Bridge.xyz / BVNK / Circle / Iron integration, not in x402 foundation, no Mastercard Agent Pay or Visa Intelligent Commerce participation despite IO being a Mastercard credential. Mercury has shipped agent-AI rails ahead of stablecoin rails — inverse to where x402-style agent commerce is forming. **Slash.com is already marketing on this exact gap**.

- **[product_evolution.md](product_evolution.md)** — Q-by-Q changelog 2017→2026. Five eras: Stealth + YC (2017-2019) → Public launch + free wires (2019-2020) → Treasury + IO Card (2021-2022) → SVB inflow + Mercury Vault + Raise (2023) → Synapse migration + Personal GA + Column N.A. + "ambitious companies" rebrand (2024) → AI agents + Spend Insights + Sequoia Series C + Central acquisition (HR/payroll) → **OCC conditional approval Apr 27 2026** (charter era begins). **Killed/de-emphasized**: cryptocurrency accounts (closed 2021-2023), Evolve as deposit partner (winding down), parts of the original "for startups" identity. **Strategic arc**: from YC-niche checking account → SMB/mid-market financial OS → chartered bank competing directly with Brex (now Capital One) and Ramp.

---

## Solana-developer / AI × crypto specific findings

For the user's AI × crypto research thesis:

1. **Mercury and Ramp are the first two business banks with first-party MCP servers.** Mercury's at `https://mcp.mercury.com/mcp` (34 tools, hosted, OAuth 2.0 + DCR, read-only by design); Ramp's at `ramp-public/ramp_mcp` (open-source, analytics-focused). Mercury MCP is technically more ambitious (hosted + DCR) but more conservative (read-only); Ramp's is the inverse.
2. **Mercury's explicit anti-agent-execution stance is a strategic statement, not a stack limitation.** Immad: "I don't think Claude is going to go build a bank." This is *intentional* read-only philosophy from the CEO — not a roadmap delay. A third party who wants to ship agent-initiated Mercury writes must build outside the official rail.
3. **The Phantom case study is the most underrated signal.** Mercury's Web3 page directly markets to crypto-wallet builders ("perfect for web3 founders looking for a crypto-friendly and streamlined experience"). This is a meaningful softening from the 2021-2023 mass-closure era of crypto-business accounts. Whether the softening is durable depends on the OCC charter posture once Mercury Bank N.A. activates — chartered banks face more direct regulator scrutiny on crypto-adjacent customers.
4. **The stablecoin gap is the most addressable buildable opportunity.** Mercury holds fiat only — no USDC/PYUSD custody, no Bridge.xyz / BVNK / Circle integration. A third-party MCP that bridges Mercury read-only data + a Bridge or BVNK off-ramp could ship "USDC payout from Mercury balance" as a single tool call. The unofficial `klodr/mercury-invoicing-mcp` write-tool + safety-guard pattern is a reference implementation.
5. **Mercury IO is a Mastercard, not Visa — and Mercury is not in Mastercard Agent Pay.** Ramp Agent Cards run on Visa Intelligent Commerce. Mercury has no equivalent on Mastercard's Agent Pay launch program despite Mastercard moving aggressively on agentic credentials in 2025-2026. This is the single largest "obvious adjacency, not pursued" in the file set.
6. **Mercury vs Ramp on developer surface is asymmetric**: Mercury wins on sandbox quality (`api-sandbox.mercury.com` pre-populated) + on first-party CLI. Ramp wins on SCIM 2.0 (free everywhere) + Agent Cards (VIC tokens) + OpenAPI surface depth + already-supported AI cards. Neither has stablecoin custody, neither has x402.

---

## Sources used (top-tier)

Primary: mercury.com, mercury.com/blog, mercury.com/customers, mercury.com/web3, docs.mercury.com, support.mercury.com, mcp.mercury.com/mcp (live MCP endpoint), cli.mercury.com.

Press (Mercury-specific): Fortune (2025-11-07 $650M revenue interview; 2025-03-07 Synapse coverage), TechCrunch (2019 A round, 2021 Coatue B, 2023 SVB inflow, 2023 Vault expansion, 2025 Sequoia C), **The Information** (Michael Roddan Mar 28 2024 "Inside Mercury's Stumble from Fintech Hero to Target of the Feds"), Bloomberg, American Banker, Banking Dive, Sifted (mass-closure coverage), CNBC, BusinessWire (OCC announcement), Kyiv Independent + Tech in Africa (international-founder mass closure).

Founder voice: Immad Akhund (X annual letters 2024 / 2025, Lenny's Podcast, First Round Review, Acquired-style interviews).

Code: GitHub `klodr/mercury-invoicing-mcp` (unofficial MCP reference), npm registry (no official Mercury SDK), pypi (community wrappers only).

Regulatory: FDIC Choice Financial Group consent order (Jan 26 2024), OCC conditional approval announcement (Apr 27 2026), NMLS 2606284 (Mercury Lending LLC), Mercury Bank N.A. application.

Comparison + analyst: Sacra Mercury profile, Banking Dive, Fintech Business Weekly, NerdWallet.

Sentiment: Trustpilot, BBB, G2, Reddit r/startups, r/ycombinator (search "Mercury bank"), X/Twitter (search "@mercury" + Immad's account).

---

## How to use this folder

If you have **30 seconds**, read the headline above. If you have **5 minutes**, read this README + `marketing_vs_reality.md` honest one-liner. If you're a **founder evaluating Mercury vs Brex/Ramp**, read `use_cases_and_examples.md` (named customers + the July 2024 international-closure story) + `marketing_vs_reality.md`. If you're a **builder thinking about AI × crypto integration**, read `developer_experience.md` (the AI × crypto gap + Slash.com's marketing positioning) + the AI × crypto findings above. If you're an **investor doing diligence on the post-OCC narrative**, read `deep_dive.md` (Choice consent order timeline + the Information piece) + `product_evolution.md` (the strategic arc from BaaS-consumer to chartered bank). If you're a **product/strategy reader interested in MCP / agent-payments architecture**, read `architecture.md` + `developer_experience.md` together (Mercury and Ramp are the two reference points for what business-banking MCPs look like in 2026).
