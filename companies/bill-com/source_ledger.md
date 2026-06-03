# Bill.com — Source Ledger

Source-by-source provenance for the BILL research. Reliability per playbook §1:
- **High** — primary regulatory filing, direct docs, customer-authored proof, audited report
- **Medium** — reputable press, investor post, founder interview, partner announcement
- **Low** — company marketing page, unsourced metric, cached snippet, directory profile

## Primary regulatory / financial filings (HIGH)

| Source | Type | Date | What it proves |
|---|---|---|---|
| [BILL FY2025 10-K (SEC EDGAR)](https://www.sec.gov/Archives/edgar/data/0001786352/000178635225000037/bill-20250630.htm) | 10-K | Aug 2025 | FY25 revenue $1.46B, customer count ~493.8K, float revenue $161.8M, NRR 94%, banking partners discussion, redundancy language |
| [BILL FY2024 10-K (SEC EDGAR)](https://www.sec.gov/Archives/edgar/data/0001786352/000178635224000035/bill-20240630.htm) | 10-K | Aug 2024 | FY24 revenue $1.29B, comparative data for the FY25 deceleration thesis |
| [BILL Q3 FY2026 8-K (May 2026)](https://www.sec.gov/Archives/edgar/data/0001786352/000162828026032064/bill-2026331xexx991.htm) | 8-K | May 7, 2026 | First GAAP profitability, 30% workforce reduction announcement, $1B buyback authorization, Q3 FY26 revenue $406.6M |
| [BILL Q4 FY2025 8-K](https://www.sec.gov/Archives/edgar/data/0001786352/000178635225000033/bill-20250630xexx991.htm) | 8-K | Aug 2025 | Q4 FY25 results $383M revenue, "nearly 500K SMBs", FY25 segment economics |
| [BILL Q3 FY2026 10-Q](https://www.sec.gov/Archives/edgar/data/0001786352/000162828026032387/bill-20260331.htm) | 10-Q | May 2026 | Most recent customer count, segment detail, float trajectory |
| [BILL Q1 FY2025 10-Q](https://www.sec.gov/Archives/edgar/data/0001786352/000178635224000045/Financial_Report.xlsx) | 10-Q | Nov 2024 | Funds held for customers $3.80B; FBO account composition |
| [BILL SVB Impact 8-K, March 2023](https://www.sec.gov/Archives/edgar/data/0001786352/000119312523068403/d459924dex991.htm) | 8-K | Mar 2023 | $370M of $3.3B was at SVB; remainder at "multinational bank processors" — names confirmed FBO architecture |
| [Starboard Schedule 13D filing](https://www.sec.gov/Archives/edgar/data/0001786352/000092189525002532/ex2tosc13d06297bill_09042025.htm) | 13D | Sep 4, 2025 | Starboard 8.5% stake disclosed |
| [Starboard 13D/A Sept 5, 2025](https://www.sec.gov/Archives/edgar/data/0001786352/000092189525002554/ex991to13da106297bill_090825.htm) | 13D/A | Sep 5, 2025 | Starboard nominates 4 directors |
| [8-K Oct 16, 2025 — Starboard cooperation agreement](https://www.sec.gov/Archives/edgar/data/0001786352/000119312525240860/d64649d8k.htm) | 8-K | Oct 16, 2025 | Board expanded; Feld + Kirkpatrick added; Stephen Fisher resignation |
| [SEC 8-K Divvy acquisition](https://www.sec.gov/Archives/edgar/data/0001786352/000156459021024959/bill-ex991_6.htm) | 8-K | May 2021 | $2.5B Divvy deal mechanics — $625M cash + $1.875B stock |
| [SEC 8-K Invoice2go acquisition](https://www.sec.gov/Archives/edgar/data/0001786352/000119312521263249/d187351d8k.htm) | 8-K | Sept 2021 | $625M Invoice2go deal mechanics |

## Direct BILL documentation (HIGH for product docs, MEDIUM-LOW for marketing)

| Source | Type | Reliability | What it proves |
|---|---|---|---|
| [developer.bill.com v3 reference](https://developer.bill.com/reference/api-reference-overview) | API docs | High | API base URLs, auth model, session timeout, endpoints |
| [BILL v3 API getting started](https://developer.bill.com/docs/bill-v3-api-get-started) | API docs | High | Sandbox vs prod base URLs, devKey + organizationId model |
| [BILL API rate limits](https://developer.bill.com/docs/api-rate-limits) | API docs | High | Hourly cap, error BDC_1144, exponential retry pattern |
| [BILL Spend & Expense API authentication](https://developer.bill.com/docs/authentication-with-api-token) | API docs | High | Separate token-based auth for S&E vs core API |
| [BILL Help Center — clearing account](https://help.bill.com/direct/s/article/115005449786) | Product docs | High | FBO clearing account mechanics, daily $0 sweep model |
| [BILL Help Center — payment timing](https://help.bill.com/direct/s/article/115005322726) | Product docs | High | 1-3 business day floats verified |
| [BILL Help Center — connect to vendor / ePayments](https://help.bill.com/direct/s/article/115005307443) | Product docs | High | Network member-to-member matching mechanics |
| [BILL Help Center — virtual card FAQ](https://help.bill.com/direct/s/article/360021237411) | Product docs | High | Visa + Mastercard both supported |
| [BILL Security page](https://www.bill.com/security) | Marketing/security | Medium | SOC 1/2 Type II, FinCEN MSB, 50-state MTL list (verified externally) |
| [BILL Pricing page](https://www.bill.com/product/pricing) | Marketing | Medium | $45/$55/$79-89/custom tier list |
| [BILL Accountant Partner Program](https://www.bill.com/accountant-partner-program) | Marketing | Medium | $49/month Console; tier structure |
| [BILL Accountant Resource Center — benefits](https://www.bill.com/accountant-resource-center/articles/your-accountant-partner-program-benefits) | Marketing | Medium | Bronze/Silver/Gold/Platinum tier points; $500 referral |
| [BILL Connect for banks](https://www.bill.com/banks) | Marketing | Medium | Named bank partners JPM Chase, Wells, PNC, KeyBank, Commerce, FNBO |
| [BILL Network Payments](https://www.bill.com/product/network-payments) | Marketing | Low | 8M member claim (definition: any vendor BILL has paid) |
| [BILL AI product page](https://www.bill.com/product/ai) | Marketing | Low | "250M+ trained" claim; 80% / 89% / 99% / 75% metrics — methodology unstated |
| [BILL "Friction Crisis" blog Feb 2026](https://www.bill.com/blog/the-future-of-finance-is-touchless) | Marketing | Low | 250M invoice claim first surfaced here |
| [BILL Press release — Oct 2025 AI Agents](https://www.bill.com/press-release/bill-launches-new-ai-agents) | Press | Medium | W-9 Agent, Touchless Receipts, Invoice Coding Agent launched Oct 28, 2025 |
| [BILL Finmark acquisition press](https://www.bill.com/press-release/bill-acquire-finmark) | Press | Medium | Finmark deal announcement Nov 2022 |
| [BILL Divvy completion press](https://www.bill.com/press-release/billcom-completes-acquisition-divvy) | Press | High | Closed June 1, 2021 confirmed |
| [BILL Invoice2go completion press](https://www.bill.com/press-release/billcom-completes-acquisition-invoice2go) | Press | High | Closed Sept 1, 2021 confirmed |
| [BILL Spend & Expense rebrand blog](https://www.bill.com/blog/divvy-becoming-bill-spend-and-expense) | Marketing | Medium | Sept 2023 rebrand of Divvy → BILL Spend & Expense |
| [BILL leadership: René Lacerte](https://www.bill.com/leadership/rene-lacerte) | Marketing | Medium | Lacerte bio: Stanford BS/MS Industrial Eng, 5 years at Intuit, PayCycle founder |

## Customer case studies (LOW — BILL-authored)

These prove that BILL claims a customer and a result. They do not independently prove the metric.

- [Armanino case study](https://www.bill.com/case-study/customer-success-story-armanino) — 30% time reduction, 9.6 work-weeks/year
- [Bookkeeper360 case study](https://www.bill.com/case-study/customer-success-story-bookkeeper360) — 130 hrs/month claim
- [ThinkLeader, Supporting Strategies, Lindsay Leasing, Mubarak, Mark Cuban Companies, Love Catering, O&M Restaurant Group, Lescault & Walderman, hiline, Blue Fox, MBS, Furey, Accountfully/BELAY case studies](https://www.bill.com/case-study) — all BILL-authored

## Third-party press and analysts (MEDIUM)

| Source | Type | Reliability | What it proves |
|---|---|---|---|
| [TechCrunch IPO coverage Dec 2019](https://techcrunch.com/2019/12/12/bill-coms-ipo-pricing-is-good-news-for-unprofitable-startups/) | Press | Medium | $22 IPO price, $37.25 open, +61% close |
| [Bill.com Wikipedia](https://en.wikipedia.org/wiki/Bill.com) | Reference | Medium | Founding history; Cashboard → Cashview → Bill.com timeline |
| [Fortune Leadership Next March 2024](https://fortune.com/2024/03/13/leadership-next-bill-ceo-rene-lacerte/) | Press | Medium | Lacerte family lineage, "fourth-generation entrepreneur" framing |
| [Inc. magazine June 2004 "Runs in Family"](https://www.inc.com/magazine/20040601/runsinthefamily.html) | Press | Medium | Pre-Bill.com Lacerte family background |
| [Mixergy — Lacerte interview](https://mixergy.com/interviews/rene-lacerte-bill-interview/) | Founder interview | Medium | PayCycle 1999-2009, Intuit acquisition for ~$170M |
| [DCM Ventures — Bill.com lesson in patient capital](https://medium.com/the-global-frontier/bill-com-a-lesson-in-patient-capital-1b36d10a14b8) | Investor post | Medium | DCM as early-stage lead investor |
| [Emergence Capital — Bill.com road to Wall Street](https://www.emcap.com/thoughts/bill-com-lessons-from-the-road-to-wall-street) | Investor post | Medium | Series B lead Sep 2007 |
| [PYMNTS — BILL Series H + Mastercard partnership 2019](https://www.pymnts.com/news/b2b-payments/2019/bill-com-funding-mastercard-virtual-cards-accounts-payable/) | Press | Medium | Mastercard equity + commercial partnership; $1B+ post-money valuation |
| [Macrotrends BILL stock history](https://www.macrotrends.net/stocks/charts/BILL/bill-holdings/stock-price-history) | Data | High | Stock prices verified; $342.26 ATH Nov 9, 2021 |
| [Public.com BILL market cap](https://public.com/stocks/bill/market-cap) | Data | Medium | $3.83-3.94B market cap as of June 1, 2026 |
| [stockanalysis.com BILL revenue 2018-2025](https://stockanalysis.com/stocks/bill/revenue/) | Data | High | FY20-FY25 revenue verified |
| [Payments Dive — Bank of America relationship 2024](https://www.paymentsdive.com/news/bill-holdings-bank-of-america-SMB-digital-payments-contract/707238/) | Press | High | BoA confirmed banking partner; relationship being revamped |
| [Payments Dive — Starboard / Bill restructuring](https://www.paymentsdive.com/news/bill-holdings-starboard-workforce-reduction/803120/) | Press | High | Layoff connection to activist pressure |
| [Payments Dive — BILL ends Intuit partnership 2023, Melio takes QB Bill Pay](https://www.paymentsdive.com/news/bill-intuit-partnership-embedded-payments-smb-competition-b2b/691269/) | Press | High | BILL lost the Intuit embed in 2023 — important top-of-funnel loss |
| [Hedgeweek — Starboard 8.5% stake](https://www.hedgeweek.com/starboard-to-launch-bill-holdings-board-challenge-after-building-8-5-stake/) | Press | High | Starboard activist context |
| [Hedgeweek — Barington pushes sale](https://www.hedgeweek.com/barington-takes-stake-in-bill-holdings-and-pushes-for-sale/) | Press | High | Barington activist context |
| [Sahm Capital — Elliott Management stake](https://www.sahmcapital.com/news/content/bill-holdings-shares-soar-on-elliott-management-stake-is-an-activist-battle-brewing-2025-09-10) | Press | Medium | Elliott activist context |
| [Investing.com — Hellman & Friedman acquisition talks](https://www.investing.com/news/stock-market-news/bill-holdings-stock-soars-on-potential-acquisition-talks-with-hellman--friedman-93CH-4491545) | Press | Medium | PE bidder name |
| [Bankrate / Merchant Maverick — Divvy card review](https://www.bankrate.com/credit-cards/reviews/divvy-business-card/) | Press | High | Cross River Bank as card issuer confirmed |
| [Salt Lake Tribune — Divvy deal](https://www.sltrib.com/news/2021/05/10/divvy-utah-financial-tech/) | Press | Medium | Divvy founder Blake Murray, Utah HQ context |
| [BusinessWire — Finmark acquisition](https://www.businesswire.com/news/home/20221103006281/en/BILL-to-Acquire-Finmark-a-Financial-Planning-and-Analysis-Software-Company) | Press | Medium | Finmark deal announcement Nov 3, 2022; Rami Essaid context |
| [Motley Fool — Q3 FY2026 earnings call transcript](https://www.fool.com/earnings/call-transcripts/2026/05/08/bill-bill-q3-2026-earnings-call-transcript/) | Transcript | High | Lacerte's current strategy narrative, GAAP profitability claim, mid-market pivot |
| [Insider Monkey — Q2 FY2025 transcript](https://www.insidermonkey.com/blog/bill-com-holdings-inc-nysebill-q2-2025-earnings-call-transcript-1446056/) | Transcript | High | Accountant-channel growth metrics; channel-revenue framing |
| [CPA Practice Advisor — Feb 2026 AI release](https://www.cpapracticeadvisor.com/2026/02/10/bill-releases-new-and-enhanced-ai-agents/177829/) | Press | Medium | Second wave AI agents launch |
| [CPA Practice Advisor — Divvy rename Sept 2023](https://www.cpapracticeadvisor.com/2023/09/07/divvy-renamed-as-bill-spend-expense/94305/) | Press | Medium | Spend & Expense rebrand details |
| [Finovate — Procurement April 2025](https://finovate.com/bill-launches-new-procurement-capabilities-for-small-businesses/) | Press | Medium | BILL Procurement launch context |
| [Mergr — Lacerte Software acquired by Intuit 1998](https://mergr.com/lacerte-software-acquired-by-intuit) | Reference | Medium | 1998 acquisition for ~$400M cash |
| [Tax Notes — Intuit/Lacerte release](https://www.taxnotes.com/research/federal/other-documents/washington-roundup/intuit-release-on-acquiring-lacerte/11wlr) | Press | Medium | Cross-reference for Lacerte Software Intuit deal |
| [PR Newswire — NetSuite + BILL IPA](https://www.prnewswire.com/news-releases/netsuite-and-bill-partner-to-accelerate-accounts-payable-processes-302577217.html) | Press | High | NetSuite IPA partnership Oct 2025 |
| [PR Newswire — Ramp $32B valuation](https://www.prnewswire.com/news-releases/ramp-reaches-32-billion-valuation-doubling-revenue-and-customers-in-past-year-302616510.html) | Press | High | Ramp competitive context |
| [TechCrunch — Mercury Bill Pay launch](https://techcrunch.com/2024/05/07/startup-neobank-mercury-is-taking-on-brex-and-ramp-with-new-bill-pay-spend-management-software/) | Press | High | Mercury "no middleman" pitch context |
| [Intuit press — QuickBooks Bill Pay](https://investors.intuit.com/news-events/press-releases/detail/30/intuit-introduces-quickbooks-bill-pay-expanding-money-platform-to-deliver-business-to-business-payments-with-ap-automation) | Press | High | Native QB Bill Pay competitive threat |
| [Stocktitan — May 2026 8-K, 30% layoff, $1B buyback](https://www.stocktitan.net/sec-filings/BILL/8-k-bill-holdings-inc-reports-material-event-a30cd671905e.html) | Filing summary | High | Layoff + buyback figures |

## Practitioner / customer-experience sources (MEDIUM, but important)

| Source | Type | Reliability | What it proves |
|---|---|---|---|
| [Trustpilot BILL reviews](https://www.trustpilot.com/review/bill.com) | Reviews | Medium (aggregate) | 3.1/5; consistent pattern on ACH delays, CS quality, holds |
| [BBB BILL complaints](https://www.bbb.org/us/ca/alviso/profile/payment-processing-services/billcom-llc-1216-1000005293/complaints) | Complaints | Medium | Specific account-freeze incidents, fund-hold patterns |
| [G2 BILL AP/AR reviews](https://www.g2.com/products/bill-ap-ar/reviews) | Reviews | Medium (aggregate) | Pricing complaints, sync break complaints, support complaints |
| [Stampli — BILL reviews compendium](https://www.stampli.com/blog/accounts-payable/bill-com-reviews/) | Competitor analysis | Low (competitor) | Verified complaint patterns; biased but factually grounded |
| [MakersHub — Why BILL isn't working for modern AP teams](https://makershub.ai/discover/blog/why-bill-com-isnt-working-for-modern-ap-teams) | Competitor analysis | Low (competitor) | Header-only capture critique, line-item limitations |
| [Ramp — Customers who switched from BILL to Ramp](https://ramp.com/blog/accounts-payable/customers-who-switched-from-bill-to-ramp) | Competitor marketing | Low | Mix Talent case; "rising fees" pattern |
| [Ramp — Top BILL alternatives](https://ramp.com/blog/top-bill-alternatives) | Competitor marketing | Low | Competitive framing |
| [Tekpon — BILL Pricing 2026](https://tekpon.com/software/bill-com/pricing/) | Independent | Medium | Independent corroboration of pricing tiers |
| [Vendr marketplace — BILL pricing](https://www.vendr.com/marketplace/bill-com) | Independent | Medium | Procurement-side pricing reality (discount data) |
| [hhhypergrowth — BILL deep dive](https://hhhypergrowth.com/a-bill-com-deep-dive/) | Investor analysis | Medium | Independent fundamental analysis |
| [Sacra — Ramp profile](https://sacra.com/c/ramp/) | Analyst | Medium | Ramp's TPV growth data ($22.3B → $57B) for competitive context |
| [Interviewpal — BILL layoffs](https://www.interviewpal.com/layoffs/bill) | Data aggregator | Medium | 709 jobs cut figure |
| [Layoffhedge — BILL Holdings layoff history](https://layoffhedge.com/company/bill-holdings) | Data aggregator | Medium | Historical layoff timeline |

## Founder podcast transcripts (HIGH for non-marketing facts)

All saved as .txt files in `/Users/fuyofulo/research/ai_crypto/companies/bill-com/transcripts/`:

| File | YouTube URL | Date | What it proves |
|---|---|---|---|
| `fintech-leaders-lacerte-bill-history-2025-11.txt` | https://www.youtube.com/watch?v=rP0hV4QRhtg | Nov 2025 | Lacerte's strategic narrative around Intuit / PayCycle / why-BILL-can't-be-built-internally-by-incumbents |
| `cnbc-lacerte-ipo-debut-2019-12.txt` | https://www.youtube.com/watch?v=gO2zE6i3RIw | Dec 2019 | IPO day positioning, "fundamentals not hype" framing |
| `leadership-lacerte-building-bill.txt` | https://www.youtube.com/watch?v=5WtMmTDeSsw | n/a | Hardest part of building BILL — leadership lessons |
| `ice-house-lacerte-ipo-paper-checks-2020-02.txt` | https://www.youtube.com/watch?v=Hijh-ofQA8s | Feb 2020 | "90% paper checks" stat origin; family DNA quote about Lacerte's father |
| `armanino-lacerte-fortune-5-million.txt` | https://www.youtube.com/watch?v=PkibzEu9ey8 | n/a | "Fortune 5 Million" positioning origin |
| `bill-20yr-journey-billion-revenue.txt` | https://www.youtube.com/watch?v=eTmyui5WLaQ | n/a | 20-year arc, punch-cards-to-IPO story |
| `lacerte-one-stop-shop-accounting.txt` | https://www.youtube.com/watch?v=nR4DdIh7QYk | n/a | One-stop-shop accounting framing |
| `bill-lacerte-founder-ceo-interview.txt` | https://www.youtube.com/watch?v=L6OwzSTu0oQ | n/a | Bill.com founder/CEO interview |

**Failed transcript fetches (kome.ai returned no transcript available):**
- https://www.youtube.com/watch?v=ebZ75nQPQ3I (Fortt Knox 2020)
- https://www.youtube.com/watch?v=gtvV9xS85UE (Fortt Knox Update 2024)

## Reliability summary

- **Primary regulatory filings** (10-K, 10-Q, 8-K, 13D) ground all financial and strategic facts.
- **Direct BILL product/API docs** ground architectural facts (clearing accounts, payment flow, API).
- **Founder podcast transcripts** ground founding-story facts and surface candid commentary not in marketing.
- **Third-party press** (Payments Dive, TechCrunch, Fortune, Bloomberg-adjacent) corroborates events and timing.
- **Customer reviews** (Trustpilot, BBB, G2) ground the customer-experience reality — used in aggregate, not as single anecdotes.
- **Competitor marketing** (Ramp, Mercury, Stampli, MakersHub) is used carefully — facts are usually verifiable; framing is biased.
- **BILL marketing** (homepage, blog, AI page, press releases) is treated as LOW reliability when the claim has no methodology disclosed.

The single biggest source weakness: BILL deliberately does not publish a complete list of FBO custodian banks. The FBO architecture is verified; the specific bank distribution is partial inference.
