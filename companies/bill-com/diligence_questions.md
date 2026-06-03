# Bill.com — Diligence Questions

Questions to ask before investing in BILL, building against BILL, partnering with BILL, or competing with BILL.

## Top 10 ranked by importance (for a competitor / a buyer / an investor)

1. **What is BILL's gross retention (excluding upsell) by cohort?** The 94% net retention is in the 10-K. Gross is hidden. If gross is 88-90%, the SaaS engine is broken at the SMB end and only the accountant channel is keeping the business alive.
2. **What % of subscription revenue comes from the accountant-firm channel?** Never broken out publicly. If it's >60%, the whole thesis is "an accountant-firm business with an AP-platform attached." If <40%, the SMB direct business has more standalone value.
3. **What is the realistic outcome of the strategic review?** PE take-private at a premium? Spin-off of Spend & Expense? Stand-alone restructuring? CEO succession? Each implies different competitive dynamics over the next 18 months.
4. **What is the rate-cycle sensitivity of float income — quantified per 25bps?** Float is ~11% of revenue at 100% margin. A 100bps Fed cut likely takes ~$30-40M off the float line. Compounding rate cuts compress operating margin disproportionately.
5. **What does Spend & Expense (Divvy) actually look like inside the segment financials?** TPV growth, take rate, customer overlap with AP/AR, contribution margin. Goodwill on the balance sheet is ~$2.4B — any sign of an upcoming impairment in FY26?
6. **What's the Bank of America relationship state in 2026?** BoA notified BILL it was restructuring its payments approach in 2024. If BoA fully exits, what's the replacement architecture and how disruptive is the migration?
7. **What are BILL's actual KYC/KYB vendors and fraud-detection tools?** "Proprietary + third-party" is the disclosure. Knowing the actual vendors (Persona? Alloy? Middesk?) reveals BILL's anti-BEC posture and where it can be attacked.
8. **What is the practical effective price for a 100-employee mid-market customer?** List pricing is $45-89/user/month + transaction fees + hidden FX margins. What's a typical 100-user deal value, after discounting? This determines whether mid-market upmarket pivot is a real margin story or a defensive narrative.
9. **What is the line-item coding accuracy — actually?** BILL claims 99% header / 75% reduction in multi-line processing time. Independent benchmark vs Claude/GPT + RAG with customer-specific GL history. If a Claude-based startup can match in 6 months, the AI moat is non-existent.
10. **What's the customer-facing roadmap of the AI agent fleet vs. Ramp's?** BILL has Invoice Coding, W-9, Touchless Receipts, Vendor Q&A. Ramp has procurement, controllers' suite, full-fleet positioning. The narrative race is being lost; what's BILL's plan to catch up — or is the strategy to be acquired before it matters?

---

## By area

### Product

1. What's the actual accuracy delta between BILL's AI Coding Agent and an off-the-shelf Claude Sonnet 4.6 + customer-history-RAG approach?
2. What's the line-item accuracy for complex invoices (multi-currency, multi-line, multi-PO)?
3. What's the latency of an end-to-end intake-to-coded experience? Is it real-time or batch?
4. What customer-side controls exist on AI auto-coding (human-in-loop toggles, confidence thresholds, vendor-specific bypass)?
5. Why is the "Audit Agent" mentioned in marketing but not yet in product? What's the ship date and scope?
6. How does the Procurement product (April 2025) compare to Ramp Procurement (April 2026)? Adoption?
7. Are there meaningful AI features specific to the Spend & Expense card flow, or is it still mostly OCR + auto-categorize?
8. What's the BILL Connect (bank-embedded white-label) adoption to date? Active partner count? Revenue share?

### Customers

1. What % of net new customer adds in FY26 came through the accountant channel vs direct?
2. What's the typical customer's revenue size, headcount, and number of bills/month at point-of-purchase?
3. Among the ~700K Accountant Console-managed clients, how many are paying BILL directly vs. paying the firm a bundled fee?
4. What's the average # of clients per accountant firm? The Pareto: how concentrated is firm revenue in the top 10% of firms?
5. How many vertical-specialty firms (construction, hospitality, real estate, healthcare) are in the customer base?
6. International customers — how many BILL customers are non-US-incorporated, even though BILL is US-rails-only?
7. Of the customers who churn, where do they go — Ramp, Mercury, QBO native, Tipalti, Stampli, in-house?

### Revenue / pricing

1. Real average revenue per direct customer (excl. accountants) trend last 8 quarters
2. Real average revenue per accountant firm trend
3. ACH transaction fee elasticity — if BILL raised from $0.49 to $0.79, how much churn?
4. International FX margin contribution to revenue — basis points and absolute dollars?
5. Spend & Expense interchange revenue trajectory; vs. Ramp/Brex per-card-spend efficiency
6. What's the customer-mix shift target (SMB direct vs. accountant-managed vs. mid-market vs. enterprise) over the next 4 quarters?

### Unit economics

1. CAC trend by channel (direct, accountant, partner-embedded)
2. Payback period on a direct SMB customer ~ vs. accountant-channel customer
3. Customer-acquisition spend per net new add — running below historical average?
4. Free-tier (Spend & Expense card-only) → paid AP/AR seat conversion rate and time
5. Per-transaction gross margin trend (declining as Ramp/Mercury compress prices?)
6. Float-revenue margin sensitivity to 100bps Fed move (linear or convex?)

### Security / compliance / legal

1. Specific state-by-state Money Transmitter License list and renewal cadence
2. SOC 2 Type II report — most recent date, exceptions noted, remediation timeline
3. PCI DSS for Spend & Expense — who is the merchant of record (Cross River vs. BILL)?
4. BSA/AML compliance program annual cost, FinCEN inquiry history
5. Litigation history — any class-action consumer suits, BEC-defense suits, state-AG actions?
6. Data export terms (customer-data lock-in) — what % of customers actually retrieve historical bills on exit?
7. Subprocessor list — Cloudflare, AWS, Snowflake? Where is data stored geographically?

### Technical architecture

1. What's the FBO custodian list as of mid-2026, and what % of customer funds are at each?
2. ACH origination dependency chain — who would need to replace BoA in a forced migration?
3. KYC/KYB vendor identity and switching cost
4. Risk engine — what's the false-positive rate of "limit review" holds?
5. Sync architecture with QBO/NetSuite/Intacct — what's the failure rate at month-end?
6. API platform — what % of customers actually use it? Webhooks live or in beta?
7. Cross-border architecture — who's the FX counterparty (Convera? major bank?)
8. Mobile app feature parity with web — recent mobile-AP launch (Sept 2025) — adoption?

### Operations / human-services ratio

1. How big is the in-house Risk Operations team that handles BSA/OFAC reviews and account freezes?
2. Customer Support team size, ticket volume, SLA targets, first-response medians
3. KYC review queue — average resolution time for new vendor verification
4. Implementation services revenue — does BILL sell paid onboarding, or is everything channel-led?
5. Post-layoff (May 2026 -30%), which functions were cut hardest — engineering, sales, support, ops?
6. What's the operational impact on customer-facing reliability? Status page incident rate trending up?

### Competition

1. Ramp's actual customer migration tooling — how many BILL customers have used Ramp's published migration playbook in the past 12 months?
2. Mercury Bill Pay attach rate to Mercury banking customers — is the "no middleman" pitch converting?
3. QuickBooks native Bill Pay (now Melio-powered) — what % of QBO users actively use it?
4. Tipalti's competitive wins in mid-market — has Tipalti's slow-and-steady eaten BILL's upmarket plans?
5. Capital One + Brex post-acquisition — does CapOne push Brex Bill Pay into its own SMB banking customer base?
6. NetSuite IPA (Oct 2025) — has the embed driven actual incremental customer wins, or just defended share?
7. Any banks (besides JPM/Wells/PNC) considering BILL Connect as their AP-embedded offering?

### Founder / company history

1. Lacerte's current ownership stake post the recent decline
2. Executive churn rate at VP+ level over the past 3 years
3. Board independence after the Starboard cooperation agreement
4. Is there evidence of CEO-succession planning, formal or informal?
5. What's the Founder/CEO's commitment level if a PE buyer wants Lacerte to stay vs. exit?

### Strategic / M&A

1. If BILL is sold to Hellman & Friedman (or similar PE), what's the expected operational playbook (multiple expansion via cost cuts? Spin-off Divvy? Bolt-on acquisitions?)
2. What's a realistic standalone EBITDA path if no sale happens?
3. Could BILL be acquired by a larger strategic — Intuit, Stripe, an enterprise bank, an ERP vendor (Oracle, SAP)?
4. What's the breakup value (sum-of-parts) of BILL today: AP/AR + Spend & Expense + Accountant Console?
5. What's the precedent multiple for similar SMB AP businesses sold at this scale? (Tipalti, Stampli historical raises; ServiceTitan-like vertical SaaS multiples)

---

## Questions a Decimal-style competitor should specifically ask

1. **What's BILL's actual cross-border payment volume and FX margin contribution?** This is the most attackable surface in the entire pricing model.
2. **What's the BILL ACH-to-RTP transition timeline?** If BILL stays on slow batch ACH, instant-settlement-as-marketing wedge stays viable.
3. **What's the % of customers whose vendor concentration includes 5+ international vendors?** This is the addressable wedge for a stablecoin-rails competitor.
4. **Is BILL exploring stablecoin / crypto rails internally?** If yes, the window is short; if no, the window is open.
5. **What's the share of Accountant Console clients that also use a separate cross-border product (Wise, etc.)?** Reveals the cross-sell opportunity for a unified TradFi+stablecoin offering.
6. **Has BILL responded to the Mercury "no middleman" critique publicly or in product?** No evidence of response yet. Window open.
7. **What's the realistic timeline for an Intuit-native bill-pay that competes with BILL on the QBO-installed-base?** Intuit removed BILL as embedded partner in 2023 (now Melio). Could become BILL's existential threat by 2027.
8. **What's BILL's churn-curve shape past 18 months on the deck (declining at controllable rate, or accelerating)?** Determines whether the activist case lands at "sell now" or "restructure standalone."
9. **What % of BILL revenue is exposed to a single failure mode (BoA partner, Cross River regulatory, Solana-equivalent outage)?** Reveals operational concentration risk for a partner / acquirer / competitor.
10. **What would a "BILL-on-stablecoins" reference architecture cost to build standalone?** Likely $5-15M over 18 months for the AP/AR + multisig + corridor + ERP-sync stack. This is the "build vs. buy vs. partner" math.
