# Brex - Deep Dive

Date: 2026-05-09

## Executive summary

Brex is a financial software and payments platform for companies. Current homepage positioning says "Finance built for speed and control" and markets "modern cards, banking, expenses, accounting, and more - in 120+ countries." The product suite includes corporate cards, expense management, travel, bill pay, business accounts, treasury/vault products, accounting automation, budgets, reporting, mobile app, support, and APIs.

The most important current fact: Brex is no longer an independent venture-backed fintech. Capital One announced a definitive agreement to acquire Brex for $5.15B in stock and cash on January 22, 2026, and announced completion on April 7, 2026. Brex's current legal footer and platform agreement identify Brex LLC as a wholly owned subsidiary of Capital One, N.A.

Brex is best understood as three products in one:

1. A card and credit product: corporate cards with controls, underwriting, rewards, physical/virtual issuance, and repayment.
2. A finance workflow product: expenses, approvals, budgets, reimbursements, travel, bill pay, purchase orders, accounting sync, and close automation.
3. A regulated-finance wrapper: business checking, treasury, vault/deposit sweep, payments, card issuing, and money movement through partner entities.

## What Brex sells

Current public product categories:

- Corporate cards: physical and virtual cards, Mastercard/Visa acceptance, no personal guarantee positioning, high limits, spend controls, rewards, mobile controls.
- Expense management: AI-assisted receipts, memos, approval routing, policy checks, reimbursements, real-time spend visibility, and accounting sync.
- Travel: booking and travel management inside the same expense/spend platform.
- Bill Pay/AP: invoice intake, purchase orders, two-way matching, scheduled batches, ACH/check/wire payments, vendor management, approval workflows, ERP sync.
- Business accounts: checking, ACH/wires/checks, deposits, treasury return, vault/deposit sweep, and cash-management products.
- Accounting automation: GL coding, ERP integrations, journal entry export, reconciliation support.
- Intelligence/AI agents: Brex Assistant for employee expense help, Audit Agent for monitoring expenses and potential violations, Review Agent for low-risk approvals/escalations, plus AI-based expense/compliance/accounting automation.
- Developer API: REST/OpenAPI APIs for accounting, budgets, expenses, fields, onboarding, payments, team, transactions, travel, and webhooks.

Sources: [homepage](https://www.brex.com/), [pricing](https://www.brex.com/pricing), [developer portal](https://developer.brex.com/), [bill pay](https://www.brex.com/product/bill-pay), [intelligent finance](https://www.brex.com/platform/intelligent-finance).

## Origin and founder story

Brex was founded in 2017 by Brazilian founders Henrique Dubugras and Pedro Franceschi. The original product became famous because startups could get corporate cards without the traditional bank process or founder personal guarantees. The early underwriting edge was that Brex looked at startup cash, funding, revenue, and financial data rather than underwriting like a traditional small-business card issuer.

By January 2022, Brex said it had raised $1.2B total and was valued at $12.3B after a $300M Series D-2 led by Greenoaks and TCV. The company was already describing itself as a unified global spend platform, not only a card.

In April 2022, Brex launched Brex Empower, a spend management platform meant to become the foundation for all Brex products. DoorDash was one of the flagship early customers. In October 2022, Brex said Empower was generally available and claimed the integrated card/spend product supported over 100 countries.

Sources: [Brex Series D-2 announcement](https://www.brex.com/journal/press/brex-appoints-karandeep-anand-as-chief-product-officer-raises-usd300-million-in-series-d-2-round), [Brex Empower launch](https://www.brex.com/journal/press/brex-extends-into-financial-software-with-the-launch-of-brex-empower), [Empower GA](https://www.brex.com/journal/press/brex-ga-empower), [CNBC profile](https://www.cnbc.com/2022/05/17/brex-disruptor-50.html).

## Capital One acquisition

Capital One announced on January 22, 2026 that it had entered a definitive agreement to acquire Brex in a stock-and-cash transaction valued at $5.15B. Capital One described Brex as an AI-native intelligent finance platform that lets businesses issue corporate cards, automate expense management, and make secure real-time payments.

Capital One announced completion on April 7, 2026. The completion announcement says Pedro Franceschi would continue as Brex CEO, and says Brex combines smart corporate cards, spend management software, and banking.

This changes the strategic interpretation:

- Brex is no longer only competing with banks. It is now part of one.
- Capital One gets enterprise software, startup/growth-company relationships, AI-native finance workflows, and commercial deposits/cash-management adjacency.
- Brex gets bank-scale balance sheet, underwriting, distribution, and compliance infrastructure.
- The product can become much harder for pure software spend-management competitors to copy if Capital One deeply integrates card network, underwriting, deposits, and credit.

Sources: [Capital One acquisition announcement](https://ir-capitalone.gcs-web.com/news-releases/news-release-details/capital-one-acquire-brex), [Capital One completion announcement](https://www.capitalone.com/about/newsroom/capital-one-completes-acquisition-of-brex/).

## Regulated and partner structure

Brex is a fintech platform, not a bank. Current legal pages and footers matter:

- Brex LLC is a wholly owned subsidiary of Capital One, N.A.
- The Brex business account includes Checking, a commercial checking account provided by Column N.A., Member FDIC.
- Treasury and Vault are cash-management services provided by Brex Treasury LLC, Member FINRA/SIPC and a Capital One company.
- Treasury funds are not FDIC-insured and involve money-market fund risk.
- Vault funds at program banks may be eligible for FDIC insurance, but funds are not FDIC-insured until they arrive at program banks.
- Mastercard corporate cards are issued by Emigrant Bank, Fifth Third Bank N.A., or Airwallex entities, depending on program.
- The Brex Commercial Card is issued by Sutton Bank for Visa.
- Certain payment services are provided by Brex Payments LLC, a licensed money transmitter with NMLS #2035354 and a Capital One company.

This is not unusual for fintech. The important point is that "banking" is a product experience, not a single Brex bank charter.

Sources: [Platform Agreement](https://www.brex.com/legal/platform-agreement), [pricing footer](https://www.brex.com/pricing), [legal page](https://www.brex.com/legal).

## Customer segment

Brex sells to startups, growing companies, mid-market companies, and enterprises. Public customer logos and stories include DoorDash, SeatGeek, Signifyd, Alchemy, Scale AI, Coinbase, Anthropic, OpenAI, Plaid, ServiceTitan, Reddit, TikTok, and others.

The product is bought by founders, CFOs, controllers, heads of finance, procurement leaders, accounting leaders, and operations teams. Day-to-day users include every employee who spends company money: engineers buying software, sales teams traveling, recruiters booking candidate travel, executives using cards, finance teams approving bills, and accountants closing the books.

Brex's strongest fit is a company with:

- Many employees spending across cards, travel, reimbursements, and vendor payments.
- Multiple entities or countries.
- High need for spend control and close automation.
- A finance team that wants real-time visibility instead of month-end cleanup.
- Enough spend volume to make card economics, software subscription, and workflow automation attractive.

## Business model

Brex likely monetizes through a mix of:

- Card interchange and card economics.
- Software subscription plans: Essentials at $0/user/month, Premium at $12/user/month, Enterprise custom pricing, and Smart Card custom pricing.
- Treasury/cash-management economics.
- Payment services and money movement economics.
- Implementation/services for enterprise customers.
- Potential credit/float economics, especially after Capital One ownership.

Public pricing is transparent at the entry and mid-tier level, but enterprise pricing, card economics, treasury economics, underwriting economics, and partner economics are not public.

Source: [pricing](https://www.brex.com/pricing).

## Why Brex is hard to build

Brex looks simple if you only see a card and an expense dashboard. The hard part is the integrated operating system:

- Credit underwriting and risk monitoring.
- Card issuing and controls.
- Real-time policy enforcement before or during spend.
- Receipt, memo, attendee, merchant, MCC, and GL-code automation.
- Entity, department, location, budget, user, role, approval, and ERP mapping.
- AP/vendor payment flows across ACH, check, and wire.
- Bank account, treasury, and deposit sweep integrations.
- Global card/reimbursement/travel complexity.
- Enterprise implementation and support.
- Security, SOC/compliance, auditability, and change management.

The moat is not any one feature. The moat is data, integrations, risk, trust, distribution, and workflow depth.

## Strategic lesson for us

Brex shows the end-state shape of a serious CFO stack:

- You need money movement.
- You need controls before money moves.
- You need accounting/reconciliation after money moves.
- You need role-based workflows for every human involved.
- You need integrations with ERP/accounting/HRIS/SSO.
- AI is strongest when it sits on top of proprietary structured workflow data.

For a Solana/stablecoin-native version, Bridge/BVNK solve fiat/stablecoin rails. Squads/Grid can solve programmable wallet control. Brex shows the business workflow layer we would still need to build: budgets, approvals, AP, travel/expense, vendor controls, reconciliation, close automation, and finance-team UX.
