# frames.ag — Deep Dive

> Companion to [`./how_it_works.md`](./how_it_works.md). Founders, funding, traction, custody model — the things outside the README.
> **Date:** 2026-05-02
> **Sources:** Web research agent + live API queries to `frames.ag/api/network/pulse` + GitHub + ETHGlobal showcase

---

## TL;DR — what we actually found

**frames.ag is a 4-month-old, ~2-person Lisbon-based project** built as a UX wrapper on top of **Privy** (confirmed via `privyWalletId` field in their public API responses). The founder is **Luís Freitas** ([@microchipgnu](https://x.com/microchipgnu)), former CTO of Bitte Protocol (NEAR-ecosystem AI-agent infra). The project began as **MCPay** (ETHGlobal hackathon submission, mid-2025), incorporated as **Frames Engineering, Inc.** in early 2026, GitHub org created **2026-01-07**.

**Live numbers from `/api/network/pulse` as of May 1, 2026 23:11 UTC:**
- **2,160 total wallets**
- **24 active in last 24h** (~1% DAU/total)
- **4,544 transactions in last 24h** but **$0.00 USDC volume**
- **$75.22K cumulative volume** since launch

**The $0 real volume is the headline.** All 4,544 daily transactions are internal calls to frames.ag's own API registry (Exa search, CoinGecko, etc.) using promo-credit balances they front-load on new wallets. **Real economic adoption is essentially zero.**

**They are not** what the README implied:
- ❌ Not custodying keys themselves — **using Privy underneath**
- ❌ Not Coinbase-backed or x402 Foundation member (not listed in [x402.org/ecosystem](https://x402.org/ecosystem))
- ❌ Not Stripe MPP partnership — self-integrated against public spec
- ❌ Not a sister of "Moltbook" — Moltbook is Matt Schlicht's project (acquired by Meta March 2026); frames.ag is a *skill in Moltbook's registry*, not a sibling product
- ❌ "CASH" token is **not** theirs — external stablecoin-style asset

**They are:**
- ✅ A **GTM-distribution wedge** wrapping Privy with a clever skill-file install pattern
- ✅ **Back-doored into a Meta agent surface** (Moltbook is now Meta-owned)
- ✅ Run by a **competent founder** with prior agent-infra experience
- ✅ The **single best-executed example of skill-file distribution** for a wallet today

**Strategic bottom line:** Treat as a **promising experiment, not production infrastructure**. The wedge (skill-file distribution) is real but fragile — when Coinbase's CDP / AgentKit ships the same UX, it collapses. Underlying trust is Privy, not Frames Engineering.

---

## 1. The company / founder

### Luís Freitas — founder, lead builder

| Channel | Link |
|---|---|
| GitHub | [github.com/microchipgnu](https://github.com/microchipgnu) |
| X / Twitter | [@microchipgnu](https://x.com/microchipgnu) |
| LinkedIn | [linkedin.com/in/microchipgnu](https://www.linkedin.com/in/microchipgnu/) |
| Personal site | microchipgnu.pt |

- **Location:** Lisbon, Portugal
- **Prior role:** **CTO / co-founder at [Bitte Protocol](https://www.bitte.ai/)** — NEAR-ecosystem AI agent infrastructure. *Note: his GitHub bio still references the Bitte identity; unclear whether he's fully left Bitte or this is a moonlight project.*
- **Code dominance:** authored 391 of ~477 commits in the original [MCPay repo](https://github.com/microchipgnu/MCPay) — by a wide margin the lead builder
- **Project Twitter:** [@framesag](https://x.com/framesag), legacy [@mcpaytech](https://x.com/mcpaytech)

### Marcelo Kunze — second contributor

- [github.com/marcelokunze](https://github.com/marcelokunze)
- Twitter: `@marcelokunze`
- Also Lisbon-based
- 86 commits on MCPay repo (engineering #2)
- No public title, but commit volume + geography suggest co-founder or first engineer

### Team & corporate

- **Legal entity:** Frames Engineering, Inc. (per footer of [frames.engineering](https://frames.engineering))
- **Team size:** Best estimate **2–4 people**. The frames-engineering GitHub org has **8 followers**, **4 public repos**, and **0 public members listed** — they are intentionally opaque about team
- **Telegram community:** 177 members, 16 online ([t.me/mcpay_tech](https://t.me/mcpay_tech))

### Timeline

| Date | Event |
|---|---|
| Mid-2025 | MCPay built as ETHGlobal hackathon project ([showcase](https://ethglobal.com/showcase/mcpay-fun-y16d3)) |
| **2026-01-07** | Frames Engineering GitHub org created |
| 2026-02-02 | Founder's own AgentWallet account created |
| Spring 2026 | Rebrand from MCPay → Frames |
| 2026-05-02 | Today — ~4 months old as a company, ~10 months old as a project |

---

## 2. Funding — none publicly announced

Searched Crunchbase, PitchBook, Tracxn, Messari, RootData, and general news. **Nothing found** for "frames.ag", "Frames Engineering", or "MCPay" as a venture round.

- **Homepage has a "BACKED BY" section** but the logos render client-side and are absent from static HTML. Either **stealth investors** or **placeholder section they haven't removed**. Either way: low-trust signal.
- **No accelerator confirmed** — not in the visible cohorts of a16z CSX, Colosseum, OnePiece Labs, Outlier Ventures Base Camp, or Coinbase Ventures portfolio listings
- **No token launched.** README's airdrop tier system (Bronze/Silver/Gold/Diamond with 1×–3× multipliers) is **a pre-launch points farm** — the airdrop is "coming," not real
- **MCPay had ETHGlobal Cannes 2025 prize history** + other Vercel/AI hacks; specific amounts not confirmed
- Founder's prior Bitte Protocol equity / NEAR ecosystem grants likely the runway source

**Verdict:** **bootstrapped or pre-seed friends-and-family.** Anyone considering business reliance on frames.ag should treat as a **pre-seed-stage solo-or-duo project**, not a funded company.

---

## 3. Traction — live numbers and the $0 volume problem

Pulled directly from `https://frames.ag/api/network/pulse` (public, no auth):

| Metric | Value |
|---|---|
| Total agents/wallets | **2,160** |
| New agents in last 24h | 0 |
| Active agents in last hour | 5 |
| Active agents in last 24h | **24** |
| Transactions last hour | 147 |
| Transactions last 24h | **4,544** |
| **USDC volume last 24h** | **$0.00** |

Homepage cumulative counters: 371,388 transactions, **$75.22K total volume**.

### Reading these numbers carefully

**The 1% DAU/total ratio is bad** — 24 active out of 2,160 means most wallets are dormant.

**The $0 real volume is the killer.** 4,544 daily transactions × $0.00 USDC volume = **all internal promo-credit transactions**. Their product description ("All new wallets funded with free cash") confirms this — they front-load wallets with promotional balance, agents call frames.ag's own API registry (Exa, CoinGecko, OpenRouter, Twitter) at sub-cent prices, transactions tick up, but **no real merchant flow exists yet**.

**Trending APIs are entirely frames.ag's own registry endpoints.** Top API has 1,500 calls/hour — i.e., the entire economy is internal subsidy.

### GitHub & social signals

- [microchipgnu/MCPay](https://github.com/microchipgnu/MCPay): **86 stars** (legacy public repo)
- frames-engineering org repos: **4 stars** on `skills`, 2 on `wordspace`, 0 on others
- Twitter [@framesag](https://x.com/framesag): low activity (single tweet referenced)
- Telegram: 177 members

**This is a hackathon-stage project pretending to be a startup.** The product execution is good; the actual usage is not yet there.

---

## 4. The skill-distribution model (live confirmation)

**All three skill files were successfully fetched:**

- **[skill.md](https://frames.ag/skill.md)** — v0.2.0, ~10K+ words. The full AgentWallet skill (the README the user pasted)
- **[heartbeat.md](https://frames.ag/heartbeat.md)** — periodic check-in script for agents to ping balance, referrals, tier. Designed to add to an agent's persistent loop.
- **[skill.json](https://frames.ag/skill.json)** — v0.1.12. Declares `moltbot.emoji: "$"`, `category: "finance"`, lists triggers and required bins (`curl`)

### Where the skill lives (registries it's published to)

1. **Moltbook's "moltbot" skill format** — confirmed by `moltbot` metadata block in skill.json. **Moltbook is now Meta-owned** (acquired March 2026). frames.ag has back-doored into a Meta agent surface as a finance skill.
2. **OpenClaw** ([openclaw.ai](https://openclaw.ai), Peter Steinberger's "personal AI assistant on any platform") — listed on frames.ag homepage as supported client
3. **Their own [frames-engineering/skills](https://github.com/frames-engineering/skills) GitHub repo** — 4 stars, last updated 2026-04-15
4. **Claude Code, Cursor, OpenCode, Codex** — all listed on the homepage as supported clients (consumed via the same skill.md fetch pattern)

**This confirms the architectural thesis from `how_it_works.md` — distribution is via skill files read by agent runtimes, not via developer SDKs.**

---

## 5. Custody model — confirmed Privy wrapper

**Confirmed via API response inspection:** Wallets carry a `privyWalletId` field. **frames.ag is a Privy reseller / UX wrapper.**

What this means:
- Underlying signing: **Privy MPC** (TEE-backed since their 2024–2025 architecture)
- frames.ag holds the Privy app credentials
- Users get an `mf_` API token that authorizes frames.ag to instruct Privy to sign
- **Email OTP only** for onboarding — no full KYC, no document upload, no geo-fencing
- **Server-side custody = users do not hold keys.** A frames.ag outage means users can't move funds without a Privy-side recovery flow (which Privy supports but frames.ag has not surfaced in the public docs)

### Regulatory exposure

This is **unhosted-wallet-as-a-service from a Portuguese company serving global users with no KYC**:
- Under **FinCEN** interpretation: borderline MSB. Probably below the de minimis perimeter at $75K cumulative volume; unambiguously over it at $10M+
- Under **MiCA** (Portugal enforces): email-only KYC almost certainly does not satisfy CASP requirements above any reasonable threshold
- **They are pre-regulatory at this scale; if they grow, this breaks.**

The trust profile is therefore: **trust Privy** (good — well-architected MPC), **be aware Frames Engineering is the access layer** (less trusted — small, no funding, no compliance posture). If frames.ag rugs or shuts down, Privy's recovery is the backstop, but the UX is undefined.

---

## 6. Token / airdrop reality check

- **No token launched.** Despite the airdrop tier system in the README
- **No TGE date** announced
- **"CASH" token in their tokens list is NOT frames.ag's token** — it's an external stablecoin-style asset they accept (likely [Cash by Catena Labs](https://catenalabs.com/) or similar agent-native unit of account)
- **The airdrop is a pre-launch points farm** — Bronze/Silver/Gold/Diamond tiers (1×–3× multipliers) are gamification levers to drive referral signup before any TGE
- **No airdrop snapshot date** published

This is **classic pre-token funnel-building** to drive top-of-funnel before a potential token launch. Whether the token ever materializes depends on:
- Whether real volume materializes (currently $0 organic)
- Whether they can attract any actual VC capital
- Whether the regulatory environment in 2026–27 makes a token feasible

---

## 7. Competitive positioning (corrected)

| Competitor | Custody | Distribution | Differentiator | vs frames.ag |
|---|---|---|---|---|
| **Privy** (Stripe) | MPC + TEE | Developer SDK | The infra layer — **frames.ag uses this under the hood** | Strictly upstream of frames.ag |
| **Crossmint** | MPC + custodial | SDK / API | Multi-chain, NFTs, enterprise. $23.6M Series A | More mature, more verified volume |
| **Coinbase AgentKit** | TEE-backed CDP wallets | SDK + CDP | First-party Coinbase, deep onramp, x402 native | **Existential threat** when they ship same UX |
| **Skyfire / KYAPay** | Custodial | API for agents | KYC + spending controls, more compliance-forward | Less GTM-native, more enterprise |
| **Turnkey** | TEE-backed signing | Developer API | Pure infra, no UX | Different layer |
| **Catena Labs (ACK)** | Custodial agentic banking | Spec + API | Sean Neville (USDC inventor), $18M seed | Different category — regulated FI play |
| **Halliday** | Smart accounts | Workflow builder | Agent workflow orchestration | Different category |
| **frames.ag** | **Privy underneath** | **Skill-file / agent-runtime native** | Agents read URL, no developer SDK install | The wedge |

### The differentiated wedge

**frames.ag is not building infra — it's a distribution wrapper around Privy with two specific innovations:**
1. **Skill-file distribution** (the agent reads markdown, not the developer reads SDK docs)
2. **Pre-integrated x402/MPP API registry** (Exa search, CoinGecko, OpenRouter — the agent has things to call right out of the box)

**The bet:** "AI agent reads markdown and onboards itself" beats "developer integrates an SDK" as the dominant adoption pattern.

### The risk

When **Coinbase ships the same UX through CDP / AgentKit** (they're getting close — see [Payments MCP](https://www.coinbase.com/developer-platform/discover/launches/payments-mcp)), the wedge collapses. Coinbase has:
- First-party stablecoin onramp
- Native x402 (they invented it)
- Deeper compliance posture
- Brand trust
- Massive distribution

**The window for frames.ag to establish itself before Coinbase moves is probably 6–12 months.** They're 4 months in with $0 real volume. The clock is short.

---

## 8. The Tempo (MPP) integration reality

The README declares `mpp.methods: ["tempo"]` and `mpp.endpoint: /api/wallets/{username}/actions/mpp/pay`. The agent confirmed:

- **Tempo (eip155:4217)** is Stripe + Paradigm's stablecoin chain — [mainnet launched March 2026 with MPP](https://www.theblock.co/post/394131/tempo-mainnet-goes-live-with-machine-payments-protocol-for-agents)
- frames.ag is among the early MPP integrators
- **No formal Stripe partnership announcement** naming frames.ag
- Most likely they self-integrated against the public MPP spec
- **24h pulse data shows $0.00 USDC volume** — the MPP path is wired but receiving no traffic

So technically integrated, commercially absent.

---

## 9. Coinbase / x402 ecosystem positioning

- **Not in [x402.org/ecosystem](https://x402.org/ecosystem)** despite being one of the earliest x402 implementers. Either:
  - Falling out / political tension with Coinbase, or
  - Simply hasn't submitted, or
  - Deemed too small to feature
- **Not an x402 Foundation member.** [The April 2026 Linux Foundation announcement](https://www.coindesk.com/tech/2026/04/02/coinbase-s-ai-payments-system-joins-linux-foundation-gathers-support-from-google-stripe-aws-and-others) lists Cloudflare, Stripe, Adyen, AWS, Amex, Base, Circle, Fiserv, Google, KakaoPay, Mastercard, Microsoft, Polygon, Shopify, Solana Foundation, Thirdweb, and Visa — **frames.ag / MCPay are absent**
- **Coinbase Onramp use** is just public CDP API integration — not a partnership
- **No Coinbase Ventures investment**

This positioning matters: as Coinbase consolidates the x402 ecosystem under the Linux Foundation governance, **frames.ag is on the outside looking in.** That's a structural disadvantage.

---

## 10. Red flags / structural concerns

1. **Server-side custody = single point of failure.** If frames.ag rugs or goes down, Privy's recovery is the backstop but UX is undefined
2. **Email OTP only, no KYC** — fine at $75K total volume, fatal at $10M
3. **$0.00 of real 24h USDC volume** despite 4,544 transactions — internal subsidy pattern. **No real economic adoption yet.**
4. **Founder still listed as "@frames-engineering" but bio identical to his Bitte identity** — unclear if fully left or moonlighting
5. **GitHub org has 0 public members** — intentionally opaque team
6. **"BACKED BY" section without visible logos** — either stealth backers or vaporware section. Both are low-trust signals
7. **Not in official x402 ecosystem listing** — outside the Coinbase orbit
8. **Heavy dependency on Moltbook (now Meta)** — if Meta deprioritizes the moltbot skill registry, a major distribution channel evaporates
9. **6–12 month window** before Coinbase ships the same UX via CDP and the wedge closes

---

## 11. Strategic takeaway

**For our research thesis (problems in AI × crypto worth solving):**

- ✅ **The skill-file distribution model itself is a real insight worth studying.** Even if frames.ag fails, the GTM pattern of "agent reads markdown, onboards itself" is novel and probably correct. Worth noting for any agent-payment product we'd build.
- ✅ **The Moltbook → Meta backdoor is genuinely interesting.** A 2-person Lisbon team has wired itself into a Meta agent surface. That's clever leverage that an established player wouldn't bother to do.
- 🟡 **frames.ag's actual position:** A clever distribution layer wrapping Privy that targets a window before Coinbase consolidates. Could either become a real wallet for AI agents OR get acqui-hired into a bigger ecosystem (Coinbase, Stripe via Privy, or Meta via Moltbook). VC-trajectory-wise, it's a pre-seed bet on the founder.
- 🔴 **Don't model it as competitive infra.** The custody, compliance, and capital are all someone else's. Treat as UX layer, not infra.

**For the "build a better Credible" thesis (per `markets/payfi/liquidity_models.md`):**

- frames.ag is not in Credible's market. It's an **agent-payments wrapper**, not a cross-border B2B remittance orchestrator. They occupy adjacent slots in the agent-payments stack.
- If you were building "Credible for AI agents" (autonomous-agent cross-border payouts), frames.ag's wallet-issuance layer + Credible's payment orchestration could plug together. **That's the lateral-useful angle.**

**For founder credibility:**

Luís Freitas is a real builder with real prior experience (Bitte Protocol CTO) shipping clean products fast. Worth following on X regardless of frames.ag's outcome — his next project may be the more interesting one.

---

## 12. YouTube content

Single substantive founder appearance found:

- **[Payments for MCPs: Building the Future with x402 and AP2 — Luís Freitas (Pragma New Delhi 2025)](https://www.youtube.com/watch?v=0oi8ZEPILaI)** — Luís presenting MCPay at the Pragma summit. The single most substantive founder source.

Other:
- [MCPay.fun ETHGlobal showcase](https://ethglobal.com/showcase/mcpay-fun-y16d3) — original hackathon submission with demo video
- No major podcast appearances under either MCPay or frames.ag branding

Worth pulling the Pragma talk transcript if we want to dig into Luís's framing of the x402 + AP2 thesis. Want me to do that?

---

## Sources

**Live API queries (this session):**
- [frames.ag/api/network/pulse](https://frames.ag/api/network/pulse) — public stats endpoint
- [frames.ag/api/wallets/microchipgnu](https://frames.ag/api/wallets/microchipgnu) — confirms Privy custody via `privyWalletId`
- [frames.ag/skill.md](https://frames.ag/skill.md), [heartbeat.md](https://frames.ag/heartbeat.md), [skill.json](https://frames.ag/skill.json)

**Founder identity:**
- [github.com/microchipgnu](https://github.com/microchipgnu)
- [linkedin.com/in/microchipgnu](https://www.linkedin.com/in/microchipgnu/)
- [@microchipgnu on X](https://x.com/microchipgnu)

**Project surface:**
- [github.com/frames-engineering](https://github.com/frames-engineering) — 4 repos, 8 followers, 0 public members
- [github.com/microchipgnu/MCPay](https://github.com/microchipgnu/MCPay) — 86 stars
- [@framesag](https://x.com/framesag), [@mcpaytech](https://x.com/mcpaytech)
- [t.me/mcpay_tech](https://t.me/mcpay_tech) — 177 members
- [docs.mcpay.tech](https://docs.mcpay.tech/), [vlayer partner page](https://docs.mcpay.tech/partners/vlayer)
- [frames.engineering](https://frames.engineering) — corporate site

**Moltbook context:**
- [moltbook.com](https://moltbook.com)
- [Meta acquires Moltbook (Axios, March 2026)](https://www.axios.com/2026/03/10/meta-facebook-moltbook-agent-social-network)
- [Matt Schlicht profile (Fortune)](https://fortune.com/2026/02/02/meet-matt-schlicht-the-man-behind-moltbook-bots-ai-agents-social-network-singularity/)

**Tempo / MPP / x402 ecosystem:**
- [Tempo mainnet launch (The Block)](https://www.theblock.co/post/394131/tempo-mainnet-goes-live-with-machine-payments-protocol-for-agents)
- [Stripe MPP blog](https://stripe.com/blog/machine-payments-protocol)
- [x402.org/ecosystem](https://x402.org/ecosystem) — frames.ag absent
- [x402 joins Linux Foundation (CoinDesk)](https://www.coindesk.com/tech/2026/04/02/coinbase-s-ai-payments-system-joins-linux-foundation-gathers-support-from-google-stripe-aws-and-others)

**Founder talk:**
- [Pragma New Delhi 2025 — Luís Freitas on x402/AP2](https://www.youtube.com/watch?v=0oi8ZEPILaI)
- [MCPay.fun ETHGlobal showcase](https://ethglobal.com/showcase/mcpay-fun-y16d3)
