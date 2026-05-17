# Mercury (mercury.com) — Banking Stack & Technical Architecture

**Scope.** Deep technical map of Mercury Technologies, Inc. — the San Francisco / Bay Area fintech founded in 2017 by Immad Akhund. Disambiguation: this is *not* Mercury Layer, Mercury Insurance, Mercury Systems, Mercury Marine, Mercury Fund, Mercury Financial, or any of the other ~20 "Mercury" trade names. Subject of this document is the business banking platform at https://mercury.com that, as of May 2026, serves **300,000+ businesses and individuals** ([Mercury / OCC conditional approval release, Apr 2026](https://www.heygotrade.com/en/news/mercury-wins-occ-conditional-approval-for-national-bank-charter/)).

Confidence legend: ✅ verified by primary source / multiple independent sources · 🟡 single source or inferred · 🔴 widely repeated but not primary-sourced / contradicted.

---

## 0. Executive snapshot — the stack at a glance

| Layer | Vendor / Counterparty | Confidence |
|---|---|---|
| Deposit holder banks (legacy) | **Choice Financial Group** (Fargo, ND), **Column N.A.** (Chico, CA), **Evolve Bank & Trust** (Memphis, TN — wind-down 2025) | ✅ |
| Deposit holder banks (current, post-Evolve) | **Choice Financial Group**, **Column N.A.**, **Patriot Bank, N.A.** (Stamford, CT) | ✅ |
| Future direct charter | **Mercury Bank, N.A.** — OCC conditional approval Apr 2026, HQ Utah | ✅ |
| Sweep network (Vault) | Choice and Column sweep programs — up to 20 partner banks, $5M FDIC | ✅ |
| Debit cards (business + personal) | Issued by **Choice Financial Group** & **Column N.A.** on **Mastercard** | ✅ |
| IO charge card (credit) | Issued by **Patriot Bank, N.A.** on **Mastercard** | ✅ |
| Issuer processor | **Lithic** (formerly Privacy.com) — both debit and credit | ✅ |
| Treasury custody | **Apex Clearing Corp.** (FINRA-regulated broker-dealer, SIPC-insured) | ✅ |
| Treasury funds | **J.P. Morgan U.S. Treasury Plus MMF** (JTCXX) + **Morgan Stanley Ultra-Short Income** (MULSX) | ✅ |
| Working Capital originator | **Mercury Lending, LLC** (NMLS 2606284), serviced by **Mercury Servicing, LLC** (NMLS 2606285) | ✅ |
| Venture Debt originator | **Evolve Bank & Trust** (historical; future state unverified post-Evolve exit) | 🟡 |
| External account aggregation | **Plaid** (Auth, Balance, Assets); Mercury exposed as a Plaid endpoint | ✅ |
| KYB / KYC vendor | Unverified (Persona / Alloy / Middesk not publicly disclosed) | 🔴 |
| Public API | `api.mercury.com/api/v1`, Basic Auth (token) + OAuth2 for partner integrations | ✅ |
| Webhooks | `x-mercury-signature` HMAC-SHA256 | ✅ |
| AI surface | **Official Mercury MCP server** (hosted, OAuth, read-only at launch; write tools on roadmap) | ✅ |
| Crypto stance | "Supports thousands of web3 startups, DAOs, funds." Does **not** support MSBs or exchanges. Fiat-only accounts. | ✅ |

---

## 1. Banking partners, charters, and the sweep network

### 1.1 The "core" banks

Mercury is not a bank. It is a Delaware-incorporated tech company whose deposits sit at FDIC-insured partner banks under direct deposit agreements. The official disclosure language as of May 2026 reads: *"Mercury is a financial technology company, not a bank. Banking services provided through Choice Financial Group, Column N.A., and Patriot Bank, N.A., Members FDIC."* ([Mercury / how partners work, 2026](https://mercury.com/blog/how-mercury-works-with-partner-banks); ✅).

| Bank | HQ | Charter type | FDIC Cert # | Role at Mercury |
|---|---|---|---|---|
| **Choice Financial Group** | 4501 23rd Ave S, Fargo, ND | Commercial bank, state charter, Fed non-member, FDIC-supervised | **9423** | Core deposit holder + sweep program operator + debit-card issuer (business & personal) |
| **Column N.A.** (fka Northern California National Bank) | 1717 Mangrove Ave, Chico, CA | National bank (OCC), Federal Reserve member | **58224** | Core deposit holder + sweep program operator + debit-card issuer |
| **Patriot Bank, N.A.** | Stamford, CT | National bank (OCC) | **33928** | Issuer of the IO charge card; agreements governed by Connecticut law |
| **Evolve Bank & Trust** | Memphis, TN | State-chartered bank | 1299 | Legacy core bank; Mercury announced exit Mar 2025, migration complete by year-end 2025 |

Sources: [Choice Financial Group FDIC detail](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/9423); [Column N.A. FDIC detail #58224](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/58224); [Patriot Bank FDIC detail #33928](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/33928); [Mercury / Banking Dive, Mar 2025 — pivot from Evolve](https://www.bankingdive.com/news/mercury-pivot-partner-bank-evolve/742704/).

**Column N.A. backstory** (matters for Mercury's strategy): William Hockey, the Plaid co-founder, bought NorCal National Bank for ~$50M in 2021, rebranded it Column in April 2022, and rebuilt the core on a from-scratch ledger in San Francisco. Column is one of the very few US national charters in fintech-native hands ([TechCrunch / Plaid co-founder, Apr 2022](https://techcrunch.com/2022/04/21/plaid-cofounders-next-venture-is-a-bank-to-power-fintech-apps/); [American Banker / De novo Column](https://www.americanbanker.com/news/de-novo-column-bank-gives-partners-a-sandbox-to-build-banking-tools); ✅). When Mercury added Column as a deposit holder in 2023, it was a partial backstop against Evolve concentration risk — and in retrospect, the right call.

**The Evolve exit.** On 12 Mar 2025, Mercury publicly announced it was severing its relationship with Evolve Bank & Trust, with migration to Choice or Column to be completed by end of 2025 ([Bloomberg, 12 Mar 2025](https://www.bloomberg.com/news/articles/2025-03-12/fintech-neobank-mercury-severs-its-relationship-with-evolve-bank); [Banking Dive](https://www.bankingdive.com/news/mercury-pivot-partner-bank-evolve/742704/); ✅). Stated reason: "Mercury outgrew the relationship." Real reason: Evolve was named in the Synapse bankruptcy mess and hit with a June 2024 Fed enforcement action on BSA/AML and risk management deficiencies. Customer rollover was completed in batches — affected customers had to re-KYC and accept new T&Cs with the receiving bank, but kept uninterrupted platform access ([American Banker, Mar 2025](https://www.americanbanker.com/news/small-business-fintech-mercury-bank-partner-evolve-split); ✅).

### 1.2 Mercury Bank, N.A. — the OCC charter

On **27 April 2026**, Mercury received **conditional OCC approval** to establish Mercury Bank, N.A., a national bank to be headquartered in Utah ([Mercury / press release, 27 Apr 2026](https://www.businesswire.com/news/home/20260427949683/en/Mercury-Receives-OCC-Conditional-Approval-to-Establish-Mercury-Bank-N.A.); [Fintech Brainfood analysis](https://www.fintechbrainfood.com/p/ai-checkout); ✅). The original charter application was filed in **December 2025** ([Mercury / OCC charter application, 19 Dec 2025](https://www.businesswire.com/news/home/20251219760269/en/Mercury-Applies-for-OCC-National-Bank-Charter-to-Become-the-Bank-for-Builders); ✅).

Open conditions: Mercury must complete the bank-organization phase, satisfy remaining OCC requirements, and obtain separate sign-offs from the **FDIC** (deposit insurance) and the **Federal Reserve** (membership / supervisory). Until those are in hand, the charter is not "live." Strategic implications when it does launch:

- Direct **Zelle** access (currently absent — a real product gap vs. Brex).
- Direct **Fedwire / FedACH** participation, eliminating partner-bank settlement latency.
- In-house **lending balance sheet** instead of Mercury Lending LLC fronting against external warehouse lines.
- Reduction of bank-partner spread; potential APY uplift for customers without Treasury.

### 1.3 Mercury Vault — the sweep network mechanics

Mercury Vault sweeps customer deposits across up to **20 partner banks**, providing up to **$5,000,000** in aggregate FDIC insurance ($250k per bank × 20). It is not a single product — it is operated separately by each of Mercury's two core banks ([Mercury / blog, sweep network explainer](https://mercury.com/blog/understanding-bank-sweep-network); [Mercury / blog, Vault launch](https://mercury.com/blog/mercury-vault-announcement); ✅).

- **Choice Financial Group Sweep Program** — operates under the [Choice Sweep Program Deposit Placement and Custodial Agreement](https://mercury.com/legal/choice/sweep-program-deposit-placement-and-custodial-agreement). Full bank list published in the [Choice — Mercury Deposit Program Disclosure Statement (latest filed PDF 05_01_24)](https://co-mercury-prod.s3.amazonaws.com/legal/Choice+-+Mercury+Deposit+Program+Disclosure+Statement+-+05_01_24.pdf).
- **Column N.A. Sweep Program** — operates under the [Column Sweep Program Deposit Placement and Custodial Agreements](https://mercury.com/legal/column/sweep-program-deposit-placement-and-custodial-agreements).

Vault was launched in March 2023 as the direct response to the SVB collapse (8–10 Mar 2023), going from concept to GA in days ([FintechLabs / SVB response coverage](https://fintechlabs.com/reacting-quickly-to-svb-fallout-mercury-launches-vault-with-5m-fdic-deposit-insurance/); ✅).

**Sweep partner banks — what is and isn't verifiable.** The S3 PDF disclosure pages contain the full bank list, but the published page-level list is not enumerated in any search-indexed surface I could read without a paywall-style direct fetch (WebFetch was denied in this session). Repeated unverified mentions across reseller/affiliate pages allude to names like **Cross River**, **First Internet Bank**, **Customers Bank**, **Pacific Western**, **Sterling**, **HSBC USA**, **EagleBank**, **Citizens Bank** etc. — but **I cannot confirm those without the legal PDF**, and the network composition rotates ([sweep network unverified bank list, 2024](https://mercurydocumentation.com/banking-interface-partner-sweep-network-5m-fdic); 🔴). Apex Clearing is **not** a sweep network participant on the cash side — that vendor is the Treasury (brokerage) custodian, a separate program (see §4).

> **Known unknown #1: the actual 20-bank sweep list.** Confirmable only by retrieving the current Choice and Column Disclosure Statement PDFs from `co-mercury-prod.s3.amazonaws.com/legal/`. The Choice PDF I found was dated `05_01_24`; an earlier copy `12_21_22` is also archived.

---

## 2. Card issuing — Mercury Debit, Mercury IO

Two separate programs sit under the Mercury brand:

### 2.1 Mercury Debit Card (business + personal)

- **Issuing banks:** Choice Financial Group and Column N.A. (the same bank holding the underlying deposit issues that customer's debit card). ✅ [Mercury / Choice Commercial Debit Card Agreement](https://mercury.com/legal/choice/commercial-debit-card-agreement); [Mercury / Choice Consumer Debit Card Agreement](https://mercury.com/legal/choice-personal/consumer-debit-card-agreement)
- **Network:** **Mastercard** (no Visa option). ✅
- **Form factor:** Virtual + physical; supports Apple Pay / Google Pay tokenization.
- **Daily limits:** Set per card with weekly card limits added in April 2023.

### 2.2 Mercury IO — corporate charge card

- **Issuing bank:** **Patriot Bank, N.A.**, Stamford CT. ✅ [Patriot Bank, N.A. IO Charge Card Agreement](https://mercury.com/legal/io-charge-card-agreement)
- **Network:** **Mastercard**. ✅
- **Launched:** September 2022 ([Mercury / IO launch, 12 Sep 2022](https://www.businesswire.com/news/home/20220912005228/en/Mercury-Introduces-IO-A-New-Corporate-Credit-Card-To-Help-Startups-Scale-Their-Business); ✅).
- **Product mechanics:** Charge card (not revolving credit). 30-day repayment cycle. **0% APR** because it's net-30. **No annual fee**. **No personal guarantee, no credit check** at the entity. **1.5% cashback** on all spend including international.
- **Underwriting:** Limit is computed off Mercury balances + (optional) linked external bank balances. There is no consumer-bureau pull. Patriot Bank receives Mercury-provided Company Information and can deny / close accounts at its discretion.

### 2.3 Issuer processor — Lithic (✅, primary source)

Mercury's issuer processor is **Lithic** ([Lithic / Mercury case study](https://www.lithic.com/mercury-case-study); [Lithic / blog, Mercury scale](https://www.lithic.com/blog/how-mercury-scaled-cards-with-lithic); ✅). Lithic powers **both** debit and credit (IO) on Mercury, runs 3DS, and provides the per-card programmability used by Mercury's spend-controls UX. Mercury is one of Lithic's anchor customers — Lithic publicly cited Mercury "processing hundreds of millions monthly, $95B+ in 2023 card transactions, 100K+ businesses" in its case-study materials. This contradicts a common assumption that Mercury uses Marqeta — **it does not**.

Lithic was the former issuer-processing arm of Privacy.com that spun out to serve fintech enterprises; it speaks directly to Visa, Mastercard, and Amex over bare-metal connections and advertises 99.99% uptime.

---

## 3. Payment rails

### 3.1 ACH

- **NACHA standard ACH** for credit and debit transactions. ✅
- **Same-day ACH** is supported on the originating side. ([Mercury / blog, ACH vs wire](https://mercury.com/blog/differences-ach-versus-wire-transfer); ✅).
- Typical post timing 9-11am PT, Mon–Fri. Transactions arrive 0–2 business days.
- **Free** outbound ACH on all plans (incl. free Standard plan). ✅
- ACH debit on invoicing costs $1/transaction (Plus/Pro plans only) ([Mercury / pricing page](https://mercury.com/pricing); ✅).

### 3.2 Wire (Fedwire / SWIFT)

- **Domestic wires (Fedwire):** Free on all plans. ✅ Daily cutoff **1:30pm PT**; if submitted before cutoff, recipient typically receives same-day evening.
- **International USD wires (SWIFT):** Free. Optional flat **$15** "OUR" fee to make Mercury bear intermediary correspondent-bank charges. ([Mercury / international wires support article](https://support.mercury.com/hc/en-us/articles/28773111244436-Covering-recipient-fees-for-USD-international-wires); ✅).
- **Non-USD international wires:** **1% FX conversion fee**; negotiable >$200k/month. ([Mercury / non-USD support](https://support.mercury.com/hc/en-us/articles/28772836414228-Sending-non-USD-international-wires); ✅).
- Reported performance: **99.6% of domestic payments in 2025 arrived ≤1 business day** ([Mercury / Business Payments page, 2026](https://mercury.com/business-payments); ✅).

> **Known unknown #2: the FX vendor.** Mercury supports outbound non-USD international wires (sending in EUR, GBP, etc.) and now inbound non-USD as well after the Evolve transition. The actual underlying FX rail (Convera, CurrencyCloud/Visa, Western Union Business Solutions, Wise Platform, etc.) is **not disclosed** on any mercury.com surface or any third-party source surfaced in this research. Internally most likely a single FX provider behind Column or Choice — but **unverified**. 🔴

### 3.3 Check infrastructure

- **Inbound check deposit (mobile RDC):** Direct in-app capture with a check-image upload. No third-party RDC vendor name (e.g., Ingo Money, Mitek, Deluxe) is publicly disclosed. Most likely the RDC is operated under one of the partner banks' core RDC stacks (Choice / Column). **Vendor unverified.** 🔴
- **Outbound paper checks:** Mailed via Bill Pay or direct check send. Vendor for check-printing/mail-house is **unverified** — likely Lob, Deluxe, or Checkbook.io class infrastructure; no public source confirms.

### 3.4 Bill Pay

- **In-house** product. Customers can pay vendors via ACH, wire, or paper check directly from Mercury without going through Bill.com / Routable / Melio. ✅ [Mercury / Bill Pay overview](https://support.mercury.com/hc/en-us/articles/28768945847316-Bill-Pay-overview).
- "No middleman" framing is intentional product differentiation against Bill.com (which holds funds in its own clearing accounts).
- Vendors don't need a Mercury account to receive.
- Bill Pay is free for unlimited bills.

---

## 4. Mercury Treasury

Treasury is Mercury's brokered money-market product for idle cash, separated from FDIC-insured deposits.

- **Custody / brokerage:** **Apex Clearing Corp.**, FINRA-regulated broker-dealer, **SIPC**-insured (not FDIC; SIPC covers $500k including $250k cash). Accounts are held *in the customer's name* at Apex. ✅ [Mercury / Apex disclosure on Treasury page](https://mercury.com/treasury); [Mercury / Treasury blog](https://mercury.com/blog/mercury-treasury-funds).
- **Funds available:**
  - **JPMorgan U.S. Treasury Plus Money Market Fund** (ticker varies by share class; JTCXX cited) — lower-risk, US Treasury bills + notes + UST-backed obligations. Same-day liquidity if request before 3pm ET.
  - **Morgan Stanley Ultra-Short Income Portfolio** — **MULSX**. Higher yield via commercial paper, CDs, repos. Settlement 1–2 (up to 4) business days.
- **Yield representation:** Mercury publishes the 7-day SEC yield for JTCXX (the MMF) and 30-day SEC yield for MULSX (the ultra-short bond portfolio) updated weekly. Net yield representation as of 8 May 2026 — target up to **~4.35% net APY** per Mercury's own marketing, though actual customer net yield varies by share class and current rates ([Mercury / net yield support article, May 2026](https://support.mercury.com/hc/en-us/articles/44370115553044-How-net-yield-is-calculated-in-Mercury-Treasury); ✅). The Fed Funds target as of May 2026 has been gradually cut; current MMF yields likely sit in the 3.8–4.4% band.
- **November 2025 share-class upgrade:** Mercury upgraded the institutional share class on both funds, gaining ~5bps from reduced expense ratios. The minimum that would normally apply ($50M institutional minimum) is **waived** for Mercury Treasury customers — the Treasury program aggregates flows into one omnibus account at Apex ([Mercury / Treasury share class upgrade Nov 2025](https://support.mercury.com/hc/en-us/articles/41821273524116-Treasury-share-class-upgrade-November-2025); ✅).
- **Eligibility:** **$250,000 minimum balance** across Mercury accounts, **US-addressed beneficial owners** only. Not available to customers with beneficial owners in restricted jurisdictions ([Mercury / Qualifying for Treasury](https://support.mercury.com/hc/en-us/articles/41673479637908-Qualifying-for-a-Treasury-account); ✅).
- **Custody pathway:** Mercury → Apex Clearing Corp → omnibus position in JTCXX or MULSX. Customer name is on the Apex sub-account. SIPC insurance attaches at Apex level. FDIC does **not** apply to Treasury balances — this is brokerage, not bank custody. The distinction matters legally and to CFOs.

---

## 5. Mercury Working Capital + Venture Debt

### 5.1 Mercury Working Capital (e-commerce term loans)

- **Originator of record:** **Mercury Lending, LLC** — NMLS **2606284**. Serviced by **Mercury Servicing, LLC** — NMLS **2606285**. ✅ [Mercury / Working Capital FAQs](https://support.mercury.com/hc/en-us/articles/31280145967380-Mercury-Working-Capital-FAQs); [Mercury / Working Capital landing](https://mercury.com/working-capital-loans).
- **Critically: this is NOT originated by Cross River, Celtic, WebBank, or other classic fintech lending banks.** Mercury is a direct lender via Mercury Lending LLC. (Cross River is widely speculated — the speculation is **wrong** based on Mercury's NMLS disclosures.)
- **Structure:** Term loan, unsecured, non-dilutive. **4–6 month** terms, **weekly repayments**, **flat origination fee** (no compounding APR). The fee is a % of advance amount calculated upfront.
- **Underwriting input:** Real e-commerce sales across Shopify, Amazon (Seller Central), WooCommerce, etc. Plaid cash-flow inputs likely (Mercury's broader stack uses Plaid), but the canonical underwriting source is e-commerce platform data.
- **Eligibility:** US-incorporated e-commerce brand, **$250k+** annual sales, **6+ months** trading history.
- **Funds delivery:** Loan proceeds deposited into a Mercury account (customers must hold a Mercury account to receive).
- **Launched:** September 2024 ([Mercury / LinkedIn launch post](https://www.linkedin.com/posts/mercuryhq_icymi-we-launched-mercury-working-capital-activity-7239343134562828288-G7E3); ✅).

> **Known unknown #3: warehouse line behind Mercury Lending LLC.** Mercury Lending originates *on its own balance sheet* but presumably has a warehouse line from a money-center bank or asset-backed facility. Not publicly disclosed. 🔴

### 5.2 Mercury Venture Debt

- **Originator:** Loans were historically extended via **Evolve Bank & Trust** ([Mercury / Venture Debt page](https://mercury.com/venture-debt); ✅). With Evolve being phased out in 2025, Mercury's Venture Debt facility's current originator-of-record is **unverified** — likely transitioned to one of Choice / Column or to Mercury Lending LLC. 🟡
- **Launched:** March 2022.
- **Terms:** Up to **48 months** total loan duration with an interest-only period up to **18 months**. Customers can draw funds during the IO period.
- **Pricing:** **8–12% interest**, with warrants typically **0.5–5% of company equity**. ([Mercury / blog, venture debt 101](https://mercury.com/blog/venture-debt-101); [LTSE / Mercury head of credit guide](https://ltse.com/insights/a-startup-founders-guide-to-venture-debt-282ec); ✅).
- **Eligibility:** Already raised **$2M+** from institutional investors.
- **Head of Credit:** Chase Little (per third-party coverage).

---

## 6. Authentication & security

### 6.1 2FA

Mercury supports **four** second-factor methods ([Mercury / Setting up 2FA](https://support.mercury.com/hc/en-us/articles/28776867856404-Setting-up-2FA); [Mercury / blog, MFA approach](https://mercury.com/blog/multi-factor-authentication); ✅):

1. **TOTP** (6-digit codes from authenticator apps; 30-second rotation).
2. **WebAuthn** (FIDO2-compatible; YubiKey, Windows Hello, Touch ID).
3. **Passkeys** (passwordless; Face ID / Touch ID / device PIN; can bypass both password and TOTP).
4. **Security keys** (physical, e.g. YubiKey).

SMS-based 2FA is **not** the recommended primary factor (Mercury de-emphasized SMS after the SIM-swap risk patterns became well-known in fintech). It may be available as a backup but is not the default offered.

### 6.2 SSO (SAML / OIDC)

This is the **biggest gap** in Mercury's enterprise security posture. There is **no publicly documented SAML 2.0 or OIDC SSO** at any plan tier as of May 2026. The third-party SAAS Pass listing claims to "support Mercury SSO" but that is a password-manager-style overlay (single-sign experience), not native SAML federation. ([Mercury Help — searches return no SAML/SSO article](https://support.mercury.com); 🔴 — actively unverified, leaning negative).

> **Known unknown #4: SSO at Pro plan.** Mercury Pro ($350/mo) is positioned as the enterprise tier with "dedicated support, more integrations, greater bill pay capabilities" but the support article for SSO/SAML is absent from search indexing. Either (a) it doesn't exist, (b) it's gated behind enterprise contracts not documented publicly, or (c) it's coming with the Mercury Bank charter. The absence is conspicuous compared to Brex (SAML on Premium) and Ramp (SAML across plans).

### 6.3 Approval workflows

Mercury has best-in-class approval flow controls (probably the strongest of the neobank cohort):

- **Per-payment approvals** with **multi-rule stacking** by dollar threshold ([Mercury / Navigating approvals](https://support.mercury.com/hc/en-us/articles/28776049990548-Navigating-approvals); ✅).
- **Dual-admin policy** — requires two admins on file before enabling; covers payments and external transfers above a custom daily max, plus admin-permission changes ([Mercury / Enabling dual admin approvals](https://support.mercury.com/hc/en-us/articles/28768929696788-Enabling-dual-admin-approvals); ✅).
- **Custom roles** — reusable permission sets, edited centrally, propagated to all assignees.
- **Plan limits:**
  - Standard plan: small team (default 3 users referenced in some reviews).
  - Plus plan: 20 users.
  - Pro plan: 250 users.

### 6.4 Compliance attestations

- **SOC 2 Type II** — completed, attestation available on request ([Mercury / SOC 2 compliance](https://support.mercury.com/hc/en-us/articles/28768937741076-SOC-2-compliance); ✅).
- PCI-DSS — required because of card issuance; managed in conjunction with Lithic.
- BSA/AML — operated under partner-bank programs; Mercury maintains a designated BSA officer per FinCEN/OCC bank-partner expectations.
- No public **ISO 27001** certification is documented.
- No **HIPAA BAA** offered (not in scope for banking customers).

---

## 7. KYB / KYC stack

This is the second-biggest "unverified" hole:

- **No public disclosure** of which KYB/KYC orchestrator Mercury uses. None of [Persona](https://withpersona.com), [Alloy](https://alloy.com), [Middesk](https://middesk.com), [Plaid IDV](https://plaid.com/products/identity-verification/), [Socure](https://socure.com), or [Footprint](https://onefootprint.com) is named on mercury.com legal pages, status pages, or vendor lists.
- The most probable stack given Mercury's age, scale, and tech sophistication: **Middesk** for business entity verification (SoS / IRS records, OFAC), **Persona or Alloy** as identity decisioning orchestrator, and **Plaid IDV / Identity** for individual KYC on consumer (Mercury Personal) flows. But this is **inference, not verified**. 🔴
- **Stripe Atlas integration** — Mercury and Stripe Atlas partner so Atlas-incorporated founders can flow their pre-filled corporate documents (incorporation, EIN, beneficial owners) directly into a Mercury application, eliminating manual re-entry. This is particularly valuable for international (non-US) founders who form a US Delaware C-Corp via Atlas. ✅ [Mercury / Stripe Atlas partnership](https://mercury.com/blog/mercury-stripe-atlas-partnership). However, Atlas does **not** issue the EIN itself; the IRS does, and EIN wait times remain a real bottleneck.
- **Time to approval:** Marketed as "minutes" for the simplest US C-Corp founder cases; in practice ranges from **same-day to 2 weeks** depending on entity structure complexity and beneficial-owner geography.

### Geographic restrictions

Mercury has progressively tightened country eligibility for non-US-resident founders. In **March 2022**, Mercury froze ~30 accounts of YC/Techstars-backed African startups, blaming "a backend bank" (Evolve) ([TechCrunch, Mar 2022](https://techcrunch.com/2022/03/01/mercury-restricted-a-number-of-accounts-linked-to-african-startups-and-didnt-exactly-say-why/); ✅). In **July 2024**, Mercury announced it would stop serving startups in Ukraine, Nigeria, Croatia, and several other countries ([TechCrunch, 23 Jul 2024](https://techcrunch.com/2024/07/23/mercury-bank-fintech-sanctions-ukraine-nigeria/); ✅) — citing US sanctions compliance and bank-partner BSA constraints.

---

## 8. Public API

Mercury's public API is genuinely usable — read-write, OAuth2 for third-party integrations, webhooks. Base URL: `https://api.mercury.com/api/v1`. ✅ [docs.mercury.com](https://docs.mercury.com/).

### 8.1 Auth model

Two distinct paths:

- **Direct-customer tokens (Basic Auth).** Customer-generated API keys, used as Basic Auth **username** with an empty password ([Mercury / Getting Started](https://docs.mercury.com/docs/getting-started); ✅). Three token classes:
  - **Read-only** — list/get account, transactions, recipients, statements, cards.
  - **Read-and-Write** — initiate transactions and manage recipients. **Requires IP allowlist** as a hardening step.
  - **Custom** — explicit scope selection.
- **OAuth2 for partner integrations.** ([Mercury / OAuth2 integrations](https://docs.mercury.com/docs/integrations-with-oauth2); ✅). Used by partners like accounting tools and AI assistants. Prior approval is required; pre-vetted partners (e.g., QuickBooks, Xero, NetSuite, Mercury's own MCP) use this path. Scopes are per-resource. The `offline_access` scope is required to maintain a refresh-token flow without re-prompting the user.

### 8.2 Endpoint inventory (confirmed from changelog + reference docs)

| Resource | Method/Path | Notes |
|---|---|---|
| Accounts | `GET /accounts` | Paginated, cursor (limit/order/start_after/end_before) |
| Account | `GET /account/{id}` | Single account |
| Transactions (cross-org) | `GET /transactions` | Top-level filterable list across all accounts |
| Transactions (per account) | `GET /account/{id}/transactions` | With date / status / search filters |
| Transaction (create — send money) | `POST /account/{id}/transactions` | Outbound payment; may require approval |
| Recipients | `GET /recipients`, `POST /recipients`, `DELETE /recipient/{id}` | |
| Cards | `GET /account/{id}/cards` | |
| Statements | `GET /account/{id}/statements` | Monthly, paginated |
| Treasury transactions | `GET /treasury/{id}/transactions` | Treasury accounts use account-id from `/accounts` |
| Attachments | (upload to transactions + recipients) | Returns download URL |
| Webhooks | `POST /webhooks` (createwebhook) | Create endpoint |
| Org info | `GET /organization` | EIN, legal name, DBAs |
| Invoicing & Customers | `/invoices`, `/customers` | **Plus plan or higher**; 403 on Free/Standard |
| Expense categories | `GET /categories` | |

Sources: [Mercury / Reference index](https://docs.mercury.com/reference/getting-started-with-your-api); [Mercury / Accounts ref](https://docs.mercury.com/reference/accounts); [Mercury / List transactions](https://docs.mercury.com/reference/listtransactions); [Mercury / Create transaction](https://docs.mercury.com/reference/createtransaction); [Mercury / Treasury txns changelog](https://docs.mercury.com/changelog/get-transactions-for-a-mercury-treasury-account).

### 8.3 Rate limits

**100 requests/minute** baseline ([apitracker.io / Mercury](https://apitracker.io/a/mercury-co); 🟡 — confirmable on api page only). Mercury's docs note "obey limits, contact us for higher" without publishing tier-specific caps.

### 8.4 Webhooks — signing

- POST callbacks with payloads in JSON.
- Signature header: **`x-mercury-signature`**.
- Algorithm: **HMAC-SHA256** of the raw request body, keyed by the per-endpoint webhook secret.
- Verification recommendation: use timing-safe comparison (`crypto.timingSafeEqual` in Node, `hmac.compare_digest` in Python).
- Source: [Mercury / Webhooks ref](https://docs.mercury.com/reference/webhooks); ✅.

### 8.5 SDKs

- **No first-party Mercury SDK** is published on npm or PyPI under the Mercury organization as of May 2026. (Mercury maintains REST docs but doesn't ship official SDKs — Stripe-style.)
- **Community SDKs / CLIs:**
  - `mercury-cli` by [ex3ndr](https://github.com/ex3ndr/mercury-cli) — Node-based CLI wrapper.
  - `mcp-mercury-banking` by [jbdamask](https://github.com/jbdamask/mcp-mercury-banking) — Python MCP server (read-only).
  - `mercury-invoicing-mcp` by [klodr](https://github.com/klodr/mercury-invoicing-mcp) — MCP focused on invoicing API (gated to Plus+).
- Third-party automation: [Pipedream](https://pipedream.com/apps/mercury), [Make](https://apps.make.com/mercury-ylw6p3), Zapier integrations are all wrappers on top of the REST API.

---

## 9. Integrations

### 9.1 Accounting

- **Direct integrations:** **QuickBooks Online**, **Xero**, **NetSuite** ([Mercury / Accounting Automations](https://mercury.com/accounting-automations); [Mercury / QBO integration](https://support.mercury.com/hc/en-us/articles/28775977522068-Integrating-with-QuickBooks-Online); [Mercury / Xero integration](https://support.mercury.com/hc/en-us/articles/28777055778580-Integrating-with-Xero); ✅).
- NetSuite is the marquee "enterprise" integration added later. Sage Intacct is not directly supported (CSV / generic OFX only).
- For non-supported accounting platforms, CSV export is available.
- Transaction-level integration includes auto-sync of GL codes and rule-based categorization.

### 9.2 Payroll

- **No direct integration** with Gusto, Rippling, or Deel that exposes payroll-specific syncing. Mercury supports payroll *as a payee* — you wire / ACH out to the payroll provider. ([Mercury / Setting up payroll with ACH debits](https://support.mercury.com/hc/en-us/articles/30884083345812-Setting-up-payroll-with-ACH-debits); ✅).
- Mercury launched its own internal payroll feature variants in 2023.

### 9.3 E-commerce / payment processors

- Mercury connects with **Stripe**, **Shopify**, **Amazon Seller Central** **as a payout destination** — you provide Mercury account/routing numbers to the platform. There is no native OAuth integration into these platforms ([Mercury / Integration FAQs](https://support.mercury.com/hc/en-us/articles/28777021143828-Integration-FAQs); ✅).
- For Working Capital underwriting, Mercury ingests sales data from Shopify, Amazon, and WooCommerce — likely via direct OAuth pulls on the Mercury side (not customer-side connectors).

### 9.4 Plaid

- Mercury **is exposed as an institution endpoint on Plaid** ([Plaid / Mercury institution page](https://plaid.com/institutions/mercury/); ✅). Supported Plaid products: **Auth, Balance, Assets**. *Transactions* product status is not explicitly documented on the Plaid institution page (assume present but not separately verified).
- **Inbound:** Mercury uses Plaid for external-account linking (to pull funds from another bank into Mercury). ([Mercury / Linking external bank accounts](https://support.mercury.com/hc/en-us/articles/28777004830228-Linking-external-bank-accounts); ✅).
- **Outbound:** customers can connect their Mercury account *to* third-party apps via Plaid (e.g., to a budgeting app or DEX onramp).

### 9.5 "Mercury Connect" marketplace

- There is **no published "Mercury Connect" app marketplace** at present. ("Mercur" — different brand entirely — is an open-source marketplace platform, unrelated.) Mercury exposes integrations through its main app and the API, but lacks a Brex-style integrations marketplace. 🔴 (verified absence).

---

## 10. AI / agent surface

This is where Mercury has, somewhat surprisingly, moved fastest.

### 10.1 Mercury MCP (the official, hosted server)

- **Product:** [What is Mercury MCP](https://docs.mercury.com/docs/what-is-mercury-mcp) — Mercury's official, hosted Model Context Protocol server. ✅
- **Architecture:** Hosted server between AI client and Mercury's public API. Connects via **OAuth2**. Designed for ChatGPT, Claude, Google AI Studio, Cursor, etc.
- **Safety posture at launch:** Limited to **read-only actions** to reduce risk surface. The Mercury MCP page describes write tools (payments, categorizations, invoice creation, receipt upload) on the roadmap.
- **Tool inventory (read tools confirmed):** [Supported tools on Mercury MCP](https://docs.mercury.com/docs/supported-tools-on-mercury-mcp); ✅
  - List accounts and attachment details (with download URLs)
  - List debit & credit cards per account
  - List monthly statements per account
  - List customers and invoices (paginated)
  - List credit accounts for the organization
  - Get organization info (EIN, legal name, DBAs)
  - List custom expense categories (cursor pagination)
- **Bucketed write controls (architecture for upcoming writes):** [Speakeasy / Mercury MCP catalog](https://www.speakeasy.com/product/mcp-gateway/catalog/mercury) describes a dual-window cap design — every write tool has both a daily (24h rolling) and monthly (30-day rolling) limit. Either window hitting cap rejects the call. This is explicitly to prevent a runaway agent from draining accounts by pacing under the daily limit.
- **Strategic significance:** Mercury is, alongside Ramp, one of the **first two business banks** to publish a first-party MCP server. Brex's MCP is still partial/community. This positions Mercury for an Anthropic / OpenAI co-marketing slot.

### 10.2 Community MCPs

- **[mcp-mercury-banking](https://github.com/jbdamask/mcp-mercury-banking)** (Python) — read-only via direct Mercury API.
- **[mercury-invoicing-mcp](https://github.com/klodr/mercury-invoicing-mcp)** (Node) — banking + invoicing + recurring invoice creation; invoicing endpoints require Plus plan (returns 403 on Free/Standard).
- **[dragonkhoi/mercury-mcp](https://hexmos.com/freedevtools/mcp/business-tools/dragonkhoi--mercury-mcp/)** — older community implementation.

### 10.3 Visa Intelligent Commerce / Mastercard Agent Pay

- Mercury is **not publicly named** as a launch participant in Visa Intelligent Commerce or Mastercard Agent Pay programs as of May 2026. ✅ (verified absence — none of the launch coverage of [Visa / VIC](https://corporate.visa.com/en/sites/visa-perspectives/innovation/visa-mcp-server-agent-acceptance-toolkit.html), [Mastercard Agent Pay](https://www.digitalcommerce360.com/2025/10/16/visa-mastercard-both-launch-agentic-ai-payments-tools/), or the [Visa MCP toolkit GitHub repo](https://github.com/visa/mcp) lists Mercury). Since Mercury issues exclusively on **Mastercard**, the natural future participation channel is Mastercard Agent Pay.
- This is meaningfully different from Ramp, which is a marquee VIC partner with named "Agent Cards" (Ramp's MCP cards are co-branded with Visa).

### 10.4 x402

- **No Mercury x402 integration** as of May 2026. ✅ (verified absence). Mercury is fiat-only and outside the stablecoin-rail layer that x402 currently sits on. The [x402.org launch coverage](https://www.x402.org/) names AWS Bedrock AgentCore, Cryptorefills, and Coinbase Commerce — not Mercury.

### 10.5 Stablecoins / crypto

- Mercury accounts hold **only fiat (USD)**. ✅ No native USDC, PYUSD, or other stablecoin custody.
- **Crypto policy posture (2025–2026):** Mercury's [/web3 page](https://mercury.com/web3) markets to crypto/web3 startups, DAOs, and funds, but **does not support Money Services Businesses (MSBs) or crypto exchanges** as customers. This is a real underwriting line. Many crypto-native founders have reported declines (TechCabal, Offshorecorptalk threads).
- **Stance evolution since 2022:** In 2022 Mercury restricted ~30 African startup accounts amid Evolve compliance pressure. In 2024 it pulled out of several countries entirely. The 2025–2026 stance is "web3 friendly but not exchange-friendly" — softer than 2022 but still narrower than Bridge or Brex.
- **No on-chain rails.** No USDC inbound/outbound, no Bridge integration, no Stripe Bridge integration disclosed, no Circle Mint custody, no Layer 1 settlement.

> **Known unknown #5: Mercury's stance on the Stripe Bridge stack.** With Stripe Atlas as Mercury's onboarding partner and Bridge now part of Stripe, there is a natural product question — will Mercury add stablecoin on/off-ramping via Bridge? No public statement either way. 🔴

---

## 11. Cross-cut: Mercury Personal (consumer banking)

Important context: Mercury launched **Mercury Personal** in April 2024 ([BusinessWire, 17 Apr 2024](https://www.businesswire.com/news/home/20240417396140/en/Mercury-Launches-Personal-Banking); ✅) and re-launched it as a **premium $240/year subscription product** in December 2025 ([BusinessWire, 11 Dec 2025](https://www.businesswire.com/news/home/20251211260682/en/Mercury-Launches-Premium-Consumer-Banking-for-Builders-and-Founders); ✅).

- Debit card issued by **Choice Financial Group** on **Mastercard**.
- **5.00% APY** on high-yield savings (likely passed-through MMF or partner sweep — exact mechanic unverified).
- Up to **$5M FDIC** through partner-bank sweep network (same Vault mechanics).
- US residents 18+ only.
- Aimed at builders / founders (intentional spillover from business).

This product is meaningful for the AI/agent surface because consumer-side Mercury accounts can plausibly become the rail behind a future "Agent Card" / agent-pay flow tied to individual operators rather than companies.

---

## 12. Mercury vs the competitor cohort — vendor stack delta

| Layer | Mercury | Brex | Ramp |
|---|---|---|---|
| Core bank(s) | Choice / Column / Patriot (Evolve gone) | Column / various | Evolve / Cross River / various |
| Card issuer (debit/charge) | Patriot (IO) + Choice/Column (debit), Mastercard | Multiple, Mastercard | Sutton Bank, Visa |
| Issuer processor | **Lithic** | Marqeta (legacy) + in-house | Marqeta + Stripe Issuing |
| Treasury custody | Apex Clearing | Treasury via Brex Asset Mgmt | Ramp Treasury via Apex / similar |
| MMF | JPMorgan + Morgan Stanley | DFA / state-street | Goldman / similar |
| Loans (commercial) | Mercury Lending LLC (direct) | Brex direct | Various |
| MCP server | **Yes (official, hosted)** | Partial / community | **Yes (official)** |
| VIC / Agent Pay | Not yet | Reported partner | **VIC named partner with Agent Cards** |
| SAML SSO | Not publicly documented | Premium tier | All paid plans |
| Stablecoin support | No | Limited | Limited |
| Own bank charter | **Conditional (Apr 2026)** | No | No |

Mercury's **direct lending stack** (Mercury Lending LLC) and **own-charter trajectory** are the structural differentiators. Mercury's **lack of SAML SSO** and **non-participation in VIC / Agent Pay launch programs** are the structural gaps.

---

## Sources used

### Section 1 — banks / sweep / OCC charter
- [Mercury / How Mercury works with partners blog](https://mercury.com/blog/how-mercury-works-with-partner-banks)
- [Banking Dive / Mercury to pivot from Evolve, Mar 2025](https://www.bankingdive.com/news/mercury-pivot-partner-bank-evolve/742704/)
- [Bloomberg / Mercury severs ties with Evolve, 12 Mar 2025](https://www.bloomberg.com/news/articles/2025-03-12/fintech-neobank-mercury-severs-its-relationship-with-evolve-bank)
- [American Banker / Mercury & Evolve split](https://www.americanbanker.com/news/small-business-fintech-mercury-bank-partner-evolve-split)
- [Mercury press / OCC charter app, 19 Dec 2025](https://www.businesswire.com/news/home/20251219760269/en/Mercury-Applies-for-OCC-National-Bank-Charter-to-Become-the-Bank-for-Builders)
- [Mercury press / OCC conditional approval, 27 Apr 2026](https://www.businesswire.com/news/home/20260427949683/en/Mercury-Receives-OCC-Conditional-Approval-to-Establish-Mercury-Bank-N.A.)
- [FDIC BankFind / Choice Financial Group #9423](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/9423)
- [FDIC BankFind / Column National Association #58224](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/58224)
- [FDIC BankFind / Patriot Bank, N.A. #33928](https://banks.data.fdic.gov/bankfind-suite/bankfind/details/33928)
- [TechCrunch / Plaid co-founder buys NorCal, Apr 2022](https://techcrunch.com/2022/04/21/plaid-cofounders-next-venture-is-a-bank-to-power-fintech-apps/)
- [American Banker / De novo Column](https://www.americanbanker.com/news/de-novo-column-bank-gives-partners-a-sandbox-to-build-banking-tools)
- [Mercury blog / Vault launch](https://mercury.com/blog/mercury-vault-announcement)
- [Mercury blog / understanding sweep network](https://mercury.com/blog/understanding-bank-sweep-network)
- [Mercury legal / Choice sweep custodial agreement](https://mercury.com/legal/choice/sweep-program-deposit-placement-and-custodial-agreement)
- [Mercury legal / Column sweep custodial agreement](https://mercury.com/legal/column/sweep-program-deposit-placement-and-custodial-agreements)
- [Mercury deposit disclosure (Choice) PDF 05_01_24](https://co-mercury-prod.s3.amazonaws.com/legal/Choice+-+Mercury+Deposit+Program+Disclosure+Statement+-+05_01_24.pdf)

### Section 2 — cards
- [Mercury legal / Choice Commercial Debit Card Agreement](https://mercury.com/legal/choice/commercial-debit-card-agreement)
- [Mercury legal / Choice Consumer Debit Card Agreement](https://mercury.com/legal/choice-personal/consumer-debit-card-agreement)
- [Mercury legal / Patriot Bank IO Charge Card Agreement](https://mercury.com/legal/io-charge-card-agreement)
- [Mercury / IO launch BusinessWire, 12 Sep 2022](https://www.businesswire.com/news/home/20220912005228/en/Mercury-Introduces-IO-A-New-Corporate-Credit-Card-To-Help-Startups-Scale-Their-Business)
- [Lithic / Mercury case study](https://www.lithic.com/mercury-case-study)
- [Lithic blog / how Mercury scaled with Lithic](https://www.lithic.com/blog/how-mercury-scaled-cards-with-lithic)

### Section 3 — rails
- [Mercury / Business Payments page](https://mercury.com/business-payments)
- [Mercury blog / ACH vs wires](https://mercury.com/blog/differences-ach-versus-wire-transfer)
- [Mercury support / Processing times for payments](https://support.mercury.com/hc/en-us/articles/28773186865684-Processing-times-for-payments)
- [Mercury support / Covering recipient fees](https://support.mercury.com/hc/en-us/articles/28773111244436-Covering-recipient-fees-for-USD-international-wires)
- [Mercury support / Non-USD international wires](https://support.mercury.com/hc/en-us/articles/28772836414228-Sending-non-USD-international-wires)
- [Mercury / Bill Pay overview](https://support.mercury.com/hc/en-us/articles/28768945847316-Bill-Pay-overview)

### Section 4 — Treasury
- [Mercury / Treasury landing](https://mercury.com/treasury)
- [Mercury / Treasury funds blog](https://mercury.com/blog/mercury-treasury-funds)
- [Mercury support / How net yield is calculated](https://support.mercury.com/hc/en-us/articles/44370115553044-How-net-yield-is-calculated-in-Mercury-Treasury)
- [Mercury support / Treasury share class upgrade Nov 2025](https://support.mercury.com/hc/en-us/articles/41821273524116-Treasury-share-class-upgrade-November-2025)
- [Mercury support / Qualifying for Treasury](https://support.mercury.com/hc/en-us/articles/41673479637908-Qualifying-for-a-Treasury-account)

### Section 5 — lending
- [Mercury / Working Capital landing](https://mercury.com/working-capital-loans)
- [Mercury support / Working Capital FAQs (NMLS)](https://support.mercury.com/hc/en-us/articles/31280145967380-Mercury-Working-Capital-FAQs)
- [Mercury / Venture Debt landing](https://mercury.com/venture-debt)
- [Mercury blog / Venture Debt 101](https://mercury.com/blog/venture-debt-101)
- [LTSE / founder's guide to venture debt with Mercury Head of Credit](https://ltse.com/insights/a-startup-founders-guide-to-venture-debt-282ec)

### Section 6 — security
- [Mercury support / Setting up 2FA](https://support.mercury.com/hc/en-us/articles/28776867856404-Setting-up-2FA)
- [Mercury support / Understanding 2FA](https://support.mercury.com/hc/en-us/articles/28776257818772-Understanding-two-factor-authentication-2FA-at-Mercury)
- [Mercury blog / Multi-factor authentication](https://mercury.com/blog/multi-factor-authentication)
- [Mercury support / SOC 2 compliance](https://support.mercury.com/hc/en-us/articles/28768937741076-SOC-2-compliance)
- [Mercury support / Navigating approvals](https://support.mercury.com/hc/en-us/articles/28776049990548-Navigating-approvals)
- [Mercury support / Enabling dual admin approvals](https://support.mercury.com/hc/en-us/articles/28768929696788-Enabling-dual-admin-approvals)
- [Mercury support / Managing roles and permissions](https://support.mercury.com/hc/en-us/articles/28768978787860-Managing-roles-and-permissions)
- [Mercury / Security landing](https://mercury.com/security)

### Section 7 — KYB / onboarding
- [Mercury blog / Stripe Atlas partnership](https://mercury.com/blog/mercury-stripe-atlas-partnership)
- [TechCrunch / Mercury restricted African startups, Mar 2022](https://techcrunch.com/2022/03/01/mercury-restricted-a-number-of-accounts-linked-to-african-startups-and-didnt-exactly-say-why/)
- [TechCrunch / Mercury halts service in some countries, Jul 2024](https://techcrunch.com/2024/07/23/mercury-bank-fintech-sanctions-ukraine-nigeria/)

### Section 8 — API
- [Mercury docs / Welcome](https://docs.mercury.com/docs/welcome)
- [Mercury docs / Getting Started](https://docs.mercury.com/docs/getting-started)
- [Mercury docs / Getting Started reference](https://docs.mercury.com/reference/getting-started-with-your-api)
- [Mercury docs / OAuth2 integrations](https://docs.mercury.com/docs/integrations-with-oauth2)
- [Mercury docs / API Token Security Policies](https://docs.mercury.com/reference/api-token-security-policies)
- [Mercury docs / Webhooks](https://docs.mercury.com/reference/webhooks)
- [Mercury docs / Create webhook](https://docs.mercury.com/reference/createwebhook)
- [Mercury docs / Webhooks now available changelog](https://docs.mercury.com/changelog/webhooks-now-avaliable)
- [Mercury docs / List transactions](https://docs.mercury.com/reference/listtransactions)
- [Mercury docs / Get accounts](https://docs.mercury.com/reference/getaccounts)
- [Mercury docs / Create transaction (send money)](https://docs.mercury.com/reference/createtransaction)
- [Mercury docs / Treasury transactions changelog](https://docs.mercury.com/changelog/get-transactions-for-a-mercury-treasury-account)
- [Mercury / API marketing](https://mercury.com/api)
- [apitracker.io / Mercury (rate limit hint)](https://apitracker.io/a/mercury-co)
- [GitHub / ex3ndr/mercury-cli](https://github.com/ex3ndr/mercury-cli)

### Section 9 — integrations
- [Mercury / Accounting Automations landing](https://mercury.com/accounting-automations)
- [Mercury support / QuickBooks Online](https://support.mercury.com/hc/en-us/articles/28775977522068-Integrating-with-QuickBooks-Online)
- [Mercury support / Xero](https://support.mercury.com/hc/en-us/articles/28777055778580-Integrating-with-Xero)
- [Mercury support / Integration FAQs (Stripe / Shopify / Amazon)](https://support.mercury.com/hc/en-us/articles/28777021143828-Integration-FAQs)
- [Mercury support / Linking external bank accounts](https://support.mercury.com/hc/en-us/articles/28777004830228-Linking-external-bank-accounts)
- [Plaid / Mercury institution page](https://plaid.com/institutions/mercury/)
- [Mercury support / Setting up payroll with ACH debits](https://support.mercury.com/hc/en-us/articles/30884083345812-Setting-up-payroll-with-ACH-debits)

### Section 10 — AI / agents
- [Mercury docs / What is Mercury MCP](https://docs.mercury.com/docs/what-is-mercury-mcp)
- [Mercury docs / Supported tools on Mercury MCP](https://docs.mercury.com/docs/supported-tools-on-mercury-mcp)
- [Mercury / API marketing page (MCP mention)](https://mercury.com/api)
- [PulseMCP / official Mercury MCP](https://www.pulsemcp.com/servers/mercury)
- [MintMCP / Mercury server](https://www.mintmcp.com/servers/mercury)
- [Speakeasy / Mercury MCP catalog (34 tools)](https://www.speakeasy.com/product/mcp-gateway/catalog/mercury)
- [Composio / Mercury MCP toolkit](https://docs.composio.dev/toolkits/mercury_mcp)
- [GitHub / klodr/mercury-invoicing-mcp](https://github.com/klodr/mercury-invoicing-mcp)
- [GitHub / jbdamask/mcp-mercury-banking](https://github.com/jbdamask/mcp-mercury-banking)
- [OpenBankingTracker / Agentic Banking & MCP](https://www.openbankingtracker.com/agentic-banking-and-mcp)
- [Visa Perspectives / Visa MCP server + Agent Acceptance Toolkit](https://corporate.visa.com/en/sites/visa-perspectives/innovation/visa-mcp-server-agent-acceptance-toolkit.html)
- [GitHub / visa/mcp](https://github.com/visa/mcp)
- [DigitalCommerce360 / Visa + Mastercard agentic AI tools, Oct 2025](https://www.digitalcommerce360.com/2025/10/16/visa-mastercard-both-launch-agentic-ai-payments-tools/)
- [Mercury / web3 page](https://mercury.com/web3)
- [x402.org](https://www.x402.org/)

### Section 11 — Mercury Personal
- [BusinessWire / Mercury launches Personal, Apr 2024](https://www.businesswire.com/news/home/20240417396140/en/Mercury-Launches-Personal-Banking)
- [BusinessWire / Premium Consumer Banking, Dec 2025](https://www.businesswire.com/news/home/20251211260682/en/Mercury-Launches-Premium-Consumer-Banking-for-Builders-and-Founders)

### General context
- [Mercury / Pricing](https://mercury.com/pricing)
- [Mercury support / Mercury pricing plans](https://support.mercury.com/hc/en-us/articles/28769703794580-Mercury-pricing-plans)
- [Fintech Brainfood / AI checkout + Mercury OCC approval](https://www.fintechbrainfood.com/p/ai-checkout)
- [Contrary Research / Mercury report](https://research.contrary.com/company/mercury)
- [Wikipedia / Mercury Technologies](https://en.wikipedia.org/wiki/Mercury_Technologies)
- [Wikipedia / William Hockey](https://en.wikipedia.org/wiki/William_Hockey)

---

## Known unknowns (facts I could not verify with confidence)

1. **Full 20-bank sweep network composition.** The Choice and Column Disclosure Statements are linked but the page-level bank list isn't search-indexed. Need direct PDF retrieval of `co-mercury-prod.s3.amazonaws.com/legal/Choice+-+Mercury+Deposit+Program+Disclosure+Statement+-+05_01_24.pdf` (and the matching Column file) to enumerate the participating banks. Names like Cross River, First Internet Bank, Customers Bank, Pacific Western, EagleBank circulate online but I could not confirm them as members.
2. **International-wire FX vendor.** No public source names Convera / CurrencyCloud / Wise Platform / Western Union Business Solutions as Mercury's FX engine. Likely lives behind Choice or Column, but unconfirmed.
3. **Outbound check vendor + mobile RDC vendor.** Mercury has remote-deposit and outbound paper check products but does not disclose Ingo Money / Mitek / Lob / Deluxe / Checkbook. Most likely operated under the partner banks' core RDC.
4. **KYB / KYC vendor.** Persona, Alloy, Middesk, Plaid IDV all plausible — none disclosed publicly anywhere I could find.
5. **SAML SSO status.** No public Mercury support article documents SAML/OIDC on any plan tier (Standard / Plus / Pro). May be (a) absent, (b) gated to enterprise contracts not on the website, or (c) coming with Mercury Bank N.A.
6. **Warehouse line behind Mercury Lending LLC.** Mercury originates Working Capital on its own balance sheet — but the upstream funding facility (most fintech direct lenders use a money-center warehouse line) is undisclosed.
7. **Current originator-of-record for Venture Debt** post the Evolve exit. Historically Evolve; current state unverified.
8. **Treasury current net APY snapshot.** Mercury claims "up to ~4.35%" but the live customer-side APY in May 2026 (after MMF rate-cut transmission) is published only inside the Mercury dashboard.
9. **Token / OAuth scope inventory.** The full list of named OAuth scopes for the partner API is implied (per-resource) but not enumerated in any indexed page I retrieved.
10. **Mercury participation in Mastercard Agent Pay launch wave.** Given Mercury is exclusively Mastercard-issuing, this is the natural next move — but no announcement as of May 2026.
11. **WebFetch was denied in this session**, so primary-source page text of mercury.com/security, mercury.com/legal, and docs.mercury.com endpoints had to be inferred from search snippets rather than direct retrieval. Items 1, 2, 3, 4, 5, 9 above would all be resolvable with WebFetch access.

---

*Document prepared May 2026. All confidence ratings reflect source quality at time of writing; please reverify before quoting in regulatory or investment contexts.*
