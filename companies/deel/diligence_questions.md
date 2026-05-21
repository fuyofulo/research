# Deel — Diligence Questions

*Compiled 2026-05-21. The buyer/investor/competitor question bank. Organized by area, ranked at the end.*

---

## Product

1. Of the "150+ countries" claim, how many countries have a **Deel-owned legal entity** vs **partner EOR** vs **contractor-only support**? Publish the country-by-country breakdown.
2. What is the depth-of-integration across the six product SKUs (Contractor, EOR, PEO, Global Payroll, Engage, IT)? Is the underlying ledger and identity layer truly unified, or is the product still federated post-M&A?
3. How autonomous is "Deel AI"? What % of compliance questions, contract drafts, expense categorizations are handled with zero human touch? What's the accuracy bar, and how is it measured?
4. Where does the developer API hit limits? Which actions can be fully API-automated (contractor onboarding, payment) and which require human-in-the-loop review (EOR hire, dispute, sanctions escalation)?
5. What's the actual two-way sync quality of the QuickBooks / Xero / Workday integrations? Real-time, batch, conflict resolution rules?
6. How many sub-entities can a single customer have? For holdco/multi-LLC operators, where does the UX or operations start to break?

## Customers

7. What is the **net dollar retention** by product cohort and customer-segment? Specifically: NDR for EOR customers in countries where Deel has its own entity vs partner EOR; NDR for Contractor customers that started SMB and scaled.
8. Of the "50,000+ customers" claim, what's the active-customer definition? Minimum monthly volume, minimum balance, minimum tenure?
9. What's the customer-concentration distribution? Top 10 / top 100 / top 1% of customers as % of ARR.
10. Has any Tier-1 customer logo (Shopify, Notion, Klarna, Reddit, Forbes, BCG, Nike, Cloudflare) reduced or canceled their Deel usage post-Rippling lawsuit? Even if not publicly, what's the internal data?
11. What's the contractor churn rate (workers leaving the platform)?
12. What's the corridor-level customer concentration? E.g., what % of contractor payments flow through Argentina, Brazil, India, Philippines, Nigeria, Ukraine?
13. What's the crypto-payouts share of total volume? Trending up or down?

## Revenue / pricing

14. What's the actual revenue mix between (a) EOR fees, (b) contractor SaaS, (c) Global Payroll, (d) PEO, (e) FX markup, (f) float income (interest on escrow), (g) card interchange, (h) immigration, (i) add-ons (Hofy, Engage, etc.)?
15. What's the published fee schedule, in detail — including same-day ACH, international wire fees, FX markup methodology per corridor, expedited card replacement, returned-payment fees, EOR statutory-employer pass-through markup, immigration case fees?
16. What's gross margin per product? EOR has high gross margin but is competing on price; Global Payroll has lower margin; FX has near-100% margin; software-SaaS has 80%+.
17. **Is "$1B ARR" GAAP revenue, or is it a forward-annualized recurring-fees figure that includes float income and FX markup?** This is a critical S-1 disclosure question.
18. What's the EBITDA, GAAP net income, and free cash flow on an audited basis? Bouaziz tweets EBITDA-positive — what's the underlying audited number?

## Unit economics

19. What's CAC across segments (SMB self-serve vs enterprise sales-led)?
20. What's payback period? LTV/CAC?
21. What's the contribution margin of a typical EOR employee account in a (a) Deel-owned-entity country, vs (b) partner-EOR country? The partner-routed economics are structurally worse.
22. What's the float economics? With $1B+ in float and 4-5% short rates, the interest income is $40-50M/year. How is this allocated to which revenue line?
23. What's the contractor-side ops cost (KYC, sanctions screening, support tickets, dispute resolution) per active contractor per month?

## Security / compliance / legal

24. **What is the current state of the Rippling v. Deel litigation, both in U.S. District Court (N.D. Cal.) and the Irish High Court?** Settlement status, discovery findings, deposition schedule, trial date.
25. Has the Keith O'Brien affidavit's allegations against Alex Bouaziz and Philippe Bouaziz been corroborated by independent evidence in discovery? What's Deel's defense?
26. Have the DOJ or UK SFO made any formal contact regarding the Rippling case? Even a referral letter? (Stream-4 cited an FT report; deep_dive could not corroborate.)
27. What's the outcome (or current status) of the **internal board investigation** reportedly commissioned in late 2025?
28. Are there any other pending litigations against Deel? Contractor wage claims, customer disputes, sanctions enforcement actions?
29. What's the actual scope of OFAC compliance issues from the 2022 Russia/Belarus episode? Has Deel been sanctioned, fined, or formally warned by OFAC?
30. SOC 2 Type 2 + ISO 27001 — when last audited, by which firm, any unresolved findings?
31. What's Deel's KYB rejection rate? How many businesses are turned away?
32. What's the AML/sanctions stack — Persona/Onfido/Sumsub for KYC, ComplyAdvantage/Refinitiv for screening — and what's the false-positive rate?

## Technical architecture

33. What's the actual card issuer-processor for Deel Card — Stripe Issuing, Marqeta, Lithic, or something else? Contract terms?
34. What's the partner-bank stack for US ACH/wire originations? Single-bank or multi-bank routing?
35. What's the Bridge / Circle integration status for stablecoin payouts? Volume share?
36. How is the country-specific payroll engine architected — is it a unified ledger with country plugins, or 40 different engines stitched together?
37. What's Deel's disaster-recovery posture — RTO/RPO, regional failover, data residency for EU/APAC?
38. What's the LLM stack architecture? Which features use which model, what data leaves the customer's tenant, what's the cost structure?

## Operations / services ratio

39. What's the actual headcount split — engineering / product / design vs sales / support / compliance / HR ops / legal / risk?
40. How many "Country Manager" / "Legal Entity Setup Specialist" / "HR Ops" headcount does Deel run? This is the services side.
41. What's the support ticket volume per active customer per month? Time-to-first-response, time-to-resolution?
42. What's the dispute / chargeback rate? Win rate?
43. How is the partner-EOR roster managed? Who chooses the partner per country, how is quality monitored, how often do partners churn?

## Competition

44. What happens to Deel if **Rippling** wins the lawsuit and gets significant damages? Reputation, balance-sheet impact, ARR.
45. What happens to Deel if **Mercury or Workday** ship a competing EOR-as-a-feature within 12 months?
46. **Multiplier** is undercutting EOR pricing 30-40% in emerging markets. How does Deel respond — match, segment, or accept margin compression?
47. **Remote.com** is positioning on transparency (publishing entity ownership, fees). How does Deel match without giving away float/FX economics?
48. What's defensible long-term — the entity footprint, the compliance corpus, the integration breadth, the customer logos, the M&A integration capability, or something else?

## Founder / company history

49. What's the full story of Alex Bouaziz's prior ventures (MagicBus, Sarah's Music)? Why did they fail, and what did he learn?
50. What's Philippe Bouaziz's pre-Deel CFO history? Specifically the Praxis Capital Markets / Praxis Tech Ltd context — what was his role, and what's the regulatory history of those entities?
51. Why is Alex Bouaziz reportedly spending significant time in Dubai? Is this permanent? Does it affect Delaware C-corp governance?
52. What's the actual founder ownership at $17.3B? The Bouaziz family share?
53. Has the board structure changed since the Rippling lawsuit? Have any board members resigned? Have any major investors signaled governance concerns?
54. Why no Series C from a new lead since 2022? Coatue has led every priced round. Is this lead-investor lock-in, or a signal that new investors are pricing in litigation risk?

## IPO

55. When does Deel expect to file an S-1? What are the gating items — Rippling settlement, audit completion, market conditions?
56. What's the expected S-1 risk-factor section structure? Specifically: how would the company disclose the affidavit naming sitting executives?
57. What's the expected revenue restatement / reclassification — float income as separate line, FX markup as separate line, services revenue separated from software?

---

## Top 10 questions (ranked by importance)

1. **What is the current state and likely outcome of the Rippling v. Deel litigation, and what's the financial exposure if Deel loses?** — Everything downstream depends on this. Reputational damage, S-1 viability, potential personal liability for the Bouazizes.
2. **Of the "150+ countries" claim, how many are Deel-owned entities vs partner-routed?** — Determines whether the 150-country marketing is mostly real infrastructure or mostly partner orchestration.
3. **Is "$1B ARR" GAAP revenue, or does it include float income + FX markup as recurring fees?** — Critical for valuing the company at software vs services multiples.
4. **What's net dollar retention by EOR cohort?** — EOR has a built-in churn driver (graduate to own entity). NDR is the most important undisclosed metric.
5. **What's the actual gross margin and EBITDA on an audited basis?** — Bouaziz tweets EBITDA-positive; the audited number determines whether the IPO economics work.
6. **What's the headcount split between engineering/product vs services/compliance/HR-ops/legal?** — Tells you whether this is a software business or a services business with a software wrapper.
7. **Has the internal board investigation produced any findings, and have any board members resigned?** — Governance signal beyond the litigation itself.
8. **What's Deel's actual partner-bank stack, and is there multi-bank routing?** — Existential tail risk if a single partner-bank disruption (post-Synapse-style) hits Deel.
9. **What's the share of revenue from crypto-payroll (USDC) vs traditional rails, and how is it trending?** — Tells you whether crypto is still a wedge or has been displaced by mainstream rails.
10. **Why has the IPO slipped from 2022 to 2026, and what are the specific gating items today?** — Reveals what management knows that the market doesn't.
