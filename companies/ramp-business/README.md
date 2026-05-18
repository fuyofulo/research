# Ramp Business (ramp.com) — Research Folder

Compiled May 2026 by deep-dive playbook (6 parallel research streams).

> **Disambiguation:** This folder is exclusively about **Ramp Business** (ramp.com), the NYC corporate-card / spend-management / AI-native finance fintech. It is **not** Ramp Network (rampnetwork.com), the Warsaw/London-founded fiat-to-crypto on/off-ramp — see `../ramp-network/` for that one. The two companies have actually litigated over the "Ramp" trademark (USPTO TTAB, June 2022).

---

## Headline finding

Ramp is the **most-funded "AI-native" software company that is not an LLM lab** — $2.3–2.83B raised cumulative, $32B valuation Nov 2025 (Lightspeed-led), in talks at $40B+ as of May 7 2026 (Iconiq + GIC co-leads, ~$750M round). Founded March 2019 by Eric Glyman + Karim Atiyeh + Gene Lee (ex-Paribus → Capital One). $1B+ ARR (CEO-stated, Aug-Nov 2025). 50,000+ business customers, $100B+ annualized purchase volume. **Brex was acquired by Capital One for $5.15B in April 2026 — less than a quarter of Ramp's current paper mark** — closing a poetic loop (Capital One bought the Paribus founders' first company in 2016, and is now buying their main competitor). Ramp's regulatory model is "thin": no bank charter, no MTLs of its own. Cards via Sutton + Celtic Bank (Visa, processed by Marqeta + Stripe Issuing). Treasury via First Internet Bank of Indiana (Increase BaaS) + Apex Clearing (FUGXX MMF). Bill Pay via Increase. **AI shift dated to May 18, 2023** (Ramp Intelligence GPT-4 launch); "Agents for AP" Oct 2025; "Procurement Agents fleet" Apr 2026; **Visa Trusted Agent Protocol partnership Mar 31 2026** for agentic Bill Pay. Headcount ~2,900. **No public layoffs in 2022–2025.**

The "honest one-liner": *Ramp is a fast-moving, well-funded corporate-card-and-spend-management software company that bundles a partner-issued Visa charge card with an integrated AP, expense, procurement, treasury, and travel stack. They keep ~50–80 bps of every swipe, charge $15/seat for the advanced tier, and are aggressively layering LLM-powered automations on top of a category that historically ran on rules. Their main edge is product velocity and brand momentum; their main vulnerability is that ~$1B of the ~$1B ARR is interchange-dependent, and at a $40B+ valuation they need the AI-agents narrative to hold up to justify a 28-32x ARR multiple. Today the agents recommend more than they decide. They're winning, but priced as if the win is already complete.*

---

## Folder structure

```
companies/ramp-business/
├── README.md                   ← you are here
├── deep_dive.md                ← founders (Paribus → Capital One → Ramp), funding, regulatory model, board
├── architecture.md             ← product SKUs, card mechanics, Bill Pay/Treasury, AI stack, agents
├── use_cases_and_examples.md   ← Perplexity, Notion, Eventbrite, Snapdocs, Quora, Joffrey Ballet walkthroughs
├── marketing_vs_reality.md     ← 30-claim audit, "save 5%" methodology autopsy, valuation premium analysis
├── developer_experience.md     ← Ramp Developer API, MCP server, Agent Cards (VIC), x402/AP2 angle
├── product_evolution.md        ← Q-by-Q changelog 2019→2026; killed features; acquisitions feeding products
└── transcripts/                ← (empty; founder podcast .txt files would go here)
```

---

## File index

- **[deep_dive.md](deep_dive.md)** — Eric Glyman (Harvard '12), Karim Atiyeh (Harvard SEAS '11), Gene Lee co-founders. All ex-Paribus (acquired by Capital One Oct 2016). Founded March 17, 2019, NYC HQ. Cap table led by **Founders Fund** (Keith Rabois, 5 of 7 priced rounds), with Stripe (Series B), Iconiq (Series E-2 lead at $22.5B), Lightspeed (Nov 2025 lead at $32B), GIC, Coatue, Thrive, Sands, Khosla. **Sequoia notably absent.** Acquisitions: Buyer (Aug 2021, ~$30M), Cohere.io (Jun 2023, AI customer support → seeded Ramp Intelligence), Venue (Jan 2024, procurement), Jolt AI (Oct 2025, 3-person engineering acqui-hire), Juno (Mar 2026, guest travel), Billhop (Mar 2026, Stockholm — first EU acquisition). Veho/Glean/Intriduce **did not** acquire Ramp (likely name-conflations). No public layoffs in 2022–2025 — Glyman uses this as a recruiting talking point.
- **[architecture.md](architecture.md)** — Visa-only card network (no Mastercard SKU). **Sutton Bank** (commercial card) + **Celtic Bank** (corporate card). **Marqeta** as issuer-processor (with Stripe Issuing for parts of program). **Increase** as BaaS for Bill Pay; **First Internet Bank of Indiana** for the deposit account; **Apex Clearing + Invesco FUGXX** for the money-market fund. The "2.5% APY" on Ramp Business Account is paid as a **Ramp-funded cash reward** (not deposit interest) — clever regulatory structuring. AI infra: **Applied AI Service** (internal LLM proxy, swap GPT-5.x ↔ Claude Opus ↔ Gemini 3 Pro by config) + LangChain/LangGraph/LangSmith + Modal sandboxes + OpenCode + Braintrust evals. **Inspect** (internal coding agent) writes >30% of merged PRs. Architectural pivot in early 2026: from "many small agents" → "one unified agent with thousands of skills" + Omnichat.
- **[use_cases_and_examples.md](use_cases_and_examples.md)** — Six substantive walkthroughs: **Perplexity** (Patricia, sole GL accountant, Accounting Agent codes 97% of 7-9K monthly txns straight-through, claimed $5M saved), **Notion** (multi-entity 10+ countries, 94% in-policy, $1M+ saved blocking out-of-policy at swipe), **Eventbrite** (card issuance 3 weeks → 1 day), **Snapdocs** (consolidated Brex+Expensify+Bill.com → 5-6 hr recon → <30 min), **Quora** (Bill Pay 5-8 min → 1-2 min, close 2-3 hr → 15-20 min), **Joffrey Ballet** (nonprofit, eliminated 30-50 manual checks/week). Plus REVA Air Ambulance, Construction One, Causal, Glossier, Squared Away, Elementus, FirstBlood. **Vertical mix: software <10% of customers** — diversification is genuine. G2 4.8 / 5; Trustpilot 3.2 (vs Brex 1.7) — bot-heavy first-line support is the structural complaint at scale. Forrester TEI: 503% ROI / $90K NPV over 3 years — composite of 4 customer interviews (paid-for methodology).
- **[marketing_vs_reality.md](marketing_vs_reality.md)** — 30-claim adversarial audit. The "Save 5%" / "Save 3.5%" composite includes (1) interchange-rebate dollars Ramp itself charges, (2) imputed time-savings priced at chosen wage, (3) "savings" against counterfactual alternatives — unfalsifiable without external auditor. **Valuation premium analysis**: $32B / $1B ARR = 32x; vs Marqeta ~3-4x, Bill.com ~6-8x, public AI infra (Datadog) 12-18x. **Brex's exit at $5.15B / $700M ARR ≈ 7x** is the cleanest market-priced comparable — Ramp carries ~5x more multiple. AI-agents framing materially overstates current autonomy ("Agents for Procurement work autonomously" → actually triage + recommend + route to human). Quietly de-emphasized: original 1.5% cashback hook, Buyer's "27.3% saved" claim, Travel module (post-bug-reports). Pricing creep: ACH bill pay $0.59/txn from June 2026. Full-stack honest 30-second pitch in §13.
- **[developer_experience.md](developer_experience.md)** — Ramp Developer API at `api.ramp.com/developer/v1`. OAuth 2.0 with PKCE, three grant types, 10-day client_credentials token TTL. Full endpoint catalog with scopes (`<resource>:<read|write>`, no admin super-scope — least-privilege). HMAC-SHA256 webhooks. **SCIM 2.0 free on every plan** (unusually generous). **Ramp MCP server** open-sourced ([ramp-public/ramp_mcp](https://github.com/ramp-public/ramp_mcp)) — natural-language analytics over Developer API. **Ramp Agent Cards** (Mar 2026) — VIC-based tokenized single-use cards for AI agents. No first-party SDKs in any language (community: r0aringthunder/ramp-api Python, ramp-api Rust crate). Docs ~6.7/10 overall — well below Stripe-tier. **AI x crypto angle** (§19): Ramp does NOT support x402/AP2 natively, but a thin shim — "x402 facilitator that issues Ramp Agent Cards on demand for fiat-only merchants" — is a buildable Solana-side weekend project. Two concrete bets articulated in §20.
- **[product_evolution.md](product_evolution.md)** — Quarter-by-quarter changelog Q1 2019 → Q2 2026. Four eras: Card v1 (2019-2021) → Spend management (2021-2023) → Finance automation (2023-2024) → AI-native / agentic (2025-2026). **Pivot timeline**: cashback corporate card (Feb 2020) → expense mgmt SW (Aug 2020) → Bill Pay (Oct 2021) → Ramp Flex BNPL (Aug 2022) → cross-border (Oct 2022) → Ramp Intelligence (May 18, 2023, GPT-4) → Procurement (Aug 2023) → Ramp Plus paid tier (Sept 2023) → Travel (Jun 2024) → App Center (Oct 2024) → Treasury (Jan 2025) → Stripe stablecoin partnership (May 2025) → Agents for Controllers (Jul 10, 2025) → Agents for AP (Oct 7, 2025) → Procurement Agents fleet (Apr 29, 2026). **Killed/dropped features**: original Ramp Financial brand, Buyer.co standalone, Cohere.io product, Jolt AI product, Copilot brand absorbed into Ramp Intelligence. Discrepancies vs the clean narrative: AI pivot is recursive (acqui-hire-driven) not greenfield; valuation has detached from public comp multiples; Founders Fund concentration unusual (5 of 7 priced rounds).

---

## Solana-developer / AI × crypto specific findings

For the user's AI × crypto research thesis:

1. **Ramp owns a unique transactional dataset on AI vendor spend.** Glyman has publicly disclosed Ramp can see foundation-model market share shift in real time (49% → 9% in 10 months, Oct 2024). This is the closest thing to a "Bloomberg terminal" for AI consumption that exists.
2. **Visa Trusted Agent Protocol partnership (Mar 31, 2026)** + **Ramp Agent Cards** (single-use VIC tokens for agents) is the **most addressable AI × crypto bridge** today. There is no published x402/AP2 facilitator using Ramp Agent Cards — this is a buildable side-project niche.
3. **Ramp's Stripe relationship is structurally important.** Stripe is a Series B investor; cards run on Stripe Issuing for parts of the program; Stripe-Bridge owns the obvious adjacent stablecoin rail. Ramp is keeping Stripe at arm's length on agent payments by partnering with Visa instead — the strategic dynamic is worth watching.
4. **Brex absorbed by Capital One Apr 2026** removes Ramp's most direct competitor and replaces it with a balance-sheet bank with credit underwriting capacity. Watch Capital One's product roadmap.
5. **The "autonomous finance in 3 years" Glyman thesis** maps onto agentic crypto payments. If AI agents will execute B2B payments autonomously by 2027, the rail underneath is contested — and stablecoins/crypto are a credible substitute for ACH/card. Ramp has not publicly committed to crypto rails despite the obvious adjacency.

---

## Sources used (top-tier)

Primary: ramp.com, docs.ramp.com, builders.ramp.com, ramp.com/blog/2025-release-notes, support.ramp.com.

Press: TechCrunch (deep coverage of every funding round and product launch), Fortune, Bloomberg, CNBC, Information, PRNewswire, Crunchbase News, Stratechery (2022 long-form), Newcomer, PYMNTS, CFO Dive, Acquired, Logan Bartlett Show.

Founder voice: Glyman (X, Stratechery, Logan Bartlett, 20VC, Sequoia Training Data podcast), Atiyeh (Invest Like the Best EP 445).

Code: GitHub `ramp-public/ramp_mcp`, Postman public collection, npm/community wrappers (r0aringthunder, ramp-api Rust crate).

AI infra: Anthropic case study at claude.com/customers/ramp, Modal blog on Inspect, LangChain BreakoutAgents, ZenML LLMOps DB, Microsoft Azure AI customer story, Stripe customer story.

Analyst: Sacra (Ramp + Brex profiles), Contrary Research, Pitchbook, Tracxn, Lightspeed thesis post.

Sentiment: G2 (~2,400 reviews), Capterra, Trustpilot.

---

## How to use this folder

If you have **30 seconds**, read the headline above. If you have **5 minutes**, read this README + `marketing_vs_reality.md` §13 (honest 30-second pitch). If you're a **CFO evaluating Ramp**, read `marketing_vs_reality.md` (especially §16 "what's missing from the pitch") + `use_cases_and_examples.md`. If you're a **builder thinking about AI × crypto integration**, read `developer_experience.md` §19-20 (AI × crypto angle + verdict). If you're a **product/strategy reader interested in fintech-as-AI**, read `architecture.md` (especially the AI infrastructure section) + `product_evolution.md`. If you're an **investor doing diligence at the rumored $40B+ mark**, read `marketing_vs_reality.md` end-to-end and treat all volume/ARR claims as CEO-stated until audited.