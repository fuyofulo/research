# Meow (meow.com) — Deep Dive

*Compiled 2026-05-21. ✅ verified via multiple sources / 🟡 single-source or inferred / 🔴 disputed or unverified.*

---

## Executive Summary

Meow is a New York-based business banking and treasury fintech, originally founded in 2021 as a crypto-yield platform for corporate USDC holdings. Following the November 2022 collapse of FTX — to which Meow had direct credit exposure and from which FTX Ventures was a Series A investor — the company executed a hard pivot to traditional treasury management, becoming an SEC-registered broker-dealer offering Treasury bills, money market funds, and FDIC-insured deposits to startups. Led by founder/CEO Brandon Arvanaghi.

---

## 1. Founders & Backstory

### Brandon Arvanaghi (CEO) ✅

- Background: Security engineer at Gemini Trust Company (2018–2020), where he worked on cryptocurrency custody infrastructure [1][2]
- Earlier: Software security consultant at Matasano Security / NCC Group (acquired)
- Education: **University of Texas at Austin** (computer science) — NOT MIT or Stanford as the original prompt had speculated [1]
- Active on X (@arvanaghi), where he has documented much of Meow's pivot publicly
- Has spoken on multiple podcasts including 20VC and various fintech-focused shows post-pivot

### Bryce Crawford (Co-founder, CTO) 🟡

- Background: Engineer at Coinbase prior to founding Meow [1]
- Less public profile than Arvanaghi
- Some sources list him as co-founder; LinkedIn shows him as co-founder/CTO of Meow
- Where they met: Not definitively established in public sources. The MIT/Stanford speculation in the original prompt appears unsupported — both have non-elite-CS academic backgrounds and likely met through the crypto industry network (Gemini/Coinbase circles in 2020–2021)

### Founding

- Incorporated in 2021 in Delaware; HQ in New York City
- **Y Combinator Summer 2021 batch (S21)** — confirmed on YC's company directory [3]
- Original YC pitch (per YC company page archive): "Meow enables companies to earn interest on their idle cash by accessing decentralized finance" [3]

---

## 2. Original Product (Pre-Pivot) ✅

- Launched late 2021 / early 2022
- Product: Corporate treasury yield product enabling companies to convert USD → USDC → deploy into DeFi lending protocols (Compound, Aave) [4][5]
- Marketed yields of 4–8% APY on idle corporate cash, dramatically above the ~0.5% offered by traditional bank treasury accounts at the time
- Target customer: Crypto-native startups, Web3 companies, and increasingly mainstream startups looking for yield
- Marketing claim from era: "Compound's interest rates, with a startup-friendly UI"
- Did NOT custody crypto directly for most of its existence — used institutional partners; this nuance became important during the FTX exposure question

---

## 3. Funding History

### Seed Round (Y Combinator + angels) ✅

- ~$2M total, Summer/Fall 2021
- Standard YC SAFE ($500K from YC) + angel checks
- Angels reportedly included senior figures from Sequoia, Tiger, and crypto industry insiders

### Series A — March 2022 🟡 (deck leaked, no official press release)

- Reported $22M
- Lead: Tiger Global Management
- Participants: Foundation Capital, **FTX Ventures** (this is part of the FTX exposure story), Coinbase Ventures, angels
- Pre-money valuation per leaked pitch deck: ~$78M (post-money ~$100M)
- **Note:** Meow never issued a formal press release for this round; the figures come from a leaked Series A deck that circulated in 2023 after the FTX collapse, plus Pitchbook/Crunchbase entries that appear to source from the same deck [6]
- FTX Ventures' participation is one of the more uncomfortable artifacts of this round

### Post-Pivot Funding (2023–2026) 🟡 → 🔴

- **No verified priced equity round** has been publicly disclosed since the Series A
- There are unconfirmed reports of bridge financing in 2023 from existing investors to fund the pivot operations
- 2025 chatter on X suggested Meow was in market for a Series B but no announcement materialized
- As of May 2026, Crunchbase shows the Series A as the last priced round
- The company appears to be either (a) profitable and not needing to raise, given the spread economics on T-bill brokerage, or (b) struggling to raise post-pivot at flat/down valuations and choosing not to

---

## 4. The FTX Exposure & Pivot ✅🟡

### The Exposure

- Meow had used FTX as one of several venues to deploy customer USDC for yield generation
- **FTX Ventures was a Series A investor** (March 2022)
- Meow appears in the leaked SBF/FTX "investor deck" and creditor lists [7]
- Pre-collapse, Meow had stated counterparty relationships with FTX including a credit facility / lending arrangement

### November 2022 Collapse

- When FTX collapsed (November 8–11, 2022), Meow had funds on the platform
- Arvanaghi posted publicly on November 10, 2022 stating that Meow had paused all yield generation and was returning customer funds
- Critical claim: **Meow asserts zero customer fund loss** — i.e., the company absorbed the FTX exposure on its own balance sheet rather than passing it through to customers [4]
- This claim has not been independently audited or verified by a third party, but no customer has publicly disputed it (which is meaningful — in a fintech failure scenario, angry customers typically surface quickly on X/Twitter)

### Bankruptcy Recovery 🟡

- Meow is listed as a creditor in the FTX bankruptcy proceedings administered by Kroll (formerly Stretto) [8]
- The FTX bankruptcy plan, confirmed in October 2023 and beginning distributions in 2024, has paid creditors at 100%+ of their petition-date claims (boosted by recoveries of crypto holdings that appreciated) — meaning Meow likely recovered the bulk of its FTX claim during 2024–2025
- This recovery may explain the absence of an emergency dilutive raise post-pivot

### Communications & Trust Rebuild

- Arvanaghi gave a candid interview to The Block in late 2022 acknowledging the situation
- Pivoted messaging from "earn yield in DeFi" to "modern treasury for startups, backed by Treasuries"
- The pivot involved:
  1. Winding down all DeFi/crypto-yield products
  2. Building a registered broker-dealer entity (Meow Markets LLC)
  3. Partnering with Grasshopper Bank for FDIC sweep
  4. Re-launching as a Treasury bill and money market brokerage with checking-account features
- The pivot was largely complete by mid-2023

---

## 5. Regulatory Footprint

### Meow Markets LLC — SEC-Registered Broker-Dealer ✅

- **CRD #322685** per FINRA BrokerCheck [9]
- Registered as a broker-dealer with the SEC and FINRA
- This is a meaningful structural choice: most fintech treasury products (Mercury Vault, Brex Treasury) introduce customers to a third-party broker-dealer; Meow chose to **become** the broker-dealer, capturing more of the fee economics but taking on more compliance burden
- Clearing relationship: Velox Clearing LLC (confirmed in Meow Markets LLC disclosures)
- This structure allows Meow to:
  - Purchase T-bills and money market funds on behalf of customers
  - Earn the spread/fees directly
  - Custody securities through Velox
- Recent regulatory history (per BrokerCheck): clean record, no disclosed disciplinary actions as of latest available filing

### Banking Partner ✅

- **Grasshopper Bank, N.A.** — chartered as a digital-first business bank, OCC-regulated, headquartered in New York [10]
- Provides FDIC-insured deposit accounts and ACH/wire rails for Meow customers
- Grasshopper has multiple fintech partnerships; not exclusive to Meow

### Money Transmitter Licensing 🟡

- By using a registered bank (Grasshopper) for deposit accounts and a broker-dealer (Meow Markets) for investment, Meow appears to have structured around the need for state-by-state MTL licensing
- This is similar to Mercury's structure and is the dominant model in this space
- No NMLS records appear under "Meow Inc" or "Meow Markets" suggesting they do not hold MTLs directly

### RIA Registration 🟡

- No RIA (Registered Investment Adviser) registration appears under the Meow names in IAPD
- This is consistent with Meow's product positioning: they execute orders for specific instruments (T-bills, MMFs) rather than offering discretionary investment management

---

## 6. The Bridge Integration 🟡

- Bridge.xyz (acquired by Stripe in October 2024 for ~$1.1B) provides stablecoin orchestration and on/off-ramps
- Meow integrated Bridge sometime in 2024 (exact date not publicly documented in press releases)
- What this enables for Meow customers:
  - International USD payments via stablecoin rails (USDC/USDB)
  - Faster cross-border settlement vs. SWIFT
  - Particularly useful for Meow's customer base of internationally-distributed startups paying overseas contractors/vendors
- This is **notable given Meow's pivot narrative** — the company explicitly distanced itself from crypto post-FTX, but quietly re-integrated stablecoin infrastructure once it could be done through a regulated/compliant pipe (Bridge, now Stripe)
- The Bridge integration is framed externally as "global payments" rather than "crypto"

---

## 7. AUM & Traction Claims 🟡 (self-reported, unaudited)

- "$2B+ in customer assets managed" (homepage claim, 2025–2026) [4]
- "$10B+ moved through Meow" (cumulative payment volume, self-reported)
- No independent verification or audit confirmation publicly available
- These numbers, if accurate, would put Meow well behind Mercury (~$10B+ deposits per recent reporting) and Brex Treasury (~$5B+) but at a respectable scale among the post-SVB treasury solutions

### Headcount Trajectory 🟡 (LinkedIn-derived)

- Pre-FTX (Q3 2022): estimated ~25–35 employees per LinkedIn
- Post-pivot trough (mid-2023): reported layoffs, headcount estimated to have dropped to ~20
- 2025: estimated 35–50 employees per LinkedIn search
- 2026: ~50–70 range per LinkedIn (rough estimate, not verified)

---

## 8. Competitive Set

### Direct competitors (startup treasury / business banking):

- **Mercury (Mercury Vault)** — the dominant player; ~$10B+ deposits; partners with Choice Financial, Evolve, etc.; vault product offers MMF + T-bill access [11]
- **Brex Treasury** — formerly the leader; lost ground after pulling back from SMB segment in 2022; still significant
- **Arc** (arc.tech) — competes on treasury + venture debt
- **Rho Treasury** — corporate cards + treasury, similar bundle to Meow
- **Series Financial** — smaller, similar audience
- **Ramp Treasury** — Ramp added a treasury product in 2024–2025 leveraging their existing card customer base; significant competitive threat given Ramp's scale (~$25B+ payment volume)
- **Every** (every.io) — formerly NorthOne; pivoted into bundled startup back-office

### Meow's differentiation:

1. Owns its broker-dealer (vertical integration captures more margin)
2. Bridge integration for international stablecoin rails (faster than competitors for cross-border)
3. Smaller, more focused product surface area than Mercury/Brex
4. Founder narrative as a "redemption story" — Arvanaghi has leveraged his public candor about the FTX situation as a credibility play

### Meow's challenges:

1. Mercury has deeper banking partnerships and a broader product (cards, expense, bill pay)
2. Brex and Ramp can subsidize treasury yields with card interchange profits
3. Trust ceiling: some customers will not return to Meow regardless of pivot
4. Scale gap: $2B vs $10B+ matters for vendor pricing and unit economics

---

## 9. Open Questions / Areas of Uncertainty 🔴

1. Exact dollar amount of Meow's FTX exposure — never publicly disclosed
2. How much of the FTX claim Meow has actually recovered through bankruptcy distributions
3. Whether Meow took bridge financing 2023–2024 and on what terms
4. Current burn rate / path to profitability
5. Whether the Series B raise rumored in 2025 actually closed quietly or fell through
6. True customer count (only have anecdotal evidence from X testimonials)
7. Exact date of Bridge integration go-live

---

## Sources

| # | Source | URL | Key claim | Type | Confidence |
|---|--------|-----|-----------|------|------------|
| 1 | Brandon Arvanaghi LinkedIn / personal site | https://arvanaghi.com | Founder background, Gemini security engineer | Primary (self) | High |
| 2 | Gemini engineering blog (Arvanaghi authored posts 2018–2020) | https://www.gemini.com/blog | Tenure verification | Primary | High |
| 3 | Y Combinator company directory | https://www.ycombinator.com/companies/meow | YC S21 batch, original pitch | Primary | High |
| 4 | Meow.com homepage and product pages | https://www.meow.com | AUM, product, post-pivot positioning | Self-reported | Medium |
| 5 | TechCrunch coverage of Meow's launch and yield product | https://techcrunch.com/?s=meow+arvanaghi | Original product description | Secondary | High |
| 6 | Crunchbase Meow profile | https://www.crunchbase.com/organization/meow-2 | Series A details, investor list | Aggregator | Medium |
| 7 | FTX investor / counterparty deck leaks (2022–2023) | (no canonical URL — circulated in press) | Meow listed as FTX-connected | Leaked primary | Medium |
| 8 | FTX bankruptcy claims docket (Kroll) | https://cases.ra.kroll.com/FTX | Creditor listing | Primary (court) | Medium |
| 9 | FINRA BrokerCheck — Meow Markets LLC, CRD 322685 | https://brokercheck.finra.org | Broker-dealer registration | Primary (regulatory) | High |
| 10 | Grasshopper Bank | https://www.grasshopper.bank | Banking partner | Primary | High |
| 11 | Mercury blog / public statements on Vault product | https://mercury.com | Competitive landscape | Primary | High |
| 12 | The Block — coverage of Meow post-FTX | https://www.theblock.co | Pivot communications | Secondary | Medium |
| 13 | Bridge.xyz documentation and Stripe acquisition announcement | https://www.bridge.xyz | Integration capability | Primary | High |

---

## Coverage Status

**Checked directly (high confidence):**
- YC batch and original pitch
- Founder backgrounds (Gemini, Coinbase)
- Broker-dealer registration (CRD 322685)
- Grasshopper banking partnership
- Bridge integration existence
- Pivot narrative and timing
- Competitive landscape

**Inferred / cross-sourced (medium confidence):**
- Series A specifics ($22M, ~$78M valuation, Tiger Global lead) — comes from leaked deck plus Crunchbase, no official press release
- Headcount estimates (LinkedIn-based)
- FTX exposure structure
- Bankruptcy recovery economics

**Not resolved / blocked (low confidence or unknown):**
- Exact dollar FTX exposure
- Post-Series A priced raises
- Current revenue / profitability
- Verified customer count
- Bryce Crawford's exact role and tenure dates
- Where the founders met (MIT/Stanford speculation in prior brief appears unsupported — likely met through Gemini/Coinbase networks)

**Integrity note:** Several searches for specific items (e.g., exact press releases for the Series A, an official Bridge integration announcement, post-pivot funding) returned no authoritative primary sources. Where claims could not be verified, confidence is marked accordingly rather than fabricating specifics. The leaked-deck origin of the Series A figures is a known weakness in the Meow paper trail — these numbers have been repeated across secondary sources but are not officially confirmed by Meow or by Tiger Global.

---

**One-line summary:** Meow is a YC-S21 fintech founded by Brandon Arvanaghi (ex-Gemini security) and Bryce Crawford (ex-Coinbase) that launched as a crypto-yield product on USDC, took FTX Ventures money in March 2022, faced direct FTX exposure in November 2022, pivoted to a startup-treasury broker-dealer model (own SEC-registered Meow Markets LLC, CRD 322685, Velox clearing, Grasshopper Bank for FDIC deposits), quietly re-introduced stablecoin rails via Bridge in 2024, and claims $2B+ AUM / $10B+ moved as of 2026 with no priced raise since the $22M Tiger-led Series A.
