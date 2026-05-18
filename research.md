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
├── explain_like_new_teammate.md → dumb-questions explanation: what it does, who buys it, how the product flows, why it matters
├── product_flow.md           → canonical step-by-step user/data/money flow, including failure cases and handoffs
├── source_ledger.md          → source-by-source provenance: what each source proves and how reliable it is
├── contradictions.md         → conflicting claims, stale metrics, copy drift, and unresolved inconsistencies
├── diligence_questions.md    → what to ask before investing, buying, partnering, or competing
├── developer_experience.md   → API/SDK quality, sandbox, KYB, pricing reality, gotchas (only when company has a developer-facing product)
├── product_evolution.md      → quarter-by-quarter changelog (only when company has 2+ years of history worth tracing)
├── on_chain_truth.md         → for blockchain-native companies — direct mirror-node / explorer pulls comparing claimed TVL/volume to verified reality
└── transcripts/              → founder podcast / interview transcripts as .txt files
```

The five core files for any non-trivial company are: **deep_dive, architecture, use_cases_and_examples, marketing_vs_reality**, and a fifth that depends on company type — `developer_experience` for API companies, `on_chain_truth` for protocols, `product_evolution` for mature companies with rich history.

The five **understanding/provenance files** should be produced for every serious company research run unless the company is too small or source-poor: **explain_like_new_teammate, product_flow, source_ledger, contradictions, diligence_questions**. These are not optional polish. They are what make the research usable after the long-form deep dives are written.

### The quality bar — structure is not enough

A complete folder is not automatically good research. The target standard is:

> **Dense competitive intelligence + clear explanation + explicit provenance.**

Every serious research run should hit all three:

1. **Rich factual density** — the report should contain hard numbers, named entities, dated events, product mechanics, pricing, API details, legal structures, and customer examples. Avoid vague filler.
2. **Adversarial interpretation** — the report should say what is real, what is marketing, what is inferred, what is weak, and what a competitor should learn from it.
3. **Reusable clarity** — the report should still be understandable to a new teammate who does not know the category.

When reviewing your own output, ask: **would this help us make a build/buy/partner/compete decision, or is it just a polished company summary?** If it only summarizes, it is not done.

### Minimum factual density checklist

Every serious company file set should aggressively look for and include:

- Funding rounds, round dates, leads, total raised, valuations, and strategic investors.
- Revenue, ARR, volume, AUM, TPV, customer count, user count, headcount, geography, and growth claims.
- Founder history, prior exits, prior employers, unusual founder-market-fit signals.
- Legal entities, incorporation jurisdictions, license names, license numbers, regulator names, and current ownership/acquisition status.
- Bank partners, card issuers, issuer processors, payment processors, custodians, broker-dealers, KYC/KYB vendors, liquidity providers, stablecoin issuers, custody vendors, and infrastructure vendors by name.
- Product SKUs as customers buy them, not only marketing categories.
- Pricing, fees, spreads, FX markups, take rates, APY/yield terms, minimums, volume tiers, and footnotes.
- Named customers, named use cases, disclosed savings, implementation times, support burden, customer complaints, and review-site sentiment.
- API base URLs, auth model, scopes, webhooks, idempotency, rate limits, SDK/package names, GitHub/npm stats, sandbox behavior, and docs quality.
- Recent product launches, killed/de-emphasized features, roadmap claims, and copy drift over time.

If a fact cannot be found, write that down. A missing bank partner, missing sandbox, missing license number, or missing customer metric is often itself a finding.

### Richness rubric

Use this rubric before calling a research folder complete:

| Dimension | Weak output | Strong output |
|---|---|---|
| Numbers | "Fast-growing fintech" | "$100B+ annualized purchase volume, 50K+ customers, $1B+ ARR, valuation $32B, all company/press-claimed unless audited" |
| Partners | "Uses partner banks" | "Cards issued by Sutton/Celtic; processor Marqeta; Bill Pay via Increase; treasury via First Internet Bank + Apex + FUGXX" |
| Developer detail | "Has an API" | "Base URL, OAuth/Bearer model, scopes, endpoint families, webhook signing, sandbox limits, SDKs, package stats" |
| Customers | "Used by enterprises" | "Perplexity: 7-9K monthly transactions, 97% straight-through coding; Notion: 10+ countries, 94% in-policy" |
| Marketing audit | "Claims are mostly true" | "30-claim table; each claim translated into verified / inferred / marketing; hidden fees and methodology issues identified" |
| Competitive value | "They compete with X" | "Here is the wedge they own, the moat that is real, the gap a startup can target, and why it matters for our thesis" |
| Usability | "Long report" | "README one-liner, product flow, new-teammate explainer, source ledger, contradictions, diligence top 10" |

The best research combines both columns: it is dense enough for strategy and clear enough for onboarding.

### Understanding/provenance files

#### `explain_like_new_teammate.md`

This is the file for "dumb questions." Write it as if a smart new teammate knows nothing about the company or category but must understand it by tomorrow.

Required sections:

- What does the company do in one sentence?
- What problem exists before this product?
- Who buys it?
- Who uses it day to day?
- What exactly happens step by step inside the product?
- What data, money, or state moves through the system?
- Why is this hard?
- Why now?
- What is actually impressive?
- What is still unclear?
- The mental model: "Think of this company as..."

#### `product_flow.md`

This is the canonical flow file. It should be simple enough to explain verbally, but specific enough that an engineer/operator can see the moving pieces.

Required sections:

1. User starts here.
2. Data enters here.
3. The system transforms it here.
4. External tools/partners/rails are called here.
5. Money/data/state changes here.
6. User sees output here.
7. Failure cases go here.
8. Human handoffs happen here.
9. Mermaid diagram of the primary product flow.

#### `source_ledger.md`

Inline citations are necessary but not sufficient. The source ledger prevents accidental over-reliance on company-authored marketing.

Use this table:

| Source | Type | Date | What it proves | Reliability | Notes |
|---|---|---|---|---|---|

Source types: company page, docs, blog, case study, investor post, press release, regulatory filing, third-party press, customer-authored source, podcast/interview, analyst report, social profile, explorer/on-chain data.

Reliability labels:

- **High** — primary legal/regulatory filing, direct docs, on-chain pull, customer-authored proof, audited report.
- **Medium** — reputable press, investor post, founder interview, partner announcement.
- **Low** — company marketing page, unsourced metric, cached snippet, directory profile, scraped profile.

#### `contradictions.md`

Start this file even if it is short. Startups change copy fast; stale snippets and metric drift are findings.

Use this table:

| Claim | Source A | Source B | Conflict | Why it matters | Current interpretation |
|---|---|---|---|---|---|

Look specifically for:

- metric drift (`$600M` vs `$1B`, `90%` vs `98.8%`)
- product-scope drift
- geography/license drift
- customer-count drift
- "launched" vs "coming soon"
- legal entity mismatches
- old brand vs new brand
- acquired vs partnered vs integrated

#### `diligence_questions.md`

This is the buyer/investor/competitor question bank. Organize it by:

- Product
- Customers
- Revenue/pricing
- Unit economics
- Security/compliance/legal
- Technical architecture
- Operations/services ratio
- Competition
- Founder/company history

Every diligence file should end with the **top 10 questions** ranked by importance.

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
- Current ownership status, acquisition offers, completed acquisitions, and whether current copy still reflects standalone status
- Major acquisitions made by the company (e.g., BVNK acquired System Pay Services for the EMI license)
- Press timeline as a structured table — useful for spotting clustering of events
- Geography: incorporation, HQ, offices, where engineering vs sales sits
- Regulatory licenses: enumerate each one with jurisdiction, license type, license number
- Headcount, hiring footprint, layoffs, offices, and leadership changes
- Revenue/ARR/volume/customer/user metrics, with exact source and confidence label
- Founder-market-fit signals: prior exits, domain background, investor relationships, regulatory experience, distribution history

### Stream 2 — Architecture and products

- The actual product SKUs (not the marketing categories — the real things customers buy)
- Banking partners: who holds the fiat? Get NAMES not "tier-1 banks"
- Card issuers, issuer processors, networks, card program managers, payment processors, broker-dealers, custodians, sweep banks, trust companies, KYC/KYB vendors, and compliance vendors
- Liquidity / mint mechanics: how does fiat actually become stablecoin? Is there an internal float? Where does the float get replenished?
- On-chain custody: self-custody, MPC, Fireblocks, Privy, in-house? Be specific
- Settlement chains supported with stablecoins per chain
- Local rails: enumerate as a matrix — country / rail / mechanism / direct vs partner-routed
- API base URL, authentication model (Bearer? API key? Hawk? OAuth?)
- Idempotency, webhooks, error handling
- SDK availability and quality (count GitHub stars/forks/last-commit; read package.json publish date)
- Sandbox limitations (what works, what doesn't — sandbox lies are common)
- Pricing: any public rate card? FX spread caps in the Fee Disclosure Statement? Volume tiers?
- Security/compliance artifacts: SOC 2, ISO 27001, PCI, pen tests, audits, status page, trust center, subprocessors
- What is built in-house vs partner-routed vs manual operations
- What breaks if a named partner disappears

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

Also include:

- **What does not survive scrutiny** — inflated metrics, hidden spreads/fees, stale claims, non-exclusive partnerships, roadmap features marketed as live, regulatory footnotes, support complaints, or weak moats.
- **What is genuinely impressive** — real moats, execution speed, distribution, regulatory depth, customer trust, unusual technical depth. Skeptical does not mean dismissive.
- **Competitor wedge** — what a new entrant should target, what is not worth attacking, and what would be hard to copy.
- **Business-model tell** — where the company likely makes money, what scales with software, what requires humans/capital/licenses/partners, and what margin pressure exists.
- **AI reality check** for AI-marketed companies — what is actually automated, what is human-reviewed, what is just extraction/classification, and what evidence supports autonomy.

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

## 6. Phase 2 — normalize evidence and explain it simply

After the parallel streams return, do **not** jump straight from raw reports to final prose. Add a Phase 2 pass that converts evidence into understanding.

### Step 1 — normalize the evidence

Create or update:

- `source_ledger.md`
- `contradictions.md`

Rules:

- Every source that materially supports the research goes into the ledger.
- Every material mismatch gets written down, even if the likely explanation is "old copy."
- Company-authored case studies prove that the company claims a customer/result; they do not independently prove the result.
- Investor posts are useful but still promotional.
- Directory profiles are weak evidence unless they point to another primary source.

### Step 2 — decide the actual category

Before writing final analysis, force a category decision:

| Question | Answer |
|---|---|
| What category does the company say it is in? | |
| What category do buyers likely think it is in? | |
| What category do incumbents likely think it is in? | |
| What category is it actually in? | |
| Which adjacent categories are misleading comparisons? | |

This prevents lazy competitor lists. A company can mention "AI," "payments," "contracts," or "stablecoins" without actually being an AI infrastructure company, PSP, CLM, or protocol.

### Step 3 — map the product flow

Create `product_flow.md` before writing the final architecture summary. The flow should answer:

- What is the user trying to do?
- What is the first object created or connected?
- What systems does the product read from?
- What transformations happen?
- What is written back to external systems?
- What happens when the happy path fails?
- Where do humans intervene?
- What would break if the product disappeared tomorrow?

### Step 4 — explain it to a new teammate

Create `explain_like_new_teammate.md` last. This file should be low-jargon and high-clarity. It should not be dumbed down; it should be made legible.

The target reader should walk away able to answer:

- What does this company actually do?
- Why does anyone pay for it?
- What does the product do in order?
- What is the business model likely to be?
- What is impressive?
- What is risky or unresolved?

### Step 5 — write the diligence file

Create `diligence_questions.md` after the skeptical read. Ask the questions that would decide whether the company is real, scalable, defensible, and safe to buy/use/invest in.

Always include questions about:

- unit economics and gross-margin pressure
- human-operations vs software automation
- pricing and contract structure
- customer concentration
- compliance and legal entity details
- security artifacts and subprocessors
- claims methodology
- data export and lock-in

---

## 7. Business model and unit economics

Every company research run should include business-model reasoning somewhere, usually in `deep_dive.md`, `marketing_vs_reality.md`, or `diligence_questions.md`.

Answer:

- What does the company charge for?
- Is pricing seat-based, usage-based, volume-based, transaction-based, platform-fee, spread-based, AUM-based, or services-based?
- Is pricing public or sales-led?
- What is likely high-margin software?
- What requires humans, capital, licenses, support, or partner fees?
- What gets cheaper with scale?
- What gets harder with scale?
- What is the wedge?
- What is the expansion path?
- What could compress margins?

For AI/automation companies, explicitly estimate the **software vs services ratio**:

| Workflow | Pure software | AI-assisted | Human ops | Unknown |
|---|---:|---:|---:|---:|

For fintech/crypto companies, explicitly estimate the **capital/partner dependency**:

| Workflow | Own license/rail | Partner-routed | Manual/ops-heavy | Unknown |
|---|---:|---:|---:|---:|

---

## 8. The marketing-vs-reality discipline (most important section)

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

## 9. Common pitfalls to avoid

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
11. **Skipping the dumb-questions explanation.** If you cannot explain the company simply, you do not understand it yet.
12. **Treating customer case studies as independent proof.** They prove the vendor is willing to publicly claim the result; they do not prove the metric unless the customer independently confirms it.
13. **Ignoring metric drift.** Conflicting numbers across current pages, cached snippets, and press releases are findings. Put them in `contradictions.md`.
14. **Missing the unit-economic tell.** High-touch support, partner routing, capital needs, manual compliance, and concierge operations can be the product, but they change the business model.

---

## 10. Git workflow

Every company deep-dive ends in a series of commits to the GitHub research repo:

1. **One commit per file** — `companies/<name>/deep_dive.md`, `companies/<name>/architecture.md`, etc.
2. **Separate commit for the README index update** — adding the folder structure and the index entries.
3. **Distinct commits, not monolithic.** Each commit does exactly one thing. Easier to review, easier to selectively revert.
4. **Commit messages**: lead with `<area>:` (e.g., `bvnk:`, `companies/bvnk:`, `docs:`), one-line summary, then a 5-15 line body explaining the substance — what's verified, what's the headline finding.
5. **Push when the research is complete** — a single `git push origin main` at the end is fine. Force-push only with `--force-with-lease` and only if the user explicitly asks for a history rewrite.

---

## 11. Quick checklist (use this every time)

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
- [ ] `source_ledger.md` created with source type, proof, and reliability
- [ ] `contradictions.md` created, even if it says no material contradictions found
- [ ] Mermaid diagrams for architecture and money flows
- [ ] `product_flow.md` explains happy path, failure cases, and human handoffs
- [ ] Customer walkthroughs are SPECIFIC (named users, named cities, named banks, dollar figures)
- [ ] Marketing-vs-reality file ends with the honest 30-second pitch
- [ ] `explain_like_new_teammate.md` answers the dumb questions in simple language
- [ ] `diligence_questions.md` lists buyer/investor/competitor questions and ranks the top 10
- [ ] Business model / unit economics / software-vs-services ratio is addressed
- [ ] On-chain claims verified against block explorer reality (for protocols)

Quality-gate before calling it done:
- [ ] The folder contains enough numbers to support strategic judgment, not just category description
- [ ] Named partners/entities are included wherever public; if not public, the absence is called out
- [ ] Developer-facing products include API base URL/auth/scopes/webhooks/sandbox/SDK/package-quality notes
- [ ] Marketing-vs-reality includes "what does not survive scrutiny," "what is genuinely impressive," and "competitor wedge"
- [ ] Customer examples include named customers and concrete workflows, not only logo lists
- [ ] The research states what this means for our product thesis or competitive strategy
- [ ] A new teammate can understand the company from `README.md` + `explain_like_new_teammate.md`
- [ ] A skeptical investor/buyer can pressure-test the company from `marketing_vs_reality.md` + `diligence_questions.md`

While committing:
- [ ] One file per commit
- [ ] README updated with folder structure + index entries
- [ ] Pushed to GitHub

---

## 12. The mindset

The default mode of company-research is **breathless summarization** of the company's own marketing. The default mode of *good* company research is **adversarial verification** — assume every claim is a marketing artifact until verified, then say which ones survived.

This isn't hostility. It's respect for the user's time. They're going to make decisions based on this research — funding decisions, build-vs-buy decisions, competitive-positioning decisions, partnership decisions. Pretty prose that fudges what's real and what's marketing makes those decisions worse. Confidence labels make them better.

The hardest discipline is **flagging your own uncertainty.** If you couldn't verify whether a banking partner is named publicly or just inferred from press, say so with 🟡. If you couldn't find any negative customer reviews, say so as a finding ("data void, not a clean bill of health") rather than implying the company is universally loved. The user can handle uncertainty. They cannot handle false confidence.

---

## Reference deep-dives produced using this method

- [Bridge](./companies/bridge/) — 6 files, 16 named customer walkthroughs, full off-ramp coverage matrix, marketing-vs-reality on the 101-countries claim
- [BVNK](./companies/bvnk/) — 4 files, 21 named customer walkthroughs, the iGaming firewall analysis, Mastercard $1.8B deal rationale
- [Credible Finance](./companies/credible-finance/) — 9 files, on-chain ground truth pull (real TVL $1.12M vs claimed multi-million), the dual-positioning audit, 15 specific marketing claims dissected
