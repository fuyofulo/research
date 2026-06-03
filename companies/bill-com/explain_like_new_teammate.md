# Bill.com — Explain Like a New Teammate

*A dumb-questions explainer for someone who must understand BILL by tomorrow. No jargon left unexplained.*

## What does Bill.com do in one sentence?

Bill.com is a 20-year-old US software company that automates accounts payable (paying vendors) and accounts receivable (collecting from customers) for small and mid-sized businesses, with a free corporate-card spend-management product layered on top — and it routes ~$355B/year of payments through clearing accounts it controls, earning interest on the float and per-transaction fees while charging users $45-89/user/month for the software.

## What problem existed before this product?

Before Bill.com (founded 2006), a typical 50-person business paid its bills like this:
1. A vendor mailed or emailed a paper invoice.
2. An AP clerk manually typed it into QuickBooks.
3. A controller cut a paper check, stuffed an envelope, put a stamp on it, mailed it.
4. The vendor received it 5-10 days later.
5. Reconciliation back into QuickBooks happened by hand at month-end.

A single bill took ~15 minutes of human time. A 100-person company doing 200 bills/month spent ~50 hours/month just paying bills. ~90% of US business payments were paper checks. Errors were common (wrong amount, lost in mail, fraud).

## Who buys it?

Two distinct customer types:

1. **Small-to-mid businesses (SMBs)** with 10-500 employees, $1M-$100M revenue. The CFO, controller, or owner buys it directly. Examples: a regional law firm, a multi-location restaurant, a property-management company, a CPG brand. ~$45-89/user/month for AP+AR seats; the corporate card layer is free (BILL earns interchange).

2. **CPA / accountant firms** — *this is BILL's strategic center of gravity, not the end SMBs.* About 8,000 accounting firms use BILL's "Accountant Console" to run AP/AR for their underlying client base (a single firm may manage 50-200 SMB clients). 98 of the top 100 US accounting firms partner with BILL. CPA.com (the AICPA's tech arm) is BILL's institutional channel partner.

The accountants are stickier than the SMBs. SMBs can churn easily (per-seat pricing gets expensive, Ramp/Mercury offer free AP). Accountants, once trained on BILL and with 100 client books inside it, basically don't switch.

## Who uses it day-to-day?

- **AP clerk / staff accountant**: opens BILL each morning, reviews bills the AI has auto-coded, fixes exceptions, approves payments, exports reconciliation to QuickBooks.
- **Controller / CFO**: approves payments over a dollar threshold, monitors cash flow, watches for fraud flags, runs reports.
- **Vendor (on the receive side)**: a separate, lighter-weight portal where vendors get paid and can manage their bank details. Most vendors interact with BILL passively (receive an ACH and an emailed remittance).
- **CPA firm partner / accountant**: spends most of the day inside the Accountant Console managing dozens of client books in parallel.

## What exactly happens step-by-step inside the product?

Walk through one AP transaction:

1. Vendor emails the invoice PDF to `ap@yourcompany.bill.com` (or uploads to a portal).
2. BILL's AI Coding Agent extracts: vendor name, amount, due date, line items, tax. Header extraction accuracy ~99% (per BILL); line-item accuracy lower.
3. The system looks up the vendor in your historical books, suggests a GL account and class, pre-fills coding.
4. If the bill is "normal" (under your $5K threshold, known vendor, etc.), it's auto-coded and dropped into the approval queue.
5. The right approver gets an email — they click "approve" inside BILL.
6. On the chosen payment date, BILL pulls money from your bank account via ACH (1 lump sum debit covering all scheduled payments).
7. The money sits in a BILL clearing account (a "For Benefit Of" / FBO trust account at a partner bank — Bank of America, JPMorgan, others) for 1-3 days.
8. BILL releases payment to the vendor — by ACH (default), check, virtual Visa/Mastercard card, RTP, or international wire / Local Transfer for cross-border.
9. After payment lands, BILL pushes the journal entry into your QuickBooks / NetSuite / Xero / Sage Intacct / Microsoft Dynamics. Reconciliation auto-matches.

For AR (collecting from your customers), it's the inverse: you generate a BILL invoice, your customer pays online, the money lands in your bank, the GL syncs.

## What data, money, or state moves through the system?

- **Documents:** invoice PDFs, receipts, W-9 tax forms, contracts, bank-link verifications.
- **Money:** dollars flow from customer bank → BILL FBO clearing accounts → vendor (via ACH, RTP, wire, card, check).
- **Identity / routing data:** the 8M-member BILL Network is a vendor identity graph. When a vendor is already in the network, payments route faster (no new bank-link required).
- **Float interest:** while customer money sits in BILL's clearing accounts for 1-3 days, BILL invests it in money market funds and short-term debt securities, keeping ~$3.66B average balance — earning $161.8M in interest in FY25 (~11% of total revenue).
- **Accounting entries:** the AP transaction state is synced into QuickBooks / NetSuite / Xero / Sage Intacct.

## Why is this hard?

Many overlapping reasons:

- **Money movement infrastructure.** BILL is a registered Money Services Business with FinCEN, holds Money Transmitter Licenses in all 50 states, has bank partnerships, KYB/KYC vendors, fraud-detection systems. Building this from scratch is 18-24 months and millions in regulatory cost.
- **Vendor identity / routing.** Knowing that "ACME LLC", "ACME, L.L.C.", and "ACME Inc" are the same vendor across 8 million variations is genuinely hard. BILL has 20 years of this data.
- **Long-tail integrations.** Real-time bidirectional sync with QuickBooks, NetSuite, Xero, Sage Intacct, MS Dynamics — each is a multi-year integration project to keep stable.
- **Accountant-channel distribution.** CPA firms recommend tools they know. Building this network takes 10+ years.
- **Fraud and compliance ops.** BILL has a full-time human risk team handling exception cases, account freezes, BSA/OFAC checks, BEC defense. This is "in-house human ops," not pure software.

## Why now?

Three reasons BILL is in the news in 2026:

1. **Activist investors** (Starboard 8.5%, Elliott ~5%, Barington) are pushing the company toward a sale. Reuters reports Hellman & Friedman has been named as a potential PE bidder. The stock has dropped ~88% from its 2021 peak.
2. **30% workforce cut** announced May 7, 2026 (~700 of 2,333 jobs) alongside a $1B buyback — classic activist-driven margin-expansion playbook.
3. **AI agents (October 2025 + Feb 2026)** are BILL's defensive answer to Ramp's faster AI-agent fleet. BILL's pitch: "trained on 250M+ invoices, the data is the moat."

## What is actually impressive?

Cutting through the marketing:
- **The CPA.com / accountant-firm channel.** 98 of top 100 US accounting firms; 8,000+ firm partnerships; institutional AICPA backing. A 15-year-built distribution moat that competitors cannot replicate in 2-3 years.
- **NetSuite Intelligent Payment Automation.** Embedded as the default AP rail inside Oracle NetSuite (Oct 2025). Strong mid-market distribution.
- **20 years of money-transmitter operations.** All 50 US states. Real fraud-defense systems. Real anti-BEC track record. Trust-in-money-movement is hard to build.
- **GAAP profitability in FY25.** Most SMB fintechs aren't profitable. BILL is — for now.
- **The 8M-member vendor routing graph.** Not as an AI training corpus (overrated), but as an operational asset that makes 2-click payments possible for already-onboarded vendors.

## What is still unclear / risky?

- **NRR is 94%.** This means existing customer cohorts shrink ~6%/year before new adds. Below SaaS benchmark of 110-120%. Quietly the most damning number in the file.
- **Float income (11% of revenue) is rate-cycle-dependent.** As the Fed cuts, this line compresses.
- **AI moat claim is weak.** "Trained on 250M invoices" is a narrative; modern Claude/GPT + RAG can match extraction accuracy in 6 months.
- **Spend & Expense (Divvy, paid $2.5B in 2021) is being out-grown by Ramp.** Likely divestiture or write-down candidate.
- **Bank of America partner relationship has been "revamped"** and BoA itself is restructuring payments. Operational risk that BILL has managed before (SVB 2023) but it's real.
- **Customer support is consistently rated poor.** Layoffs make it worse.
- **The clearing-account "middleman" architecture** is being weaponized by Mercury, Ramp, and others. Direct-rails / instant-settlement is structurally better; BILL is locked into the FBO model because it earns the float.

## The mental model

Think of Bill.com as: **the Tipalti / Stampli / Quicken-Bill-Pay of the SMB world — a vertical SaaS for AP/AR — wedded to a regulated payments business that earns interest on customer money during transit, distributed primarily through a decade-old accountant-firm channel, now caught between AI-first neo-fintechs (Ramp, Mercury, Brex) at the SMB end and Intuit's embedded Bill Pay disintermediating from above, with three activists at the door pushing for a sale.**

Or more succinctly: **An SMB AP-automation business with a real accountant-channel moat, a real money-movement franchise, and a stock that's down 88% because the SaaS economics broke.**

## Related files in this folder

- [deep_dive.md](./deep_dive.md) — founder/funding/IPO/acquisitions history
- [architecture.md](./architecture.md) — product SKUs, banking partners, money flow, API surface
- [use_cases_and_examples.md](./use_cases_and_examples.md) — 9 named customer walkthroughs + accountant-channel deep dive
- [marketing_vs_reality.md](./marketing_vs_reality.md) — adversarial audit of 20 claims, activist case, competitive squeeze, honest one-liner
- [product_flow.md](./product_flow.md) — canonical money + data flow with failure cases
- [source_ledger.md](./source_ledger.md) — source-by-source provenance
- [contradictions.md](./contradictions.md) — conflicts and metric drift
- [diligence_questions.md](./diligence_questions.md) — what to ask before buying / building against / partnering
- [transcripts/](./transcripts/) — 8 founder podcast transcripts (Lacerte appearances 2019-2025)
