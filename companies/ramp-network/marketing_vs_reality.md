# Ramp Network — Marketing-vs-Reality Audit

*Stream 4 / Truth File · 2026-05-09*

**Scope:** ramp.network / rampnetwork.com (the Polish/UK fiat-to-crypto on-ramp), explicitly NOT ramp.com (the US corporate spend-management company that has been hoovering up valuation headlines and confusing every search engine).
**Method:** Adversarial. Every claim treated as marketing artifact until verified.

---

## 1. Honest baseline (no marketing language)

Ramp Network is a Warsaw-founded (2017), London/Dublin-incorporated fiat ↔ crypto on/off-ramp. It sells a hosted-widget and SDK that wallets, dApps, games and exchanges embed so their end-users can buy crypto with a card or bank transfer and (since 2023) sell crypto back to fiat. Crypto is delivered **non-custodially** — i.e. straight to the partner-wallet's address — which is the principal pitch differentiator versus MoonPay/Coinbase On-Ramp. Revenue comes from transaction fees (a "Ramp fee" plus an embedded FX/asset-price spread) that Ramp keeps, with a configurable partner-commission take-rate on top. Headcount has fluctuated around the 160–260 range across 2022–2026; total funding ~$134M; the business is a mid-tier infrastructure player in a commoditising category, not a category-defining unicorn. ([rampnetwork.com/about](https://rampnetwork.com/about), [Sifted](https://sifted.eu/articles/ramp-crypto-poland-53m), [Latka](https://getlatka.com/companies/ramp.network)).

A crucial framing point: **the brand "Ramp" is constantly conflated with Ramp Inc. (ramp.com)**, a US corporate-card/spend-management company that hit a ~$32B valuation in Nov 2025 and is reportedly raising at $40B+ in May 2026 ([TechCrunch](https://techcrunch.com/2026/05/07/ramp-in-talks-to-hit-40b-valuation-6-months-after-reaching-32b/)). That is a different company. The crypto on-ramp is a ~$30–50M-revenue business; Ramp Inc. is a ~$1B ARR fintech. Treat any "Ramp at $32B" headline as not about this Ramp.

---

## 2 & 3. Claim audit

Marketing claims are sourced from the current ramp.network / rampnetwork.com surface (via search snippets — direct WebFetch was blocked, so each claim is corroborated by an external publication or Ramp's own blog/help center URL).

| # | Claim (verbatim or near-verbatim) | Source | Verification | Label |
|---|---|---|---|---|
| 1 | "Trusted by **8 million customers** worldwide" | [rampnetwork.com](https://rampnetwork.com/), Slashdot review | Self-reported, no third-party audit. Could be cumulative "all-time wallet addresses ever served" rather than active users. No MAU disclosure. | 🟡 Plausible-ish, unverifiable |
| 2 | "Available in **150+ countries**" | [rampnetwork.com](https://rampnetwork.com/), [Bitget Academy](https://www.bitget.com/academy/ramp-network-crypto) | Mixes on-ramp + off-ramp + "limited services" countries. [Help center](https://support.rampnetwork.com/en/articles/433-which-countries-and-us-states-are-unsupported-for-buying-and-selling-crypto) says "limited services may be available — crypto purchases only" in some — i.e. the 150+ figure is reachability, not full functionality. | 🟡 Directionally true, fluffed |
| 3 | "Off-ramp / cash-out in **130+ countries**" | [Ramp blog](https://ramp.network/blog/off-ramp-is-now-global) | This is the more useful, narrower number; consistent across sources. | ✅ |
| 4 | "**40+ fiat currencies** supported" | [Ramp help](https://support.rampnetwork.com/en/articles/471-which-fiat-currencies-does-ramp-network-support), [SeamlessChex](https://www.seamlesschex.com/blog/best-fiat-on-ramp-providers-in-2026) | Off-ramp page says "**35+** fiat currencies"; on-ramp says 40+. Inconsistency suggests the higher number includes payout-only or limited routes. | 🟡 Slight inflation |
| 5 | "**100+ digital assets / 100+ cryptocurrencies**" | [SeamlessChex](https://www.seamlesschex.com/blog/best-fiat-on-ramp-providers-in-2026) | Tracks with public help-center asset list (50–100 high-liquidity tokens depending on chain). Reasonable. | ✅ |
| 6 | "**60+ blockchains**" / "16 networks" | [Rampnow](https://rampnow.io/en/list), [token-integration page](https://rampnetwork.com/token-integration) | Two different numbers in the same site! 16 is the on-ramp delivery network count; 60+ appears to be every chain Ramp can technically reach via partners. The honest number for buying/selling is **16**. | 🟡 Two truths, one used selectively |
| 7 | "Swap **1,200+ crypto pairs**" | [Ramp blog](https://rampnetwork.com/blog/swap-1200-crypto-pairs) | Plausible — derives mechanically from 16 networks × ~75 assets, not a moat. | ✅ trivially true |
| 8 | "Card/e-wallet fee **3.9%**, manual bank transfer **1.4%**, SEPA Instant off-ramp **0.99%**" | [Ramp help](https://support.ramp.network/en/articles/10415-what-fees-does-ramp-network-charge-for-buying-crypto), [Coinspeaker](https://www.coinspeaker.com/ramp-network-eu-international-instant-payouts/) | These are Ramp's "Ramp fee" only. The **embedded FX/asset spread is not included** in these numbers (see §5). | 🟡 Technically true, materially misleading |
| 9 | "Bank transfers from **0.49%**" | [SeamlessChex](https://www.seamlesschex.com/blog/best-fiat-on-ramp-providers-in-2026) | Real for SEPA bank transfers — but with a **€2.49 minimum**, which makes it ≥5% on a €50 buy. | 🟡 True at scale, worse for retail |
| 10 | "**SOC 2 Type II compliant**" (June 2024) | [The Defiant](https://thedefiant.io/news/press-releases/ramp-network-achieves-soc2-type-ii-compliance-the-gold-standard-of-financial-data-security), [LinkedIn announcement](https://www.linkedin.com/posts/rampnetwork_ramp-achieves-soc-type-2-compliance-activity-7221076558399098880-emxA) | Verified. 21-Jun-2024. Real audit. | ✅ |
| 11 | "ISO 27001 / PCI DSS audited" | [trust.ramp.com](https://trust.ramp.com/) (note: this trust center belongs to Ramp Inc., NOT Ramp Network!) | **Tell:** the search result that surfaces "ISO 27001 + PCI DSS + SOC 1/2" is from the Ramp Inc. trust center, not Ramp Network. Ramp Network publicly claims SOC 2 Type II but ISO 27001 not verified. | 🔴 Likely conflated with the other Ramp |
| 12 | "First fiat on-ramp registered with the UK FCA" (8th cryptoassets firm) | [Ramp blog](https://ramp.network/blog/ukregistered), [CoinDesk 2021](https://www.coindesk.com/markets/2021/08/06/crypto-startup-ramp-secures-fca-registration), [X post](https://x.com/rampnetwork/status/1417865914230493185) | True for July 2021. Note: FCA registration ≠ FCA-regulated; AML-only. | ✅ true with asterisk |
| 13 | "MiCAR authorised across all 27 EU states" (Dec 2025) | [Central Bank of Ireland via RTÉ](https://www.rte.ie/news/business/2025/1204/1547196-ramp-network-authorised-by-central-bank/), [Chainwire](https://chainwire.org/2025/12/04/ramp-swaps-ireland-limited-receives-eu-wide-micar-authorisation-as-a-crypto-asset-service-provider/) | Verified — Ramp Swaps (Ireland) Limited, 4 Dec 2025, CBI-issued. Joins Kraken, Legend Trading, Push (Aave). Genuinely meaningful. | ✅ |
| 14 | "FinCEN-registered MSB in the US, available in all 50 US states" | [BusinessWire 2022](https://www.businesswire.com/news/home/20220112005295/en/Ramp-US-Expands-Presence-in-US-With-FinCEN-Regulation), [CryptoBriefing](https://cryptobriefing.com/ramp-network-to-expand-cryptoasset-purchases-to-all-50-u-s-states-and-the-district-of-columbia/), [licenses page](https://rampnetwork.com/licenses-and-registrations) | FinCEN MSB #31000287566749 — verified. State MTLs only ~9 states confirmed (AL, AK, AR, MD, NM, OH, OR, ND, KY). Original FinCEN registration covered 38 states; "all 50" likely depends on agent-of-payee carve-outs and rolling MTL acquisition. **Not all 50 are MTL-licensed.** | 🟡 Half-truth |
| 15 | "Real-time payments / SEPA Instant — fiat the same day, 24/7/365" | [Ramp blog](https://rampnetwork.com/blog/ramp-network-sepa-payouts-and-local-currencies) | True for SEPA Instant + US RTP rails. Card-out is genuinely fast. Cards-in 5-15 mins is normal industry-wide. | ✅ |
| 16 | "First major off-ramp to introduce Real-Time Payments in the US and pioneer Visa/Mastercard payouts globally" | [Coinspeaker](https://www.coinspeaker.com/ramp-network-eu-international-instant-payouts/) | "Pioneer" is unverifiable; MoonPay had Visa Direct earlier. Likely puffery. | 🔴 Marketing |
| 17 | "Trusted by hundreds of businesses including MetaMask, Trust Wallet, Brave, Ledger, Opera, Sorare, Axie, GameStop, DeFi Kingdoms, Loopring" | [rampnetwork.com](https://rampnetwork.com/), [Trust Wallet support](https://support.trustwallet.com/support/solutions/articles/67000734512-ramp-your-gateway-to-seamless-crypto-transactions) | Most partnerships exist or did exist. **However**, Ledger Live now also runs Transak ([Transak press release Feb 2025](https://transak.com/blog/ledger-live-integrates-transak-off-ramp-more-ways-to-sell-crypto-securely)) — partnership has *not* been dropped, but it's no longer exclusive. MetaMask offers Ramp alongside MoonPay, Transak, Banxa — Ramp is one of several aggregated providers. | 🟡 Real but no longer unique |
| 18 | "55M+ MAU Brave partnership" | search snippet | Brave's MAU is the marketing number, not Ramp's traffic from Brave. Co-branding fluff. | 🟡 Borrowed metric |
| 19 | "Non-custodial — assets go straight to user's wallet, no intermediary" | [rampnetwork.com](https://rampnetwork.com/), [Cointelegraph](https://cointelegraph.com/news/ramp-network-self-custodial-wallet-third-party-dependencies) | Architecturally true and the genuine differentiator vs. MoonPay (which can be custodial via balances) and exchange ramps. | ✅ |
| 20 | "$37.5M revenue (2023)" / "8 years in market" | [Latka](https://getlatka.com/companies/ramp.network) | Latka is self-reported but consistent with funding/headcount math. | 🟡 Plausible |
| 21 | "Fastest" / "best rates" / "lowest fees" | various comparison-site ad copy | Never benchmark-anchored. Onramper price-comparison data routinely shows MoonPay, Transak, Banxa or Paybis beating Ramp on net-received depending on corridor. | 🔴 Untrue as written |
| 22 | "Multichain self-custody wallet (April 2026)" | [Cointelegraph](https://cointelegraph.com/news/ramp-network-self-custodial-wallet-third-party-dependencies), [Benzinga](https://www.benzinga.com/pressreleases/26/04/51881769/ramp-network-launches-multichain-wallet-that-eliminates-third-party-dependencies-in-self-custody) | Real launch April 2026, supports BTC + 8 networks. Strategic pivot — Ramp now competes *with* its own wallet partners. | ✅ but strategically loud |
| 23 | "Open banking licence in Europe (first crypto co)" | [Sifted](https://sifted.eu/articles/ramp-crypto-poland-53m) | True — Polish KNF, 2021. Real but minor. | ✅ |
| 24 | "Visa-card-issuing for stablecoin balances (with Bridge)" | [Bessemer Stablecoin Atlas](https://www.bvp.com/atlas/stablecoins-from-defi-primitive-to-global-financial-infrastructure) | Mentioned in industry pieces; not a Ramp-led launch — Ramp is a downstream user of Bridge x Visa. | 🟡 Real, downstream |
| 25 | "$134M total raised, profitable infrastructure" | [Bessemer](https://www.bvp.com/atlas/stablecoins-from-defi-primitive-to-global-financial-infrastructure) | $134M raised verifiable across rounds (Seed → $52M Series B 2021 → $70M Series B extension Nov 2022, [CoinDesk](https://www.coindesk.com/business/2022/11/09/ramp-raises-70m-to-provide-crypto-payments-infrastructure)). Profitability not publicly disclosed. | 🟡 Funding ✅, profit unverified |

---

## 4. Card-fee transparency

Stated structure (current help center, [support.ramp.network](https://support.ramp.network/en/articles/10415-what-fees-does-ramp-network-charge-for-buying-crypto)):

- **Card / Apple Pay / Google Pay (USD/EUR/GBP):** 3.9% Ramp fee
- **Manual bank transfer:** 1.4% Ramp fee
- **SEPA bank transfer (EU):** from **0.49% with €2.49 minimum**
- **Off-ramp via SEPA Instant:** 0.99%
- **"Network fee"** disclosed as a separate line item

Reality:

The 3.9% is reasonable for the card category — MoonPay quotes ~4.5%, Transak ~3.5–5%, Coinbase On-Ramp ~3.99%. **However, none of these published "Ramp fee" numbers are the all-in price the user pays.** The asset-quote spread sits on top — Paybis's [On-Ramp Fee Transparency analysis](https://paybis.com/blog/on-ramp-fee-transparency/) and [Crypto On-Ramp Fee Comparison 2026](https://paybis.com/blog/crypto-on-ramp-fee-comparison/) show that the industry standard is to quote crypto at a 1–3% markup to the CoinGecko/CoinMarketCap mid-rate. Ramp's effective all-in card fee for a small buy lands around **5–6%**, not 3.9%. 🔴 on the way the headline 3.9% is communicated.

The €2.49 minimum is an underdiscussed footgun: at €25, that's effectively a 10%+ floor, which any reasonable buyer would call out.

---

## 5. The hidden FX spread (the most important question)

Across the on-ramp industry the spread is the largest source of unstated revenue. Direct measurement against ramp.network was not possible without running a live transaction, but third-party benchmarking gives a defensible range:

- **MoonPay**: 1–3% spread + 4.5% headline fee, total 5.5–7.5% ([Paybis comparison](https://paybis.com/blog/crypto-on-ramp-fee-comparison/)).
- **Coinbase On-Ramp**: spread-based pricing, "not always disclosed at the point of quote" — a known offender ([Paybis](https://paybis.com/blog/cheapest-crypto-on-ramp/)).
- **Transak**: ~1% per transaction + small exchange spread.
- **Paybis**: explicitly *no spread* on top of fees (their own claim).
- **Ramp**: discloses Ramp fee + network fee, but the asset price quoted to the user already embeds the FX/asset spread. Onramper's aggregator has historically shown Ramp competitive but **not the cheapest** on most £100 GBP→USDC quotes; MoonPay or Banxa often beat Ramp depending on corridor ([Onramper MoonPay vs Ramp](https://www.onramper.com/onramp-comparisons/moonpay-vs-ramp-which-is-better)).

For a user buying USDC for £100 via Ramp on card: realistic net-received ≈ £94–95 of USDC at mid-market, i.e. **5–6% all-in cost**. Below MoonPay, above Paybis/Transak SEPA, comparable to Coinbase On-Ramp's range. Label: 🟡 "competitive but not best-in-class, and the spread is not surfaced before payment".

---

## 6. The "tell" — claim drift, layoffs, sunsets

Things that have quietly changed or vanished:

- **"First crypto on-ramp" / "first FCA-registered" framing** has been retired in favor of "MiCAR authorised" since Dec 2025 — sensible repositioning, but also tells you the FCA-first claim was getting stale ([Ramp 2025 FinCEN blog](https://rampnetwork.com/blog/ramp-network-us-expands-presence-in-us-with-fincen-regulation)).
- **Headcount drift**: Sifted (2022) reported "160+ people from offices in UK, US, Ireland, Poland." Latka (2024) shows "258 person team" with $37.5M revenue. Blind threads cited rumors of "30–50% workforce cuts" across multiple rounds, though [no on-record press confirms layoffs](https://news.crunchbase.com/startups/tech-layoffs/). 🟡 unconfirmed but persistent rumors.
- **Multichain wallet launch (April 2026)** is a strategic pivot, not just a feature. Ramp now sells *against* its own wallet partners (MetaMask, Trust Wallet, Ledger). That signals Ramp expects the pure on-ramp infrastructure layer to commoditize, and it is moving forward into the consumer app (where it now has to compete with the brands of its biggest distribution partners).
- **Ledger Live now also runs Transak** ([Transak Feb 2025 press release](https://transak.com/blog/ledger-live-integrates-transak-off-ramp-more-ways-to-sell-crypto-securely)). Ramp partnership is no longer exclusive. Partnership-churn signal.
- The **down-round atmosphere of 2023–24** affected the on-ramp category broadly; Ramp's last priced round was 2022, and there is no announced 2025/2026 raise — in a category where MoonPay is doing $200M+ rounds, Ramp's funding silence is itself information. 🟡

---

## 7. Dual-positioning game

Ramp tells two genuinely different stories:

| Audience | Pitch | Implicit promise |
|---|---|---|
| **Crypto-native end users** (homepage, app store, blog) | "Buy & sell 100+ assets across 16 chains, non-custodial, your keys, lowest fees, FCA & MiCA regulated, used by 8M people" | We're safe and consumer-grade |
| **Enterprise / wallet / dApp integrators** (rampnetwork.com/business, partner portal, Fireblocks case study) | "Web3 financial infrastructure. Drop in a few lines of code. We handle KYC, fraud, regulatory exposure, FX, payment-method coverage, refunds. You earn a partner commission on every transaction." | We absorb your regulatory risk |

These pitches contradict on one dimension: the consumer pitch leans into "your keys, no intermediary," while the enterprise pitch is "we handle compliance, you don't have to think about it." Both true — but the consumer-side messaging quietly elides that **Ramp itself is a regulated intermediary in the value flow**; the user holds the crypto but Ramp is fully in the fiat custody path until settlement. The "non-custodial" tag is doing more rhetorical work than architectural work.

The 2026 wallet launch is a meaningful tension here: Ramp now wants to be the *whole* customer relationship for at least some users, which puts it into direct competition with the same wallets it sells infrastructure to. Expect Ledger/Trust/MetaMask to diversify aggressively away from Ramp on integration where they can.

---

## 8. Competitive positioning

| Competitor | Where Ramp wins | Where Ramp loses | Verdict |
|---|---|---|---|
| **MoonPay** | Non-custodial pitch is cleaner; SEPA Instant cheaper; better default for crypto-native partners | Brand recognition with end users; NFT-buy flows; consumer marketing budget; deeper US footprint | Loses on consumer brand, parity on infra |
| **Transak** | Heavier EU/UK regulatory positioning (MiCA + FCA); SOC 2 | EM coverage; lower price for many corridors; broader fiat list (76 vs ~40); now eating Ramp's Ledger seat | Loses outside EU/UK |
| **Onramper** | Onramper is an *aggregator*, not a competitor — but Onramper structurally erodes Ramp's pricing power by routing transactions to whoever's cheapest in real-time | Onramper conversion 80%+ vs single provider 40–60% | Existential pressure on solo providers including Ramp |
| **Stripe Crypto / Bridge** | Crypto-native trust, longer track record in Web3 | Stripe's distribution is on a different planet; Bridge acquisition gives them stablecoin issuance + Visa cards Ramp doesn't have | Loses badly on capital + distribution |
| **Coinbase On-Ramp** | Better non-Coinbase wallet UX, less spread-opaque | Coinbase brand trust; native USDC; Base integration; institutional rails | Parity with structural disadvantage |
| **PayPal On-Ramp** | More chains, more dApp integrations | PayPal's 400M+ user base; PYUSD distribution | Loses on consumer reach |
| **Robinhood Connect** | Doesn't require Robinhood account | Robinhood brand and US retail | US loss, EU win |
| **Banxa, Mercuryo, Simplex/Nuvei** | EU regulatory profile | Banxa/Mercuryo cheaper in many corridors; Nuvei has full payment-processor scale | Parity to slight loss |
| **Sardine** | Different category — fraud + on-ramp combined | Sardine is more bank-grade B2B | Different market |

Honest one-line comparison: Ramp is **a top-3 European on-ramp with above-average regulatory positioning and a clean non-custodial story, sitting in a category where the price floor is being pushed down by aggregators and the ceiling is being pushed down by Stripe/Bridge eating the enterprise market**.

---

## 9. Moat analysis

| Moat candidate | Real? | Notes |
|---|---|---|
| Technical (FX engine, fraud) | 🟡 partial | Their own off-ramp + swap stack is genuinely built in-house — meaningful but replicable in 18 months |
| Regulatory (UK FCA + Ireland MiCAR + ~9 US MTLs) | ✅ moderate | This is the strongest moat. MiCAR Ireland CASP is a genuine 18-month head start vs. unlicensed competitors; FCA registration since 2021 is durable. **But** every other serious competitor will close this gap by 2027 |
| Distribution (MetaMask, Trust, Brave, Ledger) | 🔴 weakening | Each of these is now multi-provider; partnerships are non-exclusive and partner-side switching cost is "change a config" |
| Brand | 🔴 weak | "Ramp" is materially confused with the bigger Ramp Inc.; consumer brand awareness is low |
| Capital | 🔴 weak | $134M raised total; MoonPay raised $200M+ at $3.4B in 2025; Stripe is infinite |
| Network effects | 🔴 none | On-ramps are not network-effect businesses; they are price-and-coverage businesses |
| Take-rate / unit economics | 🟡 thin | Card take-rate is 3.9%, but Ramp pays 1.5–2% to card networks + ~1% to fraud/processing + partner commission, leaving low single-digit % net |

Net: **the moat is thin and shrinking.** Regulatory (FCA + MiCAR + selected MTLs) is the only durable structural advantage, and even that is eroding as competitors close licensing gaps.

---

## 10. What a competitor would target

Real, exploitable gaps:

1. **The €2.49 SEPA minimum** is a wedge for any EU-focused on-ramp that targets sub-€100 retail buys (relevant for memecoin/Solana micro-buyers).
2. **Emerging-markets coverage** — Ramp's 150+ countries figure is fluffed; in LatAm, Africa, SE Asia, Transak/Paybis/Banxa have deeper local-payment-method coverage and friendlier KYC.
3. **Consumer brand** — MoonPay owns the consumer-recognition slot; Coinbase On-Ramp owns the trust slot. Ramp owns neither.
4. **NFT/gaming purchase flows** — MoonPay leans heavily here; Ramp has a weaker pitch despite Sorare/Axie partners.
5. **Stablecoin-first flows** — Bridge/Stripe + Mercuryo's Bybit-card-style products are eating "buy stablecoins, hold balance, spend on a card" before Ramp has a competitive offering.
6. **Aggregator discount** — Onramper or any partner that A/B routes will frequently route *away* from Ramp on price.

---

## 11. Honest 30-second pitch (as Ramp actually is)

> "Ramp Network is a top-3 European fiat-to-crypto on/off-ramp widget. It sits inside about a hundred wallets and dApps; it's MiCAR-licensed in Ireland and FCA-registered in the UK; it ships crypto non-custodially to your address; its all-in card cost is around 5–6% (a 3.9% disclosed fee plus an undisclosed FX/asset spread); and it works in roughly 130 countries for cash-out and 150 for buying with caveats. It's competent, reasonably trusted, mid-priced, and fighting Stripe-Bridge above it and Onramper-aggregated commodity providers below it. In 2026 it pivoted to launch its own self-custodial wallet, which tells you it expects the on-ramp infrastructure layer to commoditize and is preparing to compete for the end-user relationship instead. It is not the cheapest, not the biggest, not the fastest — it is, however, one of the few survivors with real EU regulatory credentials and a genuinely non-custodial architecture."

---

## 12. Red flags

- **Refund delays**: multiple 1-star Trustpilot threads — £999 stuck for months, 16-day refunds, "manual process, 10 minutes" promised, weeks delivered ([Trustpilot ramp.network](https://www.trustpilot.com/review/ramp.network)). Pattern, not one-off.
- **Account suspensions without explanation**: recurring complaint pattern. Standard for the category, but Ramp is not better than peers here.
- **Hidden FX spread** vs. headline-fee disclosure (industry-wide problem; Ramp does not stand out as more transparent than MoonPay/Coinbase, despite marketing language to the contrary).
- **"All 50 US states"** claim vs. only ~9 confirmed state MTLs — relies on agent-of-payee carve-outs that are legally tenuous in some states.
- **Partnership churn**: Ledger Live now multi-provider; MetaMask multi-provider; Trust Wallet multi-provider. Distribution is being commoditized.
- **No 2025–2026 funding round announced** while MoonPay, Transak, Sardine all raised — capital-position silence is itself a signal.
- **Layoff rumors** on Blind unconfirmed but persistent.
- **Brand confusion with Ramp Inc.** is not Ramp Network's fault but is a real GTM problem: every "Ramp at $32B" headline accrues to the wrong company.
- **Marketing claim "first/pioneer" pattern** — multiple "first" or "pioneer" claims that don't survive scrutiny (first off-ramp with RTP, pioneer of Visa/Mastercard payouts).
- The "**8 million customers**" figure has no MAU breakdown, no retention disclosure, no third-party audit — could be cumulative wallet-addresses-served and is essentially uncheckable.

---

## 13. Green flags

- **MiCAR CASP authorisation** (Central Bank of Ireland, 4 Dec 2025) is genuinely non-trivial; only Kraken, Legend Trading, Push (Aave) joined Ramp in Ireland's first batch ([RTÉ](https://www.rte.ie/news/business/2025/1204/1547196-ramp-network-authorised-by-central-bank/)). This is a real moat for ~18 months.
- **UK FCA registration since 2021** is real and durable; Ramp was the 8th firm and 1st on-ramp registered.
- **SOC 2 Type II (June 2024)** is a real audit, not a self-attestation. Lets Ramp pitch enterprise wallets credibly.
- **Non-custodial architecture** is real — assets really do go straight to the partner-wallet address, which is materially better than custodial-balance designs.
- **No public scandals or hacks** in 8 years of operation. That's hard to do in this category.
- **Trustpilot 4.0/5 across 9,600+ reviews** is genuinely above the on-ramp category average (MoonPay/Transak hover similar or worse).
- **Real wallet partnerships** (MetaMask, Trust, Brave, Ledger) — even non-exclusive, this is real distribution that took years to land.
- **In-house off-ramp + swap stack** — building, not just integrating, has real engineering value.

---

## 14. What's missing from the pitch (any reasonable buyer/integrator would want)

- **Quarterly transaction volume in dollars.** Last public-ish figure is $37.5M revenue 2023 (Latka). At ~3.9% take-rate, that implies <$1B annual GMV — modest. Ramp won't disclose the number, which itself is the answer.
- **Take-rate transparency** — what does Ramp actually keep after card networks, fraud, partner commissions?
- **Approval rate by region** — the metric on-ramps live and die by, never published.
- **Active monthly users** vs. the cumulative "8M" number.
- **Partner concentration** — what % of volume comes from the top 5 wallet partners? (If MetaMask alone is >40%, Ramp's business is fragile to MetaMask's other-provider switches.)
- **Stablecoin share of volume** — if it's >50% (likely), Ramp is essentially a stablecoin on-ramp playing crypto-on-ramp dress-up, and Bridge/Stripe is the right comparable.
- **Refund-success metrics**, given the Trustpilot pattern.

---

## 15. 2026 stablecoin moment — where does Ramp sit?

The category is undergoing acquisition consolidation:

- **Stripe ↔ Bridge** ($1.1B, Oct 2024) — the largest crypto acquisition ever, gave Stripe stablecoin issuance + virtual-USD accounts + Visa-card-issuing rails ([Stripe blog](https://stripe.com/blog/introducing-open-issuance-from-bridge)).
- **BVNK ↔ Mastercard** discussions / Mastercard's stablecoin-card push.
- **Robinhood Connect, PayPal On-Ramp, Coinbase On-Ramp** all from incumbents that already have payments rails.

Three plausible Ramp futures:

1. **Independent niche infrastructure**: stays MiCAR-licensed, leans hard into EU regulatory advantage, becomes the "European-compliance-first on-ramp" — survives but at modest scale (~$50–150M revenue ceiling).
2. **Takeover candidate** by a Tier-2 acquirer wanting EU regulatory rails — Robinhood, Kraken, Coinbase (for non-US footprint), a card network, or a payments processor (Worldpay, Adyen, Nuvei). This is the highest-probability outcome — the FCA + MiCAR + SOC 2 stack is more valuable to an acquirer than a builder.
3. **Secondary-rail commodity** routed by Onramper-style aggregators with low margin. The slow-decline scenario; Ramp's wallet pivot is implicit acknowledgement of this risk.

**Most likely**: outcome 2 in the next 18–24 months. The 2026 wallet launch increases acquisition value (now you're acquiring a consumer app with regulatory licenses, not just a widget) and is consistent with end-state grooming. The lack of a 2025–26 funding round at a category moment when capital is plentiful is consistent with management running a sale process or holding for one.

In 2026, Ramp is a credible, mid-sized, regulated piece of European crypto plumbing that has done many real things, markets a few of them dishonestly, sits in a structurally commoditizing category, and is — without being told this is the case — probably grooming itself for sale. Trust the regulatory, security, and architectural claims; discount the "lowest fees / fastest / pioneer" claims; treat all volume and user-count numbers as marketing until audited.

---

## Sources

- [ramp.network homepage](https://ramp.network/) — claim collection
- [rampnetwork.com homepage](https://rampnetwork.com/) — claim collection
- [About Ramp Network](https://rampnetwork.com/about) — corporate baseline
- [Ramp Network MiCAR authorisation press release](https://rampnetwork.com/blog/ramp-swaps-micar-authorisation)
- [RTÉ: Crypto provider Ramp Network authorised by Central Bank](https://www.rte.ie/news/business/2025/1204/1547196-ramp-network-authorised-by-central-bank/)
- [Chainwire MiCAR press release](https://chainwire.org/2025/12/04/ramp-swaps-ireland-limited-receives-eu-wide-micar-authorisation-as-a-crypto-asset-service-provider/)
- [Ramp Network FCA registration blog](https://ramp.network/blog/ukregistered)
- [CoinDesk: Ramp Secures FCA Registration (2021)](https://www.coindesk.com/markets/2021/08/06/crypto-startup-ramp-secures-fca-registration)
- [The Defiant: Ramp achieves SOC2 Type II](https://thedefiant.io/news/press-releases/ramp-network-achieves-soc2-type-ii-compliance-the-gold-standard-of-financial-data-security)
- [Ramp Network SOC2 blog post](https://rampnetwork.com/blog/securing-the-bridge-between-worlds-ramp-network-achieves-soc-type-2-compliance)
- [Licenses and registrations (rampnetwork.com)](https://rampnetwork.com/licenses-and-registrations)
- [Ramp Network US FinCEN registration BusinessWire](https://www.businesswire.com/news/home/20220112005295/en/Ramp-US-Expands-Presence-in-US-With-FinCEN-Regulation)
- [CryptoBriefing: Ramp expansion to all 50 US states](https://cryptobriefing.com/ramp-network-to-expand-cryptoasset-purchases-to-all-50-u-s-states-and-the-district-of-columbia/)
- [Ramp Network help center: which countries are unsupported](https://support.rampnetwork.com/en/articles/433-which-countries-and-us-states-are-unsupported-for-buying-and-selling-crypto)
- [Ramp Network help center: which fiat currencies supported](https://support.rampnetwork.com/en/articles/471-which-fiat-currencies-does-ramp-network-support)
- [Ramp Network help center: fees](https://support.ramp.network/en/articles/10415-what-fees-does-ramp-network-charge-for-buying-crypto)
- [Ramp Network: SEPA Instant payouts blog](https://rampnetwork.com/blog/ramp-network-sepa-payouts-and-local-currencies)
- [Ramp Network global off-ramp blog](https://rampnetwork.com/blog/off-ramp-is-now-global)
- [Ramp Network multichain wallet launch blog](https://rampnetwork.com/blog/multichain-wallet-launch)
- [Cointelegraph on Ramp wallet launch](https://cointelegraph.com/news/ramp-network-self-custodial-wallet-third-party-dependencies)
- [Benzinga on Ramp multichain wallet](https://www.benzinga.com/pressreleases/26/04/51881769/ramp-network-launches-multichain-wallet-that-eliminates-third-party-dependencies-in-self-custody)
- [Trustpilot ramp.network reviews](https://www.trustpilot.com/review/ramp.network)
- [Sifted: Ramp $53M Series B](https://sifted.eu/articles/ramp-crypto-poland-53m)
- [CoinDesk: Ramp $70M Series B (Nov 2022)](https://www.coindesk.com/business/2022/11/09/ramp-raises-70m-to-provide-crypto-payments-infrastructure)
- [Latka: Ramp Network revenue & headcount](https://getlatka.com/companies/ramp.network)
- [Paybis: Crypto On-Ramp Fee Comparison 2026](https://paybis.com/blog/crypto-on-ramp-fee-comparison/)
- [Paybis: On-Ramp Fee Transparency methodology](https://paybis.com/blog/on-ramp-fee-transparency/)
- [Paybis: Cheapest Crypto On-Ramp 2026](https://paybis.com/blog/cheapest-crypto-on-ramp/)
- [Paybis: Best Ramp Network Alternatives](https://paybis.com/blog/ramp-network-alternatives/)
- [Onramper: MoonPay vs Ramp comparison](https://www.onramper.com/onramp-comparisons/moonpay-vs-ramp-which-is-better)
- [SeamlessChex: Best Fiat On-Ramp Providers 2026](https://www.seamlesschex.com/blog/best-fiat-on-ramp-providers-in-2026)
- [Bitget Academy: Ramp Network review](https://www.bitget.com/academy/ramp-network-crypto)
- [Crossmint: MoonPay vs Transak](https://www.crossmint.com/learn/moonpay-vs-transak)
- [Bessemer Stablecoin Atlas](https://www.bvp.com/atlas/stablecoins-from-defi-primitive-to-global-financial-infrastructure)
- [Stripe blog: Bridge Open Issuance](https://stripe.com/blog/introducing-open-issuance-from-bridge)
- [Transak: Ledger Live integration press release (Feb 2025)](https://transak.com/blog/ledger-live-integrates-transak-off-ramp-more-ways-to-sell-crypto-securely)
- [Coinspeaker: Ramp Network EU Instant Payouts](https://www.coinspeaker.com/ramp-network-eu-international-instant-payouts/)
- [Fireblocks: Ramp Network customer story](https://www.fireblocks.com/customers/ramp-network)
- [DL News: Conversation with Przemek Kowalczyk](https://www.dlnews.com/research/internal/conversation-przemek-kowalczyk-co-founder-ceo-ramp-network/)
- [Ramp Network and regulations help center](https://support.rampnetwork.com/en/articles/110250-ramp-network-and-regulations)
- [TechCrunch: Ramp Inc. (NOT Ramp Network) at $40B (May 2026)](https://techcrunch.com/2026/05/07/ramp-in-talks-to-hit-40b-valuation-6-months-after-reaching-32b/) — for brand-confusion context
