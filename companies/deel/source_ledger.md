# Deel — Source Ledger

*Compiled 2026-05-21. Source-by-source provenance for every material claim across the Deel research folder.*

---

## Source-quality summary

The Deel research run had mixed source quality:

- **Stream 1 (history/founders/funding) failed on first attempt** and returned a 6-second empty stub. A retry produced the content in `deep_dive.md`. The retry's funding-round and Rippling-lawsuit details are well-sourced; the Philippe-Bouaziz / Praxis Capital Markets sidebar and the Bouaziz-Dubai-relocation claim are weaker single-source items.
- **Stream 2 (architecture)** disclosed that live WebSearch returned limited substantive content during its run. Partner-stack identifications (Stripe Issuing vs Marqeta, KYC vendors, FX providers, treasury banks) are category-pattern inferences with explicit 🟡 labels.
- **Stream 3 (customer use cases)** disclosed that several deel.com case-study URLs were permission-blocked and that X/Twitter scraping was limited. The Andela / Yellow Card Lagos engineer flow is the strongest concretely sourced customer walkthrough; most other customer flows are illustrative-and-inferred.
- **Stream 4 (marketing-vs-reality)** ran extensive searches but the agent itself flagged that specific URLs to court filings, DOJ referrals, and certain Information/WSJ stories are "reconstructed from search results" rather than directly fetched. The macro facts (lawsuit exists, O'Brien flipped, Bouaziz personally accused under oath, $17.3B valuation, $1B ARR, acquisitions) are well-corroborated across multiple outlets.

The strongest claims in this folder: funding rounds, the YC W19 crypto-pivot story, the major acquisitions (Hofy, PaySpace, Atlantic Money, Zavvy, Capbase, Legalpad), the Rippling lawsuit existence and timeline, the $17.3B April 2025 secondary, the $1B ARR milestone. The weakest claims: specific partner-bank / card-issuer / KYC-vendor names, the exact DOJ/SFO referral status, exact Deel-owned EOR entity count, the Bouaziz Dubai relocation, partner-EOR roster.

---

## Source table

| Source | Type | Date | What it proves | Reliability | Notes |
|---|---|---|---|---|---|
| [ycombinator.com/companies/deel](https://www.ycombinator.com/companies/deel) | YC company page | current | YC W19 batch, founders Bouaziz + Wang | **High** | YC directory is authoritative for batch confirmation |
| [TechCrunch — Deel becomes a unicorn](https://techcrunch.com/2021/10/11/deel-becomes-a-unicorn-just-15-months-after-its-series-a/) | Third-party press | 2021-10-11 | Series C $50M @ $1.25B, founder backstory | **High** | Reputable press |
| TechCrunch — multiple funding-round articles (2020-2025) | Third-party press | rolling | Series A through 2025 secondary | **High** | Aggregate-level corroborated |
| [TechCrunch — $17.3B secondary tender April 2025](https://techcrunch.com/2025/04/22/deel-raises-secondary-round-at-17-3b-valuation/) | Third-party press | 2025-04-22 | Confirms $17.3B secondary | **High** (likely; URL is among stream-4 reconstructed items — re-verify) | Multiple outlets cover this |
| [Bloomberg — Deel $1B ARR milestone](https://www.bloomberg.com/news/articles/2025-01-23/deel-hits-1-billion-arr-as-ipo-speculation-mounts) | Third-party press | 2025-01-23 | $1B ARR claim, IPO speculation | **High** (likely; stream-4 reconstructed URL) | Self-reported by Deel to Bloomberg, not audited |
| [Reuters — Rippling sues Deel](https://www.reuters.com/legal/rippling-sues-deel-corporate-espionage-2025-03-17/) | Third-party press | 2025-03-17 | Rippling lawsuit filing date and core allegations | **High** | Standard reputable press; macro facts well-corroborated |
| [Bloomberg — O'Brien affidavit](https://www.bloomberg.com/news/articles/2025-06-14/deel-spy-flips-on-bouaziz-irish-court-affidavit) | Third-party press | 2025-06-14 | The O'Brien affidavit naming Alex + Philippe Bouaziz | **High** (macro), 🟡 (specific URL) | Stream-4 agent flagged URL as reconstructed; the macro story is well-attested across Bloomberg/WSJ/The Information |
| [The Information — O'Brien deposition](https://www.theinformation.com/articles/deel-mole-keith-obrien-affidavit-bouaziz) | Third-party press | 2025 | Detailed reporting on the affidavit | 🟡 | Specific URL is reconstructed; the existence of TII coverage is well-known |
| [WSJ — Deel board internal probe](https://www.wsj.com/articles/deel-board-internal-probe-rippling-lawsuit) | Third-party press | 2025 (late) | Internal investigation existence | 🟡 | Reconstructed URL |
| [FT — DOJ/SFO referrals](https://www.ft.com/content/deel-doj-sfo-referrals-rippling) | Third-party press | 2026-03 | Reported DOJ + UK SFO referrals | 🔴 | Stream-4 flagged this URL as reconstructed; no independent corroboration in `deep_dive.md`. Treat as unverified pending direct source check. |
| [CourtListener — Rippling v. Deel docket](https://www.courtlistener.com/docket/69862493/rippling-people-center-inc-v-deel-inc/) | Court records | rolling | Federal docket of the lawsuit | **High** | Authoritative if the docket ID is correct; verify on CourtListener directly |
| [Forbes — Russia contractor payments](https://www.forbes.com/sites/davidjeans/2022/03/deel-russia-contractor-payments) | Third-party press | 2022-03 | Russia/Belarus sanctions scrutiny | **High** (macro), 🟡 (specific URL path) | Macro story attested; specific path may be slightly different |
| [Sacra — Deel profile](https://sacra.com/c/deel/) | Third-party analyst | rolling | Revenue mix, entity-count estimate | **Medium** | Sacra is reputable but not audited; revenue mix is estimated |
| [Glassdoor — Deel reviews](https://www.glassdoor.com/Reviews/Deel-Reviews-E2531683.htm) | Customer/employee-authored | rolling | Culture critiques, "boiler room" descriptors | **Medium** | Self-selected reviewer pool; useful for direction, not magnitude |
| [Trustpilot — Deel reviews](https://www.trustpilot.com/review/deel.com) | Customer-authored | rolling | Contractor complaints (FX, withdrawal, KYC, account freezes) | **Medium** | Review-aggregator with light moderation; bimodal distribution |
| [Crunchbase — Deel](https://www.crunchbase.com/organization/deel) | Aggregator | rolling | Funding rounds aggregate, investor list | **Medium** | Crunchbase data is crowd-sourced |
| deel.com (homepage, product pages, pricing, About) | Company-authored | rolling | Marketing claims, "150+ countries," $49/$599 pricing | **Low** | Marketing copy — every claim 🟡 or 🔴 until cross-verified |
| deel.com/newsroom | Company-authored | rolling | Acquisition announcements (Hofy, PaySpace, Atlantic Money, etc.) | **Medium** | Press releases — facts of acquisitions are reliable, framing is promotional |
| deel.com/blog | Company-authored | rolling | Customer case studies (Shopify, Notion, Klarna, Forbes, etc.) | **Low** | Vendor-authored case studies prove only that Deel claims a result |
| developer.deel.com | Company-authored | current | API surface existence and endpoints | **Medium** | Reasonably authoritative for technical claims |
| @alexbouaziz (X) | Founder social | rolling | $1B ARR, EBITDA-positive claims, customer-milestone tweets | **Medium** | Direct founder disclosure; inherently promotional |
| @shuowang (X) | Founder social | rolling | Operational updates, country expansions | **Medium** | Same caveats |
| Yellow Card | Third-party (customer-of-customer) | current | Africa USDC off-ramp documentation supporting Andela flow | **High** | Direct documentation of the off-ramp economics |
| Reddit (/r/cscareerquestions, /r/Argentina, /r/Mexico, /r/India, /r/Brazil, /r/RemoteJobs, /r/Entrepreneur, /r/HR, /r/PayrollProfessional) | Customer-authored | rolling | Contractor + employer sentiment | **Medium** | Useful for direction, not specific dollar figures |
| G2 / Capterra reviews | Customer-authored | rolling | Side-by-side comparisons (Deel vs Rippling/Remote/G-P) | **Medium** | Self-selected, vendor-influenced |
| 20VC / Lenny's Podcast / Logan Bartlett — Bouaziz appearances | Founder interview | rolling | Pivot story, MagicBus reference, founder framing | **Medium** | Founder-narrated, inherently promotional |

---

## Sources NOT successfully used (gaps for follow-up)

The following sources should have been used and were not, either due to agent constraints or because they require direct fetch:

| Source | What it would prove | Why we don't have it |
|---|---|---|
| Live deel.com/pricing page | Current $49/$599 pricing, regional EOR variance, fee disclosure | Not fetched directly |
| Live deel.com/legal/* and trust center | Subprocessors list, SOC 2 status, named partners, FDIC sponsor for Deel Card | Not fetched |
| Live developer.deel.com | Endpoint catalog, OAuth scopes, rate limits, sandbox limitations | Not fetched |
| The actual Rippling v. Deel complaint PDF (PACER/CourtListener) | Exact allegations, specific paragraphs cited | Not fetched |
| The Keith O'Brien Irish High Court affidavit text | Direct quotes from the affidavit | Not fetched |
| Wayback Machine snapshots of deel.com (2021, 2022, 2024, 2026) | Marketing drift, country-count drift, customer-count drift | Not pulled |
| Card BIN lookup against a Deel Card image | Exact issuer + processor + network | Not run |
| Job postings on deel.com/careers | Engineering stack leaks (Marqeta vs Stripe Issuing vs Lithic, KYC vendors, etc.) | Not fetched |
| NMLS state-by-state license search | Exact Deel MTL footprint | Not run |
| FT, Information, Bloomberg, WSJ articles by direct URL | Verbatim Rippling-coverage quotes | Cited URLs are stream-4 reconstructions |
| FinCEN MSB registry | Deel's MSB registration status | Not checked |
| Deel's S-1 (when filed) | The full Bouaziz family employment disclosure, audited revenue, entity-ownership list, litigation risk factors | Not filed as of 2026-05-21 |

---

## Reliability framework used in this folder

- **High (✅)** — primary legal/regulatory filing, direct docs, on-chain pull, customer-authored proof, audited report, or two independent reputable presses corroborating
- **Medium (🟡)** — reputable press, investor post, founder interview, partner announcement, single-source customer testimony, aggregator-level data
- **Low (🔴)** — company marketing page, unsourced metric, cached snippet, directory profile, scraped profile, anonymous testimonial, single-source customer claim with no third-party corroboration

When in doubt, a claim is downgraded one level. For Deel specifically, anyone using this folder for a real decision (build/buy/partner/invest) should re-verify by direct fetch of deel.com's legal pages, the actual court filings, and at least one Wayback Machine snapshot.
