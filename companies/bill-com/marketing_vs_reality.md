# Bill.com / BILL Holdings — Skeptical Marketing-vs-Reality Audit

**Date:** June 2026 | **Ticker:** NYSE: BILL | **Market cap:** ~$3.5-5B (post-decline) | **All-time-high to today:** -88% from $342 peak (Nov 2021)

## Executive Setup

BILL Holdings is a company in active strategic distress as of mid-2026. Three activist investors are circling (Starboard 8.5%, Elliott ~5%, Barington ~$25M), management just cut 30% of headcount on May 7, 2026 (same day as a $1B buyback), and Reuters reported the company is exploring a sale with Hellman & Friedman among the bidders. The marketing claims and the underlying business reality are now sharply divergent — and that gap is the entire opportunity for a competitor.

---

## 1. The Claims Audit (20 specific public claims)

| # | Claim (verbatim or paraphrased) | Source | Verdict | Translation |
|---|---|---|---|---|
| 1 | "Trusted by 480K+ businesses" | bill.com homepage; 10-K FY25 says ~493,800 | 🟡 | Number is roughly accurate, but it counts **businesses that used the platform** — including those managed via accountant firms and Spend & Expense card-only users. Not 480K paying enterprise SaaS contracts. |
| 2 | "AI trained on 250M+ invoices" | bill.com blog Feb 5, 2026 ("Friction Crisis"); never audited | 🟡 | Number is plausible given 20+ years of payment history but is **self-reported, unaudited, and the architectural benefit is unclear** — modern frontier LLMs match invoice extraction with prompt engineering. |
| 3 | "Insights from $1T+ in payments, 1B+ documents, 8M+ network members" | FY25 10-K + AI blog | 🟡 | Cumulative-since-inception figures, not annualized. The $1T is across a 19-year history. Headline-friendly, but the marginal AI training value of 20-year-old payment data is questionable. |
| 4 | "80% manual work reduction" | bill.com product/AI pages | 🔴 | **Specific to the W-9 Agent and Invoice Coding Agent only** — not a platform-wide claim. Methodology unstated. Trustpilot users describe the opposite experience (ACH delays, doc-loops, customer-service queues). |
| 5 | "99% accuracy on multi-line invoice coding" | bill.com product/AI page | 🟡 | Self-reported; no independent benchmark; "accuracy" definition not disclosed (per-field, per-line, per-invoice?). |
| 6 | "533% increase in transactions coded entirely by AI" | bill.com AI blog | 🟡 | True but meaningless without baseline — 533% of a tiny number is still a small number. Classic relative-growth optics. |
| 7 | "Stopped 8M fraud attempts in FY25" | bill.com AI blog | 🟡 | Likely counts every flagged event including duplicates/false positives. Without a precision/recall figure this is theater. |
| 8 | "Net Revenue Retention 94% (inclusive of FI)" | FY25 10-K | ✅ | True, but **94% NRR means the average customer cohort shrinks each year** — well below the 110-120% SaaS benchmark. This is one of the most damning metrics in the file. |
| 9 | "Core revenue grew 16% YoY in FY25" | FY25 10-K, Q4 FY25 8-K | ✅ | Verified. FY25 core revenue $1.30B on $1.46B total. |
| 10 | "Float revenue $161.8M in FY25 (~11% of total)" | FY25 earnings, quarterly breakdown | ✅ | True; declining each quarter as rates fall (Q2 $42.9M → Q3 $37.9M → Q4 $37.4M). Float is a **vulnerability**, not a moat. |
| 11 | "Network of 8M members, +18% YoY" | FY25 filings | 🟡 | True by their definition, but "member" = any vendor BILL has ever paid, not active counterparties. Definition is generous. |
| 12 | "98 of top 100 US accounting firms use BILL" | bill.com accountant program page | ✅ | Plausibly true and **genuinely defensible** — the CPA.com strategic alliance is the single strongest moat in the file. |
| 13 | "Mid-market growth focus, ARPU expansion" | Q2/Q3 FY26 commentary | 🟡 | Reframe for the truth: **AP/AR net customer adds are decelerating** (~4,000/quarter, "lumpy", guided lower). They're pivoting upmarket because the SMB end is being eaten by Ramp/Brex/Mercury. |
| 14 | "Industry's first AI-enabled B2B payments platform" | press release | 🔴 | Marketing puffery. Tipalti, Stampli, AvidXchange, AppZen, and others had AI extraction years before BILL's agent rebrand. |
| 15 | "Touchless B2B transactions" | Oct 2025 AI agent launch | 🟡 | Aspirational. The agents announced (W-9, reconciliation, onboarding) are **narrow back-office automations**, not end-to-end agentic AP. |
| 16 | "AI Coding Agent reduces coding steps by 89%" | bill.com product page | 🟡 | "Number of steps" is a chosen metric, not time-savings. Steps-eliminated framing is consultant-speak. |
| 17 | "BILL is the leader in SMB AP automation, ~20-25% market share" | UBS estimate | 🟡 | Plausible top-line share, but **competitive share is collapsing at the new-customer level** — Ramp added more revenue ($524M) in TTM than BILL grew core revenue ($179M). |
| 18 | "Subscription pricing $45-$89/user/month" | bill.com pricing page | 🔴 | True for list price, but **published pricing hides ACH ($0.59), wire ($19.99 international), check ($1.99), failed-ACH penalty ($50), void-check ($25), card surcharge (2.9%), and embedded FX margins** on cross-border. Not surfaced in onboarding. |
| 19 | "$0 international wire fees in local currency" | bill.com pricing | 🔴 | "Hidden fee through non-market exchange rate, costs hundreds on larger payments" — direct quote from review aggregators. Classic FX-margin hide. |
| 20 | "NetSuite Intelligent Payment Automation, powered by BILL" | Oct 2025 partnership PR | ✅ | Real, and a genuine win — embeds BILL into Oracle NetSuite's AP workflow. The strongest defensive move BILL has made in 18 months. |

---

## 2. The "250M Invoices" Claim — Deep Dive

**First public appearance:** The "trained on 250M+ bills" framing appears most prominently in Bill.com's February 5, 2026 blog post "BILL AI is Solving the Friction Crisis for the Fortune 5 Million", and earlier variants tied to the October 28, 2025 AI Agents launch.

**Independent audit:** None exists. No third-party model card, no peer-reviewed benchmark, no SEC-disclosed training methodology.

**Architectural reality check:** The claim implies BILL has a proprietary fine-tuned model trained on those invoices. In reality, modern AP automation stacks at this scale almost always combine: (a) OCR/layout extraction (Textract or similar), (b) vendor matching from a customer-specific historical database, (c) an LLM (Claude/GPT) called via API for line-item classification with prompt context including the customer's chart of accounts. The 250M invoices add value as a **statistical features store** (most-likely-GL-account given vendor X) — not as fine-tuning data for a frontier model.

**The honest cross-examination:** Even if true, a Series A startup using Claude Sonnet 4.6 + Reducto/Documind + customer-specific GL history can match BILL's extraction accuracy in 6 months. The "250M invoices" framing functions as a **data-moat narrative for the activist-investor audience**, not as a real technical advantage. 🔴

---

## 3. The "80% Manual Work Reduction" Claim — Deep Dive

**The fine print:** This number specifically refers to (a) "fully automated bills increased by 80% since beginning of 2025" and (b) the W-9 Agent eliminating ">80% of W-9 collection steps." It is **not** a platform-wide productivity claim, though it's marketed as if it were.

**Methodology:** Not disclosed. No customer survey methodology, no time-and-motion study, no third-party validation, no comparison baseline (paper checks vs. QuickBooks vs. earlier BILL).

**Contradicting customer evidence (Trustpilot, G2, third-party reviews):**
- Trustpilot average: 3.1/5 with consistent complaints about ACH payments stretching to 14 days
- "Service declined significantly since 2025 layoffs"
- "Accounts held hostage in recursive verification loops"
- "Constant 2-3 week lag between payables"
- "Held my money 4-7 days, either to earn interest or upsell expedited fees"

The reality on the ground is **slower** AP, not 80% faster. The 80% number measures internal automation rate (system metric), not customer-experienced productivity. 🔴

---

## 4. The 480K Customer Count — Deep Dive

**Latest 10-K (FY25, fiscal year ended June 30, 2025):** ~493,800 businesses used the platform. Roughly: ~227K BILL AP/AR core SMB customers + ~40K Spend & Expense + accountant-firm-managed clients + Divvy card-only users. The number is not "paying SaaS contracts."

**Growth trajectory:** AP/AR net adds running ~4,000/quarter in FY26, guided to trend **slightly lower**. This was 6,000-8,000/quarter at peak. Customer growth is decelerating measurably.

**ARPU offset:** Management's public pivot is "we're going upmarket so ARPU grows even as customer adds decline." Truth: this is a defensive pivot because the low end is being conceded to free competitors (Ramp Bill Pay, Mercury Bill Pay, QuickBooks Bill Pay native).

**Net Revenue Retention: 94%.** This is **the** number that matters and it's hidden in plain sight in the 10-K. Best-in-class SMB SaaS NRR is 110-120%. Average healthy SaaS is 105-110%. 94% means the average cohort shrinks 6%/year before new adds. ✅ for transparency, 🔴 for what it implies.

---

## 5. The Clearing-Account / "Middleman" Critique

**How it works:** BILL operates an FBO (For Benefit Of) bank account. Customer money is debited from customer bank → held in BILL's clearing account → released to vendor on schedule. 3-5 day floats are documented in BILL's own help center.

**The harms (real, not just Mercury sniping):**
1. **Float interest captured by BILL, not customer.** $161.8M of FY25 revenue = ~11% of total. That's customer money earning interest BILL keeps. Mercury's "no middleman" pitch is technically and economically accurate.
2. **Bankruptcy/regulatory risk on customer funds.** FBO accounts have ambiguous protection vs. direct ACH. Customer money is briefly an unsecured claim against BILL if anything goes sideways (low probability, but real).
3. **Speed disadvantage.** Direct rails (FedNow, RTP) settle in seconds. BILL's batch model adds 3-5 days by architecture.
4. **Lock-in vector.** Reconciling the clearing account in QuickBooks/Xero is non-trivial — multiple BILL help center articles exist just for this. Sticky friction.

**Is this architecturally required?** No. It's a legacy choice from the 2006-era founding architecture. Could be migrated to direct-rails-with-instant-settlement, but it would cannibalize the $162M float line item.

**Accounting press coverage:** Mostly silent — only competitive sniping (Mercury, Ramp marketing) calls this out. Reddit r/Accounting threads occasionally complain. Not a mainstream critique yet, but a real wedge for competitors.

**Verdict 🟡:** The "middleman" critique is largely correct but **was not a major buyer-decision factor** until competitors started weaponizing it in 2024-2026.

---

## 6. The Activist Case — Confirmed and Detailed

Three activists publicly engaged, in order:

**Barington Capital Group (~$25M position)** — earliest mover. Public letter cited "slowing fundamentals, inability to deliver operating profitability, prolonged share price underperformance." Pushed for cost reduction and strategic alternatives including sale.

**Starboard Value LP (8.5% stake, disclosed Sep 4, 2025; 13D/A Nov 14, 2025 added 7M shares for $372M)** — the heavyweight. Peter A. Feld and Lee Kirkpatrick added to BILL board Oct 15, 2025 via cooperation agreement. Stephen Fisher resigned. Two more new directors named same day. This is a fully consummated board change.

**Elliott Investment Management (~5% stake)** — confirmed by Reuters Nov 12, 2025 in the sale-exploration story. Elliott's involvement is the strongest signal that take-private is being seriously evaluated.

**What they want (synthesized from public letters and outcomes):**
- Cost discipline → delivered: 6% layoffs Oct 2025; 30% layoffs May 7, 2026 (~700 jobs of 2,333 employees, $30-60M charges)
- Capital return → delivered: $1B buyback authorized May 7, 2026
- Strategic review → delivered: Reuters report Nov 12, 2025 confirms sale exploration; Hellman & Friedman publicly named as bidder
- Likely target: Spend & Expense (Divvy) divestiture, or full take-private at a premium to a beaten-down stock

**Stock reaction:** +14% after-hours on the Reuters sale report. Stock is now ~$38-40 (Mar/Apr 2026 data points), down ~88% from $342 peak.

---

## 7. The Competitive Squeeze 2024-2026

**Ramp** — The most dangerous competitor. Hit $1B ARR August 2025 (+110% YoY); $32B valuation Nov 2025; 50,000+ business customers; 2,200+ at $100K+ ARR. Ramp Bill Pay is **free**, with a published one-step migration tool from BILL ("send invoices to Ramp at cutoff date, finish out BILL invoices, done"). Capital One acquired Brex April 2026 — meaning Ramp now stands alone as the only independent at scale.

**Brex** — Acquired by Capital One Jan 2026 announcement, closed April 2026 ($5.15B). Bill Pay still free for Brex customers. Now backed by a top-10 US bank's balance sheet.

**Mercury** — 200K+ customers, $4B/month outgoing payment volume. Bill Pay launched May 2024 with explicit "no middleman" pitch. Direct bank-to-vendor rail. Customer reaction strongly positive; explicitly positioned vs. BILL.

**Tipalti** — Mid-market/enterprise focus, 200+ countries. Slow but consistent share gain in the mid-market segment BILL is now defensively retreating into.

**Melio** — SMB-focused, very low pricing, $150M raise to expand. Eats the lowest end where BILL never had margin anyway.

**QuickBooks Bill Pay (Intuit native)** — The existential threat. Intuit's claim: "48% manual entry reduction." Embedded in QBO. Bill.com has historically been Intuit's payment partner — Intuit becoming a competitor is structural disintermediation.

**Verdict 🔴:** BILL is being squeezed from every angle — free competitors at the SMB end, embedded native bill pay from Intuit at the QBO end, Tipalti at the mid-market end, and bank-backed Brex (now Capital One) at the spend-management end.

---

## 8. Spend & Expense (Divvy) Post-Acquisition Reality

**Paid:** $2.5B in May 2021 (at peak BILL stock and SPAC-era frothiness)

**State as of FY25:** Spend & Expense reportedly maintained ~24% YoY card-payment-volume growth and take rate >250bps per the FY25 commentary. **However**: Ramp's TPV grew from $22.3B (2023) → $57B (2024) — that's more than double — while Brex now sits inside Capital One. Divvy is being out-grown by both standalone competitors at the same time, in the segment it was acquired to win.

**Goodwill impairment:** None publicly disclosed yet per FY25 10-K (goodwill ~$2.4B on balance sheet). Many analysts expect one in FY26.

**Discounting pressure:** Implicit — BILL's transaction take rate is being competed down across the category.

**Spin-off case:** Strong. This is almost certainly **a Starboard demand** behind closed doors. Divvy/Spend & Expense as a standalone could be sold to a private-equity buyer or another fintech; the cash would fund the buyback. Watch for FY27.

**Verdict 🔴:** $2.5B paid for a business now being out-executed by both standalone competitors. A core part of the activist thesis.

---

## 9. The Float / Rates Story

**FY25 float revenue:** $161.8M, ~11% of total revenue
**Quarterly trajectory:** Already declining ($42.9M → $37.9M → $37.4M as rates fell through 2025)

**Why this matters:** Float is the highest-margin revenue line — essentially 100% margin. As Fed cuts continue through 2026, float compresses, which compresses both revenue **and** operating margin disproportionately. The 30% layoff is partially a defensive cost-cut to preserve margin as float erodes.

**Is it a moat?** No. Float income just requires (a) customer funds in transit and (b) a banking partner. Mercury (which is also a banking partner of choice) doesn't need it because Mercury holds deposits directly. The float is a **legacy revenue stream**, not a defensible advantage.

**Verdict 🔴:** Float is a vulnerability disguised as revenue. As rates fall and the architecture is questioned, this line will compress further.

---

## 10. The Agentic AI Play (2025-2026)

**Oct 28, 2025 launch:** BILL AI with W-9 Agent, Reconciliation Agent, onboarding agent. Framed as "first AI agents for SMB AP."

**Roadmap visibility:** Limited. February 2026 update added "enhanced agents" but no clear procurement/approval/audit agent. **Vs. Ramp, which announced a full agent fleet (procurement included) in April 2026** with broader scope.

**Architecture honesty:** BILL's AI agents are LLM-on-top + workflow automation, not custom-trained foundation models. The "trained on 250M invoices" framing is a data-moat narrative, not a true model moat.

**The 6-month-startup question:** Yes, a well-funded startup using Claude/GPT-5 + RAG over per-customer invoice history can match BILL's extraction accuracy in 6 months. The real data moat for AP is **vendor-side normalization at scale** (knowing that "ACME LLC", "ACME, L.L.C.", "ACME Limited" are the same vendor in 8M variations) — and even that is a finite engineering problem, not a multi-year moat.

**Verdict 🟡:** Real AI investment, real shipping, but **defensively pivoting to "AI-first" narrative rather than leading from real moats**. Ramp is winning the AI-agents narrative race.

---

## 11. Pricing Reality

| Item | Marketing | Reality |
|---|---|---|
| Per-seat | $45-$89/user/mo | Real; mid-market deals get discounts. |
| ACH | "Low cost" | $0.59/transaction; can hit $50 on failure |
| Check | Included | $1.99 each; $25 to void |
| Wire (intl USD) | $19.99 | Plus embedded FX margin |
| Wire (intl local FX) | "$0 fee" | **Embedded FX margin** — "hundreds extra on larger payments" |
| Card payment | "Accept cards!" | 2.9% surcharge |
| Expedited ACH | Offered | Upsell after the slow ACH delays |
| Re-debit after failed funding | n/a | $25 |

**Verdict 🔴:** List pricing materially understates true cost. The hidden FX margin is the most egregious — it's deceptive by industry-standard definitions, and it's a wedge any honest competitor can win on.

---

## 12-14. Churn, Network, TAM (compressed)

**Churn:** 94% NRR inclusive of FI; gross retention not separately disclosed but implied 90-92%. **Cohorts shrink each year before new adds.** This is the single most damning number in the file.

**Network:** 8M "members" sounds large but is cumulative-since-inception. Active vendor connections are unspecified. New customers do benefit from vendor pre-existence (fewer onboarding emails), but Mercury's BILL-net-comparable network is rapidly closing the gap.

**TAM:** US SMB AP automation ~$5-6B today, ~14% CAGR. BILL ~20-25% share per UBS. Market growing fast enough that BILL can grow even while losing share — but at decelerating pace.

---

## 15. What Is Genuinely Impressive

Being honest:
1. **The CPA.com / accountant-channel moat is real.** 98 of top 100 US accounting firms; >8,000 firms total. This is a 15-year-built distribution advantage that Ramp/Mercury/Brex cannot replicate quickly — accountants are sticky, and they recommend what they know.
2. **The NetSuite "Intelligent Payment Automation" embed (Oct 2025)** is a genuine strategic win. Being the default AP rail inside Oracle NetSuite is durable mid-market distribution.
3. **8M vendor records with verified payment-routing data** is a real (if narrow) operational moat — not for AI training, but for "your vendor is already in our network, here's their banking info, you can pay them in 2 clicks."
4. **GAAP profitability achieved in FY25.** Most SMB fintechs aren't profitable; BILL is. The margin pressure from float decline + layoffs is the activist concern, but the baseline business is real.
5. **20 years of regulatory licenses and money-transmitter operations.** A startup competing on cross-border payments has 18-24 months of regulatory build-out BILL already completed.
6. **Anti-fraud track record.** Real money is moved; real fraud is stopped. Trust-in-money-movement is harder to build than a feature.

---

## 16. The Competitor Wedge

**Genuinely hard to copy:**
- CPA.com strategic alliance (institutional lock-in via AICPA)
- 20-year vendor network (the routing-data side, not the AI side)
- Money-transmitter licenses in all US states + reg infrastructure
- 8,000 accountant-firm relationships

**Gettable in 12-18 months:**
- AI extraction accuracy (Claude/GPT + RAG matches BILL today)
- Modern UX (BILL's UX is dated; Mercury/Ramp UX is markedly better)
- Real-time settlement (FedNow, RTP — BILL still batch)
- Lower transaction fees (compete on the pricing transparency wedge)
- Direct-rails architecture (no FBO clearing account)

**Most defensible wedges for a new entrant:**
1. **Cross-border specifically.** BILL's FX-margin hide is exploitable. A stablecoin-rails approach (USDC corridor, transparent FX spread, T+0 settlement) genuinely beats BILL on speed and cost for international AP. This is the single best competitive wedge.
2. **Code-enforced policy + on-chain audit trail.** Stablecoin rails plus an Anchor program for approval gates is a real differentiator vs. BILL's permission-system-on-FBO-account.
3. **Vertical depth.** BILL is horizontal; verticalizing on construction, e-commerce, restaurants, or healthcare AP wins disproportionately (specialized vendor categories, industry-specific GL mappings).
4. **Embedded in QuickBooks (or the next-gen alternative).** BILL is being disintermediated by Intuit; a startup that's deeper-than-Intuit-but-cheaper-than-BILL inside QBO could take meaningful share.
5. **"No clearing account, instant settlement, transparent fees."** Mercury proved this narrative works; the question is who else can replicate at scale.

**Where blockchain/stablecoin specifically beats BILL:**
- Cross-border: BILL's hidden FX margin is the most-attackable surface
- Settlement speed: BILL is 3-5 days; USDC settles in seconds
- Multi-party approvals: on-chain multisig is a cleaner audit trail than BILL's policy engine
- Float economics: stablecoin rails return float yield to **the customer**, not the platform — that's a 10x-better economics argument

---

## What Does Not Survive Scrutiny

- The **"trained on 250M invoices" framing as a data moat** — narratively compelling, technically meh. A 6-month-funded startup can match accuracy.
- **The "480K customers" headline** as a measure of paying SaaS contracts. It's not.
- **The 80% manual-work-reduction claim** — narrowly true for specific agents, not the whole platform; contradicted by direct customer experience on Trustpilot/G2.
- **Float as a moat** — it's actually a vulnerability; declining quarterly.
- **The Spend & Expense (Divvy) thesis as currently constituted** — $2.5B paid; out-grown by both Ramp and Brex; likely divestiture candidate.
- **"$0 international wire fees"** — actively misleading; FX margin captures the cost.
- **The "AI agent fleet" narrative** — defensive vs. Ramp; not leading the category.
- **Network effects framing** — 8M "members" is cumulative-since-inception, not active.
- **94% NRR** — quietly the most damning number. SaaS cohorts shouldn't shrink.

## What Is Genuinely Impressive

- The CPA.com alliance and 98-of-top-100 accountant-firm penetration — a real, durable, 15-year-built distribution moat.
- NetSuite IPA (Oct 2025) — strategic embed in Oracle's mid-market ERP is a genuine win.
- 20 years of regulatory operations: money-transmitter licenses in all 50 states, OFAC compliance, bank partnerships. This is invisible-but-expensive infrastructure.
- GAAP profitability in FY25 — most SMB fintechs cannot say this.
- 8M-vendor routing database — narrow but real operational data asset.
- Real anti-fraud track record on real money movement; trust-in-money-movement compounds slowly and is hard to copy.

## The Competitor Wedge

The most attackable surfaces, ranked:
1. **Cross-border payments with stablecoin rails** — BILL's hidden-FX-margin is the single most exploitable surface in the entire pricing model. Win cross-border first, then expand to domestic.
2. **Direct-rails, no-clearing-account architecture with float yield returned to customer** — Mercury proved this works narratively; a B2B-AP-pure-play version is open.
3. **Vertical depth (construction, e-commerce, healthcare, restaurants)** — BILL is horizontal; vertical wins disproportionately.
4. **Embedded inside QuickBooks/Xero/NetSuite as a feature rather than a platform** — capture the Intuit-is-disintermediating-BILL dynamic.
5. **Modern AI-first AP from day one** — not "AI added to 20-year-old workflow engine." A clean-sheet AI-native architecture matches BILL accuracy with 1/10th the workflow cruft.
6. **Pricing transparency as a marketing wedge** — publish every fee on the homepage; weaponize BILL's hidden FX margins; turn Trustpilot complaints into ads.

What is hard to take: the CPA.com lock-in, NetSuite embed, and regulatory licensing. A startup competing here should either (a) compete on a vector accountants don't gate (vertical SaaS), or (b) build a parallel distribution channel (banks, embedded fintech, neobank partnership).

## The Honest One-Liner

**Bill.com is a 20-year-old SMB AP automation business that built a durable accountant-channel moat and a real money-movement franchise, is now suffering from decelerating cohort retention (94% NRR), a float-revenue stream that's structurally compressing as rates fall, an AI narrative that's defensive rather than category-leading, and competitive pressure from free Bill Pay at every neobank — and is in active strategic review with three activists, $1B buyback, 30% layoffs, and likely PE-led take-private as the most probable 2026-2027 outcome. The marketing version is "AI-first financial operations platform for the Fortune 5 Million"; the actual version is "post-peak SaaS incumbent being squeezed simultaneously by free competitors, embedded native rails, and rate-cycle compression, defended by an accountant-firm channel that is genuinely hard to copy."

---

## Sources

- [BILL Holdings FY2025 10-K (SEC)](https://www.sec.gov/Archives/edgar/data/0001786352/000178635225000037/bill-20250630.htm)
- [BILL Holdings Q3 FY2026 8-K, May 2026 (SEC)](https://www.sec.gov/Archives/edgar/data/0001786352/000162828026032064/bill-2026331xexx991.htm)
- [Starboard Value 13D/A (SEC)](https://www.sec.gov/Archives/edgar/data/0001786352/000092189525002554/ex993to13da106297bill_090825.htm)
- [Starboard Schedule 13D filing (SEC, Sep 2025)](https://www.sec.gov/Archives/edgar/data/0001786352/000092189525002532/ex2tosc13d06297bill_09042025.htm)
- [BILL "Friction Crisis" AI blog](https://www.bill.com/blog/the-future-of-finance-is-touchless)
- [BILL Launches AI Agents press release (Oct 2025)](https://www.bill.com/press-release/bill-launches-new-ai-agents)
- [BILL Reports FY2025 Results + $300M Buyback](https://investor.bill.com/news/news-details/2025/BILL-Reports-Fourth-Quarter-and-Fiscal-Year-2025-Financial-Results-and-Announces-300-Million-Share-Repurchase-Program/default.aspx)
- [BILL Announces Addition of Four New Directors (Starboard cooperation)](https://investor.bill.com/news/news-details/2025/BILL-Announces-Addition-of-Four-New-Directors/default.aspx)
- [Activist investor targets Bill — Payments Dive](https://www.paymentsdive.com/news/activist-investor-targets-bill-performance-Starboard-accounting-software/759578/)
- [Bill CEO defends performance — Payments Dive](https://www.paymentsdive.com/news/bill-ceo-defends-company-performance-activist-Elliott-management-starboard-value/759878/)
- [Barington Pushes Bill Holdings Sale — Bloomberg Law](https://news.bloomberglaw.com/mergers-and-acquisitions/activist-barington-targets-bill-holdings-pushes-board-for-sale)
- [Pressure on Bill Holdings rises — Payments Dive](https://www.paymentsdive.com/news/pressure-on-bill-holdings-rises/807165/)
- [Hellman & Friedman acquisition talks — Investing.com](https://www.investing.com/news/stock-market-news/bill-holdings-stock-soars-on-potential-acquisition-talks-with-hellman--friedman-93CH-4491545)
- [BILL Layoffs May 2026 — Layoffhedge](https://layoffhedge.com/company/bill-holdings)
- [BILL Holdings Q3 FY2026 Earnings Call — Motley Fool](https://www.fool.com/earnings/call-transcripts/2026/05/08/bill-bill-q3-2026-earnings-call-transcript/)
- [Mercury Bill Pay product page](https://mercury.com/bill-pay)
- [Mercury Bill Pay launch — TechCrunch](https://techcrunch.com/2024/05/07/startup-neobank-mercury-is-taking-on-brex-and-ramp-with-new-bill-pay-spend-management-software/)
- [Ramp vs BILL comparison](https://ramp.com/versus/bill-com)
- [Ramp $32B valuation — PR Newswire](https://www.prnewswire.com/news-releases/ramp-reaches-32-billion-valuation-doubling-revenue-and-customers-in-past-year-302616510.html)
- [QuickBooks Bill Pay announcement — Intuit](https://investors.intuit.com/news-events/press-releases/detail/30/intuit-introduces-quickbooks-bill-pay-expanding-money-platform-to-deliver-business-to-business-payments-with-ap-automation)
- [NetSuite + BILL Intelligent Payment Automation — PR Newswire](https://www.prnewswire.com/news-releases/netsuite-and-bill-partner-to-accelerate-accounts-payable-processes-302577217.html)
- [Trustpilot BILL reviews](https://www.trustpilot.com/review/bill.com)
- [BILL G2 reviews](https://www.g2.com/products/bill-ap-ar/reviews)
- [BILL Accountant Partner Program — CPA.com](https://www.cpa.com/bill)
- [BILL pricing page](https://www.bill.com/product/pricing)
- [BILL clearing account help docs](https://help.bill.com/direct/s/article/115005449786)
- [BILL Holdings 7-year stock history — MacroTrends](https://www.macrotrends.net/stocks/charts/BILL/bill-holdings/stock-price-history)
- [Ramp company profile — Sacra](https://sacra.com/c/ramp/)
