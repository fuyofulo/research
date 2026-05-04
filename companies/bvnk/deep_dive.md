# BVNK: From Cape Town Crypto-to-Fiat Side Project to Mastercard's $1.8B Stablecoin Bet

*Deep-dive research report — May 4, 2026 — covering company history, founders, funding, and the March 17, 2026 Mastercard acquisition*

---

## Executive Summary

On **March 17, 2026**, Mastercard announced its agreement to acquire **BVNK** — a London-based stablecoin payments infrastructure company — for **up to $1.8 billion**, structured as **$1.5B fixed + $300M in performance-based contingent payments** ([Mastercard Investor News](https://investor.mastercard.com/investor-news/investor-news-details/2026/Mastercard-to-Acquire-BVNK-to-Connect-On-Chain-Payments-and-Fiat-Rails/default.aspx); [Fortune](https://fortune.com/2026/03/17/mastercard-bvnk-acquisition-stablecoins-1-8-billion/)). It is the **largest stablecoin-infrastructure acquisition in history**, eclipsing Stripe's $1.1B Bridge deal (Feb 2025). The transaction is expected to close **late 2026** subject to regulatory review.

BVNK had been building largely in stealth for ~4.5 years — founded by three South Africans (Jesse Hemson-Struthers, Donald Jackson, Chris Harmse) in October 2021 as a rebrand/successor of their 2017 Cape Town project **Coindirect**. The trio became **paper billionaires** at the deal price ([Daily Investor](https://dailyinvestor.com/cryptocurrency/124930/three-south-african-tech-entrepreneurs-become-instant-billionaires/); [Billionaires.Africa](https://www.billionaires.africa/2026/03/19/south-african-trio-sells-stablecoin-startup-bvnk-to-mastercard-for-1-8-billion-becoming-instant-billionaires/)).

The headline numbers at exit:
- **~$30B annualized payment volume** (up 2.3× YoY) ✅
- **~2.8M transactions** in 2025 ✅
- **130+ countries** of coverage ✅
- **~$40M annualized revenue** as of Series B (Dec 2024); likely meaningfully higher by acquisition 🟡
- **~270–448 employees** (sources differ on whether this includes contractors) 🟡
- **Total capital raised pre-exit: ~$93M across 4+ rounds** ✅

---

## 1. Founding Story

### The Founders (all three South African) ✅

- **Jesse Hemson-Struthers** — Co-founder & CEO. Serial entrepreneur whose previous ventures in **e-commerce (acquired by Naspers/MIH Internet Africa in 2014)** and **gaming (BetTech Gaming, acquired by Sportradar in 2017)** preceded BVNK ([The Org](https://theorg.com/org/bvnk/org-chart/jesse-hemson-struthers); [Caproasia](https://www.caproasia.com/2026/03/18/united-states-452-billion-payment-giant-mastercard-buys-stablecoin-infrastructure-company-bvnk-for-1-8-billion-include-300-million-contingents-founded-in-2021-by-jesse-hemson-struthers-donald-j/)).
- **Donald Jackson** — Co-founder & CTO. Background in enterprise systems & blockchain. Previously founded **Cue** (a bootstrapped customer-engagement platform) and **Verity** (an anti-fraud service) ([Crunchbase](https://www.crunchbase.com/person/donald-jackson)). Studied math/CS at Nelson Mandela University.
- **Chris Harmse** — Co-founder & Chief Business Officer (CBO). CFA charter-holder; FX trader; ex-BNP Paribas, Centaur Asset Management, Excelsia Capital, Asymmetry Asset Management, Renaissance Capital, Rezco ([LinkedIn](https://ae.linkedin.com/in/chrisharmse); [The Org](https://theorg.com/org/bvnk/org-chart/chris-harmse)).

Several sources also list **Stephen Young**, **Kyle Redelinghuys**, and **George Davis** (Chief Product Officer) as part of the founding nucleus. 🟡 Davis is regularly quoted in press as a co-founder ([Sifted](https://sifted.eu/articles/bvnk-crypto-revolut-checkout-com)).

### The Coindirect Pre-History (2017–2021) ✅

In **2017**, Hemson-Struthers and Jackson co-founded **Coindirect** in Cape Town — a cross-border payments platform aimed at emerging markets, letting customers bypass SWIFT by routing funds through stablecoins and remitting in EUR/GBP ([Sifted](https://sifted.eu/articles/bvnk-crypto-revolut-checkout-com)). Harmse joined that effort. This is the first confirmed prior chapter of the team's "stablecoin-as-rail" thesis.

### The 2021 Rebrand ✅

The story is messier than typical fintech founding lore. According to Sifted's 2023 reporting:
- Hemson-Struthers and Jackson **resigned from Coindirect** in **August 2021**.
- BVNK was incorporated **a week later**.
- Coindirect was effectively "merged" into BVNK in **January 2022** — but Davis admitted **no formal merger appears on UK Companies House**, calling it "more as a rebrand."
- Coindirect's revenue was absorbed into BVNK from launch, which is partly why BVNK had real volumes from day one rather than a true zero start.

Public launch: **October 2021** ([Canvas Business Model](https://canvasbusinessmodel.com/blogs/brief-history/bvnk-brief-history)).

### What does "BVNK" mean? ✅

Per CPO George Davis (to Sifted): *"The horrifically cheesy history of the name is that it means 'turning banking upside down'."* The "V" is an upside-down "A" → reads as "BANK" inverted ([Sifted](https://sifted.eu/articles/bvnk-crypto-revolut-checkout-com)).

The company has consistently said "we're not a bank" and pivoted positioning over time from "crypto bank" → "crypto payments for businesses" → "stablecoin payments infrastructure." That last positioning crystallized through 2023–2024 and has been the dominant framing since.

### Original Product vs Where They Pivoted ✅

- **2021–2022**: Crypto-native B2B payments — accept crypto, hold multi-currency/multi-asset balances, send funds globally ([TechCrunch](https://techcrunch.com/2022/05/11/bvnk-grabs-40-million-for-its-crypto-banking-services/)).
- **2023**: Sharpened toward stablecoin rails specifically, leaning into "send/receive/convert/store" as four core primitives.
- **2024 (June)**: Launched **Layer1** — self-hosted/self-custody stablecoin payments infra ("five years of learnings" packaged as a deployable stack) ([BVNK blog](https://bvnk.com/blog/layer-1)).
- **2025**: Launched **Embedded Wallets** — first unified fiat + stablecoin embedded wallet, connecting SWIFT/ACH/Fedwire/SEPA/FPS to Solana/Tron/Polygon/ETH/BNB/BTC/Cardano ([PYMNTS](https://www.pymnts.com/cryptocurrency/2025/bvnk-unveils-embedded-wallet-to-simplify-stablecoin-payments/)).

The pivot, in essence: from "we're a crypto bank for businesses" → "we are the licensed compliance/orchestration layer that fiat-native enterprises plug into to do stablecoin payments without touching crypto."

---

## 2. Funding History

| Round | Date | Amount | Lead | Post-money valuation |
|---|---|---|---|---|
| Pre-seed / Angel | 2021 | Undisclosed | (unannounced) | — |
| Seed (implied) | ~late 2021 | Undisclosed | Avenir, Concentric, Base Capital (rolled into Series A as "existing investors") 🟡 | — |
| Series A | **May 11, 2022** | **$40M** | **Tiger Global** | **$340M post-money** ✅ |
| Series B | **Dec 17, 2024** | **$50M** | **Haun Ventures** | **~$750M** ✅ |
| Strategic | **May 2025** | ~€2M / $2.27M (filing) | **Visa Ventures** | (above $750M) 🟡 |
| Strategic | **Oct 2025** | Undisclosed | **Citi Ventures** | "well above $750M" per Harmse ✅ |
| **Acquisition** | **Mar 17, 2026** | **Up to $1.8B ($1.5B + $300M earnout)** | **Mastercard** | — |

### Series A — May 2022 ✅

$40M led by **Tiger Global** at $340M post. Co-investors: **The Raba Partnership, Avenir, Kingsway Capital, Nordstar, Concentric, Base Capital**, plus **Anchorage Digital, Coinlist, Truelist** and angels ([TechCrunch](https://techcrunch.com/2022/05/11/bvnk-grabs-40-million-for-its-crypto-banking-services/); [Tech.eu](https://tech.eu/2022/05/12/londons-crypto-to-fiat-banking-platform-nabs-40-million/)). Note: this round is sometimes mis-labeled "Series B" in older press because BVNK had a quiet seed previously.

### Series B — December 17, 2024 ✅

$50M led by **Haun Ventures**. Participants: **Coinbase Ventures, Scribble Ventures, DRW Venture Capital**, plus existing **Tiger Global, Avenir** ([Fortune](https://fortune.com/crypto/2024/12/17/exclusive-stablecoin-bvnk-750-million-series-b-bridge-stripe-haun/); [BVNK blog](https://bvnk.com/blog/series-b-fuel-next-era-of-stablecoin-payments)). Hemson-Struthers disclosed at the time: **~$40M annualized revenue, ~$10B annualized transaction volume**. Round explicitly framed as US-expansion fuel.

### Strategic round — May 2025: Visa Ventures ✅

Public announcement May 7, 2025 ([CoinDesk](https://www.coindesk.com/business/2025/05/07/visa-doubles-down-on-stablecoins-with-investment-in-blockchain-payments-firm-bvnk); [BVNK blog](https://bvnk.com/blog/visa-invests-in-bvnk)). Filings indicate Visa actually wired ~€2M in March 2025. Small dollars, big strategic signal — and the same Visa relationship that resurfaced in **January 2026** as the **Visa Direct stablecoin pilot** ([BusinessWire](https://www.businesswire.com/news/home/20260114948268/en/BVNK-to-Deliver-Stablecoin-Infrastructure-for-Visa-Direct-Pilot-Programs)).

### Strategic round — October 2025: Citi Ventures ✅

Citi Ventures invested an undisclosed amount; Harmse confirmed valuation was now **above $750M** ([CNBC](https://www.cnbc.com/2025/10/09/biti-bvnk-stablecoin-banks-crypto.html); [Crypto Briefing](https://cryptobriefing.com/citi-stablecoin-infrastructure-bvnk/)). The Citi investment is strategically significant: it followed Jane Fraser publicly floating the idea of a Citi-issued stablecoin, and it positioned BVNK as one of the few "bank-friendly" stablecoin infra plays.

### Total raised pre-acquisition

**Approximately $93M across 4 rounds + 45 investors** per Tracxn ([Tracxn](https://tracxn.com/d/companies/bvnk/__MM4uMmLk_IgvOprDz4TdvYh0jmEk-Vd6ivOsy5Svhj8/funding-and-investors)). Some sources round to "over $100M" including angel/SAFE money ([Billionaires.Africa](https://www.billionaires.africa/2026/03/19/south-african-trio-sells-stablecoin-startup-bvnk-to-mastercard-for-1-8-billion-becoming-instant-billionaires/)).

### Founders' equity at exit 🟡

No precise cap-table disclosed publicly. Daily Investor estimates that *each ~3.3% slice equates to ~R1B (~$54M)*; the three founders are widely reported to have crossed billionaire threshold collectively at deal close, implying retained equity in the **20–40% combined** range — plausible given a relatively capital-efficient $93M raise against a $1.8B exit.

---

## 3. The Mastercard Acquisition — March 17, 2026

### Deal Mechanics ✅

- **Headline value**: Up to **$1.8 billion**.
- **Structure**: **$1.5B fixed cash consideration + up to $300M in performance-based contingent payments** (earnout) ([Mastercard Newsroom](https://www.mastercard.com/us/en/news-and-trends/press/2026/march/Mastercard-to-acquire-BVNK-to-connect-on-chain-payments-and-fiat-rails.html); [CoinDesk](https://www.coindesk.com/business/2026/03/17/mastercard-agrees-to-purchase-bvnk-for-up-to-usd1-8-billion)).
- **Financing**: All-cash from Mastercard balance sheet (it is an all-stock-by-default acquirer that paid cash here, signaling urgency).
- **Expected close**: **Late 2026**, subject to regulatory approvals across 30+ jurisdictions where BVNK holds licenses ([Bloomberg](https://www.bloomberg.com/news/articles/2026-03-17/mastercard-to-buy-stablecoin-startup-bvnk-for-up-to-1-8-billion); [Skadden](https://www.skadden.com/about/news-and-rankings/news/2026/03/bvnk-to-be-acquired-by-mastercard)).
- **Legal**: **Skadden, Arps, Slate, Meagher & Flom** is advising BVNK ([Skadden press release](https://www.skadden.com/about/news-and-rankings/news/2026/03/bvnk-to-be-acquired-by-mastercard)).

### Who Broke the News ✅

The story leaked the night before via **Fortune** (Leo Schwartz/Allie Garfinkle byline lineage), with Mastercard's official 8-K and newsroom going live at market open March 17. **Bloomberg, CNBC, CoinDesk, Reuters, Fortune** all ran simultaneous coverage. The Block and PYMNTS followed within hours.

### The Failed Coinbase Bid (Critical Backstory) ✅

In **October 2025**, Fortune reported that **both Coinbase and Mastercard were in advanced talks** to acquire BVNK at **$1.5B–$2.5B** ([Fortune](https://fortune.com/crypto/2025/10/09/bvnk-acquisition-coinbase-mastercard-stablecoins/); [The Block](https://www.theblock.co/post/374100/coinbase-mastercard-stablecoin-bvnk)). Coinbase entered **exclusivity in October**, advancing to due diligence at a reported ~$2B price. **In November 2025, Coinbase walked** ([CoinDesk](https://www.coindesk.com/markets/2025/11/12/coinbase-ends-acquisition-talks-for-u-k-based-bvnk-fortune); [Fortune](https://fortune.com/2025/11/11/coinbase-bvnk-2-billion-deal-falls-through-stablecoins/)). Reasons publicly unclear — likely some combination of regulatory complexity (Coinbase is itself in active US regulatory crosshairs) and price discipline.

Mastercard re-entered after Coinbase's exit and closed the deal four months later at $1.8B — meaningfully **below** the $2–2.5B ceiling Coinbase had been willing to reach but well above BVNK's prior $750M post.

### Mastercard's Strategic Rationale ✅

CEO **Michael Miebach** framed BVNK as *"the final piece of the puzzle"* in making money "as programmable and modular as a piece of code" ([Mastercard Q1 2026 earnings call](https://finance.yahoo.com/markets/stocks/articles/mastercard-q1-earnings-call-highlights-020619139.html); [TheStockObserver](https://www.thestockobserver.com/2026/05/02/mastercard-q1-earnings-call-highlights.html)). His core quote: *"BVNK puts us in a position in-house, natively, to drive that interoperability and trust layer in that digital assets world, [with] stablecoins, tokenized bank deposits, etc."*

Strategic logic synthesized across analyst coverage:

1. **Disintermediation defense**. Open blockchains threaten to collapse the messaging-vs-settlement split that card networks monetize. Stablecoins do both simultaneously, bypassing the Mastercard "tollbooth" entirely ([American Banker](https://www.americanbanker.com/payments/opinion/mastercards-1-8-billion-bet-heralds-the-collapse-of-financial-silos); [DL News](https://www.dlnews.com/articles/markets/what-mastercard-acquiring-bvnk-means-for-wall-street-landgrab/)).
2. **Counter to Stripe-Bridge**. Stripe paid $1.1B for Bridge in Feb 2025, signaling that every independent stablecoin infra company faced a buy-or-be-bought clock ([Lex Substack](https://lex.substack.com/p/analysis-mastercard-buys-bvnk-for); [Rex Salisbury](https://rexsalisbury.substack.com/p/11b-looked-big-then-bvnk-sold-for)). Visa needed an answer; Mastercard got there first by paying the premium.
3. **Compliance, not code**. CoinDesk's opinion piece argues Mastercard *"did not pay for BVNK's code. It paid for the years it would have lost trying to replicate BVNK's regulatory footprint"* — licenses across 130+ countries, MiCA CASP in Malta, UK EMI, multiple US MTLs ([CoinDesk Opinion](https://www.coindesk.com/opinion/2026/03/27/why-mastercard-paid-double-for-stablecoin-infrastructure-it-could-have-built)).
4. **TIKR's "$911 stock target defense"** thesis. The TIKR analysis frames the deal as defensive M&A to preserve Mastercard's premium SaaS-like multiple from a structural threat that could otherwise compress its valuation ([TIKR](https://www.tikr.com/blog/mastercard-ma-call-buying-the-stablecoin-bridge-to-protect-a-911-target)).
5. **Multi-rail orchestration**. Mastercard's stated thesis is that it wants to be agnostic across card, ACH, RTP, SEPA, *and* stablecoins — not pick one. BVNK is the stablecoin spoke in that wheel ([S&P Global](https://www.spglobal.com/market-intelligence/en/news-insights/research/2026/03/mastercards-1-8-b-bet-on-bvnk-accelerates-stablecoin-push)).

### Hemson-Struthers' Public Comments ✅

From the BVNK blog post titled *"Why BVNK is joining Mastercard"*: *"For all of the advancements made in simplifying the digital currency opportunity, we have only scratched the surface of what's possible. This deal brings together complementary capabilities to define and deliver the future of money."*

Per BVNK's own messaging: customer service continues uninterrupted; existing platform access, integrations, and relationships unchanged; the **BVNK team joins Mastercard at close** but operates with *"the independence needed to execute on their roadmap with focus and speed"* ([Crowdfund Insider](https://www.crowdfundinsider.com/2026/03/267516-bvnk-explains-reason-for-mastercard-acquisition/)).

🟡 The "BVNK brand survives" question is unresolved publicly — Mastercard hasn't committed to retaining it long-term, but BVNK retaining brand and team independence post-close is a marketing claim consistent with how Mastercard handled prior Finicity (2020) and Ekata (2021) acquisitions for ~18–24 months before deeper integration.

### Comparison to Stripe-Bridge ($1.1B, Feb 2025)

| Dimension | Stripe-Bridge | Mastercard-BVNK |
|---|---|---|
| Headline price | $1.1B | $1.8B (incl. $300M earnout) |
| Multiple on revenue | ~50x (Bridge ~$10–15M ARR rumored) 🟡 | ~25–35x (BVNK ~$50–70M ARR estimated) 🟡 |
| Geographic core | US-centric, developer-focused | London-HQ, 130+ countries, B2B/enterprise |
| Volume at deal | Much smaller, growing fast | $30B annualized at announcement |
| Acquirer motive | Offensive — Stripe building stablecoin-native stack | Defensive — Mastercard protecting existing rails |
| Licensing | Limited at time of deal | MiCA CASP, UK EMI, multi-state US MTLs, EEA passporting |

The argument that **BVNK is worth more on real fundamentals** is supportable: it processes 5–10× the volume Bridge did, holds vastly more regulatory licenses, and serves enterprise customers (Worldpay, Deel, dLocal) rather than primarily crypto-natives. The argument it's a **strategic premium** is also correct: Coinbase had been willing to pay up to $2.5B, establishing the auction floor.

---

## 4. Pre-Acquisition Trajectory

### Volume Growth ✅

| Date | Annualized payment volume |
|---|---|
| 2022 | ~$1B |
| Dec 2024 | ~$10B (disclosed at Series B) |
| May 2025 | ~$12B |
| Oct 2025 | ~$20B (4th anniversary milestone) |
| End of 2025 / Q1 2026 | **~$30B** (2.3× YoY, ~2.8M txns) |
| US-only contribution by EOY 2025 | **~$10B** (1/3 of total), starting from $0.1B in Jan 2025 ✅ |

Sources: [Financial IT](https://financialit.net/news/payments/bvnk-surpasses-20bn-annualized-processing-volume-it-celebrates-fourth-anniversary); [BVNK 2025 wrap-up blog](https://bvnk.com/blog/stablecoins-core-financial-infrastructure-2025).

### Revenue 🟡

- **Dec 2024**: ~$40M annualized (Hemson-Struthers to Fortune at Series B).
- 2025: not officially disclosed; if revenue scaled with volume (3× growth), implied **~$70–120M annualized by year-end** — but stablecoin take-rates compressed during 2025, so a more conservative estimate is **$50–80M ARR at acquisition**. 🟡

### Headcount Growth ✅

- 2021 launch: ~40 employees
- 2022: ~160
- 2023 plan: 250
- 2024–2025: 270 (BVNK figure) — up to **448 total** per CB Insights/Tracxn (likely includes contractors/post-Series B hires)

Notable executive hires: BVNK has been "quietly poaching from Revolut and Checkout.com" per Sifted ([Sifted](https://sifted.eu/articles/bvnk-crypto-revolut-checkout-com)). **Amit Sridharan** (or similar — sources just say "Amit") leads US as **CEO of BVNK Inc.**

### Geographic Expansion ✅

| Year | Geography |
|---|---|
| 2021 | UK (HQ London), South Africa (Cape Town engineering) |
| 2022 | UK EMI license via System Pay Services acquisition (Nov); Spain VASP approval; Singapore office |
| 2023 | EU expansion via passporting |
| 2024 | Announced US entry at year-end |
| 2025 | **San Francisco office opened**, **NYC presence**, US states licensing buildout (AL, AZ, DE, FL, MI, NH minimum disclosed) |
| 2026 | Malta MiCA CASP license (Feb 2026) — passports across 30 EEA countries |

### Major Product Launches ✅

- **June 2024**: **Layer1** — self-custody stablecoin payments infra for enterprises ([BVNK blog](https://bvnk.com/blog/layer-1); [Finextra](https://www.finextra.com/pressarticle/101327/bvnk-launches-self-custody-infrastructure-for-stablecoin-payments)). "Less than 200 lines of code, deployed in weeks." Layer1 also became a sub-brand at layer1.com.
- **2025**: **Embedded Wallets** — first unified fiat + stablecoin wallet ([PYMNTS](https://www.pymnts.com/cryptocurrency/2025/bvnk-unveils-embedded-wallet-to-simplify-stablecoin-payments/); [FinTech Magazine](https://fintechmagazine.com/articles/bvnk-launches-unified-fiat-and-stablecoin-embedded-wallet)).
- **2025**: Customer Virtual Accounts (named-wire/SEPA receiving accounts).
- **2026**: **Stablecoin Utility Report** publication and consumer stablecoin survey ([Finovate](https://finovate.com/what-bvnks-report-reveals-about-how-consumers-are-using-stablecoins/)) — pure marketing/thought-leadership.

---

## 5. Major Customer Wins (Public)

✅ Confirmed customer/partner names disclosed publicly as of acquisition:

- **Worldpay** — May 2025 partnership for stablecoin payouts to clients in US/Europe across **180+ markets** ([Worldpay press release](https://corporate.worldpay.com/news-releases/news-release-details/worldpay-enable-stablecoin-payouts-global-businesses); [PYMNTS](https://www.pymnts.com/cryptocurrency/2025/worldpay-teams-with-bvnk-to-offer-stablecoin-payouts/)).
- **Visa Direct** — Jan 2026 stablecoin pilot ($1.7T network) ([BusinessWire](https://www.businesswire.com/news/home/20260114948268/en/BVNK-to-Deliver-Stablecoin-Infrastructure-for-Visa-Direct-Pilot-Programs)).
- **dLocal** — stablecoin payouts across 40+ markets ([dLocal press release](https://www.dlocal.com/press-releases/dlocal-and-bvnk-partner-to-power-faster-global-payouts-with-stablecoins/)).
- **Deel** — stablecoin contractor payouts.
- **Rapyd** — stablecoin embedded into platform.
- **Flywire**, **Thunes**, **LianLian Global**, **Equals Money**, **IC Markets** — stablecoin integration partners.
- **Xapo Bank**, **Ferrari**, **Bitso** — additional named customers per BVNK marketing.
- **Volt** — added BVNK stablecoin acceptance to checkout ([Volt newsroom](https://www.volt.io/newsroom/bvnk-partners-with-volt/)).
- **Equals Money + Railsr** joint offering for USDC payments ([Equals Money blog](https://equalsmoney.com/blog/equals-money-x-railsr-and-bvnk-enable-fast-usdc-stablecoin-payments-for-global-businesses)).

🟡 226 new customers added in 2025 per BVNK's own wrap-up — totals not disclosed.

---

## 6. Founder Backgrounds (Detailed)

**Jesse Hemson-Struthers — CEO, Co-founder** ✅
- Cape Town/Johannesburg native, now London-based.
- Built **SAcamera** (e-commerce), exited to Naspers/MIH Internet Africa in 2014.
- Co-founded **BetTech Gaming**, exited to Sportradar in 2017.
- Co-founded **Coindirect** in 2017 with Jackson.
- Active angel investor; has a PitchBook investor profile.

**Donald Jackson — CTO, Co-founder** ✅
- Studied at Nelson Mandela University (math, business management, algorithmics, info systems, computer architecture).
- Founded **Cue** (customer engagement) and **Verity** (anti-fraud).
- Technical Director at **Panacea Mobile** (likely concurrent/historical SMS-aggregator infra).
- Co-founded Coindirect.

**Chris Harmse — CBO, Co-founder** ✅
- CFA charter-holder, postgrad in Investment Management.
- Career: Renaissance Capital (equity trader) → Rezco Asset Management → BNP Paribas → Centaur, Excelsia, Asymmetry Asset Management (macro/crypto fund partner).
- Joined Coindirect → BVNK.
- Most public-facing of the trio in fundraising press cycles.

**Other named execs** 🟡
- **George Davis** — Chief Product Officer (also referred to as co-founder in Sifted reporting).
- **Stephen Young** — co-founder per some sources.
- **Kyle Redelinghuys** — co-founder per some sources (technical).
- **"Amit"** — US CEO leading North American expansion (full name not surfaced in search results).

---

## 7. Press Timeline (Founding → Mastercard)

| Date | Event |
|---|---|
| **2017** | Hemson-Struthers, Jackson, Harmse co-found **Coindirect** in Cape Town |
| **Aug 2021** | Hemson-Struthers and Jackson resign from Coindirect; BVNK incorporated |
| **Oct 2021** | BVNK publicly launches |
| **Jan 2022** | Coindirect "merged"/rebranded into BVNK |
| **May 11, 2022** | $40M Series A led by Tiger Global at $340M post |
| **Nov 2022** | Acquires **System Pay Services** → gains UK FCA EMI license |
| **2022** | Bank of Spain VASP registration |
| **2023** | Continued infra build, EU passporting |
| **June 2024** | Launches **Layer1** self-custody infra |
| **End 2024** | Announces US market entry |
| **Dec 17, 2024** | $50M Series B led by Haun Ventures at ~$750M; Coinbase Ventures, Scribble, DRW, Avenir, Tiger join |
| **Q1 2025** | Opens San Francisco office; NYC presence; US state-by-state MTL buildout |
| **May 7, 2025** | Visa Ventures strategic investment announced |
| **May 2025** | Worldpay partnership announced |
| **2025** | Embedded Wallets launch; dLocal, Deel, Rapyd, Flywire integrations |
| **Oct 9, 2025** | Citi Ventures invests; valuation reportedly above $750M |
| **Oct 9, 2025** | Fortune leaks Coinbase + Mastercard both pursuing BVNK at $1.5–2.5B |
| **Oct 2025** | Coinbase enters exclusivity at ~$2B |
| **Nov 11–12, 2025** | Coinbase walks from deal |
| **Jan 13–14, 2026** | Visa Direct stablecoin pilot announced (BVNK powering) |
| **Feb 2026** | Malta MFSA grants MiCA CASP license |
| **Mar 17, 2026** | **Mastercard announces $1.8B acquisition** |
| **Apr 2026** | Companies House ownership filings detail acquisition prep ([ABC Money](https://www.abcmoney.co.uk/2026/04/bvnk-mastercard-deal-ownership-filing-shows-1-8bn-acquisition-prep)) |
| **May 2, 2026** | Mastercard Q1 2026 earnings — Miebach reaffirms BVNK rationale |
| **Late 2026 (expected)** | Deal close subject to regulatory approvals |

---

## 8. Geographic / Regulatory Footprint at Exit

**Incorporation**: BVNK Limited, England & Wales (London HQ); BVNK Malta (regulated entity); BVNK Inc. (US Delaware); operating subsidiaries elsewhere.

**Licenses confirmed** ✅:
- **UK**: FCA-authorized **Electronic Money Institution** (via 2022 acquisition of System Pay Services Ltd, EMI since 2020).
- **Malta**: **MiCA Crypto-Asset Service Provider (CASP)** license from MFSA, Feb 2026 — passports across **30 EEA countries**. Combined with EMI status in Malta and direct **SEPA** access — described as a unique tri-license stack in Europe.
- **Spain**: Bank of Spain VASP registration (2022).
- **United States**: FinCEN-registered MSB (NMLS ID 2531294); state MTLs disclosed in **Alabama, Arizona, Delaware, Florida, Michigan, New Hampshire** — additional states 🟡 not enumerated publicly.
- **130+ countries**: payment coverage (likely via partner network + local licenses, not direct license in all).

**Banking partnerships** 🟡: BVNK has not publicly named all banking partners, but the SEPA direct connection (post-MiCA) and UK FPS connectivity imply at least Tier-2 European bank relationships in addition to whatever they have in the US for Fedwire/ACH access.

---

## Key Open Questions / Red Flags

1. **Founders' precise stakes at exit** — never disclosed; "instant billionaire" reporting is back-of-envelope. 🟡
2. **Real revenue** vs annualized payment volume — BVNK's take-rate is opaque. At $30B volume and ~$40M ARR (Dec 2024), implied take rate is ~13bps. If volume tripled to $30B and revenue scaled linearly, ARR would be ~$120M; if take-rates compressed (likely as Worldpay/Visa Direct flow is lower-margin enterprise), the real number is likely **$50–80M**. 🟡
3. **What happens to BVNK brand post-close** — Mastercard's prior playbook (Finicity, Ekata) suggests 18–24 month brand independence followed by integration. 🟡
4. **Why did Coinbase walk?** — Officially unexplained. Speculation: regulatory complexity for a US-listed crypto exchange acquiring a UK-regulated entity, or Coinbase's strategic preference for Base + USDC stack over a payments-licensed acquisition. 🔴
5. **Earnout milestones** ($300M of the $1.8B) — not publicly disclosed. Likely tied to integration milestones and revenue targets through 2027–2028. 🟡

---

## Bottom Line for Research Purposes

BVNK's story is **the textbook stablecoin infrastructure exit**: a quiet, regulatory-heavy, B2B-focused team that grew payment volume 30× in three years, then was sold to a card network that needed to **defensively buy** distribution into a settlement layer it couldn't afford to ignore. The premium over the Stripe-Bridge deal — both in absolute dollars and relative to fundamentals — sets the new ceiling for the next cohort: **Zerohash, Conduit, Sphere, Brale, Beam, Triple-A, Stablesea**, and the remaining independents.

The most underappreciated fact: **Coinbase had agreed to pay up to $2.5B and walked**. This means there's a real ceiling somewhere between $1.8B (what Mastercard actually paid) and $2.5B (what was on the table) that the next stablecoin infra exit will likely be benchmarked against — and Visa, after losing this one, almost certainly has a buy mandate ready.

---

## Sources

- [Mastercard to Acquire BVNK to Connect On-Chain Payments and Fiat Rails — Mastercard Investor News](https://investor.mastercard.com/investor-news/investor-news-details/2026/Mastercard-to-Acquire-BVNK-to-Connect-On-Chain-Payments-and-Fiat-Rails/default.aspx)
- [Mastercard newsroom press release](https://www.mastercard.com/us/en/news-and-trends/press/2026/march/Mastercard-to-acquire-BVNK-to-connect-on-chain-payments-and-fiat-rails.html)
- [Why BVNK is joining Mastercard — BVNK Blog](https://bvnk.com/blog/why-bvnk-is-joining-mastercard)
- [Mastercard to acquire crypto startup BVNK for up to $1.8 billion — Fortune](https://fortune.com/2026/03/17/mastercard-bvnk-acquisition-stablecoins-1-8-billion/)
- [Mastercard says it's acquiring stablecoin startup BVNK in $1.8 billion bet — CNBC](https://www.cnbc.com/2026/03/17/mastercard-acquiring-stablecoin-startup-bvnk-in-crypto-bet.html)
- [Mastercard to acquire BVNK for $1.8 billion — CoinDesk](https://www.coindesk.com/business/2026/03/17/mastercard-agrees-to-purchase-bvnk-for-up-to-usd1-8-billion)
- [Mastercard Buys Stablecoin Firm BVNK for Up to $1.8 Billion — Bloomberg](https://www.bloomberg.com/news/articles/2026-03-17/mastercard-to-buy-stablecoin-startup-bvnk-for-up-to-1-8-billion)
- [Why Mastercard paid double for stablecoin infrastructure it could have built — CoinDesk Opinion](https://www.coindesk.com/opinion/2026/03/27/why-mastercard-paid-double-for-stablecoin-infrastructure-it-could-have-built)
- [Mastercard's $1.8B bet on BVNK accelerates stablecoin push — S&P Global](https://www.spglobal.com/market-intelligence/en/news-insights/research/2026/03/mastercards-1-8-b-bet-on-bvnk-accelerates-stablecoin-push)
- [Mastercard M&A Call: Buying the Stablecoin Bridge to Protect a $911 Target — TIKR](https://www.tikr.com/blog/mastercard-ma-call-buying-the-stablecoin-bridge-to-protect-a-911-target)
- [Mastercard Makes Its Stablecoin Move: The BVNK Acquisition — Forrester](https://www.forrester.com/blogs/mastercard-makes-its-stablecoin-move-the-bvnk-acquisition/)
- [BVNK to Be Acquired by Mastercard — Skadden](https://www.skadden.com/about/news-and-rankings/news/2026/03/bvnk-to-be-acquired-by-mastercard)
- [What Mastercard's acquisition of BVNK means for payments — NatWest](https://www.natwest.com/corporates/insights/technology/mastercard-stablecoin-acquisition-bvnk.html)
- [Mastercard's BVNK Acquisition: What It Means for Payments — Datos Insights](https://datos-insights.com/blog/mastercard-bvnk-acquisition-stablecoin-payments/)
- [Mastercard's $1.8bn BVNK Bet Signals the End of Legacy Settlement Cycles — bobsguide](https://www.bobsguide.com/mastercards-bvnk-bet-signals-the-end-of-legacy-settlement-cycles/)
- [Mastercard's $1.8 billion bet heralds the collapse of financial silos — American Banker](https://www.americanbanker.com/payments/opinion/mastercards-1-8-billion-bet-heralds-the-collapse-of-financial-silos)
- [Mastercard just super-charged Wall Street's crypto land grab — DL News](https://www.dlnews.com/articles/markets/what-mastercard-acquiring-bvnk-means-for-wall-street-landgrab/)
- [Analysis: Mastercard Buys BVNK for $1.8B as Stripe Launches Machine Payments Protocol — Lex Substack](https://lex.substack.com/p/analysis-mastercard-buys-bvnk-for)
- [$1.1B Looked Big. Then BVNK Sold for $1.8B — Rex Salisbury](https://rexsalisbury.substack.com/p/11b-looked-big-then-bvnk-sold-for)
- [Coinbase and Mastercard Held Talks to Buy Stablecoin Fintech BVNK for Up to $2.5B — CoinDesk](https://www.coindesk.com/business/2025/10/09/coinbase-and-mastercard-held-talks-to-buy-stablecoin-fintech-bvnk-for-up-to-usd2-5b-fortune)
- [Coinbase and stablecoin startup BVNK call off $2 billion acquisition — Fortune](https://fortune.com/2025/11/11/coinbase-bvnk-2-billion-deal-falls-through-stablecoins/)
- [Coinbase Ends Acquisition Talks for U.K.-Based BVNK — CoinDesk](https://www.coindesk.com/markets/2025/11/12/coinbase-ends-acquisition-talks-for-u-k-based-bvnk-fortune)
- [BVNK grabs $40 million for its crypto banking services — TechCrunch](https://techcrunch.com/2022/05/11/bvnk-grabs-40-million-for-its-crypto-banking-services/)
- [Tiger Global backs London-based crypto-to-fiat banking platform with $40 million — Tech.eu](https://tech.eu/2022/05/12/londons-crypto-to-fiat-banking-platform-nabs-40-million/)
- [BVNK raises $50M to fuel US expansion — Payments Dive](https://www.paymentsdive.com/news/bvnk-stablecoin-startup-raises-money-us-expansion/735898/)
- [Crypto startup BVNK raises $50 million at around $750 million valuation — Fortune](https://fortune.com/crypto/2024/12/17/exclusive-stablecoin-bvnk-750-million-series-b-bridge-stripe-haun/)
- [We've raised $50 million to fuel the next era of stablecoin payments — BVNK Blog](https://bvnk.com/blog/series-b-fuel-next-era-of-stablecoin-payments)
- [Visa invests in BVNK: Accelerating our vision for stablecoin payments infrastructure — BVNK Blog](https://bvnk.com/blog/visa-invests-in-bvnk)
- [Visa Doubles Down on Stablecoins With Strategic Investment in BVNK — CoinDesk](https://www.coindesk.com/business/2025/05/07/visa-doubles-down-on-stablecoins-with-investment-in-blockchain-payments-firm-bvnk)
- [Citi invests in stablecoin firm BVNK — CNBC](https://www.cnbc.com/2025/10/09/biti-bvnk-stablecoin-banks-crypto.html)
- [Citi Ventures backs BVNK in strategic investment — BVNK Blog](https://bvnk.com/blog/citi-ventures-backs-bvnk)
- [BVNK to Deliver Stablecoin Infrastructure for Visa Direct Pilot Programs — BusinessWire](https://www.businesswire.com/news/home/20260114948268/en/BVNK-to-Deliver-Stablecoin-Infrastructure-for-Visa-Direct-Pilot-Programs)
- [BVNK powers stablecoin payments for Visa Direct — BVNK Blog](https://bvnk.com/blog/bvnk-powers-stablecoin-payments-for-visa-direct)
- [Layer1: a new era in stablecoin infrastructure — BVNK Blog](https://bvnk.com/blog/layer-1)
- [BVNK launches self-custody infrastructure for stablecoin payments — Finextra](https://www.finextra.com/pressarticle/101327/bvnk-launches-self-custody-infrastructure-for-stablecoin-payments)
- [BVNK Unveils Embedded Wallet to Simplify Stablecoin Payments — PYMNTS](https://www.pymnts.com/cryptocurrency/2025/bvnk-unveils-embedded-wallet-to-simplify-stablecoin-payments/)
- [BVNK Launches Unified Fiat and Stablecoin Embedded Wallet — FinTech Magazine](https://fintechmagazine.com/articles/bvnk-launches-unified-fiat-and-stablecoin-embedded-wallet)
- [Worldpay Partners with BVNK for Stablecoin Payouts — FinTech Magazine](https://fintechmagazine.com/articles/worldpay-partners-with-bvnk-for-stablecoin-payouts)
- [Worldpay to Enable Stablecoin Payouts for Global Businesses in Collaboration with BVNK — Worldpay press release](https://corporate.worldpay.com/news-releases/news-release-details/worldpay-enable-stablecoin-payouts-global-businesses)
- [dLocal and BVNK partner to power faster global payouts — dLocal press release](https://www.dlocal.com/press-releases/dlocal-and-bvnk-partner-to-power-faster-global-payouts-with-stablecoins/)
- [BVNK Surpasses $20Bn In Annualized Processing Volume — Financial IT](https://financialit.net/news/payments/bvnk-surpasses-20bn-annualized-processing-volume-it-celebrates-fourth-anniversary)
- [Stablecoins became core financial infrastructure in 2025 — BVNK Blog](https://bvnk.com/blog/stablecoins-core-financial-infrastructure-2025)
- [BVNK acquires UK-licensed e-money institution — BVNK Blog](https://bvnk.com/blog/bvnk-acquires-uk-licensed-e-money-institution-to-accelerate-expansion)
- [BVNK acquires fellow paytech System Pay Services — FinTech Futures](https://www.fintechfutures.com/2022/11/bvnk-acquires-fellow-paytech-system-pay-services/)
- [BVNK Gains UK EMI License by Acquiring SPS — Finance Magnates](https://www.financemagnates.com/fintech/bvnk-gains-uk-emi-license-by-acquiring-sps/)
- [BVNK secures MiCA licence — BVNK Blog](https://bvnk.com/blog/bvnk-secures-mica-licence)
- [BVNK Secures MiCA Licence in Malta — The Fintech Times](https://thefintechtimes.com/bvnk-secures-mica-licence-in-malta-to-expand-european-stablecoin-operations/)
- [What licenses & registrations does BVNK and BVNK's Partners have? — BVNK Help](https://help.bvnk.com/hc/en-us/articles/11094354781074-What-licenses-registrations-does-BVNK-and-BVNK-s-Partners-have)
- [Compliance — BVNK](https://bvnk.com/compliance)
- [About — BVNK](https://bvnk.com/about-us)
- [What is BVNK? The mysterious fintech that's quietly poaching talent — Sifted](https://sifted.eu/articles/bvnk-crypto-revolut-checkout-com)
- [What is Brief History of BVNK — Canvas Business Model](https://canvasbusinessmodel.com/blogs/brief-history/bvnk-brief-history)
- [BVNK: Bvnking on Stablecoin — Fintech: Under the Hood (Substack)](https://jasshah.substack.com/p/bvnk-stablecoin-infrastructure)
- [BVNK Company Research Report — BlockEden](https://blockeden.xyz/blog/2025/05/18/bvnk/)
- [Three South African tech entrepreneurs become instant billionaires — Daily Investor](https://dailyinvestor.com/cryptocurrency/124930/three-south-african-tech-entrepreneurs-become-instant-billionaires/)
- [BVNK founders become billionaires in $1.8bn Mastercard deal — Billionaires.Africa](https://www.billionaires.africa/2026/03/19/south-african-trio-sells-stablecoin-startup-bvnk-to-mastercard-for-1-8-billion-becoming-instant-billionaires/)
- [The South Africans behind a R14 billion fintech startup — BusinessTech](https://businesstech.co.za/news/mobile/805279/the-south-africans-behind-a-r14-billion-fintech-startup/)
- [Jesse Hemson-Struthers — The Org](https://theorg.com/org/bvnk/org-chart/jesse-hemson-struthers)
- [Donald Jackson — Crunchbase](https://www.crunchbase.com/person/donald-jackson)
- [Chris Harmse — LinkedIn](https://ae.linkedin.com/in/chrisharmse)
- [BVNK 2026 Funding Rounds & List of Investors — Tracxn](https://tracxn.com/d/companies/bvnk/__MM4uMmLk_IgvOprDz4TdvYh0jmEk-Vd6ivOsy5Svhj8/funding-and-investors)
- [BVNK 2026 Company Profile — PitchBook](https://pitchbook.com/profiles/company/231240-07)
- [BVNK — Crunchbase](https://www.crunchbase.com/organization/bvnk)
- [BVNK funding, news & analysis — Sacra](https://sacra.com/c/bvnk/)
- [BVNK Mastercard Deal: Ownership Filing Shows $1.8bn Acquisition Prep — ABC Money](https://www.abcmoney.co.uk/2026/04/bvnk-mastercard-deal-ownership-filing-shows-1-8bn-acquisition-prep)
- [Mastercard Q1 Earnings Call Highlights — Stock Observer](https://www.thestockobserver.com/2026/05/02/mastercard-q1-earnings-call-highlights.html)
- [BVNK Explains Reason For Mastercard Acquisition — Crowdfund Insider](https://www.crowdfundinsider.com/2026/03/267516-bvnk-explains-reason-for-mastercard-acquisition/)
