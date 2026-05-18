# Brex - Diligence Questions

Date: 2026-05-09

## Product

- Which Brex modules are live for this customer segment: cards, expenses, bill pay, travel, business account, treasury/vault, reimbursements, budgets, accounting automation, AI agents?
- Which features are plan-gated between Essentials, Premium, Enterprise, and Smart Card?
- What product functionality varies by country, legal entity, or currency?
- Can Brex fully replace the buyer's current expense/AP/travel stack, or only part of it?
- How much implementation work is needed for ERP, HRIS, SSO, departments, entities, custom fields, policies, and approval chains?

## Customers

- What is current customer count by segment: funded startups, mid-market, enterprise?
- What was churn after the SMB exit and what cohorts remain strongest?
- Which customer metrics are independently verified versus company-authored case studies?
- What is the customer support load per enterprise customer?
- What does a failed Brex rollout look like?

## Revenue and pricing

- Revenue split: interchange, software subscriptions, treasury/cash-management economics, payment fees, implementation/services, credit/float economics?
- Gross margin by product line?
- Enterprise ACV and payback period?
- Are software margins high enough independent of card economics?
- What fees apply beyond public plan pricing?

## Unit economics

- Average monthly/annual card spend per customer by segment?
- Card interchange after issuer/network/rewards costs?
- Loss rate by customer type?
- Fraud rate?
- Support and implementation cost per enterprise customer?
- Brex Payments and ACH/wire/check unit economics?
- Treasury/Vault contribution margin?

## Security, compliance, and legal

- Exact legal entity used for each product?
- Which products are provided by Brex LLC, Brex Payments LLC, Brex Treasury LLC, Column, issuer banks, or program banks?
- What are the SOC/security certifications and audit rights?
- How is customer data used for AI?
- Are AI outputs logged and auditable?
- What happens if a partner bank/issuer/payment partner terminates or changes terms?
- What are the country-by-country regulatory constraints?

## Technical architecture

- What systems are authoritative for users, cards, expenses, payments, vendors, budgets, and accounting mappings?
- How does Brex handle idempotency and retries for payment APIs?
- What webhook delivery guarantees exist?
- What is the rate limit policy?
- Is there a real sandbox for customers/partners?
- What ERP integrations are native versus file/API-based?
- How are failed ERP syncs resolved?
- How are AI low-confidence outputs routed to humans?

## AI

- Which AI agents are generally available versus beta/roadmap?
- Which actions can AI take without human approval?
- What is the measured accuracy for receipt matching, invoice extraction, GL coding, and audit detection?
- How does Brex prevent hallucinated accounting entries or wrong policy decisions?
- Does Brex train models on customer data? If yes, what controls/opt-outs exist?
- Can customers inspect why an AI action was taken?

## Capital One acquisition

- What changes after Capital One ownership?
- Will Brex remain product-independent and startup-focused?
- Will Capital One move issuing/checking/treasury/payment infrastructure in-house over time?
- How will Capital One's balance sheet affect credit limits and underwriting?
- Could Capital One bundle Brex with existing business banking/card products?
- What talent retention commitments exist for Brex product/engineering leadership?

## Competition

- Why choose Brex over Ramp?
- Why choose Brex over Airbase for AP/procurement-heavy companies?
- Why choose Brex over Navan for travel-heavy companies?
- Why choose Brex over Mercury/Rho/Relay for business banking-heavy companies?
- Why choose Brex over Amex/Capital One business cards for simple card needs?
- What features would make stablecoin-native CFO software meaningfully better?

## Top 10 questions ranked by importance

1. What is Brex's revenue and gross margin split by software, interchange, treasury, payments, and services?
2. What exact functionality is available country-by-country for cards, reimbursements, banking, bill pay, and travel?
3. What AI workflows are truly autonomous, and what are the accuracy/error rates?
4. What changes in product, underwriting, and customer terms after Capital One ownership?
5. How does Brex's credit loss/fraud performance look across startup, mid-market, and enterprise cohorts?
6. What is the real total cost for an enterprise customer after plan fees, payment fees, implementation, and support?
7. How much customer churn or trust damage came from the 2022 SMB exit?
8. How deeply can Brex replace AP/procurement/travel tools versus needing parallel systems?
9. What are the legal and operational risks in the business account, Treasury, and Vault products?
10. What workflow would a stablecoin-native competitor solve better than Brex with fiat rails?
