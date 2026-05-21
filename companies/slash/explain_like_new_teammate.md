# Slash — Explain Like a New Teammate

*Compiled 2026-05-21. The "dumb questions" file. Written for a smart new teammate who doesn't know Slash or the SMB-neobank category and must understand it by tomorrow.*

---

## What does Slash do, in one sentence?

Slash is a business banking app — like Mercury, but pitched at internet-native small businesses (agency owners, Amazon sellers, creators, people running 10 LLCs) instead of VC-backed software startups.

---

## What problem exists before this product?

A small-business owner who runs, say, three Shopify brands and a digital agency has a banking problem:

- **Chase Business** treats them like a 1950s grocery store. Opening a second account requires a branch visit. Sub-accounts barely exist. Virtual cards barely exist. Categorization is manual via Excel.
- **Mercury** is excellent if you're a venture-backed software startup. Less excellent if you're a multi-LLC e-commerce operator who needs 30 virtual cards per month for ad spend, separate accounts per brand, and reconciliation against Amazon disbursements. Mercury has been adding these features but didn't start there.
- **Brex** stopped serving SMBs under ~15 employees post-2022 pivot.
- **Found / Lili** are aimed at solo 1099s, not multi-entity operators.
- **Relay** is the closest peer but more horizontal.

So the typical multi-brand e-commerce operator or agency owner ends up with:
- One Mercury account for the "main" entity
- Three Chase Business accounts for legacy LLCs
- A Shopify Balance account
- Personal Chase Ink cards used for business expenses
- A spreadsheet that tries to reconcile all of it
- An accountant who charges $X,000/year to clean it up at tax time

Slash is built for this person.

---

## Who buys it?

Six rough buyer profiles, in roughly the order Slash launched workspaces for them:

1. **Sneaker resellers / arbitrage operators** (the founding ICP — they needed many virtual cards across many merchant accounts)
2. **Amazon FBA sellers and Shopify multi-brand operators**
3. **Marketing agencies, dev shops, design studios** (sub-accounts per client retainer + virtual cards per contractor)
4. **Content creators / newsletter operators / course sellers** (spiky multi-source income + tax-set-aside)
5. **Holding-company operators** (the "I run 12 LLCs" customer Cardenas himself is)
6. **Real estate investors with sub-account-per-property workflows** (newer)

Common thread: **internet-native, transaction-heavy, often multi-entity SMBs that traditional neobanks find weird.**

---

## Who uses it day to day?

The business owner themselves, plus possibly:
- A bookkeeper or accountant who exports to QuickBooks / Xero
- Contractors who hold virtual cards with spend limits
- A virtual assistant who pays bills
- The founder's CPA at tax time

For multi-LLC holdcos: one owner, many entities, one dashboard.

---

## What exactly happens, step by step, inside the product?

1. Owner signs up, picks a vertical workspace
2. Owner verifies identity (KYC) and business (KYB) — partner bank's compliance team makes the call
3. Owner gets a business checking account (held at Lead Bank or whoever the current partner is — Slash itself is not a bank)
4. Owner spins up sub-accounts (one per client, brand, property, etc.)
5. Owner issues virtual or physical cards (with per-card limits, merchant locks, single-use options)
6. Money flows in (client wires, Amazon disbursements, Shopify payouts, Stripe transfers)
7. Money flows out (card swipes, ACH bill-pay, wires, check disbursement)
8. Slash auto-categorizes every transaction by vertical-specific defaults
9. At month-end, owner exports to QuickBooks / Xero
10. At year-end, Slash generates 1099-NEC forms for contractor payments

The "industry workspace" framing means each vertical gets different default sub-account templates, different default expense categories, different cash-back tuning, and different surfaced integrations — but the underlying ledger, card program, and rails are the same.

---

## What data, money, or state moves through the system?

- **Money** sits at a partner bank (currently Lead Bank, likely) in FBO ("for benefit of") accounts. The partner bank handles the FDIC-insured deposit, originates ACH and wires, settles card transactions.
- **A virtual ledger** at Slash represents each customer's sub-accounts and balances on top of the FBO structure. The partner bank sees aggregates; Slash sees the customer's structured view.
- **Cards** are issued by a card issuer-processor (likely Marqeta, Highnote, or Lithic) on the Visa network, with the partner bank as the issuing bank-of-record.
- **Inbound flows** from Amazon / Stripe / Shopify / Stripe Connect arrive via ACH or wire.
- **Outbound flows** go via ACH (most common), wire (high-value or international), RTP/FedNow (if supported by partner bank), or paper check (Checkbook.io / partner rail).
- **AI / categorization** runs on top of the transaction stream, tagging by vertical and feeding into QuickBooks / Xero sync.

---

## Why is this hard?

1. **Regulation:** Slash itself is not a bank. It must operate via a partner bank, follow that bank's KYC/KYB/AML rules, and survive the partner bank's risk reviews. Banking-as-a-Service is a regulated, brittle stack — see the 2024 Synapse collapse and Evolve cyber incident.
2. **Multi-tenancy at the FBO layer:** Maintaining a virtual ledger of thousands of sub-accounts inside a small number of FBO accounts at the partner bank is non-trivial. ACH routing-number mapping, dispute handling, statement generation, and audit-trail maintenance all need careful engineering.
3. **Vertical customization without forking the codebase:** Shipping six different "workspaces" without maintaining six different products requires good defaults and good extensibility. Many fintechs end up with vertical-specific bugs that linger because no one in the company owns vertical N.
4. **Compliance for high-velocity card use:** E-com / ad-buying customers generate transaction volumes that look like fraud to most banks. Onboarding them at scale requires negotiation with the partner bank's risk team.
5. **Customer support:** SMB banking support is famously bad. Doing it well costs real money and headcount.

---

## Why now?

- **The 2024 BaaS shakeout (Synapse Chapter 11, Evolve consent orders, Evolve cyber incident) cleared the field.** Many BaaS-overlay fintechs failed or were forced to migrate. Slash navigated this without losing customer funds — itself a defensible moat.
- **Multi-entity operators are growing.** "I run 12 LLCs" is a fast-growing customer archetype thanks to creator economy, holdco-style operators, and YC's "wealth-by-portfolio" memetic influence.
- **The crypto-debanking refugees need a home.** Mercury, Chase, and Brex have repeatedly de-banked crypto-adjacent operators. Slash has positioned itself (on Twitter, less so on the homepage) as more tolerant.
- **The AI-as-feature wave** lets Slash market AI bill-pay, AI categorization, AI "ask your books" — even though the underlying tech is OCR + LLM + rules, the framing matters for customer acquisition.

---

## What is actually impressive?

- **Vertical execution speed.** Shipping six workspaces in 18-ish months with one core ledger and one core card program is genuine velocity.
- **Surviving the Synapse / Evolve fallout.** Customer funds were not lost; the migration to Lead Bank (and direct partner-bank relationships) was relatively clean.
- **Capital efficiency.** Total raised ~$60-67M through Series B at $370M post-money. Brex / Ramp / Mercury have all raised an order of magnitude more.
- **Founder-market-fit.** Cardenas previously built Karat Financial (creator-economy credit cards) — so he had already operated in the "fintech for customers who look weird to banks" space before Slash.
- **The "10 LLCs from one dashboard" pitch.** If it works at the demoed quality level, it's a genuine wedge — Mercury makes you open 10 separate accounts.

---

## What is still unclear?

- **Current partner-bank stack** (Lead Bank likely, but unverified against the live deposit agreement)
- **Revenue / ARR / take rate** — never disclosed
- **Profitability** — Goodwater's "efficient growth" language implies "not yet profitable but burn is controlled"
- **Actual active-customer count** — the gap between "20K businesses" (Series B announcement) and "40K workspaces" (late-2024 marketing) is unresolved
- **AI feature depth** — whether any of it is more than OCR + LLM extraction
- **Card BIN / issuer / processor** — unverified
- **FDIC sweep mechanics + headline insured amount** — unverified
- **Whether Slash has multi-bank routing today** — important for post-Synapse resilience, unverified
- **Customer concentration in the crypto-adjacent segment** — likely meaningful but never disclosed; would change the risk profile if a partner-bank policy change forced off-boarding

---

## The mental model: "Think of Slash as..."

**Think of Slash as Mercury for the kind of small business that opens new LLCs the way most people open new Notion pages.**

It's not a startup-banking product (Mercury owns that). It's not a solopreneur product (Found / Lili own that). It's not a venture-spend-management product (Ramp / Brex own that). It's a banking product for the operator who runs *many small entities at once* and needs the UX to handle that without spreadsheets.

The actual business model underneath is a standard BaaS-overlay neobank: it makes money on (a) the spread between what its partner bank pays it on float and what it passes through to customers, (b) card interchange, (c) wire fees, (d) FX markup, with a small slice from subscription. The "AI" and "vertical software" framing is a customer-acquisition story; the float NIM is the actual business.

The big risk is the same as for every BaaS-overlay: the partner bank's solvency, the partner bank's risk-appetite changes, and a hypothetical regulatory action against the BaaS model itself. Slash has navigated one of these (Synapse / Evolve 2024); the next one will eventually come.

If you want to understand Slash, the single most useful next action is to actually open an account (or watch a demo) and see what "10 LLCs in one dashboard" really looks like. Everything else in this folder is description; that's the experience.
