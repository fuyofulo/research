# Altitude (altitude.xyz) — Marketing-vs-Reality Audit

*Stream 4 / Truth File · 2026-05-04*

---

## 1. Honest baseline (no marketing language)

**What Altitude actually is:** Altitude is a stablecoin-denominated business account product operated by **Squads Labs** (legal entity: *Selimor Investments Limited*). It sits on top of Squads' Solana smart-account program and is fronted by a web app that lets a company KYB-verify, receive ACH/Wire/SEPA into US/EU local rails, off-ramp into USDC/EURC, sit on a stablecoin balance, and earn ~5% APY in the form of USDC "rewards" routed from a tokenized US Treasury exposure. Outbound payments are settled by third-party payment service providers (Bridge/Stripe, MoonPay, Infinite, Due) — **Altitude itself is not a bank, not a money transmitter, and explicitly "an unregulated service."** Squads provides the smart-account custody UX (passkeys, Privy/Turnkey-backed key shards, optional Ledger/YubiKey) and a wrapper around stablecoin rails. The company that built it (Squads) is the same team that secures ~$15B in Solana multisig assets via its v4 program, so the underlying smart-contract pedigree is real — but the *banking surface* is a thin layer on top of partner PSPs.

In one sentence: **Altitude is a UX-and-compliance shell over partner stablecoin rails, hosted in a Solana self-custodial smart account, marketed as a "bank replacement" for businesses.**

---

## 2. Claim Inventory & Verification Table

Sources: live Altitude site ([altitude.xyz / Wayback Mar 2026](https://web.archive.org/web/20260311070719/https://altitude.xyz/)), May 2025 squads.xyz/altitude launch page ([Wayback May 14 2025](https://web.archive.org/web/20250514142442/https://squads.xyz/altitude)), Dec 2025 GA page ([Wayback Dec 10 2025](https://web.archive.org/web/20251210023449/https://squads.xyz/altitude)), [Squads $18M raise PR](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html), [The Block coverage](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude), [Blockworks exclusive](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan), [Help Center: Supported Countries](https://support-altitude.squads.xyz/en/articles/12401045-supported-countries), [Altitude Supplemental Terms](https://squads.xyz/legal/altitude), [Squads V4 Security blog](https://squads.xyz/blog/v4-security-measures), [Squads-Protocol GitHub](https://github.com/Squads-Protocol).

| # | Claim (verbatim or near-verbatim) | Confidence | Verification notes |
|---|---|---|---|
| 1 | "Banking for companies on the frontier" / "Financial Operating System for Businesses on the Frontier" | 🟡 | Marketing tagline — meaningless on its own. The product is a stablecoin account with payment rails bolted on, not a chartered bank. |
| 2 | "Available in 150+ countries" | 🟡 | Repeated everywhere. Help Center confirms "150+ countries including the US (excluding NY and AK), Canada, Europe, Australia, UAE and India." Lawful availability is real, but "supported" ≠ "regulated to operate" — it means the partner PSP network *can* serve those countries. Several ride on Bridge's compliance perimeter. |
| 3 | "Trusted by leading companies" (no logos shown on current homepage) | 🔴 | The hero says it but doesn't name anyone. Logo wall absent in March/April 2026 snapshots. Customer types described ("exporters, global agencies, crypto-native companies, cross-border remote teams") are categories, not named brands. **Tell:** if they had marquee enterprise logos they'd show them. |
| 4 | "Processed over $200 million in payments" since Dec 2025 launch | 🟡 | Cited by The Block, Blockworks, and the company's own PR Newswire release. Self-reported, not on-chain attested. ~$50M/month over ~4 months is plausible for a young product but unverifiable — could include test flows, internal volume, and one-off treasury moves. No public dashboard. |
| 5 | "5% APY rewards" / "Earn 5.00% APY" | 🟡 | Real product, but the APR is *marketing-grossed*. Per the legal footer: "Altitude does not pay interest on self-custodied digital asset balances. Eligible Altitude Account users may earn rewards from Squads based on use of the services and the Altitude Account." It is a **reward program** paid in USDC, not interest, and likely funded by Squads' margin on a tokenized Treasury position. |
| 6 | "Backed by BlackRock managed US Treasuries" (rewards source) | 🟡 | Implies — without saying — Ondo OUSG/USDY or BlackRock BUIDL exposure. Not directly confirmed by Squads as the on-chain provider. **The claim leans on BlackRock's brand without disclosing the actual tokenized vehicle.** |
| 7 | "Zero fee transfers for all pay ins and payouts" / "no platform fees" | 🟡 | Likely true today as a customer-acquisition subsidy. Partner PSPs (Bridge, MoonPay, Infinite, Due) charge somewhere — Squads is either eating spread or capturing it from float/yield. "Zero fee" rarely survives scale. |
| 8 | "Self-custodial wallet" / "non-custodial" | ✅ | The Altitude account is a Squads v4 smart account on Solana. Keys are split via Privy + Turnkey passkey/email shards, with optional Ledger/YubiKey for high-value transfers. Architecturally this is real self-custody — though "self-custodial with multi-key MPC controlled by partners" is a thinner version than holding your own seed. |
| 9 | "Built on Solana" — sub-cent payments, 24/7, instant settlement | ✅ | Solana settles transfers in seconds for fractions of a cent. Verifiable on-chain. The performance claim is one of the few cleanly true ones. |
| 10 | "Audited regularly by independent firms" (re: stablecoin reserves issued by Circle / Bridge) | ✅ (indirect) | This is Circle/Bridge attestation, not Altitude's own. Altitude rides on USDC/EURC reserve attestations from Circle and Bridge — both real and ongoing. Altitude itself doesn't issue stablecoins. |
| 11 | "Squads Protocol secures over $15 billion in assets" / "trusted by 450+ teams" | ✅ | The *Squads multisig* TVL figure, used to lend credibility to Altitude. Consistent with on-chain accounting on Squads v4. ([Fystack writeup](https://fystack.io/blog/squads-from-zero-to-the-multisig-protocol-securing-10b-on-solana)). Note: this is **secured** (i.e., held in multisigs), not Altitude-specific. |
| 12 | "Audited 7 times by OtterSec, Certora, Neodyme, Trail of Bits + 2 formal verifications" | ✅ | Verified per [Squads V4 security blog](https://squads.xyz/blog/v4-security-measures). All four firms are tier-1. Certora's formal verification on Solana was a first. ⚠️ Caveat: audits are of Squads v4, not the Altitude application/banking layer specifically. |
| 13 | Programmable smart accounts / Solana-native | ✅ | True. Altitude accounts are Squads v4 smart accounts; programmability (limits, roles, time locks, sub-accounts, lookup tables) is a real Solana program feature. |
| 14 | Continuous "sanctions screening, AML, transaction monitoring, KYB" — "processes similar to regulated fintech standards" | 🟡 | "Similar to" is the tell. Compliance functions exist, but Altitude's Terms explicitly state **"the Altitude Account is an unregulated service. It is not supervised, licensed, or endorsed by any financial services authority and is not affiliated with any regulated entity."** They KYB and screen, but they aren't a money transmitter. The licensed compliance perimeter belongs to Bridge/MoonPay/Infinite/Due. |
| 15 | "Plug into licensed PSPs: Bridge, MoonPay, Infinite, Due" | ✅ | Confirmed across press write-ups and the legal footer. Real partnerships. |
| 16 | "Open USD account in a few clicks with just an email and no U.S. entity or bank required" | ✅ (subject to KYB) | True, with the asterisk that KYB review is required and approval is not instant. Bridge issues the routing number under its compliance license. |
| 17 | "Total funding $42.9M" / "$18M strategic round led by Solana Ventures" with Coinbase Ventures, Haun, L1D, Collab+Currency, Electric Capital, Placeholder, Jump Crypto, Robot Ventures | ✅ | Cross-confirmed across PRNewswire, The Block, Crypto.News. Earlier $5.7M (Oct 2023, Placeholder-led, Multicoin participated). Cap table is genuinely strong. |
| 18 | "Altitude isn't a bank. It's what you wanted your bank to be" | 🟡 | Tagline. Half-true: not a bank legally or operationally. The "what you wanted your bank to be" hides that there's no FDIC coverage, no chartered deposits, no reserve requirements, no consumer-protection regulator. |
| 19 | Corporate cards (Visa) | 🔴 (today) / 🟡 (claim) | Explicitly labeled "Coming soon" on the current site. They are *advertising* a product that doesn't exist yet. Cards depend on a BIN sponsor and won't ship without one. |
| 20 | Bill pay, invoicing, accounting integrations (CFO stack) | 🔴 (today) | All marked "Coming soon" — the "CFO stack" headline overstates a roadmap. |
| 21 | "Trade Any Asset — swap or place limit orders on thousands of tokenized assets" (May 2025 launch page) | 🔴 (dropped) | Present in May 2025 launch page. **Removed by December 2025 / current site.** A textbook disappearing-claim — Altitude pivoted away from a "Solana exchange inside the account" pitch toward a more focused banking story. |
| 22 | "5+ years proven in production" (re: Solana) | ✅ | Solana mainnet beta launched March 2020, so 6+ years operational by May 2026. Accurate. |
| 23 | "$13.5B+ stablecoins on Solana" (X post by Altitude) | 🟡 | Order-of-magnitude consistent with DefiLlama's Solana stablecoin marketcap historicals; exact figure not separately verified. |
| 24 | "Zero fees" stablecoin on/off ramp | 🟡 | Marketing copy on March 2026 site. Bridge's published rates are not zero. Squads is either subsidizing or capturing it elsewhere. Will likely be tiered later. |
| 25 | "Granular controls, multi-step approvals, configurable MFA" | ✅ | These are native Squads v4 features. Real. |

---

## 3. The "tells" — what the marketing reveals

- **The "Coming soon" pile.** Corporate cards, bill pay, invoicing, accounting integrations are all promised on the homepage but not shipped. The "Financial Operating System" pitch is a mood-board, not the current product.
- **Disappearing "Trade Any Asset" pitch.** May 2025 launch page leaned into "swap or place limit orders on thousands of tokenized assets" — a Solana-DEX-meets-bank vibe. By Dec 2025 GA, that line is gone. They quietly narrowed scope toward classic neobank features. ([compare May 2025](https://web.archive.org/web/20250514142442/https://squads.xyz/altitude) vs [Dec 2025](https://web.archive.org/web/20251210023449/https://squads.xyz/altitude))
- **Brand laundering.** "Backed by BlackRock managed US Treasuries" implies BlackRock-tier institutional backing, but BlackRock has no relationship with Altitude — only with the BUIDL fund that downstream tokenizers use. Same trick as everyone else doing OUSG/USDY-flavored yield. **The actual yield issuer is never named on the homepage.**
- **PSP roster as compliance shield.** Listing Bridge, MoonPay, Infinite, Due in PR is doing two things at once: (a) signaling "we have real banking rails," (b) deflecting that *Squads itself isn't licensed* — the licenses belong to partners. This is what "we are an unregulated service" buried in the footer translates to in plain English.
- **"Trusted by leading companies" with no logo wall.** A common B2B move when the customer base is real but not yet recognizable.
- **"$200M processed" headline without breakdown.** No split by customer type, average ticket size, or revenue captured. In stablecoin land, $200M of throughput could be 4 customers moving treasury or 2,000 small payouts. We don't know.
- **The "frontier" framing.** "Banking for companies on the frontier" lets them dodge questions about why a non-frontier company would not just use Mercury/Brex/Wise + a Coinbase Prime account.

---

## 4. Dual-positioning game (crypto-native vs enterprise/institutional)

Altitude runs **two narratives in parallel**, and the gap is informative:

**Crypto-native pitch (X/Twitter, Solana Breakpoint, Squads protocol blog):**
- "Bank on Solana"
- "Stablecoin-native USD account"
- "Programmable smart accounts"
- "Self-custodial / non-custodial"
- "5+ years on Solana, $13.5B+ stablecoins"
- Frames Squads as Solana's autonomous finance layer; Altitude as the "killer app" proving stablecoins for biz.

**Enterprise/institutional pitch (altitude.xyz, B2B sales pages, PR Newswire releases):**
- "Banking for companies on the frontier" / "Financial Operating System"
- "Multi-currency accounts, corporate cards, global payments, APY, CFO stack"
- "Compliance similar to regulated fintech standards"
- "ACH / wire / SEPA / SWIFT"
- The word "Solana" is **mostly absent** from the enterprise homepage. "Stablecoin" is downplayed in favor of "your accounts and payment rails."

The asymmetry is deliberate. Crypto-native readers get "non-custodial Solana smart account → freedom from banks." Enterprise CFOs get "boring fintech with extra yield, don't worry about the chain." A skeptical buyer should ask which one is true at any given decision point — because for FX cutoffs, settlement risk, and compliance liability, the answer is "both, depending on what's convenient."

---

## 5. Competitive positioning

Altitude lives at the intersection of three categories. Different competitors apply to different functions.

**Stablecoin-native business banking (closest comp set):**
- **Mural Pay** — stablecoin payroll/cross-border API; $5.6M seed (Galaxy/DCG/Firstminute); $200M+ volume reported. Smaller, API-first, less flashy.
- **Conduit** — stablecoin cross-border specialist; $53M raised (Circle, Dragonfly, Altos); $10B+ annualized; 23 African countries with mobile money. **Significantly ahead on geographic coverage where it matters.**
- **Bridge (now Stripe)** — virtual USD accounts on stablecoin rails; **Altitude is literally a customer of Bridge.** Stripe's $1.1B acquisition makes Bridge an 800-pound gorilla; Squads/Altitude is dependent on a partner that could compete directly.
- **BVNK (now Mastercard, $1.8B)** — enterprise stablecoin payments. Up-market.
- **Beam** (acquired by Modern Treasury, ~$40M all-stock) — stablecoin orchestration for fintechs.
- **Sphere Pay / Sphere Labs** — Solana-native subscriptions/payments; partial overlap.
- **Sling Money** — consumer-leaning, 75+ countries, P2P; limited business overlap.

**Solana-native B2B (smaller direct comps):**
- **Sphere, Helio, CandyPay** — payments/checkout, less treasury-focused.
- **Fuse Wallet** — Squads-built consumer/business wallet; in the family.

**Traditional fintech neobanks (substitution risk):**
- **Mercury, Brex, Ramp, Slash, Meow, OneSafe, Rho** — mostly USD-only with some stablecoin features bolted on. Mercury is huge but explicitly does not support stablecoins. **Meow and Slash are the most direct head-to-heads** — Meow has zero-fee USDC send/receive directly from cash balance; Slash supports USDC/USDT/USDSL on/off ramps.

**What Altitude does better:**
- True self-custodial smart account architecture (vs Meow/Slash custodial models).
- Solana-native programmability (multisigs, time locks, sub-accounts, hardware-backed approvals).
- Genuinely top-tier underlying audits (4 firms + 2 formal verifications).
- 150+ country reach is broader than most fintech neobanks.

**What Altitude does worse:**
- Geographic depth in any single corridor (Conduit dominates Africa; BVNK dominates EU enterprise).
- Distribution to non-crypto businesses (Mercury/Brex have ~10x more accounts).
- Card product (literally not shipped vs Mercury/Brex/Ramp's mature card stacks).
- Regulatory standing (unregulated vs Mercury's BaaS partnerships with Choice/Evolve, vs Conduit/Bridge own-licensing).
- Float economics: not holding the deposits limits the classic neobank monetization lever.

**Parity:**
- Sub-cent settlement (any Solana-native competitor; matched by Bridge for stablecoin-only flows).
- USDC reward yield ~5% (table stakes; Coinbase Prime, Lead Bank rewards programs, OUSG self-custody all hit similar numbers).

---

## 6. Moat analysis

| Moat type | Real? | Notes |
|---|---|---|
| **Technical** | 🟡 partial | Squads v4 program is genuinely best-in-class smart-account infra on Solana — formally verified, four-audit pedigree. But that moat exists at the *protocol* layer, not at the *Altitude product* layer. Any competitor could build on Squads via the open-source program. The Altitude *app* (UI, PSP integrations, KYB pipeline) is replicable in 6-12 months. |
| **Regulatory** | 🔴 | None. Altitude is explicitly unregulated; the licenses live with PSP partners. Anti-moat: any of those PSPs could disintermediate. |
| **Distribution** | 🟡 | Squads' existing 450+ multisig customers + ~$15B secured assets is a genuine warm-funnel for Altitude. Probably the strongest moat they have. But it's bounded by the Solana DAO/protocol-team customer pool. |
| **Brand** | 🟡 | Squads is well-known among Solana-native teams; nearly unknown outside. "Altitude" as a brand is <12 months old. |
| **Capital** | 🟡 | $42.9M total is decent runway but trivial vs Stripe (Bridge), Mastercard (BVNK), or even private fintechs like Mercury (>$300M raised) and Brex. |
| **Network effects** | 🔴 | Account-to-account stablecoin transfers are commodity rails. No two-sided marketplace dynamics. |

**Verdict:** The only durable moat is *the Squads protocol-and-customer-base flywheel*. Strip that out and Altitude is a UI on top of Bridge.

---

## 7. What does a competitor targeting Altitude exploit?

1. **Float + interchange economics.** A licensed competitor can hold deposits, earn float, and offer richer rewards or cheaper FX. Altitude can't because it's non-custodial. A Mercury-equivalent that natively settles in USDC could undercut on monetization.
2. **PSP disintermediation.** Bridge (Stripe) could launch a direct-to-business product with the same UX and squeeze Squads' margin. Stripe has the brand, the salesforce, and the licensing.
3. **Geographic depth.** Conduit's 23-country Africa rails > Altitude's "150+ supported." Anyone building corridor depth (LATAM, SEA, Africa) can beat Altitude in actual usable corridors.
4. **Card stack.** Until Altitude ships a real Visa card with a BIN sponsor, any neobank can claim the spend side. Most exposed roadmap line.
5. **The "regulated alternative" pitch.** Sell directly against the "unregulated service" disclosure. Many CFOs simply will not put company treasury into something with that footer.
6. **Multi-chain.** Altitude is Solana-only. A competitor offering the same UX over Tron+Ethereum+Solana captures the corridors where USDT dominates (Asia, MENA, LATAM remit).
7. **Yield transparency.** Any competitor that names its yield source ("X% from Ondo OUSG, Y% from Squads subsidy") and shows the receipt undermines the "BlackRock-managed Treasuries" hand-wave.

---

## 8. The honest one-liner

> **Altitude is a slick, self-custodial business-account UX on top of partner stablecoin rails (Bridge, MoonPay, Infinite, Due), built by the same team that runs Solana's leading multisig — currently doing ~$200M of self-reported throughput, paying ~5% USDC rewards funded by tokenized T-bill exposure, advertised as "your bank replacement" while explicitly disclosing it's an unregulated service that doesn't custody, issue, or redeem anything. The thesis works if Solana stablecoin volumes keep compounding and Squads can ship the rest of the CFO stack before Stripe-via-Bridge eats them.**

---

## 9. Red flags

- 🚩 **"Unregulated service" disclosure** in legal footer paired with "Banking for companies on the frontier" hero. The marketing-vs-disclosure gap is the single biggest tell. ([Altitude Supplemental Terms](https://squads.xyz/legal/altitude))
- 🚩 **Roadmap-as-product.** Cards, bill pay, invoicing, accounting integrations all "Coming soon" but featured prominently in the homepage tour as if shipped.
- 🚩 **Disappearing "Trade Any Asset" claim** between May 2025 and Dec 2025 — pitch volatility on what the product *is*.
- 🚩 **Self-reported volume only.** No public dashboard, no DefiLlama line item for Altitude specifically, no on-chain attestation. "$200M+" must be taken on faith.
- 🚩 **Yield source obscured.** "Backed by BlackRock managed US Treasuries" without naming the actual tokenized vehicle. If it's OUSG, BUIDL, or USDY, say so. The omission is doing rhetorical work.
- 🚩 **Heavy dependency on Bridge** (a Stripe subsidiary that has every incentive to disintermediate).
- 🚩 **Selimor Investments Limited** as the operating entity is opaque — no public filings surfaced in CIMA or BVI registries via search; jurisdiction not disclosed on the site footer.
- 🚩 **Compliance language is squishy** — "processes similar to regulated fintech standards" deliberately avoids saying "we are regulated" or "we are licensed."
- 🚩 **No customer logos** despite "trusted by leading companies."
- 🚩 **Drift exploit aftermath** (April 2026) — the same Squads team published post-mortem implicating "compromised multisig signers" at a Squads-secured project. Code wasn't at fault, but it surfaces operational-security questions for any team using Squads-secured accounts. ([CryptoTimes](https://www.cryptotimes.io/2026/04/03/drift-protocol-exploit-linked-to-compromised-multisig-signers-squads/))

---

## 10. Green flags

- ✅ **Underlying smart-contract program is genuinely best-in-class.** Four audit firms (OtterSec, Certora, Neodyme, Trail of Bits), two formal verifications, AGPL-3.0 open source, public bug bounty. Few crypto products clear this bar. ([Squads V4 security](https://squads.xyz/blog/v4-security-measures), [GitHub](https://github.com/Squads-Protocol/v4))
- ✅ **Squads' v3/v4 customer base is a real distribution moat** — 450+ teams, $15B in multisig assets — and they are the highest-intent Altitude prospects.
- ✅ **Founder/team pedigree is non-anonymous.** Stepan Simkin (ex-Clifford Chance M&A) and Sean Ganser publicly attached, ~20+ employees with backgrounds at Google/Microsoft/Uber. ([Crunchbase](https://www.crunchbase.com/person/stepan-simkin), [Delphi interview](https://members.delphidigital.io/media/web3-is-frictionless-collaboration-stepan-simkin-co-founder-ceo-of-squads-protocol))
- ✅ **Cap table is signal-rich.** Solana Ventures, Coinbase Ventures, Haun Ventures, Multicoin, Placeholder, Jump, Electric Capital, Robot, Collab+Currency, L1D — both the "Solana mafia" and the chain-agnostic top tier. ([PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html))
- ✅ **Real architectural choice.** Self-custody via Privy + Turnkey shards + optional hardware factor is genuinely better security UX than custodial neobanks, and not theater.
- ✅ **Operational discipline.** They publish post-mortems on partner exploits and have an active bug-bounty program.
- ✅ **The Solana stablecoin TAM is real.** Solana stablecoin marketcap >$13B and growing; sub-cent + sub-second is a structural advantage that Ethereum L1 doesn't match.
- ✅ **Pivot judgment.** Dropping the "trade any asset" pitch and narrowing to "modern USD account + payments" between May and Dec 2025 is good product hygiene. Most teams don't kill their darlings.

---

## 11. What's missing from their pitch (the buyer's checklist)

A reasonable CFO/treasurer evaluating Altitude would want to know — and the site doesn't disclose:

1. **Insurance / loss recovery.** What happens if Bridge has an outage during a payroll cycle? Who is on the hook? No SLAs published.
2. **Yield mechanics in full.** Source, gross APY before take-rate, eligibility caps, withdrawal-conditional clauses. "Up to 5%" leaves room.
3. **Take rate.** What does Squads earn per dollar moved? FX spread? Float? Subsidy from PSP rebates? No published unit economics.
4. **Concentration risk.** What % of $200M throughput is from the top 5 customers? If it's >50% (likely for any 5-month-old B2B fintech), that's a different story than "broad adoption."
5. **Revenue.** $42.9M raised, ~20+ headcount, "zero platform fees" — runway implies they are pre-revenue or near-zero-revenue. Cash-flow positive is **not claimed** anywhere I could verify.
6. **Wind-down plan.** If Squads Labs (Selimor Investments Limited) goes dark, what happens to user accounts? Self-custody mitigates fund loss but the routing-number / Bridge relationship is owned by the operator.
7. **Sanctions / OFAC posture for self-custodial flows.** "Continuous screening" — at what step? PSP layer only? On-chain? No SOC2 / ISO 27001 mentioned.
8. **Audit of the Altitude application layer** specifically (not the Squads v4 program). Web app, KYB pipeline, reward calculation logic — none of these are in the audit set.
9. **Reserve composition for "rewards."** Is Squads pre-funding rewards or paying out of T-bill yield in real time? What happens if Treasury rates drop to 2%?
10. **Regulator engagement.** Is Altitude in conversation with any of FinCEN/MAS/FCA/MiCA? "Unregulated" today is one thing; the absence of a stated path to "regulated" is another.
11. **Chain dependency.** What's the contingency if Solana has a multi-hour outage during business hours? (Mainnet has had several historically.)
12. **Pricing sheet.** "No fees" is unsustainable; what is the eventual fee schedule, and when does it kick in?
13. **Coverage map specificity.** "150+ countries" is a single number; the actual sub-segmentation (which countries can receive ACH vs only stablecoin out, which support EUR IBAN, etc.) is in the help center but not on the homepage.
14. **Concentration of yield-asset issuer.** If rewards are funded by a single tokenized-Treasury issuer (Ondo or BlackRock BUIDL), that's a smart-contract and counterparty risk that should be disclosed.

---

## 12. Final synthesis

**What survived the audit:**
- Real product, real customers, real volume order-of-magnitude.
- Real top-tier security pedigree at the protocol layer.
- Real cap table.
- Real self-custodial architecture.
- Real pricing/UX advantage over legacy banks for crypto-native exporters and remote teams.

**What didn't:**
- "Banking" framing — they aren't a bank and aren't licensed as one.
- "CFO stack" — most of it is a roadmap, not a product.
- "Trusted by leading companies" — show the logos.
- "Compliance similar to regulated fintech" — different from "we are regulated."
- "BlackRock-backed" — name the actual issuer.
- "Zero fees" — not durable.

**The deeper question:** Altitude's bet is that Solana stablecoin throughput becomes the dominant settlement layer for cross-border B2B, Squads' multisig moat translates into account-product distribution, and Stripe doesn't pivot Bridge into a direct competitor. If two of those three break, this becomes a fintech wrapper with a great audit story and a shrinking margin.

**The cross-examine list for a follow-up conversation:**
1. What is Altitude's actual revenue today, and what's the unit economics target by 2027?
2. Who is the yield issuer, and what's the gross-to-net spread?
3. What % of volume is concentrated in the top 5 customers?
4. What's the go-regulated path? Money transmitter licenses? E-money licenses in EU?
5. How does Altitude survive if Bridge launches a competing product?
6. Is there a token? (Squads protocol has talked about one historically — implications for Altitude users.)
7. What's the audit scope on the Altitude *application* (not the Squads v4 program)?

---

**Sources:**

- [altitude.xyz current homepage (Wayback Mar 11 2026)](https://web.archive.org/web/20260311070719/https://altitude.xyz/)
- [altitude.xyz (Wayback Apr 15 2026)](https://web.archive.org/web/20260415134428/https://altitude.xyz/)
- [squads.xyz/altitude — May 2025 launch page](https://web.archive.org/web/20250514142442/https://squads.xyz/altitude)
- [squads.xyz/altitude — Dec 10 2025 GA page](https://web.archive.org/web/20251210023449/https://squads.xyz/altitude)
- [Altitude Help Center: Supported Countries](https://support-altitude.squads.xyz/en/articles/12401045-supported-countries)
- [Altitude Supplemental Terms (Squads)](https://squads.xyz/legal/altitude)
- [Squads $18M raise — PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html)
- [The Block — Solana Ventures leads $18M Squads round](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude)
- [Blockworks — Squads unveils stablecoin account exclusive](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan)
- [Crypto.News — Squads $18M raise](https://crypto.news/solana-multisig-protocol-squads-raises-18m-usd-to-scale-stablecoin-platform-altitude/)
- [TechStartups coverage](https://techstartups.com/2026/04/29/fintech-startup-squads-raises-18m-to-build-a-stablecoin-powered-financial-os/)
- [Squads V4 Security Measures](https://squads.xyz/blog/v4-security-measures)
- [Squads-Protocol GitHub org](https://github.com/Squads-Protocol)
- [Squads V4 GitHub repo](https://github.com/Squads-Protocol/v4)
- [Multicoin — Why we invested in Squads](https://multicoin.capital/2023/10/16/build-with-squads/)
- [Introducing Altitude & Haun Ventures Investment](https://squads.xyz/blog/introducing-altitude-and-a-strategic-investment-from-haun-ventures)
- [Squads — Announcing Our $5.7M Strategic Round](https://squads.xyz/blog/squads-labs-raises-strategic-round)
- [Stepan Simkin — Crunchbase](https://www.crunchbase.com/person/stepan-simkin)
- [Stepan Simkin — Delphi Digital interview](https://members.delphidigital.io/media/web3-is-frictionless-collaboration-stepan-simkin-co-founder-ceo-of-squads-protocol)
- [Fystack — Squads from zero to multisig protocol securing $10B](https://fystack.io/blog/squads-from-zero-to-the-multisig-protocol-securing-10b-on-solana)
- [Drift exploit linked to compromised multisig signers (Squads post-mortem)](https://www.cryptotimes.io/2026/04/03/drift-protocol-exploit-linked-to-compromised-multisig-signers-squads/)
- [Bessemer — Stablecoins from DeFi primitive to global financial infrastructure](https://www.bvp.com/atlas/stablecoins-from-defi-primitive-to-global-financial-infrastructure)
- [Squads on X — "Bank on Solana"](https://x.com/tryaltitude/status/1971618113088008199)
- [Altitude on X (@tryaltitude)](https://x.com/tryaltitude)
