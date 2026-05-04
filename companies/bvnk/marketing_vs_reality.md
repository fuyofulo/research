# BVNK: The Skeptical Read on Mastercard's $1.8B Stablecoin Bet

*Critical analysis as of May 4, 2026 — six weeks after announcement, regulatory close still pending late 2026*

Confidence labels used throughout:
- ✅ Verifiable from primary source / multiple independent reports
- 🟡 Reasonable inference / single source / framing issue
- 🔴 Marketing claim, hand-wavy, or contested

---

## 1. The Marketing-vs-Reality Audit

### 1.1 The "$30B annualized volume" claim — what's real and what's framing

✅ **Verifiable**: BVNK ended 2025 at ~$30B annualized payment volume (2.8M transactions), up 2.3x year-over-year. The number was reported in BVNK's own 2025 retrospective and corroborated in Mastercard's deal materials and downstream press (CNBC, Fortune, S&P Global). They were at ~$20B annualized in October 2025, suggesting genuine acceleration, not back-loading for a sale.

🟡 **Framing issue**: "Annualized" means run-rate, not trailing actual. BVNK's actual processed volume across calendar 2025 was lower — the $30B is the December-2025 monthly volume × 12. Bridge made the same kind of framing pre-Stripe ($5B "annualized" coverage was used loosely). For comparison:
- Bridge: ~$5B annualized at Stripe acquisition (Feb 2025) → $1.1B = ~22% of volume
- BVNK: ~$30B annualized at Mastercard acquisition (Mar 2026) → $1.8B = ~6% of volume

Mastercard is paying a much *lower* multiple of volume than Stripe paid for Bridge, but a much higher absolute price. The headline "Mastercard paid more than Stripe" is misleading without that framing.

🔴 **Marketing-flavored**: BVNK conflates "payment volume" with revenue throughout its decks. Real revenue is ~$40M (William Blair / Mizuho post-deal notes via CNBC) to ~$104M (CompWorth's estimate, less reliable). Take rate is implicitly 13–35 bps, which is plausible for a mix of B2B FX and stablecoin orchestration but well below what a pure-play crypto payments processor with iGaming exposure would claim.

### 1.2 "130+ countries" — same playbook as Bridge

🔴 **Marketing-aggressive**: BVNK uses both "100+ countries" and "130+ countries" depending on the page. The 130+ is "supports payouts via SWIFT/SEPA/Fedwire/CHAPS/Faster Payments/ACH." That just means *the rails exist* — every fintech with SWIFT plumbing can claim 200+ countries on the same logic.

🟡 **Reality**: The Routefusion comparison piece is unusually candid (because it's a competitor pitch): "BVNK has limited SWIFT availability and limited local rails support" outside of EU/UK/US core. Routefusion claims full SWIFT + local rails in 40+ countries, while BVNK is "primarily stablecoin-focused with limited traditional payment rail coverage." That's a competitor framing, but the underlying point — that "130 countries" ≠ "production-grade off-ramp in 130 countries" — is correct.

🟡 **The Bitso partnership is the tell**: BVNK announced the Bitso Business partnership in Sept 2025 specifically to extend LATAM coverage. If BVNK had real LATAM rails, they wouldn't need Bitso. Same playbook Bridge ran with dLocal. Both are essentially API orchestrators on top of regional partner rails — which is a legitimate business model, but not what "130 countries" implies.

### 1.3 Customer roster — name-drops vs paying flow

✅ **Verifiable production customers**:
- **Worldpay** — public partnership for stablecoin payouts (Oct 2024, expanded 2025), 180+ market footprint claim
- **Deel** — public, "100+ countries" of stablecoin freelancer payouts
- **Visa Direct** — pilot announced Jan 2026 (before Mastercard deal)
- **Bitso, dLocal, LianLian, Rapyd, Thunes, Equals Money, IC Markets, Flywire** — named in Mastercard deal materials and BVNK's 2025 retrospective

🟡 **What's not disclosed**: BVNK never breaks out volume by customer. Worldpay alone — given Worldpay's scale — could plausibly be a double-digit-percentage of BVNK's $30B volume. That's customer concentration risk Mastercard inherits silently.

🟡 **Visa is awkward**: Visa Ventures invested in BVNK (May 2025) and Visa Direct ran a stablecoin pilot with BVNK (Jan 2026). Mastercard now owns BVNK's pipes feeding Visa's payouts. Either Visa pulls the pilot post-close, or it accepts that its stablecoin payout layer is owned by its biggest competitor. This is one of the most under-discussed strategic awkwardnesses of the deal.

### 1.4 Layer1 — what it actually is

✅ **Verifiable**: Layer1 is a self-hosted stablecoin payments stack (vault/key management, asset orchestration, trading engine) that BVNK launched as a separately-marketed product. Customers can BYO licenses, custodian, and liquidity. Chainalysis and Elliptic provide the compliance layer.

🟡 **Reality check**: Layer1 is essentially "BVNK's internal infrastructure repackaged as a deployable product." The "less than 200 lines of code, in just a few weeks" claim is the kind of marketing every infra-as-a-service vendor makes — true for the toy case, not the production case.

🔴 **Framing aggression**: "Layer1 powers stablecoin payments at scale" overstates traction. There are no public anchor Layer1 customers disclosed. It looks like the same play Stripe-Bridge made with Open Issuance — packaging white-label infra for issuers. But Bridge has shipped Phantom CASH and Sui USDsui via Open Issuance, both publicly. Layer1 has no equivalent public anchor.

### 1.5 "Trillion-dollar TAM" — how it's constructed

🔴 **Aggressive**: BVNK and Mastercard both cite the BCG figure that "stablecoin payment use cases grew 50%+ in 2025, reaching ~€350B addressable." That's stablecoin *flow*, not stablecoin *payments revenue*. At a 10-30 bps take rate, the actual TAM for orchestration-layer revenue is closer to €350M–€1B. Useful for a platform like BVNK to capture maybe $100–300M of revenue at maturity — a meaningful business, not a trillion-dollar one.

🟡 **The S&P Global / Bessemer framing is more honest**: stablecoin volume hit a $122B annualized payments run-rate in 2025, of which BVNK's $30B is ~25% — which would make BVNK genuinely category-defining. But this number excludes pure-treasury and trading flows, and comes from BVNK-published data.

---

## 2. The Mastercard Deal — What It Really Means

### 2.1 The multiples

Two anchor data points:
- **Bridge → Stripe (Feb 2025)**: $1.1B / ~$5B annualized volume = **22% of volume**, ~25–30x revenue
- **BVNK → Mastercard (Mar 2026)**: $1.8B / ~$30B annualized volume = **6% of volume**, ~45x revenue (at $40M rev) or ~17x revenue (at $104M rev)

🟡 The volume-multiple compression (22% → 6%) tells you the market repriced stablecoin infra *down* on a per-dollar-of-volume basis as more deals printed. The revenue-multiple expansion (~25x → ~45x) tells you Mastercard was bidding for *strategic positioning*, not financial returns.

✅ **Verified**: Coinbase had advanced talks at ~$2B (Fortune, Oct 2025) which fell apart before Mastercard re-engaged. So $1.8B is actually a *discount* to Coinbase's prior offer. Mastercard didn't overpay relative to the auction; it underpaid relative to what an asset-hungry Coinbase would have paid.

### 2.2 Why Mastercard paid MORE than Stripe paid for Bridge

The simple arithmetic answer: BVNK was 6x bigger by volume and 18 months further along in licensing.

The strategic answer (synthesizing TIKR, Coindesk opinion, Forrester, Datos, S&P):
- ✅ **Defensive, not offensive**. TIKR's "buying the stablecoin bridge to protect a $911 target" thesis holds up. Mastercard's core fear is that blockchain rails *collapse the message + settle simultaneously*, killing the 1–2 day settlement spread that funds the network.
- ✅ **Visa-Bridge was the forcing function**. Visa's Bridge partnership expansion to 100+ countries was announced March 3, 2026. Mastercard's BVNK announcement landed March 17, 2026 — two weeks later. This is not a coincidence. Mastercard had been in talks since Q3 2025 (per Fortune's Coinbase scoop), but the Visa expansion accelerated the close.
- 🟡 **Time-to-license premium**. Coindesk's opinion piece nails it: Mastercard paid "for the years it would have lost trying to replicate BVNK's regulatory footprint." MiCA CASP from Malta + UK FCA EMI + 25+ licenses globally would take 3–5 years to assemble organically. The licensing optionality alone is worth several hundred million.

### 2.3 Mastercard's actual stablecoin strategy

✅ Mastercard now has a stack that looks like:
1. **Multi-Token Network (MTN)** — private blockchain for tokenized deposits and stablecoin settlement
2. **Crypto Credential** — wallet-aliasing + Travel Rule compliance
3. **Crypto Partner Program** — 85+ digital asset firms (Binance, Crypto.com, Bybit, Gemini, Ripple, Circle, PayPal)
4. **Stablecoin issuer enablement** — USDC, PYUSD, USDG, FIUSD, SoFiUSD all settle on the network
5. **BVNK** — orchestration, off-ramp, licensing layer that ties it all together

🟡 The deal makes BVNK the "fiat ↔ stablecoin ↔ MTN" connector. Mastercard becomes credible as a settlement layer for any stablecoin issued by anyone, on any chain — which is what neutral interoperability looks like in practice.

🔴 **The neutrality question is genuinely open**. Bridge under Stripe still issues for Phantom, Sui, MetaMask, Hyperliquid — neutrality preserved, mostly because Stripe doesn't compete with those clients. BVNK under Mastercard will face pressure to deprioritize Visa-related work and to channel issuance to Mastercard-friendly chains. Watch whether BVNK's existing Visa Direct pilot survives the close.

### 2.4 Defensive vs offensive

🟡 The honest answer is **65% defensive, 35% offensive**:
- Defensive: Stop the disintermediation by owning the rails that would replace you
- Offensive: Capture B2B cross-border (which was never well-served by cards anyway), agentic-commerce settlement (Mastercard's "agentic commerce" buzzword), and conversion-spread economics on stablecoin ↔ fiat flips

The Datos analyst framing — "neither an experiment nor a hedge against structural obsolescence in B2C, but a bet on B2B tokenized infrastructure" — is the most precise framing I've seen.

---

## 3. iGaming Reputation — Risk or Moat?

### 3.1 The unspoken history

🟡 **Founder lineage matters**: Jesse Hemson-Struthers' prior company **BetTech Gaming** was acquired by **Sportradar** (sports data, integrity, betting infrastructure). His other prior venture was **Coindirect**. The South African crypto-gaming nexus (Coingaming/Yolo, Bitcasino.io, Sportsbet.io) is well-documented as an early adopter cluster for stablecoin settlement. BVNK didn't build its early volume on Worldpay enterprise contracts — it built it on iGaming/crypto-gambling rails, then *moved upmarket*.

🔴 **BVNK never publishes vertical mix**. There's no "iGaming is X% of our 2025 volume" disclosure. The fact that BVNK still maintains an iGaming-specific marketing page (`/blog/crypto-payment-trends-shaping-igaming`) in 2026 suggests it remains a meaningful vertical.

### 3.2 Mastercard's exposure

🟡 **Mastercard already polices MCC 7995 (gambling) aggressively**. Internal compliance will absolutely audit BVNK's customer book post-close. Three plausible outcomes:
1. Off-board the worst offenders (offshore, lightly licensed casinos)
2. Ring-fence iGaming into a separate reporting entity that doesn't sit under the Mastercard brand
3. Allow current customers to grandfather, prohibit new iGaming originations

✅ The closing is "subject to regulatory review and customary closing conditions" through end of 2026. EU and UK competition regulators will examine BVNK's customer book during clearance. If iGaming is >25% of volume, expect leaked reports of carve-out demands by Q3 2026.

🟡 **No public reports of iGaming-related friction yet** — but six weeks is too early. Watch for Q2/Q3 earnings commentary from Mastercard.

---

## 4. Where BVNK Is Weak vs Bridge

| Dimension | Bridge | BVNK | Verdict |
|---|---|---|---|
| Distribution moat | Stripe's millions of merchants, instant cross-sell | Mastercard's brand and bank network — but not a customer base in the same way | 🔴 **Bridge wins decisively**. Stripe already had the demand; BVNK still has to sell. |
| US bank charter | OCC conditional approval Feb 2026 | None pursued; relies on partner banks | 🔴 **Bridge wins**. This is a 2–4 year head start on regulated reserve management. |
| Card network partnership | Visa, expanding 18→100+ countries by EOY 2026 | Now owned by Mastercard, but had been a Visa Direct partner | 🟡 **Bridge wins on consumer**, BVNK wins on B2B settlement |
| Open Issuance traction | Phantom CASH, Sui USDsui, MetaMask, Hyperliquid | None publicly anchored on Layer1 | 🔴 **Bridge wins decisively**. Issuer capture went to Bridge first. |
| Bank partner stack | Lead Bank + Modulr + Bridge's own (pending) trust charter | Cross Bank, Customers Bank, partner BIN sponsors, MFSA-licensed Maltese entity | 🟡 Roughly comparable, slight Bridge edge once trust charter closes |
| US state coverage | Federal trust charter pathway | "Full US state-wide coverage" claim — verifiable for MTLs, less so for production volume | 🟡 BVNK has wider state coverage today, Bridge will leapfrog with federal charter |

🔴 The honest summary: **BVNK is structurally behind Bridge on every consumer-facing dimension and roughly tied on B2B/enterprise**. Mastercard's buy doesn't close those gaps; it just gives BVNK a deeper-pocketed parent.

---

## 5. Where BVNK Might Be Stronger Than Bridge

### 5.1 Pricing transparency
🟡 BVNK publishes a Pricing Policy (bvnk.com/mt-mt/pricing-policy) that breaks out conversion fees (BVNK Rate + Commercial Fee), transfer fees (tiered % + fixed), onboarding/platform/MMC structure, and weekly network-fee estimates. Bridge publishes essentially nothing. The Routefusion comparison piece is unusually concrete on BVNK's stablecoin support matrix. **Minor edge to BVNK** for enterprise procurement teams that need pricing artifacts for legal/finance review.

### 5.2 EU/UK posture
✅ **Real edge**. BVNK has:
- UK FCA EMI (via System Pay Services, 2022)
- Malta MFSA EMI + MiCA CASP
- SEPA direct access
- "Three critical capabilities in single platform" (MiCA + EUR payments + SEPA) — genuinely differentiated as of late 2025

Bridge is US-anchored and has weaker EU posture. Post-MiCA full rollout (Dec 2024), BVNK is the cleaner EU choice.

### 5.3 LATAM and emerging markets
🟡 BVNK's Bitso partnership (Sept 2025) and LianLian partnership (June 2025, China cross-border) give it Asia + LATAM coverage that Bridge has *not* publicly matched. But these are partnership-derived, not native — Bridge could replicate either inside 90 days. The moat is shallow.

### 5.4 iGaming vertical
🟡 BVNK's iGaming muscle memory — KYC for high-risk merchants, chargeback management, crypto deposit/fiat settlement flows — is real expertise that Bridge does not have and will not develop. **This is genuinely differentiated**, but it's also the dimension Mastercard is most likely to deprioritize.

### 5.5 Technical / DX
🟡 Mixed. Bridge's developer experience is widely praised (Sam Boboev: "best-in-class DX for stablecoin-native payments"). BVNK's API is enterprise-feeling — "open virtual multi-currency accounts, payments across SWIFT/SEPA/FedWire/ACH and blockchains, unified ledger." That's more coverage but more friction. **Bridge wins for crypto-native devs, BVNK wins for enterprise integrators.**

---

## 6. Post-Acquisition Competitive Landscape

### 6.1 Who's left independent?

| Player | Status | Outlook |
|---|---|---|
| **Zero Hash** | Independent. Filed for OCC trust charter March 2026. Focus: trading + custody + stablecoin remittance. | 🟡 Most credible independent. Mastercard reportedly looked at Zero Hash before BVNK (per Fortune, Oct 2025). Acquisition target for Visa or a tier-2 network within 18 months. |
| **Crossmint** | Independent. MoneyGram, Western Union as clients. Wallets + stablecoin orchestration + 150+ country offramps. | 🟡 Smaller, more crypto-native. Likely raises again rather than sells. |
| **Brale** | Independent. White-label issuance focus. | 🟡 Niche. Possible Circle or Paxos M&A target. |
| **Routefusion** | Independent. Multi-rail (stablecoin + SWIFT + local) angle. | 🟡 Best positioned for the "we never wanted to be crypto-first" buyer (Western Union, MoneyGram, Wise). |
| **Circle** | Public (NYSE: CRCL). | ✅ The neutral issuer. The one player that *gained* from both Bridge → Stripe and BVNK → Mastercard, because both incumbents now have to issue/settle through Circle's USDC pipes. |
| **Paxos** | Independent, well-funded. PYUSD, USDG. | 🟡 Likely independent for now; PayPal partnership is too valuable to risk by selling. |

### 6.2 Is the window closed?

🟡 **For "Bridge/BVNK clones" — yes, it's closed**. The two payment networks have made their picks. A third pure-play stablecoin orchestration platform competing on the same axis (multi-chain, multi-currency, regulated, B2B) would struggle to find an independent buyer.

🟡 **For specialized angles — wide open**:
- iGaming-specific stablecoin rails (since both Bridge and BVNK will deprioritize this)
- LATAM-native (BlindPay, Lulo, others)
- Africa-native (Yellow Card, Onafriq)
- Agentic-commerce-native (BVNK's "agentic" buzzword is empty; nobody owns this category yet)
- Issuer-neutral, brand-agnostic (because Bridge and BVNK both have captured-distribution problems now)

### 6.3 Neutrality

🟡 The neutrality question is the single most interesting strategic question. Bridge has so far preserved neutrality (Phantom, Sui, MetaMask, Hyperliquid all built on Open Issuance). The reason: Stripe doesn't compete with wallets and L1s.

Mastercard *does* compete with banks-issuing-stablecoins (FIUSD/PYUSD partners). Mastercard *does* compete with Visa-Bridge. Mastercard owning BVNK creates structural conflicts the way Stripe owning Bridge does not. Expect at least one major BVNK customer to defect within 12 months — most plausibly someone in the Visa orbit.

---

## 7. Founders / Team Post-Deal

✅ **Confirmed (BVNK blog "Why BVNK is joining Mastercard," Mastercard press release)**: BVNK will "continue to operate independently" with Hemson-Struthers continuing as CEO post-close.

🟡 **The standard playbook**: 4-year vest cliff, with most equity tied to performance milestones (the $300M contingent payments). Founders have $300M+ each in liquid wealth at close — historical pattern says they ride out 18–24 months of integration, then exit to launch the next thing or join a venture firm. Compare:
- **Zach Abrams (Bridge)** — stayed at Stripe as Bridge CEO, still active 14 months post-close. Worked because Stripe gave Bridge real autonomy.
- **BVNK trio** — Hemson-Struthers (CEO), Jackson (CTO), Harmse (CBO) all South African, all with prior exit experience to large incumbents (Naspers, Sportradar). They know the integration playbook.

🟡 **My base case**: Hemson-Struthers stays through 2027 to hit earnouts, then exits. Jackson (CTO) is the highest flight risk — CTOs of acquired startups historically have the worst retention, and Jackson has the most fungible skill set.

🔴 No public org-chart leaks. The deal is too fresh.

---

## 8. The Dual-Positioning Game

🟡 BVNK's website positions exclusively to enterprise: "Build your stablecoin strategy," "Enterprise stablecoin payments infrastructure," 25+ licenses, SOC 2 / ISO 27001. Zero crypto-native bro-speak. Compare to Bridge's site, which leans much more developer-y.

🟡 But the **iGaming blog content** (`/blog/crypto-payment-trends-shaping-igaming`) is a separate audience play — the audience is iGaming product managers, not enterprise CFOs. So there is dual-positioning, just less obvious than Credible-type two-faced startups.

🟡 The Stablecoin Utility Report 2026 (`bvnk.com/utility`) is the third positioning surface — thought-leadership content for the institutional/policy audience. Three audiences, three surfaces. Standard enterprise playbook.

---

## 9. What Industry Insiders Are Actually Saying

### 9.1 Bullish (incumbent-friendly)

- ✅ **Mizuho's Dan Dolev**: "Stablecoins are integral to the future of payments" — generic validation
- ✅ **William Blair**: "Affirmation of the stablecoin market for cross-border commerce, rather than B2C, which is well served by card" — most precise framing of the strategic logic
- ✅ **Forrester** (Aurélie L'Hostis blog): "fintechs offering cross-border payouts must now differentiate or partner with Mastercard"
- ✅ **Datos Insights**: "neither an experiment nor a hedge — a bet on B2B tokenized infrastructure"

### 9.2 Skeptical (the more interesting takes)

- ✅ **TIKR (Mar 2026, "Buying the stablecoin Bridge to protect a $911 target")**: Frames the deal explicitly as defensive vs disintermediation. The key line: "open-source blockchains threaten to collapse this architecture by processing the message and settling the funds simultaneously, bypassing Mastercard's tollbooth entirely." Best skeptical analysis available.
- ✅ **Coindesk Opinion (Mar 27, 2026, "Why Mastercard paid double for stablecoin infrastructure it could have built")**: Argues the premium is for licensing time-to-market, not technology. "Mastercard paid for the years it would have lost trying to replicate BVNK's regulatory footprint."
- ✅ **TheStreet ("Anyone else never hear of BVNK?")**: Captures the popular-finance take — BVNK's brand recognition lags its strategic importance, suggesting Mastercard bought infrastructure value, not customer trust value.
- ✅ **a16z crypto ("The month fintechs embraced stablecoins")**: Frames Stripe-Bridge, Stripe-Privy, and Mastercard-BVNK as the *same map* — incumbents racing to lock down the new BaaS stack before it settles. Implicit: this is consolidation, not innovation.
- 🟡 **Sam Boboev's deep dive (BVNK vs Bridge vs Zero Hash)**: Most balanced comparison. Verdict: Bridge wins DX, BVNK wins enterprise infra, Zero Hash wins flexible custody. No dominant player; vertical specialization wins.
- 🟡 **Jas Shah's "Bvnking on Stablecoin" (Oct 2025)**: Pre-deal, but useful for tracing BVNK's modular product stack and Layer1 strategy. Notably, his October 2025 figure of ~$19–20B annualized matches the Mastercard deal-time disclosure of $20B in October — confirming BVNK's published trajectory.
- 🔴 **Linas Beliūnas Substack ("Mastercard paid $1.8 billion for stablecoin FinTech BVNK because it can't afford not to")**: Most pointed skeptical take — the "can't afford not to" framing implies overpayment driven by FOMO, not strategic logic. Worth reading as the most negative published take.

### 9.3 Genuinely missing from the discourse

- 🔴 No public Sacra deep-dive on BVNK post-deal as of early May 2026 (Sacra has a profile page but no fresh analysis)
- 🔴 No Bessemer Atlas update specifically on the deal (their stablecoin Atlas piece predates the announcement)
- 🔴 No Empire / Bankless / Cheeky Pint long-form podcast episode specifically on BVNK (closest is general post-acquisition discussion)
- 🔴 No major iGaming-press coverage of the deal — which itself is a signal. iGaming press would normally cover this aggressively if BVNK were a known iGaming brand. The silence suggests BVNK has successfully laundered its iGaming-adjacent origins into "enterprise B2B" positioning.

---

## 10. The Honest 30-Second BVNK Pitch

🟡 **Marketing version**:
> "BVNK is the global stablecoin infrastructure platform powering enterprise payments in 130+ countries — Worldpay, Deel, Visa, Flywire — with $30B annualized volume, MiCA-licensed, and now part of Mastercard."

✅ **Honest version**:
> "BVNK is a London-based stablecoin orchestration layer founded by South African crypto-gaming alumni in 2021. Its real edge is regulatory: it spent four years assembling MiCA + UK FCA + 25 other licenses while everyone else was chasing chains. Volume is real ($30B annualized run-rate, mostly cross-border B2B + treasury + iGaming-adjacent), revenue is modest (~$40M, possibly $100M), and the product is two things stitched together: a multi-currency virtual-account API on top of partner banks (the 'BVNK' product) and a self-hosted stablecoin stack for issuers (Layer1, no anchor customers yet). Mastercard didn't buy a tech moat — they bought 4 years of regulatory work, an enterprise customer book, and a defensive position against Visa-Bridge. At $1.8B / $30B volume, the multiple is roughly a quarter of what Stripe paid for Bridge, suggesting the market has already repriced stablecoin infra, even as the absolute headline got bigger. The interesting question isn't 'did Mastercard overpay' — they didn't, especially vs Coinbase's $2B prior offer — but 'can a Mastercard-owned BVNK stay neutral enough to keep serving Visa Direct, Phantom-style issuers, and rival fintechs?' That's where the real value is, and that's where the structural conflict starts."

---

## Confidence Summary

| Claim | Confidence |
|---|---|
| BVNK volume of $30B annualized at deal | ✅ |
| Revenue ~$40M (with $100M ceiling estimate) | 🟡 |
| Deal structure $1.5B + $300M contingent | ✅ |
| Coinbase prior $2B offer fell through | ✅ |
| Mastercard motivated primarily by Visa-Bridge defense | 🟡 (strong inference, multiple analysts agree) |
| iGaming is meaningful current vertical | 🟡 (founder lineage + maintained marketing surface, no quantified disclosure) |
| BVNK weaker than Bridge on consumer/distribution | ✅ |
| BVNK stronger than Bridge on EU regulatory posture | ✅ |
| Visa Direct pilot survives the close | 🔴 (genuine open question) |
| Founders stay through 2027 | 🟡 (base case, no announcement) |
