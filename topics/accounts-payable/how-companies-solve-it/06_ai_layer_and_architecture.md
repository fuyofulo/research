# Stage 6 — The AI/Agent Layer + Overall Architecture

*How each company applies AI across the pipeline, the autonomy claims, the moat they claim, and the architecture pattern to build.*

## The problem / question

**The shift: extraction → action.** The 2024–26 frontier is agentic AI — from *suggesting* (IDP reads, ML predicts, flags a human; touchless ~55–75%) to *acting within guardrails* (the agent pulls contract/PO/history, decides, takes the next action; ceiling ~80–95%). Each automation wave pushes the human further downstream: keying → exceptions → now *reviewing the agent's decisions and authorizing payment*.

**The honest touchless number:** average org ≈ **32.6%** (Ardent). Every 85–99% a vendor cites is exceptional/mature-state, not the field average.

**Why money movement stays human-gated** (structural, not technical): (1) fraud (79% of orgs hit in 2024; auto-pay without bank-change verification *increases* exposure); (2) irreversibility (ACH/wire don't come back); (3) errors compound into the GL + tax filings.

**Moat or commodity?** Decisive across the corpus: **extraction is commoditizing** (frontier LLM + RAG matches incumbents in ~6 months; inference cost fell ~280×). The durable moat = **proprietary data + correction loops + deep ERP sync + the orchestration layer + (crypto-only) code-enforced execution.**

## How each company solves it

| Company | AI approach | Claimed moat | Architecture | Segment |
|---|---|---|---|---|
| **Bill.com** | LLM-on-top + workflow ("BILL AI" 2025) | "250M invoices / 8M network" data narrative (*real moat = CPA channel + 20yr MTLs*) | pipeline + agents bolted on; FBO float | SMB→low-mid |
| **Tipalti** | GPT-4 (2023)→discrete agents (2025) | global rails + KPMG tax + NetSuite depth (*agents not the differentiator*) | rules-gateway (26K rules) | mid-market/enterprise global |
| **Stampli** | AP-specific ML since 2018 | "decade of AI leadership" + collaboration hub + 70 ERPs | invoice-hub + Billy; no float | mid-market |
| **Vic.ai** | purest autonomy bet (proprietary DL) | ">1B invoices + autonomy depth" | autonomy-first STP → VicPay | upper-mid/enterprise |
| **Ramp** | **most aggressive shipper; collapsed many agents → ONE unified agent + thousands of skills** (2026) | agent fleet + speed + closed-loop card+AP+procurement data | **agent-with-tools** (Omnichat → LLM-proxy → unified agent → tool catalog) | SMB→enterprise (US) |
| **Request Finance** | AI OCR (AI not the pitch) | crypto-native AP leader, non-custodial, Safe multisig | non-custodial (unsigned calldata) | crypto-native (EVM) |
| **Routable** | OpenAI OCR (AI not the pitch) | API-first payouts + onboarding + tax + sync around swappable rails (Brale stablecoin) | API-first pipeline | marketplaces/payouts |
| **Altitude** | **no AP-AI agent**; the "agent" is the programmable smart-account | self-custodial Solana custody + **code-enforced on-chain policy** + Squads' audited pedigree | **code-enforced execution** (Grid → Squads SAP) | crypto-native (Solana) |

*Brex: Brex Assistant ("handles 99% of expense reports autonomously"); spend-suite, software-enforcement-only, US.*

## The spectrum — "AI = what I extract" → "AI drafts, code executes"

1. **Extraction-as-commodity (the floor everyone stands on).** OCR + GL coding. Matchable in ~6mo with LLM+RAG. **No one should pitch this as the moat** — yet BILL's "250M invoices," Tipalti's "99% accuracy," Vic's ">1B invoices" all lean on it. Narratively compelling, technically thin.
2. **Proprietary-data + ERP-depth moat.** Vic.ai (correction loops), Tipalti (NetSuite sync — also its top complaint), Stampli (per-customer GL learning + 70 ERPs). The defensible piece is **deep two-way ERP sync, not the model.**
3. **Orchestration / agent-fleet moat.** Ramp is the leader and cleanest signal — it **abandoned hardcoded specialized-agent pipelines for one unified agent + a large tool catalog** once models got good enough. But Ramp's agents are **software-enforced and US-domestic** — recommend, human approves, rule caps backstop.
4. **Code-enforced execution (the crypto-native differentiator).** Only **Altitude** (and structurally **Request** via Safe) puts the execution gate *in code no admin/employee/agent can override*. "$5K/week" is a `SpendingLimit` PDA enforced by the SVM; m-of-n + time-locks are on-chain. TradFi (even Ramp) **structurally cannot** match this — they enforce policy in software over partner-bank balance sheets.

**No incumbent has all four.** BILL/Tipalti: #1 + partial #2. Brex/Ramp: #1 + #3 but software-only + domestic. **The defensible position is the intersection — agent-with-tools orchestration (Ramp-grade) + code-enforced multisig execution (crypto-only).**

## Build implication

1. **Build agent-with-tools + a tool registry, not hardcoded pipelines.** Strongest empirical signal in the corpus: Ramp's 2026 collapse from hundreds of hard-wired agents → one unified agent calling thousands of skills. Make every endpoint a tool (`read_pdf, lookup_counterparty, check_spend_rule, draft_proposal, suggest_gl_code, notify_signers...`); per-org memory; new features land as new *tools*, not new user-walked pipelines; all input channels (email/upload/Slack/API) converge to "input for the agent."
2. **Don't pitch extraction as the moat** (Vic.ai is the cautionary case). Say "the agent handles invoices / drafts proposals," never "we extract invoices." The agent *does work*; it never holds execution authority.
3. **Make agent mistakes structurally safe via code-enforced multisig execution — the defensible combination.** The trust contract is a strict sequence: **agent drafts → human approves → code enforces → multisig executes.** Because caps/required-signers/chains live in code that can't be overridden (Altitude proves it's real and audited on Solana), *an agent drafting a bad payment cannot execute it* — which lets you safely give the agent more autonomy than Ramp/BILL can, and directly attacks BEC (the #1 fraud vector).
4. **Respect the real table-stakes the moat analysis reveals:** deep two-way ERP sync (the true moat + biggest complaint = a quality opening), tax/compliance (Tipalti's KPMG engine; a confirmed gap for crypto-native), multi-entity. **The rail (USDC/Solana) is not the moat.**
5. **The hard part:** not the agent (table-stakes by 2027), not the rail (commodity). It's (a) deep two-way real-time ERP sync that doesn't corrupt the books; (b) the tax/compliance layer; (c) cleanly separating the **convenience layer** (agent, probabilistic, sometimes wrong) from the **security layer** (code-enforced multisig, deterministic, un-overridable). *Marketing them as one thing destroys both* — keep "code" and "agent" distinct.

*Gaps: no company publishes audited touchless rates (only Ardent's 32.6% average); BILL/Tipalti model architectures undisclosed (Ramp is the transparent exception); Altitude has no AP-AI agent to benchmark (its relevance is the code-enforced execution layer).*
