# Plan: Pitch & Raise Capital for a Solana Cross-Border Stablecoin Payments Neobank

## Context

**Why this plan exists.** A 22-year-old solo technical founder, based in India, living with parents (no immediate cash-flow pressure), has spent ~5 days producing 200KB of high-quality research on the AI × crypto stack — including deep dives on Credible Finance, frames.ag, Blockworks, agent-payments compliance, and PayFi liquidity models. They've decided to take a serious shot at building a Solana-based cross-border stablecoin payments neobank — the same wedge Credible Finance occupies but rebuilt with corrections from research (Web 2.5 honesty, multi-chain split, sharper compliance posture, better risk-transfer waterfall).

**The core constraint.** Solo, no co-founder yet, no MVP, no traction, no fundraising relationships. Real assets: technical capability (Claude Code daily), India base (cheap runway + Indian NBFC ecosystem proximity), research depth (artifact quality already higher than most pre-seed founders), and time.

**The intended outcome.** Within 60 days: shipped a thin public demo, submitted to 3+ grant programs, attended at least one demo day (StableHacks Zurich May 28), made first design-partner contact, and have a clear yes/no/iterate signal from the market on the wedge. Within 6 months: Outlier Ventures Base Camp acceptance, Stellar grant in pipeline, MVP scoping conversations with Colosseum Fall 2026 cohort.

**Why now.** The post-GENIUS Act window (US PPSI rules effective July 18, 2026) makes US-onshore stablecoin payment infrastructure newly defensible. Credible's existence proves the model — and their gaps (no published audits, no first-loss tranche, opaque LP custody, US-restricted) leave room for a better-positioned competitor.

---

## Strategic Recommendation

**Skip YC Summer (May 4) and Colosseum Spring Hackathon (May 11). Aim for StableHacks May 28 as the forcing function. Optimize the next 4 months toward Colosseum Fall (Sept 28) + Outlier Ventures Base Camp + Stellar Development Foundation grant.**

This is **Credible's exact playbook**, executed one cycle later: Outlier Spring 2024 → Cypherpunk Hackathon Dec 2024 → Colosseum Cohort 4 Mar 2026 + Stellar grant Mar 2026 = ~$525K total. Target the same pipeline.

The other two valid alternatives:
- **Aggressive:** Sprint Colosseum Spring May 11 *and* StableHacks May 28. Risk: ship two half-finished things. Worth it only if comfortable sleeping 4hrs/night for 30 days.
- **Conservative:** Skip both May deadlines. Spend 6 weeks on serious MVP + design-partner LOI. Apply Outlier mid-June. Risk: no public proof of life for 60 days.

The recommended path is the right balance: forces an early public artifact (StableHacks demo) without burning out trying to ship Anchor code in 9 days.

---

## The 6-Week Sequenced Plan

Today is **May 2, 2026 (Saturday)**. Each week ends with a tangible deliverable.

### Week 1 (May 2 – May 8): Position, don't build

**The mistake to avoid:** opening Cursor and writing Anchor code on Day 1.

- **Day 1–2:** Decide the wedge (US-onshore vs. vertical vs. open-source-compliance). This is the single highest-leverage decision. Default to US-onshore for fundability, but if the vertical pick (e.g., AI agent payments — supported by your existing `/Users/fuyofulo/research/ai_crypto/research/markets/agent_payments/compliance.md`) is genuinely sharper, commit to it. Write the 1-page narrative memo: wedge sentence, why-now, the single technical insight (3–5 day credit duration is what makes the pool solvent).
- **Day 3–4:** Build the 12-slide deck using the `create-pitch-deck` skill. Slide order: Problem → 60-sec demo concept → Wedge → Market math → Architecture (Web 2.5, honest) → Compliance posture → Competitive (vs. Credible, vs. Wise/Bridge) → 6-month plan → Ask → Founder slide → Honest "what could go wrong" → Appendix.
- **Day 5–7:** Founder narrative work. Record yourself doing the 60-sec pitch on Loom. Watch it. It's bad. Do 30 more takes. Get to 90 seconds without fillers.
- **In parallel:** File **FinCEN MSB registration** if pursuing US-onshore wedge (free, 2 hrs of paperwork). "Registered MSB" on the deck moves the needle on every subsequent conversation.
- **Deliverable:** Wedge memo + 12-slide deck PDF + Loom 90-sec pitch + 8-name warm-intro target list.

### Week 2 (May 9 – May 15): Smallest possible demo + StableHacks application

- **Day 8–10:** Build the smallest possible demo. Not the full MVP. The demo: a Next.js page, user enters $100, button click → backend calls Solana devnet program (forked from Marginfi/Kamino reference code, not custom-written) that pulls 100 USDC from a faucet-funded pool → calls Razorpay sandbox to trigger 8,500 INR test payout → shows settled transaction. **Time budget: 30 hours of building, capped.**
- **Day 11–12:** Submit StableHacks May 28 (institutional stablecoin track — your wedge fits exactly).
- **Day 13–14:** Apply to **Solana Foundation grants** (rolling). Apply to **Circle Alliance Program** (free, no equity, USDC infra + credibility logo — unambiguous +EV).
- **Deliverable:** StableHacks submission in, Circle Alliance application in, Solana Foundation grant application in, 90-sec demo video on YouTube/Loom, working devnet transaction signature you can show.

### Week 3 (May 16 – May 22): Co-founder search + first partner conversations

- **Day 15–17:** Begin co-founder search. Target shape: a fintech-operator (3–5 yrs at Razorpay, Cashfree, NIUM, Bridge — someone who's seen the rails), NOT another technical founder. **India advantage:** Razorpay/Cashfree alumni are physically reachable. Where to look: Solana Bangalore meetups, Superteam India Discord, ex-PayPal/Stripe LinkedIn India network. Send 30 cold messages with the deck. Realistic: 3 replies, 1 conversation.
- **Day 18–19:** Cold outreach to 10 potential design partners — small US-side fintechs serving India/Nigeria/Philippines (Abound, Pexx, Borderless, LemFi-tier). Pitch is *"We're building USDC-backed instant-settlement infra. Looking for 3 design partners willing to do a 30-min call and 60-day sandbox integration. No commitment."* Goal: 1 LOI by end of Week 4.
- **Day 20–21:** Apply to **OnePiece Labs × Solana APAC Bootcamp** (geo-aligned, India-friendly cohort, Credible's exact accelerator chain).
- **Deliverable:** Co-founder pipeline (5+ active conversations), 10 design-partner outreaches sent, 1+ scheduled call.

### Week 4 (May 23 – May 29): StableHacks demo day + first LOI push

- **Day 22–25:** Polish demo for StableHacks May 28. The week before any pitch event, stop building, start rehearsing. Run pitch with 5 different friends/mentors. Tighten 2 weakest slides.
- **Day 26 (May 28):** **StableHacks Zurich demo day.** Even if you don't win, the room is the prize. Talk to every founder + judge. Get 10 contacts. Follow up within 48 hours. (If travel cost is prohibitive, attend remotely — most demo days have hybrid format in 2026.)
- **Day 27–28:** Convert one design-partner conversation into a soft LOI (a Slack/email saying *"yes, we'd integrate if you ship X by Y"* is enough — doesn't need a signed PDF).
- **Deliverable:** StableHacks placement (or honest debrief), 1 design-partner LOI in writing, 5+ post-event followups in motion.

### Week 5 (May 30 – June 5): Conditional based on Week 4 results

This week branches. See Decision Points below. Default plan if no breakout in Week 4:

- **Day 29–31:** **Outlier Ventures Base Camp application** (rolling, but Spring cohort apps close ~mid-June). Use Credible playbook as social proof: *"Outlier funded Credible at this exact stage with this exact wedge. Here's why we're better-positioned for the post-GENIUS Act window."*
- **Day 32–33:** Register for **ETHGlobal NYC (June 12–14)** or **Lisbon (July 24–26)**. In-person presence matters for grant conversations even if you don't win.
- **Day 34–35:** Begin building the actual MVP (Anchor program scoped to deposit/withdraw/credit-out/repay, Postgres ledger, Persona KYC integration, Razorpay live integration). Use `scaffold-project` and `build-defi-protocol` skills. Target: usable sandbox by mid-July.
- **Deliverable:** Outlier application submitted, ETHGlobal registered, MVP scaffolded.

### Week 6 (June 6 – June 12): Build deeper or pivot

- **Day 36–38:** If LOI in hand → MVP build is the only thing that matters. Channel everything into shipping a sandbox the partner can integrate against.
- **Day 39–40:** If NO LOI → hard checkpoint. The honest read: 6 weeks in with no design partner = wedge isn't working as pitched. Iterate the wedge with people who said no. Try different corridor (Nigeria, Philippines) or different customer profile (B2B payroll vs. NRI remittance).
- **Day 41–42:** **Stellar Development Foundation grant application.** Credible got $150K from them in March 2026 — same playbook, different chain. Cross-border stablecoin payments is their explicit mandate. Application is heavy but the deck is reusable.
- **Deliverable:** Either real MVP build kickoff with LOI in hand, or documented wedge pivot. Plus Stellar grant submitted.

---

## Decision Points

- **End Week 1, if wedge undecided →** stop. The plan cannot proceed without this commitment. Default to US-onshore for fundability.
- **End Week 2, if working demo doesn't happen →** don't ship a broken one. Pull the StableHacks app and switch to Outlier Base Camp instead (no demo required).
- **End Week 3, if zero co-founder traction →** re-position deck for solo. Lead with technical depth + research as your "team substitute." Drop the co-founder ask; reframe as "first 2 hires post-funding."
- **End Week 4, if StableHacks places top 3 →** reorder everything. Skip Outlier app for now. Use placement to (a) apply to Colosseum Fall (announces ~July, apps ~August), (b) push for warm intros to Hack VC / Robot Ventures via judges, (c) publish a blog post that becomes the founder-narrative anchor.
- **End Week 4, if StableHacks doesn't place →** execute Outlier path on schedule. No emotional response. Outlier funded Credible at this stage with no hackathon win.
- **End Week 4, if 1+ design-partner LOI →** MVP build is the only thing that matters Weeks 5–10. Pause grant apps past Outlier+Stellar.
- **End Week 6, if no LOI and no grant in pipeline →** execute Plan B (see Cash-Flow section).

---

## Critical Artifacts Needed

In priority order — without these, none of this works:

1. **The wedge memo (1 page).** Written commitment to US-onshore vs. vertical vs. open-source-compliance positioning. Week 1.
2. **The 90-second Loom pitch video.** Single most-leveraged artifact. Used in every grant app, every cold email. Week 1, polished by Week 2.
3. **The 12-slide deck (PDF).** Reused across StableHacks, Outlier, Stellar, Solana Foundation, Circle Alliance, ETHGlobal sponsor convos. Week 1.
4. **The thin demo video (90 seconds).** Devnet transaction sig + Razorpay sandbox payout + dashboard screenshot. Week 2.
5. **At least 1 design-partner LOI (informal).** Turns "yet another solo founder" into "real company." Week 4.
6. **Working devnet program ID + transaction signatures.** Public proof of technical credibility. Posted on Twitter/X. Week 2.
7. **FinCEN MSB registration (if US-onshore wedge).** Free, 2 hours of paperwork. Week 1.

---

## Cash-Flow Plan B

User is living with parents in India — no immediate cash pressure. This is the biggest single advantage in the entire plan and should be guarded ruthlessly. Don't burn it on premature lifestyle expansion.

**However:** if no grant/accelerator signal lands by **end of Week 12** (early August), transition to:

1. **Superteam India bounties** — $500–5,000 per bounty in USDC, 10–15 hrs/week = $1–4K/month. Trivial to start (you live in Claude Code, you can clear these fast).
2. **Solana audit / code review work** at $100–200/hr. Listing on Superteam talent network. 10 hrs/week = $1–2K/week.
3. **Apply to Superteam Earn / Agentic Engineering Grant (200 USDG)** — small but easy. Use `apply-grant` skill.
4. **Last resort: 3-month full-time contract** at a Solana startup ($8–15K/month). Slows founder work by 60% but buys runway.

**Threshold for triggering Plan B:** end of Week 12, if zero grants accepted AND zero accelerator interviews scheduled AND zero LOIs converted.

---

## Top 2 Failure Modes + Mitigations

### Failure mode #1: "Why are you the right person to build this? Credible exists, has fintech veterans, is cash-flow positive."

This kills the pitch in 90% of investor calls. Pick one of three positions and own it:

- **Position A (US-onshore wedge):** *"Credible is UAE-based and US-restricted on the LP side. I'm building the US-onshore equivalent with Reg D 506(c) wrapper, FinCEN MSB, and B2B-only KYB — the first version US institutional capital can deposit into compliantly. The post-GENIUS Act July 2026 window makes this newly possible."* Most defensible. Recommended default.
- **Position B (Vertical wedge):** *"Credible serves remittance fintechs. I'm building the same primitive for [B2B payroll for international contractors / agentic AI payments / DePIN node payouts] — a vertical Credible explicitly hasn't gone after."* Requires picking the vertical and substantiating it.
- **Position C (Open-source compliance-forward):** *"Credible has zero published smart contract code, opaque KYC, no published first-loss tranche. I'm building the same model open-source, with explicit Reg D wrapper, published audits, first-loss tranche."* Slower but trust-compounding.

**Mitigation:** rewrite Slide 7 of the deck to lead with chosen position. Rehearse the 30-second answer until automatic.

### Failure mode #2: "Your compliance story is hand-waving."

Mitigation:
- File FinCEN MSB registration in Week 1. "Registered MSB" on the deck = serious.
- Get a written quote from a fintech-compliance lawyer on Reg D 506(c) wrapper. Quote alone signals seriousness even if not engaged.
- Name the *type* of banking partner (Cross River, Lead Bank — Credible's playbook is public). Admit honestly: *"12-month onboarding cycle, this is part of the funding ask."*
- Dedicate one slide to "what we don't have yet and how funding gets us there." Investors who fund pre-MVP companies *expect* gaps; what they punish is pretending gaps don't exist.
- Use the existing research as evidence of compliance depth: *"I've documented the 5 sharpest unsolved compliance gaps in agent payments and the corrections that need to be made to Credible's structure for US deployment. Happy to share."*

---

## India-Specific Considerations

Living in India is a meaningful asset, not a constraint, for this specific business:

- **Indian NBFC ecosystem is geographically reachable.** Credible's founder leveraged Western Fintrade NBFC board exposure as the unfair advantage. Razorpay, Cashfree, NIUM, and dozens of NBFC operators are in Bangalore/Mumbai. Cold meetings happen face-to-face, not over Zoom at 1 AM.
- **Superteam India + Solana Bangalore are active communities.** Lower-friction venue for first co-founder/operator conversations.
- **OnePiece Labs Solana APAC Bootcamp** (launched Feb 2026) is geo-aligned. Credible's exact accelerator chain.
- **India corridor is the natural Day 1 wedge** regardless of US-onshore positioning. US→India is the largest remittance corridor globally and the corridor with the strongest local rails (UPI/IMPS via Razorpay).
- **US incorporation tradeoff:** if pursuing US-onshore wedge, use **Stripe Atlas** (~$500 one-time, ~$1K/year compliance) for Delaware C-Corp. Required for Reg D 506(c) wrapper and most US grant applications. Can operate Indian Pvt Ltd in parallel for local operations.
- **Time-zone reality:** US investor calls happen 9 PM – 1 AM IST. Acceptable for 6–12 weeks; not sustainable as steady state. Plan for it.

---

## Critical Files Referenced

The plan is built on top of existing research files. **All paths below are absolute** — the executing agent should read these directly:

- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/architecture.md` — full Mermaid architecture diagrams (reuse for the deck's solution slide)
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/liquidity_architecture.md` — actual deployed mechanics (Hedera not Solana, Privy custody, Web 2.5 honesty)
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/how_to_build.md` — the phased playbook this plan adapts
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/deep_dive.md` — founder narrative + exact funding sequence
- `/Users/fuyofulo/research/ai_crypto/research/markets/payfi/liquidity_models.md` — design space + 3 alternative architectures (#3 "no-float RTP-first" relevant for early MVP)
- `/Users/fuyofulo/research/ai_crypto/research/markets/agent_payments/compliance.md` — regulatory landscape + 5 unsolved compliance gaps (substantive evidence of compliance depth in pitch)
- `/Users/fuyofulo/research/ai_crypto/research/companies/frames-ag/deep_dive.md` — example of how a small team uses skill-file distribution + Privy under the hood (relevant if expanding to AI-agent vertical)
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/transcripts/` — directory of founder interview transcripts (OnePiece Labs, Sanctum Forecast fireside, Aethir announcement, brand video) — pull direct founder quotes for the pitch
- `/Users/fuyofulo/research/ai_crypto/research/companies/credible-finance/happypath.png` — user's hand-drawn happy-path diagram of the payment flow (reference for the architecture slide)

---

## Verification

How to know the plan is working:

| Checkpoint | Pass criteria | Fail action |
|---|---|---|
| End Week 1 | Wedge memo + deck + Loom pitch + FinCEN MSB filed | If wedge undecided, stop and decide before any other work |
| End Week 2 | StableHacks submitted + demo video published + Solana Foundation app in + Circle Alliance app in | If no working demo, switch to Outlier-only path (no demo required) |
| End Week 3 | 5+ co-founder conversations + 10 partner outreaches sent + 1+ scheduled partner call | If zero traction, re-position deck for solo, drop co-founder ask |
| End Week 4 | StableHacks attended + 1 design-partner LOI in pipeline + 5 followups in motion | If no LOI, execute Outlier path Week 5 anyway |
| End Week 6 | Outlier app submitted + Stellar app submitted + MVP scaffolded OR documented wedge pivot | If neither, run honest 6-week retro |
| End Week 12 | At least 1 of: grant accepted / accelerator interview scheduled / LOI converted | Trigger Plan B (Superteam bounties + audit work) |

**The ultimate verification: ~1 yes within 60 days.** Could be a hackathon placement, a grant disbursement, an accelerator interview, or a design-partner pilot. One concrete external signal is the floor for "the plan is working." Zero signals at 60 days = wedge needs reformulation, not more execution.
