# Brex - Explain Like a New Teammate

Date: 2026-05-09

## What does Brex do in one sentence?

Brex helps companies manage money leaving the company: employee cards, expenses, travel, vendor bills, reimbursements, business accounts, approvals, accounting sync, and AI-assisted finance work.

## What problem exists before Brex?

A company normally has money workflows split across too many tools:

- Bank account at one bank.
- Corporate cards from another issuer.
- Employee reimbursements in payroll.
- Expense reports in a separate expense tool.
- Vendor invoices in Bill.com or email.
- Travel bookings in another system.
- Accounting in NetSuite, QuickBooks, Xero, or another ERP.
- Budget tracking in spreadsheets.
- Approvals in Slack/email.

This creates the classic finance mess: employees spend first, finance finds out later, receipts are missing, managers approve late, accountants manually code transactions, and CFOs only see the truth after month-end close.

## Who buys it?

Usually:

- Founder/CEO at startups.
- CFO.
- VP Finance.
- Controller.
- Head of Accounting.
- Procurement leader.
- Operations leader.

The bigger the company, the more likely the buyer is finance/procurement/accounting. The smaller the company, the more likely the founder is involved.

## Who uses it day to day?

- Employees use cards, travel, reimbursements, and receipt capture.
- Managers approve spend or manage team budgets.
- Finance admins create policies, cards, users, and limits.
- Accounting teams reconcile and export to ERP.
- AP teams pay vendor bills.
- CFO/FP&A teams monitor budgets and spend.
- Developers may use the API to connect Brex to internal systems.

## What exactly happens step by step inside the product?

Simple card expense flow:

1. Finance admin creates a policy and budget.
2. Employee gets a Brex card.
3. Employee buys something for work.
4. Brex checks card limit, policy, merchant/category, and budget context.
5. Transaction appears in Brex.
6. Brex asks for or auto-matches receipt.
7. AI/rules generate memo, category, GL code, and review status.
8. Manager or finance approves exceptions.
9. Accounting exports clean data to ERP.
10. Company pays card statement or settles through the account structure.

Vendor bill flow:

1. Vendor sends an invoice.
2. Company uploads/forwards invoice to Brex.
3. Brex extracts invoice fields.
4. Brex matches invoice to PO if available.
5. Approval route is selected.
6. Approver approves.
7. Brex sends ACH, check, or wire.
8. ERP receives bill/payment data.

## What data, money, or state moves through the system?

Data:

- Company/legal entity information.
- Users, roles, departments, locations.
- Cards and card limits.
- Budgets and policies.
- Transactions.
- Receipts and memos.
- Vendors and invoices.
- Trips.
- Accounting fields and GL codes.
- Approvals and audit logs.

Money:

- Card spend.
- ACH/wire/check payments.
- Business account balances.
- Treasury/vault cash movements.
- Reimbursements.

State:

- Expense status: draft, submitted, approved, out-of-policy, settled.
- Payment status: processing, cleared, failed, refunded, etc.
- User/card status.
- Budget remaining.
- ERP export status.

## Is Brex a bank?

No. Brex is a financial technology/software company, now owned by Capital One. The Brex product feels like banking in the app, but the legal rails are provided through partners/entities:

- Checking by Column N.A.
- Treasury/Vault through Brex Treasury and program-bank structures.
- Cards issued by issuer banks.
- Payment services by Brex Payments LLC, a licensed money transmitter.

This distinction matters for risk, FDIC coverage, money-market risk, and customer contracts.

## What is the AI part?

Brex uses AI mostly to reduce finance busywork:

- Auto-generate receipts/memos/attendees.
- Match receipts to expenses.
- Code expenses.
- Detect policy/compliance issues.
- Extract invoice data.
- Help audit spend.
- Help answer finance questions.
- Assist payment/travel/accounting workflows.

Think of the AI as a worker inside a structured finance workflow, not a free-floating chatbot.

## Why is this hard?

Because business finance is full of edge cases:

- Different legal entities.
- Different currencies/countries.
- Different tax/accounting rules.
- Different employee roles.
- Different spend policies.
- Fraud and credit risk.
- Missing receipts.
- Vendors changing bank details.
- ERP mappings that must be exact.
- Audit/compliance requirements.
- Payment failures and reversals.

If Brex makes a mistake, it can cause accounting errors, compliance issues, fraud losses, or real money movement problems.

## Why now?

Several trends made Brex possible:

- Startups and modern companies needed faster financial tools than banks offered.
- Card issuing and banking-as-a-service made fintech layering possible.
- APIs and ERPs made integrations possible.
- Remote/global teams made old expense workflows worse.
- CFOs want real-time visibility, not month-end surprises.
- AI can now automate document extraction, categorization, and review.
- Banks now want software layers, shown by Capital One buying Brex.

## What is actually impressive?

Brex managed to move from a narrow financial wedge to a broad operating system. That is hard because every new product has different regulation, risk, workflows, and buyer expectations.

The impressive parts:

- Deep customer trust around company money.
- Card + software + bank account + AP + travel + accounting in one surface.
- Developer API with real finance objects.
- Enterprise customers and implementation muscle.
- Enough workflow data for AI to be useful.
- Exit/acquisition by a major bank at multibillion-dollar scale.

## What is still unclear?

- How much of Brex's revenue is software versus card/treasury/payments economics.
- How profitable Brex is after support, implementation, credit losses, and partner costs.
- How Capital One will integrate Brex.
- How much AI is fully autonomous versus assistive.
- Exact international product parity.
- Exact customer churn/retention after the SMB exit.
- Credit performance across different customer cohorts.

## Mental model

Think of Brex as "the control room for company spending."

The card is the entry point. The bigger product is everything around the card: who can spend, how much they can spend, what counts as approved, how receipts are collected, how bills are paid, how accounting is updated, and how finance sees the company in real time.
