# Deel — Explain Like a New Teammate

*Compiled 2026-05-21. The "dumb questions" file. Written for a smart new teammate who doesn't know Deel or the global-payroll/EOR category and must understand it by tomorrow.*

---

## What does Deel do, in one sentence?

Deel is a company that hires, pays, and manages workers in countries you don't have a legal entity in — and lets you do it through one platform instead of opening foreign subsidiaries.

---

## What problem exists before this product?

Imagine you're a US-based startup. You want to hire:
- A backend engineer in **Lisbon**
- A community manager in **São Paulo**
- A growth marketer in **Lagos**

Without Deel (or a competitor), you have three options, each painful:

1. **Open a legal entity in each country.** Costs $10K-$50K per country, takes 3-6 months, requires a local accountant, local payroll, local labor compliance, local termination law. Not viable for hiring one person.
2. **Hire them as contractors via Wise or PayPal.** Fast, cheap — but worker-misclassification risk. Many countries treat full-time work for a single foreign employer as employment regardless of what you call it; tax authorities can reclassify and assess back-taxes + penalties on you.
3. **Use a local Employer of Record (EOR) provider per country.** Each has different contracts, different pricing, different UX. Operations nightmare.

Deel solves this by being **one EOR that operates in 150 countries**. Their local legal entities (or partners) employ your worker on your behalf. You pay Deel monthly; Deel handles the payroll, taxes, benefits, and labor compliance in each country.

The same platform also handles **contractor management** (cleaner contracts, automated tax forms, multi-currency payments including USDC) for cases where contractor status is legally appropriate.

---

## Who buys it?

Three primary buyer segments:

1. **Startups (seed to Series B)** that want to hire their first international engineer or designer fast. Deel Contractor at $49/contractor/month is the typical entry point.
2. **Scale-ups (Series C to pre-IPO)** that have entities in their top 2-3 markets and use Deel EOR for the "long tail" of countries where they only have 1-5 hires.
3. **Enterprise (1000+ employees)** that use Deel to consolidate vendor relationships across the 50+ smaller countries where opening an entity makes no sense.

Real named customers: Shopify, Notion, Klarna, Forbes, BCG, Reddit, Hopin, Andela, Replit, Plaid. Logos like Nike, Dropbox, Cloudflare appear in marketing.

---

## Who uses it day to day?

- **HR ops / People team** at the customer company — onboarding, offboarding, contract changes
- **Finance / AP team** — paying contractors and funding payroll runs
- **The workers themselves** — clocking time, submitting expenses, downloading tax forms
- **Bookkeepers / accountants** — exporting transactions to QuickBooks/Xero/NetSuite
- **For multi-LLC / multi-entity companies** — the founder or COO managing across entities

---

## What exactly happens, step by step, inside the product?

**For a contractor relationship:**
1. Employer signs up, completes KYB
2. Employer creates a contract for the contractor (country, currency, rate, scope) — Deel auto-generates the locally-compliant contract
3. Contractor receives invitation email, completes KYC (ID, tax form W-8/W-9 or local equivalent), connects payout method (bank, USDC wallet, Deel Card, Wise/Payoneer)
4. Contractor submits monthly invoice through Deel
5. Employer approves
6. Deel processes payment: deducts fees, applies FX, routes via chosen payout method
7. At year-end, Deel generates 1099-NEC (US) or local equivalent

**For an EOR (Employer of Record) relationship:**
1. Customer needs to hire someone in country X where they have no entity
2. Customer creates an EOR job through Deel
3. Deel's country-specific team reviews the offer (salary, benefits, statutory employer costs) and generates a compliant employment contract via Deel's local legal entity
4. Worker signs the contract — legally employed by **Deel's local entity, not the customer**
5. Each month, customer funds Deel with USD/EUR/GBP covering gross salary + statutory employer contributions + Deel's EOR fee (~$599/month or % of salary)
6. Deel's local entity runs payroll: withholds employee tax + social security, adds employer-side contributions, pays net salary to employee's local bank account
7. Deel files local payroll taxes and statutory benefits on time
8. At year-end, Deel issues the local equivalent of W-2 / P60 / Modelo 3 / etc.
9. If employee leaves: Deel handles statutory notice periods, severance, and country-specific termination paperwork

---

## What data, money, or state moves through the system?

- **Money** moves from employer's US/EU/UK bank account → Deel's segregated treasury accounts at partner banks → Deel's local entity bank accounts (or partner EOR bank accounts) → employee/contractor local bank accounts or crypto wallets
- **Local taxes** withheld from gross salary → remitted to local tax authorities monthly/quarterly per local rules
- **Statutory benefits** (social security, healthcare, pension) computed per country, contributed by employer
- **Cards** — Deel Cards funded from contractor's Deel wallet; spending on Visa/Mastercard rails
- **Stablecoins** — USDC payouts on Ethereum, Polygon, Solana, Stellar
- **Compliance docs** — contracts, tax forms, work permits, immigration filings
- **HR data** — performance reviews, time-off, expense reports, equipment records

---

## Why is this hard?

1. **Each country has different employment law.** Termination rules in France (heavy notice periods, employer-favored severance) are nothing like California (at-will). Mistakes cost money — and the EOR is the legal employer, so the EOR pays.
2. **Tax compliance varies country by country.** Different forms, different deadlines, different statutory deductions, different employer contributions.
3. **Payment rails are fragmented.** ACH (US), SEPA (EU), Fedwire, RTP, local rails in 100+ countries, plus stablecoins, plus Wise/Payoneer for emerging markets. Each has its own quirks.
4. **Cross-border FX has real cost.** Spreads, settlement timing, capital controls (Argentina, Nigeria, Venezuela).
5. **You're the legal employer.** Misclassification, missed payroll filings, late tax remittances — they all come back to Deel.
6. **The product is partially regulated services.** This isn't pure software; it's HR ops + legal + payroll bureau + FX + cards, with software at the top.
7. **150 countries is a coordination nightmare.** Country-specific updates to tax rates, statutory benefits, labor law happen constantly.
8. **AML/sanctions screening at scale.** Deel pays workers in 150 countries; the screening surface is huge.

---

## Why now?

- **Remote work normalized** post-COVID. Companies that hire globally went from rare to default.
- **Crypto-payroll wedge** opened a beachhead 2020-2022. Deel was first to ship USDC payouts to contractors at scale.
- **Aggressive M&A** (Hofy for devices, PaySpace for African payroll, Atlantic Money for FX, Zavvy for talent, Capbase for cap-table, Legalpad for immigration) consolidated the HRIS+payroll+IT+immigration stack into one platform.
- **The 2022 layoffs** in tech shrunk competitors and let Deel keep growing through what was an industry downturn.
- **The 2025 Rippling lawsuit** has dominated coverage but hasn't (yet) materially dented Deel's revenue trajectory.

---

## What is actually impressive?

- **Execution speed.** Deel went from 4 employees in early 2020 to ~5,000+ employees and $1B+ ARR by end of 2024. Among the fastest in SaaS history.
- **Three rounds in six months in 2021** (Series B, C, D) — the velocity itself is part of the story.
- **No major layoffs through 2022-2024** when most of tech was cutting deeply. Deliberate counter-positioning.
- **The M&A roll-up actually integrates.** Most fail. Deel has stitched Hofy + PaySpace + Atlantic Money + Zavvy into the platform.
- **Genuinely useful crypto-payroll wedge.** The Andela-Yellow Card-Lagos engineer flow generates measurable economic value for end users (~$300-400/month more vs Deel's direct USD→NGN route).
- **Real customer logos.** Shopify, Notion, Klarna, Forbes are confirmed.

---

## What is still unclear or risky?

- **The Rippling lawsuit.** A sworn Irish High Court affidavit names Alex Bouaziz (CEO) and Philippe Bouaziz (CFO, Alex's father) as having personally directed corporate espionage. Even if Deel ultimately wins, the cultural signal is severe. The S-1 risk-factor section becomes brutal.
- **Father-son CEO-CFO governance.** Unusual at a decacorn; flagged in the Rippling case.
- **"$1B ARR" definition.** ARR includes float income and FX markup. GAAP revenue would look different.
- **"150 countries" definition.** Conflates contractor payments (any country), EOR (Deel-owned entity OR partner), and full local payroll. The breakdown is unpublished.
- **Owned vs partner EOR entity count.** Estimates vary from 40-60 (competitor/Sacra estimate) to 110-120 (Deel marketing-anchored). Truth probably 50-120.
- **Customer "count" definition.** A 1-contractor SMB counts the same as Shopify.
- **EBITDA-positive claim.** Founder-tweet level disclosure; not audited.
- **Net dollar retention by cohort.** Never disclosed. EOR has a built-in churn driver (once you have 5+ employees in a country, the math flips to opening your own entity).
- **IPO timeline.** "IPO-ready" since 2022. Repeatedly slipped. Rippling lawsuit + S-1 disclosure complexity + valuation overhang are all blockers.
- **DOJ/SFO criminal referral.** Reported in one source, unverified.
- **Bouaziz Dubai relocation.** Reported, not officially confirmed.

---

## The mental model: "Think of Deel as..."

**Think of Deel as a global HR operations company with a software UI on top — part legal employer (for tens of thousands of workers worldwide), part payroll bureau, part FX/remittance shop, part contractor SaaS — wrapped in one platform that lets you hire anywhere without opening entities.**

It is **not** a pure software company, even though the marketing implies one. About **40% of margin contribution is software; 60% is services** (the actual legal employment, the actual local payroll filings, the actual immigration counsel, the actual customer support, the actual entity setup). This matters for valuation: software companies trade at 8-15x revenue; services companies trade at 1-3x. Deel's last private mark ($17.3B / ~$1B-1.4B ARR) implies a software multiple. A public listing would likely re-rate to a blend.

It is **not** a neutral piece of infrastructure. The Rippling lawsuit alleges (and a sworn affidavit by the paid mole supports) that the founders personally directed corporate espionage against the company's biggest competitor. Even if Deel ultimately prevails, the culture that produced this case is itself a meaningful piece of information for anyone evaluating Deel as a vendor, employer, or investment.

It is **genuinely useful**. The Lagos engineer earning $5,500/month via Andela → Deel → USDC-Stellar → Yellow Card → NGN is getting paid more efficiently than would have been possible before this stack existed. The Shopify engineer in Lisbon, the Notion community manager in São Paulo, the BCG short-term consultant in Singapore — they all exist because Deel (or a Deel-equivalent) made the friction tolerable.

If you want to understand Deel, the single most useful next action is to (a) read the actual Rippling complaint and the Keith O'Brien Irish High Court affidavit, and (b) open a free Deel contractor account and walk through onboarding to see the actual product. Everything else in this folder is description; those two are the experiences that matter.
