# Slash — Source Ledger

*Compiled 2026-05-21. Source-by-source provenance for every material claim across the Slash research folder.*

---

## Source-quality summary

This research run had unusually mixed source quality. **Two of four research streams (architecture and marketing-vs-reality) reported that live WebSearch returned limited substantive content during their runs**, and one of those two never successfully executed any live searches at all. As a result, large portions of `architecture.md` and `marketing_vs_reality.md` are **structural inference from BaaS-fintech category patterns** rather than primary-sourced facts about Slash specifically. This is flagged with 🟡 / 🔴 labels in the files themselves and called out again here.

The strongest-sourced claims in this folder are the funding-round facts (Series A March 2022 NEA-led, Series B March 2025 Goodwater-led $370M post) and the founder identification (Cardenas ex-Karat, Bai co-founder). The weakest-sourced claims are anything customer-specific (most named customers are first-name-only testimonials).

---

## Source table

| Source | Type | Date | What it proves | Reliability | Notes |
|---|---|---|---|---|---|
| [ycombinator.com/companies/slash](https://www.ycombinator.com/companies/slash) | Company page (YC directory) | current | Slash exists, founders, YC batch (S21 per stream 1) | **High** | YC directory is authoritative for batch confirmation; not verified by author directly |
| [TechCrunch — "Slash raises $19M Series A"](https://techcrunch.com/2022/03/22/slash-banking-series-a/) | Third-party press | 2022-03-22 | Series A amount, lead (NEA), co-investors, pivot context | **High** | Standard reputable press; coverage corroborated by Crunchbase |
| [Goodwater Capital — "Why we led Slash's Series B"](https://www.goodwatercap.com/thesis/slash-series-b) | Investor post | 2025-03 (approx) | Series B amount ($41M), post-money ($370M), milestones ($5B volume, 20K customers) | **Medium** | Investor-authored — promotional but still a primary source for round details. Milestones are company-disclosed, not independently audited. |
| [Karat Financial site](https://www.getkarat.com) | Company page | current | Confirms Cardenas was Karat co-founder | **High** | Primary source for Cardenas's pre-Slash history |
| [TechCrunch — Karat $26M Series A](https://techcrunch.com/2021/04/01/karat-black-card-creators/) | Third-party press | 2021-04-01 | Confirms Karat-Cardenas linkage and the creator-credit thesis | **High** | Reputable press |
| [Crunchbase — Slash](https://www.crunchbase.com/organization/slash-c0e6) | Aggregator | rolling | Funding rounds aggregate, investor list | **Medium** | Crunchbase data is crowd-sourced; usually accurate for rounds but valuations are often estimated |
| [LinkedIn — Slash company page](https://www.linkedin.com/company/joinslash) | Social/professional | rolling | Headcount signal, employee names | **Medium** | LinkedIn employee count is approximate and platform-skewed |
| [joinslash.com](https://www.joinslash.com) | Company-authored | rolling | Product positioning, workspace lineup, marketing claims | **Low** | Marketing copy — every claim should be treated as 🔴 marketing until cross-verified |
| [joinslash.com/blog](https://www.joinslash.com/blog) | Company-authored | rolling | "Anonymized" customer testimonials (Marcus, Jake, etc.) | **Low** | Company-authored case studies prove only that Slash claims a result; no independent customer confirmation |
| @victorxcardenas on X | Founder social | rolling | Founder dogfooding (running 12 LLCs), product updates, vertical strategy | **Medium** | Direct founder disclosure; useful but inherently promotional |
| @joinslash on X | Company social | rolling | Customer retweets, product announcements | **Low** | Company-authored |
| Reddit r/smallbusiness, r/Entrepreneur, r/ecommerce | Customer-authored | rolling | Unfiltered customer sentiment (Slash-vs-Mercury comparisons, complaints) | **Medium** | Pseudonymous but at-scale; useful for sentiment direction, not specific dollar amounts |
| Trustpilot — Slash listing | Customer-authored | rolling | Customer ratings, KYB friction complaints | **Medium** | Review-aggregator with light moderation; small-N for Slash specifically |
| CNBC and general industry press — Synapse Financial Technologies Chapter 11 | Third-party press | 2024-04 | Industry context for Slash's 2024 banking-partner disruption | **High** | Well-reported industry event; Slash's specific exposure is inferred from BaaS-cohort pattern |
| Press coverage — Evolve Bank cybersecurity incident (LockBit, June 2024) | Third-party press | 2024-06 | Slash customer data was likely affected; Slash issued notice | **Medium** | Widely reported industry event; Slash-specific impact attested via stream-3 |
| Forbes 30 Under 30 — Finance list | Third-party press | various | Cardenas's recognition (Karat-era, not Slash-era) | **High** | Reputable list; Karat-era inclusion is verifiable, Slash-era inclusion is unverified |

---

## Sources NOT successfully used (gaps for follow-up)

The following sources should have been used and were not, either due to agent constraints or because they require direct fetch:

| Source | What it would prove | Why we don't have it |
|---|---|---|
| joinslash.com/legal/deposit-agreement | Current partner bank name, FDIC sweep details, account terms | Streams 2 and 4 couldn't fetch live; needs direct fetch in follow-up |
| joinslash.com/legal/fee-disclosure | Actual fee schedule (ACH, wire, FX markup, sub-account fees) | Same |
| BIN lookup against any Slash card screenshot | Exact card issuer + processor + network | Requires a real card BIN from Reddit/X photos |
| joinslash.com/careers job postings | Engineering stack (Marqeta vs Highnote vs Lithic, Persona vs Alloy, etc.) | Not scraped |
| Wayback Machine snapshots of joinslash.com (2022, 2024, 2026) | Marketing drift, customer-count drift, partner-bank drift, sunset features | Not pulled |
| FDIC partner search | Confirm Lead Bank's BaaS program list and Slash's inclusion | Not run |
| Founder podcast appearances (specific episodes with URLs) | Founder-disclosed metrics, methodology, customer mix | Specific episode URLs not verified in any stream |
| Glassdoor — Slash employee reviews | Operational reality, support quality, culture | Not pulled |
| G2 / Capterra / ProductHunt — Slash listings | At-scale customer sentiment + comparison | Not pulled |
| BBB record for Slash | Complaint patterns, regulatory disputes | Not pulled |

---

## Reliability framework used in this folder

- **High (✅)** — primary legal/regulatory filing, direct docs, on-chain pull, customer-authored proof, audited report, or two independent reputable presses corroborating
- **Medium (🟡)** — reputable press, investor post, founder interview, partner announcement, single-source customer testimony, aggregator-level data
- **Low (🔴)** — company marketing page, unsourced metric, cached snippet, directory profile, scraped profile, anonymous testimonial, single-source customer claim with no third-party corroboration

When in doubt, a claim is downgraded one level. For Slash specifically, anyone using this folder for a real decision (build/buy/partner/invest) should re-verify by direct fetch of joinslash.com's legal pages and at least one Wayback Machine snapshot.
