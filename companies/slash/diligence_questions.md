# Slash — Diligence Questions

*Compiled 2026-05-21. The buyer/investor/competitor question bank. Organized by area, ranked at the end.*

---

## Product

1. What exactly is "an industry workspace"? Is the underlying ledger / card program / API identical across all six workspaces, or does each have meaningful customization beneath the UI?
2. Of the six advertised workspaces (Agency, E-com, Creator, Holdco, Contractor, Real Estate), which two or three drive the bulk of active accounts and deposit volume? Are the remaining workspaces real businesses or vanity SEO?
3. What is the actual "AI" inside the product? Is bill-pay extraction fully automated end-to-end, or is there a human review queue for first-time payees? What is the accuracy bar on auto-categorization, and what's the human-touch rate?
4. Does Slash have a developer API today? If not, is one on the roadmap? (Mercury's API has been a real moat for code-native customers; Slash's absence here is a gap.)
5. What's the depth of QuickBooks / Xero integration — one-way export, two-way sync, real-time, or batch?
6. How many sub-accounts can a single entity have before the UX or partner-bank limits start to break? Customers running 30+ entities are the most valuable but also the most likely to expose limits.

## Customers

7. What is the actual definition of "20,000+ businesses" (Series B announcement) vs "40,000+ workspaces" (late-2024 marketing)? Is the gap (a) multi-entity customers, (b) inactive accounts counted as workspaces, or (c) something else?
8. What's the active-account definition — minimum balance, minimum monthly transactions, account-open-for-N-days?
9. What's net retention? What's monthly account-closure rate? How many of those are voluntary vs partner-bank-driven de-risking?
10. Who are the three largest customers by deposit balance? What's customer concentration at the top 1%, 5%, 10%?
11. What's the cohort retention curve — of customers acquired in 2023, what fraction are still active and at what balance?
12. How much of the customer base is crypto-adjacent (e.g., businesses that hold crypto, accept crypto, or have a meaningful share of revenue from crypto-related activity)? This is the unique wedge but also the largest concentration risk.
13. How many named customers will go on record? The thin public case-study footprint is a yellow flag.

## Revenue / pricing

14. What is Slash's actual revenue mix between (a) card interchange, (b) net interest margin on deposits, (c) wire fees, (d) FX markup, (e) subscription, (f) treasury / yield spread?
15. What is Slash's effective take rate on $5B annualized volume? Is it 0.5%, 1%, 2%? Each implies very different revenue.
16. What's the average deposit balance per customer? What's the deposit-to-spend ratio?
17. What is the published fee schedule, in detail — including same-day ACH, international wire, FX markup methodology, expedited card replacement, returned-ACH fees, and per-sub-account fees beyond the free tier?
18. What does the pricing roadmap look like? Will there be a meaningful subscription tier, or is the model staying "$0 monthly fee, monetize on interchange + float"?

## Unit economics

19. What's CAC across the funnel — Twitter founder content, YC alumni referral, vertical SEO, paid?
20. What's gross margin per customer cohort after partner-bank cost-of-funds, issuer-processor fees, KYC vendor cost, support burden, and dispute / chargeback ops?
21. What's the contribution margin of the "support-heavy" vertical (e.g., crypto-adjacent or holdco-with-30-entities) vs the "support-light" vertical (e.g., solo contractor)?
22. At what scale does Slash reach operating profitability, and what's the assumed Fed-funds environment in that projection?
23. What's the cost-per-transaction split across (Slash backend) vs (partner bank cost) vs (issuer-processor cost) vs (network interchange) vs (support cost)?

## Security / compliance / legal

24. What is the current partner-bank stack, in detail — primary, backup, and what the contractual term of each relationship is?
25. Does Slash currently use multi-bank routing (deposits split across multiple partner banks for resilience), or is it still single-partner?
26. What was Slash's specific exposure to the Synapse Chapter 11 in 2024 and the Evolve cyber incident? What was the actual customer-facing impact (downtime, frozen funds, data exposure)?
27. What KYC and KYB vendors does Slash use? What's the false-positive / false-negative rate on KYB rejections?
28. What's the SOC 2 status (Type 1 vs 2)? Can the report be reviewed under NDA?
29. What's the PCI scope and how is it audited?
30. What's the AML / sanctions screening architecture — Slash's own pre-screen + partner bank's screening, or just partner bank?
31. Are there any open regulatory enforcement actions or consent orders against Slash, against its partner bank(s) specifically for the Slash program, or against any vendor in the stack?
32. Has Slash been required by its partner bank to off-board any customer segment in the past 24 months? How was that handled?

## Technical architecture

33. What is the actual card issuer-processor — Marqeta, Highnote, Lithic, or something else? What's the contract term and any volume commitments?
34. What does the ledger look like under the hood — is it a custom double-entry implementation, an off-the-shelf one (e.g., Modern Treasury Ledgering, Increase Ledgering), or something else?
35. How is FBO-to-sub-account reconciliation done? Real-time, batch end-of-day, or something else? What's the audit trail?
36. What's the disaster-recovery story — RTO/RPO, failover, data residency?
37. How is the LLM-powered functionality architected — what model providers, what data leaves the customer's tenant, what's the latency budget?

## Operations / services ratio

38. What's the actual headcount split — engineering / product / design vs sales / support / compliance / risk ops? In a 60-person company, anything under 50% engineering+product is meaningful.
39. What's the support-ticket volume per active customer per month? What's the median time-to-first-response and time-to-resolution?
40. Is dispute resolution handled in-house, or does it flow entirely through the partner bank? What's the chargeback win rate?

## Competition

41. What happens to Slash if Mercury ships a full multi-LLC / holdco product equivalent in 6 months?
42. What happens to Slash if Brex returns down-market with a multi-vertical SMB play (they've done up-market the past 3 years; the door is open for a reverse move)?
43. What's defensible long-term — the workspace UX, the partner-bank relationships, the founder distribution on X, the crypto-adjacent customer base, or something else?
44. Why hasn't a chartered bank built this? What stops Live Oak, Cross River, or Stearns Bank from launching a Slash-style product themselves?

## Founder / company history

45. Cardenas was previously a co-founder at Karat Financial. Why did he leave Karat? Is Karat still operating? What did he learn from Karat that informs Slash?
46. Slash pivoted from teen banking to SMB banking circa 2022-2023. What happened to the original teen-banking customers? What's the exact wind-down story, and were any of those customers force-migrated or refunded?
47. How aligned are Cardenas and Bai today? What's the equity split? Has either tried to leave?
48. What's the cap table look like — Series B was $370M post-money, but who actually controls the board, and what are the protective provisions?
49. Why no Series C yet (as of May 2026), 14 months after Series B? Burn runway, or strategic timing?

---

## Top 10 questions (ranked by importance)

1. **What is the actual revenue mix, gross margin per customer, and current burn rate?** — Everything downstream depends on this. The float-vs-interchange split determines whether Slash is a software business or a neobank dressed in software clothes.
2. **What is the current partner-bank stack and is there multi-bank routing?** — Single-bank dependency is existential post-Synapse; the answer determines tail-risk.
3. **What is the active-customer definition, and what's the gap between "20K businesses" and "40K workspaces"?** — Resolves whether Slash's headline metrics are growth or relabeling.
4. **What's net retention and what fraction of churn is partner-bank-driven de-risking?** — Distinguishes a sticky product from a churn-from-compliance machine.
5. **How concentrated is the customer base in the crypto-adjacent segment?** — Likely the actual growth driver; also the single largest risk if the partner bank changes policy.
6. **What's the support / risk / compliance headcount as a fraction of total?** — Tells you whether this is a software business or a fintech operations business with a software wrapper.
7. **What was the actual customer-facing impact of the 2024 Synapse / Evolve disruption?** — Tests management quality under stress and indicates true operational maturity.
8. **What's the AI-feature depth — specifically, the human-touch rate on bill-pay extraction and categorization?** — Distinguishes real automation from marketing.
9. **What happens to Slash if Mercury ships a competing multi-LLC product within 6 months?** — Tests how defensible the actual wedge is.
10. **Why no Series C in the 14 months since the March 2025 round?** — Burn-rate signal; also a leading indicator of whether the company is on track to its own internal projections.
