# How to Research a Company Deeply

*A playbook for company deep-dives, distilled from the Bridge, BVNK, Credible Finance, Blockworks, and frames.ag research runs.*

**Use this as the starting point any time we open a new company folder.** It captures the structure, the parallel-agent recipe, the confidence-labeling discipline, and the on-chain verification techniques that produced research worth committing.

---

## 1. The output — what files you should produce

Every company deep-dive should produce a folder structure that looks like this (skip files that don't apply):

```
companies/<company-name>/
├── deep_dive.md              → company history, founders, funding, key deal/event, big-picture context
├── architecture.md           → how the product actually works under the hood — technical mechanics, API surface, banking partners, on-chain custody
├── use_cases_and_examples.md → named customers with concrete end-user walkthroughs (NOT generic descriptions)
├── marketing_vs_reality.md   → the truth file — every marketing claim dissected against verifiable substrate
├── developer_experience.md   → API/SDK quality, sandbox, KYB, pricing reality, gotchas (only when company has a developer-facing product)
├── product_evolution.md      → quarter-by-quarter changelog (only when company has 2+ years of history worth tracing)
├── on_chain_truth.md         → for blockchain-native companies — direct mirror-node / explorer pulls comparing claimed TVL/volume to verified reality
└── transcripts/              → founder podcast / interview transcripts as .txt files
```

The five core files for any non-trivial company are: **deep_dive, architecture, use_cases_and_examples, marketing_vs_reality**, and a fifth that depends on company type — `developer_experience` for API companies, `on_chain_truth` for protocols, `product_evolution` for mature companies with rich history.

---

## 2. The research streams — split into 3–5 parallel agents

The single most important productivity unlock: **launch parallel research agents** instead of doing it serially. Each agent runs WebSearch/WebFetch independently and returns a focused report.

**Standard split:**

| Stream | Focus | Outputs to |
|---|---|---|
| 1 | Company history, founders, funding, key deal/event, geography, regulatory footprint, press timeline | `deep_dive.md` |
| 2 | Architecture, products, API surface, banking partners, technical mechanics, pricing | `architecture.md` (+ `developer_experience.md` if needed) |
| 3 | Customer use cases — named customers with concrete walkthroughs, end-user flows, integration patterns | `use_cases_and_examples.md` |
| 4 | Skeptical read — marketing-vs-reality audit, competitive positioning, post-deal landscape | `marketing_vs_reality.md` |

**For on-chain protocols add a fifth:**

| Stream | Focus | Outputs to |
|---|---|---|
| 5 | On-chain ground truth — pull program IDs, TVL, holder concentration, transaction history directly from explorers; compare to claimed numbers | `on_chain_truth.md` |

**Launch them in a single message with multiple Agent tool calls in parallel.** Use `run_in_background: true`. They typically each take 3-8 minutes to complete; you'll be notified as each finishes.

---

## 3. The agent prompt template

Every research-agent prompt must be **self-contained** because agents start with no context. Include these elements:

```
Do a [deep technical / critical / customer-focused] research pass on
**[COMPANY]** ([website]). Today is [DATE]. [One-sentence context of
why this company matters — recent acquisition? funding? launch?]

**Focus area: [stream name]**

Use WebSearch liberally — many search calls are fine. Try WebFetch
but expect permission denials (then rely on WebSearch snippets which
usually contain the substance).

**Specifically dig into:**

1. [Specific question with named entities to verify]
2. [Specific question with quantifiable expected output]
3. [Specific question that could surface negative signals]
... [10-15 specific questions]

**Format your output as a long-form markdown report (~3500-5000 words).
Use ✅/🟡/🔴 confidence labels (verified / inferred / marketing claim).
Cite sources inline as markdown links. Use Mermaid diagrams for
architecture/flows where useful. Output the full report as your final
message; do NOT write to files.**

**Sources to prioritize:**
- [company].com (about, blog, docs, case-studies)
- [Specific industry press relevant to the company]
- [Founder podcast appearances]
- [Analyst coverage — Sacra, a16z, Bessemer, etc.]
- [Any specific source the user has flagged]
```

**Why prompts must be specific not vague:** A prompt like *"research BVNK's customers"* produces a generic list. A prompt like *"For Worldpay, walk through one specific end-user flow with the money path step-by-step, the alternative before BVNK, and any disclosed dollar amounts"* produces something useful.

---

## 4. Confidence-labeling discipline

Every non-trivial claim must carry one of three labels:

- **✅ Verified** — found in 2+ independent sources, or directly verifiable from primary documentation. Examples: "BVNK was acquired by Mastercard for $1.5B + $300M earnout on March 17, 2026" (in Mastercard 8-K + multiple press); "Bridge uses Lead Bank as US banking partner" (named in product docs + multiple analyst pieces).
- **🟡 Inferred** — single source, partial confirmation, or strong logical inference. Examples: "BVNK iGaming exposure is likely 20-35% of $30B volume" (inferred from PSP customer mix; never disclosed); "Founders likely retain 20-40% combined equity" (back-of-envelope from raise totals).
- **🔴 Marketing claim** — appears only in company marketing, no verification possible, contested by competitor framing, or hand-wavy by construction. Examples: "$1T addressable market"; "available in 130+ countries" (when actually means payout reachability not direct rails).

**The label is non-negotiable.** Research without confidence labels is indistinguishable from marketing copy. Future-you and the user both need to know which claims are load-bearing and which are scaffolding.

---

## 5. What to look for — per stream

### Stream 1 — Company history, founders, funding

- Founders' prior companies and exits (signals founder lineage and what they actually know how to build)
- Company name origin (sometimes reveals the original thesis)
- The pivot story (what was the first idea? when did they pivot? why?)
- Funding round-by-round with leads, co-investors, valuations, and any strategic investors
- Major acquisitions made by the company (e.g., BVNK acquired System Pay Services for the EMI license)
- Press timeline as a structured table — useful for spotting clustering of events
- Geography: incorporation, HQ, offices, where engineering vs sales sits
- Regulatory licenses: enumerate each one with jurisdiction, license type, license number

### Stream 2 — Architecture and products

- The actual product SKUs (not the marketing categories — the real things customers buy)
- Banking partners: who holds the fiat? Get NAMES not "tier-1 banks"
- Liquidity / mint mechanics: how does fiat actually become stablecoin? Is there an internal float? Where does the float get replenished?
- On-chain custody: self-custody, MPC, Fireblocks, Privy, in-house? Be specific
- Settlement chains supported with stablecoins per chain
- Local rails: enumerate as a matrix — country / rail / mechanism / direct vs partner-routed
- API base URL, authentication model (Bearer? API key? Hawk? OAuth?)
- Idempotency, webhooks, error handling
- SDK availability and quality (count GitHub stars/forks/last-commit; read package.json publish date)
- Sandbox limitations (what works, what doesn't — sandbox lies are common)
- Pricing: any public rate card? FX spread caps in the Fee Disclosure Statement? Volume tiers?

### Stream 3 — Customer use cases

For each named customer, produce a section with:

1. **What is the customer's product?** (one paragraph)
2. **What problem does [company] solve for them?** (specific — "stablecoin payments" is not specific)
3. **Which products do they use?** (Orchestration vs Issuance vs Wallets vs Cards vs whatever the company's SKU lineup is)
4. **End-user walkthrough** — pick one specific user and walk through the flow step-by-step. Include named cities/countries/banks/wallets where possible.
5. **Mermaid diagram of the money path** when useful
6. **What was the alternative before [company]?** What was broken about it?
7. **Money path step-by-step**, currency by currency, chain by chain
8. **Costs disclosed publicly** (any specific dollar figures or bps numbers)

This is the most labor-intensive stream and the one most likely to fail if the prompt is too vague. Force specificity.

### Stream 4 — Marketing-vs-reality audit

This is the highest-leverage file. Approach:

1. **Enumerate every claim the company makes publicly.** Walk the homepage, product pages, blog, decks, case studies. List 10-20 specific claims.
2. **For each claim, attempt to verify.** Apply a confidence label. Note what's actually true vs hand-wavy.
3. **Look for the "tell."** Partnership announcements that paper over weaknesses. Strategic investor lists that reveal what the company can't do alone. Marketing that quietly drops earlier claims (Credible dropped "Solana" from its enterprise positioning).
4. **Identify the dual-positioning game** — does the company pitch differently to crypto audiences vs enterprise audiences? Both can be honest standalone but together suggest message-segmentation for fundraising.
5. **The honest one-liner.** End the file with a 30-second pitch describing the company as it actually is, not as it markets itself.

### Stream 5 (when applicable) — On-chain ground truth

For protocols and on-chain products, never accept claimed TVL / volume / users at face value. Verify:

- **Solana**: Solscan, Birdeye, DefiLlama, Helius RPC. Pull program IDs, account holders, token supply, transaction history.
- **Ethereum/EVM**: Etherscan, DefiLlama, Dune Analytics, Nansen. Look at top-holder concentration, contract age, recent activity.
- **Hedera**: mirror-node API directly (this is how we caught Credible's $1.12M actual TVL vs claimed multi-million).
- **Other chains**: equivalent block explorer + DefiLlama.

**Key red flags to look for:**
- One wallet holding >50% of a "decentralized" pool's supply
- Wallet creation timestamps clustered minutes after contract deploy (= team treasury, not external LPs)
- TVL flat-lining or declining over 90+ days while marketing claims growth
- Token holder count low + transaction count low (= airdrop farming, not real users)
- "Audit" link that points to a non-Big-4 or non-recognized auditor
- Public GitHub absent or empty for code that should be open

---

## 6. The marketing-vs-reality discipline (most important section)

Every company markets itself in ways that are technically true but materially misleading. The job of research is to translate marketing back into substance. Patterns to watch:

| Pattern | Example | Translation |
|---|---|---|
| "Available in N countries" | Stripe SFA "101 countries"; BVNK "130+ countries" | N = countries where you can hold a stablecoin balance. Production-grade direct fiat off-ramp is usually 3-5 countries. |
| "Volume processed" | "$60M+ processed in 11 months" (Credible) | Cumulative claim that doesn't reconcile against the May 2026 update of "$350M in 5 months" — take with skepticism. |
| "X+ licenses" | BVNK "25+ licenses" | Count includes every legal-entity registration. Operationally meaningful licenses are usually 4-6. |
| "Cash-flow positive" | Often used at low burn + low revenue | Verify with disclosed revenue. $70K six-month revenue at low burn is technically positive but not impressively so. |
| "Multi-corridor" | Credible | Verify: how many corridors are actually live in production vs roadmap? |
| "Trillion-dollar TAM" | Standard fintech deck slide | Usually flow not revenue. At 10-30 bps take rate the addressable revenue is 0.1-0.3% of the flow figure. |
| "Open-source / decentralized" | Many DeFi products | Check the actual GitHub. If the repo is empty or stale or the contracts are upgradeable-by-multisig, the framing is misleading. |
| "Zero defaults" | Credit / lending products | True at small scale, doesn't generalize. Check pool size. |
| "Direct PSP / payment processor" | Many fintechs | Often actually a credit-orchestration layer routing through partner NBFIs. Verify the named partners. |
| "Founders include [Important Name]" | Many crypto launches | Verify their actual ownership / commitment. Often advisors not founders. |

**The dual-positioning game** is its own pattern worth flagging separately. Many companies maintain two parallel narratives:
- A crypto-native narrative for hackathons, accelerators, demo days, X/Twitter
- An enterprise narrative for B2B sales pages, regulatory filings, banking-partner conversations

Neither is dishonest standalone. Together they reveal that "what the company is" depends on which deck you're reading. Document both.

---

## 7. Common pitfalls to avoid

1. **Generic descriptions.** "They do stablecoin payments" is worthless. Always force specificity: which currency pairs, which corridors, which customers, which dollar figures.
2. **Single-source claims accepted as fact.** If something only appears on the company's own marketing, label it 🔴 — even if it sounds plausible.
3. **Skipping confidence labels because the report flows better without them.** It doesn't. The labels are the value-add.
4. **Long-winded prose where a confidence-labeled bullet would do.** Tables and bullet lists outperform paragraphs for research artifacts.
5. **Dropping the "what's actually impressive" section.** Even when doing skeptical analysis, list what IS real and worth respecting. Otherwise the file reads as hostile and gets dismissed by readers.
6. **Burying competitive positioning insights.** End each marketing-vs-reality file with a "what a competitor should target" section — the moats that are real, the gaps that are exploitable.
7. **Forgetting the "honest one-liner."** Always end with the 30-second pitch in plain English.
8. **Letting agents waste tool calls on duplicated WebSearch.** When prompting parallel agents, partition the search space — don't give two agents overlapping mandates.
9. **Reading the agent's full JSONL output back into context.** It's huge. Save the final report as a file and reference the file path; never `cat` the JSONL transcript.
10. **Premature synthesis.** Save individual stream reports as separate files first. Synthesize across files later only if the user asks.

---

## 8. Git workflow

Every company deep-dive ends in a series of commits to the GitHub research repo:

1. **One commit per file** — `companies/<name>/deep_dive.md`, `companies/<name>/architecture.md`, etc.
2. **Separate commit for the README index update** — adding the folder structure and the index entries.
3. **Distinct commits, not monolithic.** Each commit does exactly one thing. Easier to review, easier to selectively revert.
4. **Commit messages**: lead with `<area>:` (e.g., `bvnk:`, `companies/bvnk:`, `docs:`), one-line summary, then a 5-15 line body explaining the substance — what's verified, what's the headline finding.
5. **Push when the research is complete** — a single `git push origin main` at the end is fine. Force-push only with `--force-with-lease` and only if the user explicitly asks for a history rewrite.

---

## 9. Quick checklist (use this every time)

Before starting:
- [ ] Created `companies/<company-name>/` folder + `transcripts/` subfolder
- [ ] Confirmed today's date for the research date stamp
- [ ] Identified 3-5 research streams appropriate to this company

While running:
- [ ] Spawned all research agents in parallel (single message, multiple Agent tool calls, `run_in_background: true`)
- [ ] Each agent prompt is self-contained, has 10-15 specific questions, names sources to prioritize, requires confidence labels
- [ ] Saved each agent's output as a distinct file when it returns

While writing:
- [ ] Every non-trivial claim has ✅/🟡/🔴 label
- [ ] Sources cited inline as markdown links
- [ ] Mermaid diagrams for architecture and money flows
- [ ] Customer walkthroughs are SPECIFIC (named users, named cities, named banks, dollar figures)
- [ ] Marketing-vs-reality file ends with the honest 30-second pitch
- [ ] On-chain claims verified against block explorer reality (for protocols)

While committing:
- [ ] One file per commit
- [ ] README updated with folder structure + index entries
- [ ] Pushed to GitHub

---

## 10. The mindset

The default mode of company-research is **breathless summarization** of the company's own marketing. The default mode of *good* company research is **adversarial verification** — assume every claim is a marketing artifact until verified, then say which ones survived.

This isn't hostility. It's respect for the user's time. They're going to make decisions based on this research — funding decisions, build-vs-buy decisions, competitive-positioning decisions, partnership decisions. Pretty prose that fudges what's real and what's marketing makes those decisions worse. Confidence labels make them better.

The hardest discipline is **flagging your own uncertainty.** If you couldn't verify whether a banking partner is named publicly or just inferred from press, say so with 🟡. If you couldn't find any negative customer reviews, say so as a finding ("data void, not a clean bill of health") rather than implying the company is universally loved. The user can handle uncertainty. They cannot handle false confidence.

---

## Reference deep-dives produced using this method

- [Bridge](./companies/bridge/) — 6 files, 16 named customer walkthroughs, full off-ramp coverage matrix, marketing-vs-reality on the 101-countries claim
- [BVNK](./companies/bvnk/) — 4 files, 21 named customer walkthroughs, the iGaming firewall analysis, Mastercard $1.8B deal rationale
- [Credible Finance](./companies/credible-finance/) — 9 files, on-chain ground truth pull (real TVL $1.12M vs claimed multi-million), the dual-positioning audit, 15 specific marketing claims dissected
