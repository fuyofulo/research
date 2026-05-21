# Meow — Diligence Questions

*Compiled 2026-05-21. The buyer/investor/competitor question bank. Organized by area, ranked at the end.*

---

## Product

1. What is the actual MMF that Meow uses for liquidity holdings — BlackRock TTTXX (per stream 2) or Goldman Sachs FTGXX (per stream 4)? Resolve via meow.com's brokerage account agreement and the underlying fund factsheet.
2. Does Meow operate a card program today? Stream 2 couldn't verify; stream 4 said yes. If yes, who is the issuer/processor/network?
3. What is the actual depth of the stablecoin yield offering, if any? Does Meow pay yield on USDC balances held in the Meow account? If so, what's the underlying mechanism — MMF wrapping, counterparty lending, T-bill collateral?
4. What's the developer API surface (if any)? OAuth, webhooks, documented endpoints?
5. What integrations work in production today vs marketing roadmap? QuickBooks, Xero, payroll, ATS?
6. What's the multi-user / multi-entity feature depth? Approval workflows, role-based permissions, multi-LLC consolidation?

## Customers

7. What is the **true customer count** — not "thousands of high-growth companies" but the actual number with $X+ balance and Y monthly activity?
8. What is the customer-concentration distribution? Top 1%, 5%, 10% of customers as % of total AUM?
9. What's net dollar retention by cohort? How many post-FTX-pivot customers are still active?
10. How many customers have left for Mercury Vault, Brex Treasury, or direct T-bill brokerage? What's the churn rate?
11. Which Tier-1 named customers can be publicly disclosed for case studies?
12. What's the geographic distribution — US-only, or international startups using virtual USD accounts via Bridge?
13. What % of customer base is crypto-native vs traditional VC-backed startups? The dual-positioning game depends on this.

## Revenue / pricing

14. **What is the actual yield spread Meow captures?** Underlying TTTXX yield minus customer APY = spread. Disclose the methodology.
15. What's the revenue mix between (a) yield spread on T-bills/MMF, (b) FDIC-sweep spread, (c) card interchange (if any), (d) FX markup on Bridge corridors, (e) SaaS/platform fees, (f) float income?
16. What's gross margin per product line?
17. What's the published fee schedule on meow.com, in detail — wire fees, ACH fees, international wire fees, FX markup methodology, card interchange share, broker-dealer transaction fees?
18. Is Meow profitable on an EBITDA basis? On a GAAP net income basis?

## Unit economics

19. What's CAC across segments — founder-referral, X/Twitter content, paid outbound, partner-channel?
20. What's payback period? LTV/CAC?
21. What's the actual ARR? Estimated at $8-22M; verify.
22. What's the burn rate? Has Meow needed bridge financing since the pivot?
23. At what scale does the yield-spread business become defensible vs Mercury Vault undercutting?
24. What's the all-in cost of running Meow Markets LLC (FINRA fees, compliance staff, audit, clearing fees) — and what % of revenue does it consume?

## Security / compliance / legal

25. What is the **FINRA BrokerCheck record for Meow Markets LLC (CRD 322685)** — registration history, principal personnel, disciplinary actions, current net capital, FOCUS report data?
26. What's the exact relationship structure with Velox Clearing? Fully-disclosed clearing? Self-clearing? Net capital implications?
27. **What was Meow's exact FTX exposure dollar amount** in November 2022? How much was customer money vs Meow's balance sheet?
28. How was the "zero customer fund loss" actually achieved — investor backstop, debt, founder personal capital, or some combination?
29. How much has Meow recovered from the FTX bankruptcy estate to date? What's the projected total recovery?
30. **Did the NYAG actually settle with Meow** (per stream 3's unverified claim)? If yes, what were the terms?
31. What's the AML / sanctions screening stack? KYC/KYB vendors?
32. What's the Chainalysis/Elliptic-class stablecoin transaction monitoring approach for the Bridge integration?
33. SOC 2 Type II status? Trust center URL?
34. Has Meow ever had a regulatory action against its broker-dealer arm?

## Technical architecture

35. What is the actual partner-bank stack — single (Grasshopper) or multi-bank routing? Backup arrangements?
36. What's the FDIC sweep network (likely IntraFi ICS) — verify the partner identity and the "up to $125M" mechanics?
37. What's the Bridge integration depth? Are there fallback stablecoin rails (Circle Mint direct, Brale, etc.)?
38. What's the disaster-recovery posture — RTO/RPO, regional failover?
39. Where is the Meow Markets LLC custody data stored, and how is it backed up?

## Operations / services ratio

40. What's the actual headcount split — engineering/product vs compliance/operations/support?
41. What's the support model — founder-led for early customers, ticket-based for SMBs? Time-to-first-response?
42. How is dispute resolution handled — ACH returns, wire reversals, stablecoin transaction disputes?

## Competition

43. What happens to Meow if Mercury Vault ships explicit yield pass-through with 0 bps spread? Mercury has the deposit base and brand to do this.
44. What happens to Meow if Stripe builds a competing treasury product on Bridge?
45. What happens to Meow if Brex Treasury moves down-market to compete on the SMB tier?
46. What's the defensible long-term moat — the own-broker-dealer structure, the founder's FTX-survival brand equity, the Bridge integration, the customer relationships, or something else?

## Founder / company history

47. What's the full backstory of Brandon Arvanaghi and Bryce Crawford? Where did they meet (NOT MIT per stream 1)?
48. What's Bryce Crawford's exact role today? He has a much lower public profile than Arvanaghi.
49. What was the actual Series A — $22M Tiger Global @ ~$78M valuation per the leaked deck (per stream 1) or something different?
50. Has Meow raised any priced round since the March 2022 Series A? Bridge financing? SAFE rounds?
51. What's the cap-table look like today — FTX Ventures position (likely written to zero?), Tiger Global, YC, other angels?
52. Why hasn't Meow IPO'd or been acquired — what's the strategic plan?
53. What's the founder ownership today?

## IPO / Exit

54. Is the most likely outcome acquisition by Mercury, Brex, or a mid-tier bank in the $200-400M range, as the marketing-vs-reality analysis suggests?
55. Has Meow run an acquisition process? Were there bidders post-pivot?

---

## Top 10 questions (ranked by importance)

1. **What was Meow's exact FTX exposure dollar amount, and how was the "zero customer fund loss" actually achieved?** — This is the single most important diligence question. The "Arvanaghi made customers whole" narrative depends on the mechanism. If investor backstop, that has cap-table implications. If founder personal capital, that's both inspiring and risky.
2. **What is the actual yield spread Meow captures (underlying MMF yield minus customer APY)?** — Distinguishes the business model from "yield pass-through" claims and tells you whether the company has pricing power.
3. **What is the FINRA BrokerCheck record for Meow Markets LLC (CRD 322685)?** — Definitive on broker-dealer status, clearing arrangement, disciplinary history, net capital. Single highest-leverage missing verification.
4. **Is Meow profitable on an audited basis, and what's the burn rate?** — Determines whether the absence of post-Series-A priced rounds reflects strength (profitable, no need to raise) or weakness (struggling to raise at flat/down valuation).
5. **What's the true active-customer count and the customer concentration distribution?** — The "$2B AUM" claim is meaningless without knowing if it's 10 customers or 10,000.
6. **What's net dollar retention by cohort, including pre-FTX vs post-pivot cohorts?** — Tests whether the trust rebuild actually worked at scale.
7. **What happens to Meow's stablecoin product if Stripe ships a competing treasury rail using Bridge natively?** — Strategic question that determines the upside ceiling.
8. **Does Meow offer yield on USDC balances, and if so, what's the underlying mechanism?** — This is the FTX-pattern-replay risk. If counterparty lending is involved, customers should understand the recovery waterfall.
9. **Did the NYAG (or any state regulator) settle with Meow post-FTX?** — Stream 3 mentioned this; no other stream corroborated. Material if true.
10. **What's the exit path — acquisition target, IPO trajectory, or wind-down?** — Determines whether the current customer base should be planning their own treasury migration.
