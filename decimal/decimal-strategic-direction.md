# Decimal — Strategic Direction

Living document capturing the strategic decisions made about Decimal's positioning, customer, moats, and architecture. Used to keep all future feature / milestone / pitch decisions consistent. Read this before opening a new strategic discussion.

Each entry is dated. Order is chronological. Newer thinking can supersede older thinking; both stay in the document so the *why* of changes is preserved.

---

## 2026-05-21 — Who Decimal is for (TAM-first thinking)

**Decision:** Decimal is built for TradFi B2B finance teams, not for crypto-native teams.

**Reasoning:**
- "Stablecoin-native businesses on Solana" is roughly 500-2,000 companies globally. Even at 100% capture and $500/mo, that's $3-12M ARR. Not a billion-dollar trajectory.
- The actual market — cross-border B2B AP — is $100B+ in fees globally. Bill.com / Tipalti / Ramp / Brex / Mercury / Deel all play here at $1B+ valuations.
- Decimal must penetrate TradFi *while bringing stablecoin / blockchain capability under the hood*.

**Anti-decision:** Don't pursue the "Solana CFO Bloomberg terminal" or any narrow crypto-niche play as the wedge. Those become add-ons later, not the wedge.

---

## 2026-05-21 — The two real moats blockchain gives us

**Decision:** The only two things blockchain provides that TradFi cannot replicate are:

1. **Cross-border speed and cost** — USDC moves at internet speed across 50+ countries for ~$0.001 in fees. SWIFT is bank-speed and $25-50.
2. **Code-driven security** — multisig + smart-contract policy enforcement that no admin, no employee, no agent can override.

Programmability is a corollary of #2 — the ability to write rules into the execution layer that traditional banks cannot enforce because they're built around human banker intervention.

**Anti-decision:** Don't market "DeFi yield," "tokenization," "multichain support," "on-chain identity" or any other crypto-feature that doesn't map to one of these two outcomes. They distract from the only two things customers care about.

---

## 2026-05-21 — De-cryptofication of customer-facing positioning

**Decision:** Decimal does not market itself as a blockchain company to customers. The blockchain bits are infrastructure benefits, not the product story.

**The customer-facing pitch:**
> AI-powered AP for global teams. Code-enforced approval policies no admin can override. Instant cross-border payouts to 50+ countries. Audit trail you can prove to any regulator.

Zero references to Solana, USDC, multisig, smart contracts, on-chain, or any other crypto-language. Every blockchain advantage is translated into a customer outcome (BEC-proof, fast, audit-clean).

**Anti-decision:** No "Solana" / "Squads" / "USDC" logos on the customer landing page. Move them to a "Built with" or developer-facing surface only.

**Grant audience exception:** Solana Foundation grant pitch leans hard into the blockchain narrative because that's what the grant funds. The grant pitch and the customer pitch are two different documents for two different audiences. Don't let one leak into the other.

---

## 2026-05-21 — The competitive set (corrected)

**Decision:** Decimal competes with TradFi AP / payments / payroll players, not with crypto-native infrastructure players.

**Direct competitors:**
- Bill.com (AP automation, US-domestic-heavy)
- Tipalti (international AP, legacy-feeling, no AI agent fleet)
- Ramp Business (spend management + bill pay, US-centric)
- Brex (card + expense + bill pay, US-centric)
- Mercury (banking + automation, US-only)
- Deel (global payroll, EOR; adjacent to AP)
- Flex (owner-operator banking + AP)

**Infrastructure providers Decimal uses, not competes with:**
- Bridge (on/off-ramp; partner)
- BVNK (stablecoin settlement; partner)
- Altitude (Solana stablecoin account; partner or skip)
- Velocity (enterprise stablecoin; partner at enterprise tier later)
- Squads / Grid (treasury infrastructure; partner)
- Privy (wallet infrastructure; partner)

**Anti-decision:** Stop benchmarking against Altitude / Bridge. They're not the bar. Bill.com and Tipalti are the bar.

---

## 2026-05-21 — Why extraction is no longer a moat

**Decision:** AI invoice extraction is commodity. Do not pitch it as a moat.

**Data:**
- Bill.com's Invoice Coding Agent trained on 250M+ invoices, claims 80% manual work reduction
- Tipalti claims 98-99% extraction accuracy
- Brex Assistant handles 99% of expense reports autonomously
- Ramp shipped a full procurement agent fleet in April 2026
- Monk handles AR end-to-end with collections agents that talk to customer AP portals

The frontier has moved from "AI extracts data" to "AI agents take actions across the full workflow." Customers will not pay a premium for "we extract invoices well." They will pay for "the agent does the entire month-end close for you."

**Anti-decision:** Do not say "we use vision models to extract invoices" in any customer-facing material. Say "the agent handles invoices."

---

## 2026-05-21 — Code vs Agent — the critical distinction

**Decision:** Decimal makes a hard architectural and marketing distinction between *code* and *agent*. They are different things, with different trust models, marketed differently.

**Code:**
- Deterministic. Does exactly what is written, every time.
- The multisig threshold. Spend caps. Time-locks. Required signer counts. Required approval chains.
- Cannot be overridden by humans, admins, employees, or agents.
- This is the *security* layer. The moat. The thing that makes BEC fraud structurally impossible.
- Customer pitch: "code-enforced policies that no one can override."

**Agent:**
- Probabilistic. Makes recommendations. Sometimes wrong.
- Reads invoices, drafts proposals, looks up vendors, normalizes CSVs, answers questions, replies to vendor emails.
- *Always* requires human approval before execution.
- This is the *automation* layer. The convenience. The thing that does work for you.
- Customer pitch: "the agent does the work for you."

**Why this matters:**
- Customers do not yet trust AI agents with money authority. Pitching "multisig as audit agent" is the wrong framing — it suggests the agent has authority. The agent has *zero* execution authority. It only drafts.
- The agent making a mistake is fine because code-enforced rules catch it before execution.
- The agent and the code are complementary, not the same layer. Marketing them as one thing destroys both.

**Anti-decision:** Never describe code-enforced rules as "agent decisions." Never give the agent any execution authority. The agent drafts; humans approve; code enforces; multisig executes.

---

## 2026-05-21 — Agent-with-tools architecture, not pipelines

**Decision:** Decimal's product architecture is an agent with a tool registry, not a sequence of hardcoded pipelines.

**Why:**
- Pipelines are brittle. Every new input type or workflow requires re-architecting.
- Agents with tools are flexible. New tools added → agent uses them automatically. New input types → agent figures it out with existing tools.
- The infrastructure must support tomorrow's features without rebuilding today's.

**What this means in practice:**

*Old (pipeline):*
```
upload PDF → vision model extracts → user reviews → creates proposal →
signers vote → execute → mark paid
```
Hardcoded. One pathway.

*New (agent):*
```
agent receives input (invoice / email / chat / CSV / "pay these 12 people")
→ agent decides what to do
→ agent calls tools as needed:
   read_pdf, read_email, read_csv,
   lookup_counterparty, lookup_payment_history,
   check_spend_rule, check_treasury_balance,
   draft_proposal, suggest_gl_code,
   send_for_review, notify_signers,
   reply_to_vendor_email, query_quickbooks,
   ...
→ agent reports to user, user approves
→ code-enforced multisig executes
```

The agent figures out the sequence. The product gets smarter without new pipelines.

**Engineering implications:**
- Tool registry, not hardcoded routes. Every existing endpoint becomes a tool the agent can call.
- Agent memory per org (past decisions, vendor patterns, user preferences, recurring intents).
- Compliance / policy rules encoded separately from agent reasoning — some become code-enforced, some are agent-respected constraints.
- Multiple input channels (email, web upload, Slack, chat, API) all converge to "input for the agent."
- The agent never holds execution authority. It drafts. Code executes.

**Customer-facing line:**
> Forward us anything. The agent figures out what to do. You approve. Code makes sure no one breaks the rules.

**Anti-decision:** Do not extend the current pipeline architecture. New features should land as new *tools* the agent can use, not new pipelines users walk through.

---

## 2026-05-21 — Trust framing for agents

**Decision:** Position agents as "doing the work for you," never "having authority over you."

**Why:**
- Public trust in AI agents handling money is still low and earned, not granted. The "agent autonomously moved $500K" headlines are bad headlines.
- The agent is a tool. The user is the authority. Code enforces the rules.
- This framing dovetails with the code-vs-agent distinction above.

**Phrasings to use:**
- "The agent reads your invoices."
- "The agent drafts your payment proposals."
- "The agent looks up your vendor history."
- "The agent suggests when to pay."

**Phrasings to avoid:**
- "The agent decides who gets paid."
- "The agent overrides your approval."
- "The agent has authority to..."
- "AI takes over your..."

**The agent does work. The user approves. Code enforces. Multisig executes.** That sequence — that order — is the trust contract.

---

## 2026-05-21 — The AI moat for Decimal specifically

**Decision:** Decimal's AI moat is not extraction. It is the *combination* of:

1. **Action-taking agents** at the level Brex / Ramp / Bill.com / Monk have shipped — table-stakes by 2027, must be matched.
2. **A flexible agent-with-tools architecture** that adapts to new workflows without re-engineering.
3. **Code-enforced execution at the multisig gate** that makes agent mistakes safe — the agent can draft a bad payment, but the multisig + spend rules + required approvers can stop it deterministically.
4. **Cross-border-corridor-intelligent** agents that know to route a payout via USDC + off-ramp instead of SWIFT.

None of the incumbents have all four. Bill.com and Tipalti have #1 and partial #2 but not #3 or #4. Brex and Ramp have #1 and #2 but are domestic-only and software-enforcement-only. The combination is the moat.

---

## 2026-05-21 — End goal: monopoly via full-stack ownership

**Decision:** The long-term game is to own the full stack — banking rails, payment flows, licenses, partnerships, AI orchestration. Same playbook as Deel (payroll + immigration + cap-table + IT) or Corgi (quoting + underwriting + claims + operations) or Mercury (banking + treasury + lending + custody charter).

**Implications:**
- Decimal's product surface widens over time. AP today, AR tomorrow, treasury, lending, FX, compliance, consumer payments (decimal.pay).
- Each layer reinforces the others — the agent gets smarter as it sees more of the customer's finance stack.
- Acquisitions of adjacent capabilities become a viable growth lever.

**Future products mentioned in passing:**
- **decimal.pay** — consumer mobile app for cross-border payments. Built on the same AI + code-enforced infrastructure. Vision-stage; not building today; AI infrastructure built for B2B AP becomes the foundation.

---

## 2026-05-21 — What the research told us, and what it didn't

**The competitor research is input, not output.** The research tells us:
- What features the incumbents have (so we know what's table-stakes vs differentiator)
- What workflows are valuable enough to charge for (so we know the AI agent's job)
- What the market caps and exit paths look like (so we can size the opportunity)

The research **does not** tell us what to build. That decision is ours, and it follows from:
- TAM-first thinking (TradFi B2B AP, not crypto-native)
- The two blockchain moats (cross-border + code-enforced security)
- The agent-with-tools architecture (flexibility over pipelines)
- The code vs agent distinction (trust contract)

---

## Reference documents

- `outputs/decimal-state-of-the-product.md` — what's built today
- `outputs/decimal-feature-catalog.md` — full feature survey from competitor research
- `outputs/feature-spec-ap-intake.md` — detailed specs for AP intake + counterparty intelligence + cut decisions
- `outputs/grid-integration-plan.md` — Grid integration phasing
- `outputs/quickbooks-research.md` — QuickBooks integration research brief
- `outputs/competitor-landscape.md` — 18-company landscape analysis
- `outputs/ai-in-fintech-research.md` — AI in fintech deep dive
- `outputs/production-env-contract.md` — current runtime env contract

---

## Open strategic questions (not yet decided)

1. **SMB-first or enterprise-first GTM?** SMB requires Bill.com-scale customer counts. Enterprise puts us against Altitude / Velocity. The escape route is a workflow defensible at SMB scale (Corgi pattern).
2. **Domestic-first or cross-border-first?** Cross-border is one of the two blockchain moats. Domestic AP is where Bill.com / Tipalti are strongest. Logic suggests cross-border-first as differentiation.
3. **Vertical focus?** Generic SMB AP vs specific vertical (agencies, e-commerce, consulting, etc.) where AI patterns can be deeply trained.
4. **QuickBooks scope.** One-way export vs bidirectional sync vs the "agent natively queries/writes QuickBooks as one of its tools" approach.
5. **Grid dependency timeline.** Phase 2 of Grid is blocked on sandbox access. If access takes another 30 days, do we build Spend Governance directly on Squads first and migrate later?
