# Altitude (altitude.xyz) — Deep Dive

*Company history, founders, funding, regulatory/legal footprint*
*Compiled 2026-05-04*

---

## TL;DR

Altitude is **not its own company** — it is the flagship product of **Squads Labs** (the team behind Squads Protocol, Solana's dominant multisig/smart-account standard). The Solana developer asking about altitude.xyz is really asking about Squads Labs' newest go-to-market wedge: a "stablecoin-native USD account for businesses" that uses Squads' programmable smart-account primitives as the underlying custody layer and Solana as the settlement layer. ✅ ([Squads PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html), [Blockworks](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan), [The Block](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude))

Altitude was teased at end-2024 / early-2025, **publicly launched in December 2025**, and as of the **April 29, 2026** funding announcement has processed **>$200M** in payments. ✅ Squads/Altitude has cumulatively raised **~$42.9M across 4 disclosed rounds** (Oct 2021 seed, Feb 2022 round, Oct 2023 strategic, Jun 2024 Series A, Apr 2026 strategic). ✅ It runs as an **unregulated self-custodial product** plumbed into licensed PSPs (Bridge, MoonPay, Infinite, Due) for the regulated leg of money movement — it does **not** itself hold money-transmitter, MSB, MiCA, FCA, or MAS licenses. 🟡

Confidence legend: ✅ verified from multiple independent sources / primary disclosures; 🟡 inferred from a single source or strong indirect signal; 🔴 marketing claim or company-controlled disclosure not independently verified.

---

## 1. What is Altitude and what problem does it solve?

Altitude is positioned as a **"financial operating system for businesses on the frontier"** — multi-currency USD/EUR business accounts, corporate Visa cards, ACH/wire/SEPA + USDC/EURC payments, ~5% APY on stablecoin balances, and a CFO stack (invoicing, bill pay, batch payments) — where **every business "account" is actually a programmable smart account on Solana** rather than a bank ledger row. ✅ ([Squads/Altitude product page](https://squads.xyz/altitude), [Squads PR](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html))

**The core wedge:** stablecoins replace fractional-reserve banking for the *holding* layer; Solana replaces SWIFT/ACH for the *settlement* layer; and Altitude wraps both in a self-custodial smart account that businesses already trust through Squads (which secures >$10B for 250+ Solana teams). ✅ Squads' framing in the launch press: "We're not adding a blockchain to a bank — we're building a bank on the blockchain." 🔴 (marketing, but consistent across Blockworks, The Block, Crowdfund Insider).

**Yes — this entity is genuinely Solana-native.** The Altitude X account states bluntly: *"Altitude is built on @solana to deliver cheaper, faster global financial services."* ✅ ([Altitude on X](https://x.com/tryaltitude/status/1971618113088008199)) Smart-account custody is provided by Squads Protocol v4/v5 deployed on Solana mainnet. ✅

> Note: there are several unrelated "Altitude" companies (Altitude AI, Altitude Aerospace, Altitude Group PLC, Altitude by Geotab, Altitude ISP). The Solana-native one at **altitude.xyz** is unambiguously the Squads product. ✅

---

## 2. Founders

Altitude has no separately-named founders — it is built by the Squads Labs founding team:

| Founder | Title | Background | Handles |
|---|---|---|---|
| **Stepan Simkin** | Co-founder & CEO | Former M&A / corporate restructuring attorney at **Clifford Chance LLP** (international law firm). Originally a "non-technical" founder; started Squads at the Solana Season Hackathon 2021. Prior angel investments include **Tensor** and **Helius**. ✅ | X: [@SimkinStepan](https://x.com/SimkinStepan); [Crunchbase](https://www.crunchbase.com/person/stepan-simkin) |
| **Deni Ershtukaev** | Co-founder & COO | Based Paris, France. Sometimes referred to in early press as "Danny." Long-time friend of Stepan, finance background. ✅ | [LinkedIn](https://www.linkedin.com/in/deni-ershtukaev-4b9a17359/), [Crunchbase](https://www.crunchbase.com/person/deni-ershtukaev) |
| **Sean Ganser** | Co-founder & technical lead | M.S. Integrated Digital Media, NYU Polytechnic. Previously founder of "Ganser Applied Dynamics." Based in Greenville-Spartanburg-Anderson, SC area. Built the multisig program. ✅ | [LinkedIn](https://www.linkedin.com/in/sean-ganser/) |

**Solana / DeFi / fintech / banking experience prior to Squads:** None of the three founders have prior Solana-, DeFi-, or banking-stack experience — the team came in cold via the Solana Season hackathon. 🟡 Stepan's *legal* fintech experience (M&A and restructuring at Clifford Chance) is the closest adjacency, and likely explains the company's unusual sophistication on entity structuring and compliance posture. ✅

A notable later hire is **Garrett Harper**, Head of Business Development since Feb 2024, ex-Blockworks and ex-AgriDigital — he is the public co-spokesman with Stepan (joint Lightspeed-style podcast appearances). ✅ ([TheOrg](https://theorg.com/org/squads-labs/org-chart/garrett-harper))

---

## 3. Founding date, jurisdiction, HQ, where engineering lives

- **Founded:** Project originated at the **Solana Season Hackathon** mid-2021; Squads Labs incorporated by ~late 2021 (first round closed Oct 28, 2021). ✅
- **Mainnet launch:** February 2022, announced at Solana Hacker House Moscow. ✅
- **Registered HQ:** **19 Waterfront Drive, Road Town, Tortola, British Virgin Islands** — i.e., a BVI Business Company. 🟡 ([Tracxn](https://tracxn.com/d/companies/squads-labs/__w-oFrbs6QHvWfW7xl0qG_ieZ6G9pIBeOwMa843YHDx0))
- **Operational hubs:** **Paris** (where COO Deni is based) and **Dubai**, with team members distributed across US, Europe, UAE, Asia. 🟡
- **Engineering:** Distributed (US-based technical lead in SC; eng contributors visible in GitHub commits across timezones). 🟡
- **Business/sales:** Garrett Harper (US-based) leads BD; the announcement-engine and PR is run NY-flavored (Blockworks, The Block, CoinDesk). 🟡

The BVI HQ + global remote pattern is consistent with the typical Solana-native crypto-company structure (offshore protocol entity + distributed team), though notably it is **not** the Cayman-foundation pattern more common with token-issuing DeFi protocols (see §8). ✅

---

## 4. Funding history — round by round

| Round | Date | Amount | Lead(s) | Co-investors / angels | Total to date | Source |
|---|---|---|---|---|---|---|
| Seed | **Oct 28, 2021** | **$1.5M** | Collab+Currency | Reciprocal Ventures, Volt Capital, Chaotic Capital, 6thman Ventures, Republic Capital, 8186 Capital, Solana Capital. Angels: Ryan Selkis (Messari), Ryon Nixon, Chris Hermida, Julia Lipton ✅ | $1.5M | [Squads Medium](https://squads.medium.com/squads-raises-1-5-million-in-its-seed-round-fa41c5dbaafb), [Crunchbase](https://www.crunchbase.com/funding_round/squads-45a1-seed--ffe29d0d) |
| Seed extension / "Seed II" | **Feb 24, 2022** | **$5.0M** | **Multicoin Capital** | Jump Capital, Delphi Digital, Collab+Currency, SeedClub Ventures, Volt Capital ✅ | $6.5M | [The Block](https://www.theblock.co/post/257727/solana-based-multisig-protocol-squads-raises-5-7-million-from-multicoin-placeholder-and-others), [Decrypt](https://decrypt.co/93589/squads-5-million-supercharge-daos-solana) |
| Strategic | **Oct 16, 2023** | **$5.7M** | **Placeholder VC** | 6th Man Ventures, L1 Digital, Solana Ventures, Multicoin, Jump Crypto, Delphi Ventures, Layer One Ventures, Everstake. **Angels: Anatoly Yakovenko (Solana co-founder), Mert Mumtaz (Helius CEO), Lucas Bruder (Jito Labs CEO)** ✅ | $12.2–12.5M | [Squads Blog](https://squads.xyz/blog/squads-labs-raises-strategic-round), [Multicoin memo](https://multicoin.capital/2023/10/16/build-with-squads/) |
| **Series A** | **Jun 10, 2024** | **$10.0M** | **Electric Capital** | RockawayX, Coinbase Ventures, L1 Digital, Placeholder ✅. Structured as equity + token warrants; valuation undisclosed. ✅ | $22.5M | [CoinDesk](https://www.coindesk.com/business/2024/06/10/squads-labs-raises-10m-series-a-unveils-smart-wallet-for-public-testing-on-ios), [The Block](https://www.theblock.co/post/299287/solana-multisig-protocol-squads-funding-fuse) |
| Strategic ("Altitude round") | **Apr 29, 2026** | **$18.0M** | **Solana Ventures** | **Coinbase Ventures, Haun Ventures, L1D, Collab+Currency, Electric Capital, Placeholder, Jump Crypto, Robot Ventures** ✅ | **~$42.9M** | [PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html), [The Block](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude), [Blockworks exclusive](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan) |

**Valuations:** Not publicly disclosed for any round. Stepan declined to confirm Series A valuation to CoinDesk. ✅

**Note on the Haun Ventures sequencing:** Per Blockworks, Stepan first met Chris Ahn of Haun Ventures ~2 years prior to the April 2026 announcement. Haun made an earlier strategic investment specifically tied to the *Altitude* concept ("roughly a year ago" relative to April 2026, i.e., spring 2025) — the amount of that pre-launch Haun check was **not disclosed**, and Haun then participated again in the April 2026 $18M round. 🟡 ([Blockworks](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan))

---

## 5. Strategic investors / notable angels

This is one of the strongest founder-network signals in the Solana ecosystem. Mapped against your asks:

- **Solana ecosystem:** ✅ **Solana Ventures** (lead, 2026 round; participant 2023), ✅ **Anatoly Yakovenko** personally (angel, Oct 2023), ✅ **Mert Mumtaz / Helius** (angel), ✅ **Lucas Bruder / Jito** (angel), ✅ **Multicoin** (lead 2022; multi-round), ✅ **Jump Crypto**, ✅ **Solana Capital**.
- **Crypto-native fintech tier-1:** ✅ **Coinbase Ventures** (Series A + 2026), ✅ **Electric Capital** (Series A lead), ✅ **Placeholder** (2023 lead), ✅ **Haun Ventures**, ✅ **Robot Ventures** (Tarun Chitra / Robert Leshner orbit).
- **DeFi protocol leadership angels (Aave/Compound/Maker):** None publicly disclosed. 🔴
- **TradFi / banking angels:** None publicly disclosed.
- **Other notable angels (Oct 2021 seed):** Ryan Selkis (Messari founder), Ryon Nixon, Chris Hermida, Julia Lipton. ✅

The Anatoly + Mert + Lucas trio in 2023 is the smoking gun that Squads has the *unofficial* blessing of Solana's core founder network — a meaningful regulatory and distribution moat. ✅

---

## 6. Acquisitions

No acquisitions made by Squads Labs are publicly disclosed. ✅
No acquisitions of Squads Labs (or parts of it) are disclosed; the company remains independent. ✅
*Adjacent context:* Bridge (a key Altitude PSP partner) was acquired by **Stripe for $1.1B** in late 2024, and BVNK (similar PSP space) was acquired by **Mastercard for $1.8B** — both cited in the April 2026 Squads PR as validation of the stablecoin-PSP thesis. ✅ ([PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html))

---

## 7. Regulatory licenses

This is the most important section for a Solana developer evaluating Altitude as a partner or competitor. **The short answer: Altitude itself holds no financial licenses anywhere.** The legal architecture is the increasingly common "self-custodial software + licensed PSP rails" model.

From the Squads/Altitude legal addendum at [squads.xyz/legal/altitude](https://squads.xyz/legal/altitude):

> *"The Altitude Account service is an unregulated service that is not supervised, licensed, or endorsed by any financial services authority and is not affiliated with any regulated entity."* ✅

**Enumeration:**

| Jurisdiction | License type | Status | Notes |
|---|---|---|---|
| US — FinCEN MSB | None | n/a | Self-custodial software claim. ✅ |
| US — State money transmitter (NMLS) | None disclosed | n/a | Not in NMLS as of last public sweep. 🟡 |
| US — Broker-dealer | None | n/a | No securities offering. ✅ |
| EU — MiCA CASP | None | n/a | Operates without MiCA registration; EUR rails come via PSP partners. 🟡 |
| UK — FCA | None | n/a | Not on FCA register. 🟡 |
| Singapore — MAS PSA | None | n/a | Not on MAS register. 🟡 |
| Cayman — VASP | None | n/a | No Cayman entity disclosed. 🟡 |
| BVI — Financial Services Commission | None | n/a | BVI Business Company registration only ≠ a financial license. ✅ |

**Compliance is delegated:** Altitude plugs into **licensed PSPs**: **Bridge** (now a Stripe subsidiary, US MTLs + BSA program), **MoonPay**, **Infinite**, and **Due**. ✅ ([PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html))

**In-house compliance stack:** Altitude operates a proprietary engine doing continuous sanctions screening, AML checks, transaction monitoring, and KYB verification. ✅ Squads also recently posted a **"Senior Internal Controls & Compliance Specialist"** role ($140k–170k, US) — strong signal they're building a regulated-fintech-grade operations team without (yet) holding a license themselves. ✅ ([Web3.career](https://web3.career/web3-companies/squads))

**Risk read:** This is the same regulatory positioning used by self-custodial crypto wallets pre-2023. The model has held up under enforcement so far (FinCEN's 2019 guidance and the dropped Tornado Cash US criminal case both lean toward this being defensible), but it is **not a license** and Altitude users should not assume FDIC coverage, SIPC coverage, or banking deposit protections. ✅

---

## 8. Legal entity structure

Public disclosure is partial, but the visible structure is:

- **Operating / IP entity:** **Squads Labs** — registered in Tortola, BVI ([Tracxn](https://tracxn.com/d/companies/squads-labs/__w-oFrbs6QHvWfW7xl0qG_ieZ6G9pIBeOwMa843YHDx0)). 🟡
- **Token-issuing entity:** **None — there is no Squads token.** Series A funds were structured as equity + token warrants, indicating optional future token issuance, but no SQUAD/SQDS token has launched as of May 2026. ✅ ([CryptoRank](https://cryptorank.io/ico/squads), [CoinDesk Series A piece](https://www.coindesk.com/business/2024/06/10/squads-labs-raises-10m-series-a-unveils-smart-wallet-for-public-testing-on-iOS))
- **DAO foundation:** **No DAO foundation disclosed.** Squads Protocol is open-sourced and audited but governance is not yet token-driven. ✅
- **Cayman foundation + Delaware C-corp pattern (typical for Solana DeFi):** **Not present.** Squads has chosen a more fintech-flavored single-entity BVI structure rather than the bifurcated DeFi-protocol pattern. This is consistent with their product trajectory (B2B fintech, not a tokenized DeFi protocol). 🟡
- **Altitude as separate entity:** No separate Altitude legal entity is publicly visible. The Altitude Supplemental Terms are explicitly bolted onto Squads' main ToS, suggesting Altitude is a *product* of Squads Labs rather than a spun-out subsidiary. ✅ ([squads.xyz/legal/altitude](https://squads.xyz/legal/altitude))

---

## 9. Press timeline

| Date | Headline | Source | Takeaway |
|---|---|---|---|
| 2021-Q3 | Wins/builds at Solana Season Hackathon as mobile-first DAO governance app | [Solana Compass / Solfate Pod 33](https://solanacompass.com/learn/Solfate/governance-and-squads-multi-sig-protocol-feat-stepan-co-founder-of-squads-solfate-podcast-33) | Origin story; hackathon team of 6, did not finish project. ✅ |
| 2021-10-28 | Squads raises $1.5M seed led by Collab+Currency | [Squads Medium](https://squads.medium.com/squads-raises-1-5-million-in-its-seed-round-fa41c5dbaafb) | Original thesis: DAO generator (treasury + voting + chat). ✅ |
| 2022-02-24 | Squads raises $5M to "supercharge DAOs on Solana", launches mainnet at Solana Hacker House Moscow | [Decrypt](https://decrypt.co/93589/squads-5-million-supercharge-daos-solana), [The Block](https://www.theblock.co/post/257727/solana-based-multisig-protocol-squads-raises-5-7-million-from-multicoin-placeholder-and-others) | Multicoin lead validates pivot toward multisig primitive. ✅ |
| 2023-Q3 | Squads Protocol v4 launched with formal verification by Certora + audits by OtterSec, Neodyme, Trail of Bits, Bramah | [Squads blog](https://squads.xyz/blog/v4-security-measures), [docs.squads.so](https://docs.squads.so/main/security/security-audits/squads-protocol-v4) | Security positioning hardens; v4 becomes Solana multisig standard. ✅ |
| 2023-09-19 | Stepan on Solfate Podcast #33 — "Solana governance and Squads multi-sig protocol" | [Solana Compass](https://solanacompass.com/learn/Solfate/governance-and-squads-multi-sig-protocol-feat-stepan-co-founder-of-squads-solfate-podcast-33) | Best long-form on the early pivot. ✅ |
| 2023-10-16 | $5.7M strategic round led by Placeholder, with Anatoly/Mert/Bruder as angels | [Squads blog](https://squads.xyz/blog/squads-labs-raises-strategic-round), [Multicoin memo](https://multicoin.capital/2023/10/16/build-with-squads/) | Solana founder network goes long Squads; signals smart-wallet pivot. ✅ |
| 2024-02 | Garrett Harper joins as Head of BD | [LinkedIn post](https://www.linkedin.com/posts/garrett-harper-84989670_very-excited-to-share-that-im-joining-squads-activity-7153421472223399936-1U3C) | Hire sets up retail/consumer push. ✅ |
| 2024-06-10 | $10M Series A led by Electric Capital; **Fuse smart wallet** launched on iOS TestFlight | [CoinDesk](https://www.coindesk.com/business/2024/06/10/squads-labs-raises-10m-series-a-unveils-smart-wallet-for-public-testing-on-ios), [The Block](https://www.theblock.co/post/299287/solana-multisig-protocol-squads-funding-fuse) | First major B2C product. ✅ |
| 2024-09 | **Breakpoint 2024 keynote:** Squads Protocol v5 announced; **Fuse Pay** virtual Visa card with **Bridge** as PSP partner | [Solana Compass keynote](https://solanacompass.com/learn/breakpoint-24/breakpoint-2024-product-keynote-squads-labs-accelerating-the-onchain-economy) | First disclosed PSP partnership; Bridge relationship is what later powers Altitude. ✅ |
| 2025-02-21 | Bybit/Safe{Wallet} $1.46B exploit; Stepan/Squads issue "comprehensive review" statement | [bitcoinethereumnews.com](https://bitcoinethereumnews.com/tech/solana-multisig-provider-conducting-comprehensive-review-after-safe-exploit/) | Squads positions formal verification as differentiator vs. Safe; PR moment. ✅ |
| ~2025 spring | Strategic check from **Haun Ventures** (Chris Ahn) tied to Altitude concept; amount undisclosed | [Blockworks exclusive](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan) | Marker for shift from multisig infra to fintech product. 🟡 |
| **2025-12** | **Altitude publicly launches** | [Multiple — Squads PR](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html) | Begins onboarding businesses; will process >$200M in <5 months. ✅ |
| 2026-04-29 | **Squads raises $18M strategic** led by Solana Ventures (Coinbase, Haun, L1D, Electric, Placeholder, Jump, Robot, Collab+Currency); total $42.9M | [PR Newswire](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html), [The Block](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude), [Crowdfund Insider](https://www.crowdfundinsider.com/2026/05/276883-squads-raises-18m-for-stablecoin-operating-system/), [TechStartups](https://techstartups.com/2026/04/29/fintech-startup-squads-raises-18m-to-build-a-stablecoin-powered-financial-os/) | Solana Ventures choosing to lead is the headline signal — Solana Foundation explicitly betting on stablecoin-as-banking-replacement narrative. ✅ |
| 2026-04-29 | Stated metric: **>$200M processed since Dec 2025** | [Squads PR](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html) | Customer profile: exporters, global agencies, crypto-native firms, distributed teams. 🔴 (company-disclosed, no third-party verification) |
| 2026-04-29 | "Altitude Bill Pay" feature blog | [Squads blog](https://squads.xyz/blog/introducing-altitude-bill-pay) | Feature expansion alongside the round. 🟡 |

---

## 10. Has the company ever pivoted? Original thesis vs current

**Yes — twice.**

1. **Pivot 1 (late 2021 → Feb 2022):** Original Solana Season hackathon thesis was a **mobile-first all-in-one DAO governance platform** (treasury + on-chain voting + chat). Stepan's own framing (Solfate #33): *"We first got to a governance framework or a governance platform. And then we even stripped it down further to multi-sig primitive."* They stripped the product down to the **multisig primitive** because that was the lowest-level missing piece on Solana. ✅
2. **Pivot 2 (2024 → 2026):** From **B2B treasury infra-only** (Squads Multisig) to a **two-product company**: (a) Squads Multisig as the dev-trust infrastructure and (b) **Altitude as the consumer-of-that-infra product** — a stablecoin business bank. Fuse (consumer wallet, 2024) was an intermediate step that arguably served as the engineering scaffold for Altitude (same passkey/Privy/Turnkey + Bridge plumbing reappears in Altitude). 🟡

The company is *currently* positioned as **"the financial OS for businesses on the frontier"** — a far cry from the 2021 DAO governance pitch. ✅ The through-line is "smart-account programmability is the right primitive"; the customer surface has moved from DAOs → crypto-native treasuries → all global businesses.

---

## 11. Team size & notable hires/departures

- **Mid-2024 (Series A press):** ~17 employees per CoinDesk reporting. ✅
- **Mid-2025 — present:** Stated as "20+" by Solana Compass ✅; LinkedIn shows ~512 followers on the company page (small but consistent with a 25–40-person team). 🟡 Hiring pages show roles in Customer Support, Senior Internal Controls & Compliance Specialist, Head of BD, and other Altitude-specific positions ($140k–$170k bands). ✅
- **Notable hire:** **Garrett Harper** as Head of BD (Feb 2024, ex-Blockworks/AgriDigital) — the public-facing #2 alongside Stepan. ✅
- **No notable departures publicly disclosed.** ✅

Reasonable estimate: **~25–40 FTEs as of May 2026**, growing fast post-April-2026 round. 🟡

---

## 12. Public-facing audits

Audits exist for **Squads Protocol (the underlying smart-account program)**, not for Altitude as an application. This is important — there is **no public smart-contract audit specifically of Altitude's frontend or off-chain compliance engine** that I could surface. ✅

**Squads Protocol v4 audits** (relevant because Altitude accounts run on these programs):

| Auditor | Type | Year | Findings |
|---|---|---|---|
| **OtterSec** | Manual + formal verification | 2023 (also v3 in 2022) — [v3 PDF](https://github.com/Squads-Protocol/squads-mpl/blob/main/Squads%20V3%20-%20OtterSec%20Audit.pdf) | No critical issues in final report. ✅ |
| **Neodyme** | Manual audit | 2023 | Reports posted in [v4 audits/ folder](https://github.com/Squads-Protocol/v4) ✅ |
| **Trail of Bits** | Manual audit | 2023 | Tier-1 review. ✅ |
| **Certora** | Formal verification + audit | Dec 2023 + 2024 final report | "No major security flaws"; among the first formally verified Solana programs. ✅ ([Certora report PDF](https://github.com/Squads-Protocol/v4/blob/main/audits/certora_squads_v4_security_report_and_formal_verification.pdf)) |
| **Bramah Systems** | Manual audit | Mentioned in security materials | 🟡 |

**No Zellic audit** of Squads is publicly disclosed. 🟡

---

## 13. Social signals & community traction

- **X (Altitude):** [@tryaltitude](https://x.com/tryaltitude) — separate Altitude handle exists. Follower count not surfaced; given Dec-2025 launch and ~$200M processed, likely 5k–25k range. 🟡
- **X (Squads parent):** [@SquadsProtocol](https://twitter.com/SquadsProtocol), [@SquadsLabs](https://x.com/squadslabs) — order-of-magnitude tens-of-thousands. 🟡
- **X (Stepan personal):** [@SimkinStepan](https://x.com/SimkinStepan) ✅
- **GitHub:** [Squads-Protocol](https://github.com/Squads-Protocol) org — public repos include `v4` (the live program), `squads-mpl` (legacy v2/v3), `squads-v4-public-ui` (Next.js), `smart-account-program`, plus client SDKs. The v4 repo has public audit PDFs in-tree which is unusual transparency. ✅
- **Discord:** A Squads community Discord exists; not specifically surfaced for Altitude. 🟡
- **Adoption traction:** **>$10B–15B secured**, **450+ teams**, **$3B+ stablecoin transfers** via Squads Multisig. ✅ Customer logos cited include: **Jupiter, Jito, Pyth, Kamino, Backpack, Helius, Drift, Tensor, Mango, Orca**. ✅ ([Solana Compass](https://solanacompass.com/projects/squads), [Fystack blog](https://fystack.io/blog/squads-from-zero-to-the-multisig-protocol-securing-10b-on-solana))
- **Altitude-specific:** **>$200M processed in 4–5 months** since Dec 2025 launch. 🔴 (company-disclosed)

This is one of the strongest distribution moats on Solana: the parent product (Squads Multisig) is already inside the treasuries of essentially every major Solana DeFi/infra protocol, and Altitude can be sold into those same teams as a CFO upgrade. ✅

---

## 14. Litigation, regulatory enforcement, public complaints

**None found.** ✅
- No SEC enforcement actions targeting Squads Labs or Altitude.
- No state money-transmitter enforcement actions.
- No public lawsuits.
- No high-profile customer complaints surfaced in search.
- The closest "incident" is a community Medium post discussing **secure signing best practices** after general industry signing-process incidents — *not* a Squads-specific exploit. ✅ ([West on Medium](https://medium.com/@west_XE/securing-squads-4f43944e4c59))
- Squads' response to the Feb 2025 **Bybit/Safe{Wallet} exploit** (Ethereum, not Solana, and not their software) was to issue a "comprehensive review" of their own signing UX — proactive, not defensive. ✅

The clean record + formally verified codebase + tier-1 auditors is the single strongest technical credibility signal for the company.

---

## 15. Founder podcast appearances and long-form interviews

For your transcript-grabbing pipeline:

| Date | Show | Episode | Host | URL |
|---|---|---|---|---|
| **2022-03-22** | The Delphi Podcast | "Web3 is Frictionless Collaboration: Stepan Simkin, Co-Founder & CEO of Squads Protocol" | Delphi | [Delphi Digital](https://members.delphidigital.io/media/web3-is-frictionless-collaboration-stepan-simkin-co-founder-ceo-of-squads-protocol) / [Apple Podcasts](https://podcasts.apple.com/us/podcast/web3-is-frictionless-collaboration-stepan-simkin-co/id1438148082?i=1000554864265) ✅ |
| **2022 (mid)** | Law of Code | #39 — "Stepan Simkin: Building for DAOs (after a Legal Career)" | Jacob Robinson | [Apple Podcasts](https://podcasts.apple.com/us/podcast/39-stepan-simkin-building-for-daos-after-a-legal-career/id1578287932?i=1000558629674) — [companion essay #19 "From Lawyers to CEO"](https://lawofcode.substack.com/p/19-from-lawyers-to-ceo) ✅ |
| **2023-09-19** | Solfate Podcast | #33 — "Solana governance and Squads multi-sig protocol" | Solfate | [YouTube](https://www.youtube.com/watch?v=fahTUDvPpCw) ✅ |
| **2024 (post-Series A)** | YouTube — "Powering Solana's Onchain Economy" | Stepan Simkin + Garrett Harper | Unclear host | [YouTube](https://www.youtube.com/watch?v=k-6hkq4Ej4w) ✅ |
| **2024** | Logan Jastremski Podcast | #36 — "Stepan Simkin, Co-Founder of Squads Protocol, Solana's Multisig" | Logan Jastremski | [YouTube](https://www.youtube.com/watch?v=57aXBTRBUew) ✅ |
| **2024-09 (Breakpoint)** | Solana Compass — Breakpoint 2024 keynote | "Squads Labs: Accelerating the Onchain Economy" | Stepan Simkin (solo keynote, not interview) | [YouTube](https://www.youtube.com/watch?v=duEz_ePt6SU) ✅ |
| **2025** | Validated podcast (about.solanacompass.com) | "Why multisigs are becoming the default security paradigm w/ Stepan Simkin" | Solana Compass / Validated | [Solana Compass](https://about.solanacompass.com/learn/Validated/validated-why-multisigs-are-becoming-the-default-security-paradigm-w-stepan-simkin-squads) ✅ |
| **2025–2026 various** | "How Squads Secured $15B in Assets on Solana" | Stepan Simkin + Garrett Harper | Frictionless / unclear | [YouTube](https://www.youtube.com/watch?v=GfmHbuJZAa0) ✅ |
| **2025-Q4 (era)** | Nation Blog interview | "Building what's best for the ecosystem — a conversation with Squads' Stepan Simkin" | Nation | [nation-blog.ghost.io](https://nation-blog.ghost.io/building-what-the-ecosystem-needs-but-has-never-seen-before-a-conversation-with-squads-stepan/) ✅ |

**Not surfaced:** dedicated episodes on Bankless, Lightspeed (Blockworks), Empire (Blockworks), or Unchained (Laura Shin). Stepan has been *quoted* in Lightspeed newsletters but no Lightspeed full episode appearance surfaced. 🟡

---

## Bottom line for a Solana developer

- **What Altitude is:** Not an independent company. It is **Squads Labs' B2B fintech product**, sitting on top of Squads' formally verified Solana smart-account programs, plumbed into licensed PSPs (Bridge being the load-bearing one) for the regulated banking leg. ✅
- **Who's behind it:** A 3-founder team (Simkin/Ershtukaev/Ganser) with no prior Solana/fintech track record but extraordinary execution since Q3-2021 and the unofficial backing of Anatoly + Mert + Lucas. ✅
- **Capital:** $42.9M total, latest round (Apr 2026) led by Solana Ventures itself — the most explicit signal yet that Solana Foundation–adjacent capital views stablecoin business banking as the *post-DeFi* killer app on the chain. ✅
- **Regulatory shape:** Self-custodial software (no licenses), BVI entity, no token, no DAO foundation, no Cayman/Delaware bifurcation. Compliance outsourced to PSP partners + an in-house engine + a hire for a Senior Internal Controls & Compliance Specialist. 🟡
- **Audits:** Excellent on the protocol layer (OtterSec, Neodyme, Trail of Bits, Certora formal verification, Bramah). No public Altitude-application-layer audit. ✅
- **Risks worth flagging:**
  - "Unregulated service" disclaimer in the ToS is real — no FDIC/SIPC equivalent. ✅
  - Single-PSP risk: Bridge being acquired by Stripe could change terms; alternates (MoonPay, Infinite, Due) exist but Bridge appears load-bearing. 🟡
  - Token warrant overhang from Series A — a SQUAD token is structurally possible, market timing unclear. ✅
  - BVI-only entity may complicate enterprise contracts with conservative US/EU customers. 🟡
- **What's interesting for a builder:** The "every account is a Solana smart account" architecture means Altitude could plausibly expose APIs/SDKs that let developers embed *self-custodial business banking* into their own dApps — that's a real platform play and is hinted at in their docs ("Builders can use Altitude to embed self-custodial smart accounts into their dApps or wallets"). ✅ This is the angle most worth interrogating in the architecture and customer files.

---

### Sources

- [altitude.xyz](https://altitude.xyz/) — landing page
- [squads.xyz/altitude](https://squads.xyz/altitude) — product page
- [squads.xyz/legal/altitude](https://squads.xyz/legal/altitude) — Altitude Supplemental Terms
- [Squads PR — $18M, Apr 29 2026 (PR Newswire)](https://www.prnewswire.com/news-releases/squads-raises-18m-to-build-business-finance-on-stablecoin-infrastructure-302757563.html)
- [The Block — Solana Ventures leads $18M round](https://www.theblock.co/post/399386/solana-ventures-squads-funding-stablecoin-altitude)
- [Blockworks exclusive — Squads launches Altitude](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan)
- [Crowdfund Insider — $18M For Stablecoin OS](https://www.crowdfundinsider.com/2026/05/276883-squads-raises-18m-for-stablecoin-operating-system/)
- [TechStartups — $18M Squads stablecoin OS](https://techstartups.com/2026/04/29/fintech-startup-squads-raises-18m-to-build-a-stablecoin-powered-financial-os/)
- [CoinDesk — $10M Series A + Fuse, Jun 2024](https://www.coindesk.com/business/2024/06/10/squads-labs-raises-10m-series-a-unveils-smart-wallet-for-public-testing-on-ios)
- [The Block — Series A coverage](https://www.theblock.co/post/299287/solana-multisig-protocol-squads-funding-fuse)
- [Squads blog — $5.7M strategic round](https://squads.xyz/blog/squads-labs-raises-strategic-round)
- [Multicoin memo — Build with Squads](https://multicoin.capital/2023/10/16/build-with-squads/)
- [The Block — $5.7M from Multicoin/Placeholder](https://www.theblock.co/post/257727/solana-based-multisig-protocol-squads-raises-5-7-million-from-multicoin-placeholder-and-others)
- [Squads Medium — $1.5M seed Oct 2021](https://squads.medium.com/squads-raises-1-5-million-in-its-seed-round-fa41c5dbaafb)
- [Decrypt — $5M to supercharge DAOs (Feb 2022)](https://decrypt.co/93589/squads-5-million-supercharge-daos-solana)
- [Crunchbase — Squads org](https://www.crunchbase.com/organization/squads-45a1)
- [Crunchbase — Stepan Simkin](https://www.crunchbase.com/person/stepan-simkin)
- [Crunchbase — Deni Ershtukaev](https://www.crunchbase.com/person/deni-ershtukaev)
- [Tracxn — Squads Labs](https://tracxn.com/d/companies/squads-labs/__w-oFrbs6QHvWfW7xl0qG_ieZ6G9pIBeOwMa843YHDx0)
- [Solana Compass — Squads project review](https://solanacompass.com/projects/squads)
- [Solana Compass — Solfate Podcast 33](https://solanacompass.com/learn/Solfate/governance-and-squads-multi-sig-protocol-feat-stepan-co-founder-of-squads-solfate-podcast-33)
- [Solana Compass — Breakpoint 2024 Squads keynote](https://solanacompass.com/learn/breakpoint-24/breakpoint-2024-product-keynote-squads-labs-accelerating-the-onchain-economy)
- [Solana Compass / Validated — Stepan on multisigs](https://about.solanacompass.com/learn/Validated/validated-why-multisigs-are-becoming-the-default-security-paradigm-w-stepan-simkin-squads)
- [Squads blog — v4 security measures](https://squads.xyz/blog/v4-security-measures)
- [Squads blog — Certora formal verification](https://squads.xyz/blog/certora-formal-verification-squads-protocol-v4)
- [GitHub — Squads-Protocol/v4](https://github.com/Squads-Protocol/v4)
- [GitHub — Squads-Protocol org](https://github.com/Squads-Protocol)
- [Squads docs — Security](https://docs.squads.so/main/basics/security)
- [Fystack blog — Squads from Zero to $10B](https://fystack.io/blog/squads-from-zero-to-the-multisig-protocol-securing-10b-on-solana)
- [Apple Podcasts — Law of Code #39](https://podcasts.apple.com/us/podcast/39-stepan-simkin-building-for-daos-after-a-legal-career/id1578287932?i=1000558629674)
- [Apple Podcasts — Delphi Pod 2022](https://podcasts.apple.com/us/podcast/web3-is-frictionless-collaboration-stepan-simkin-co/id1438148082?i=1000554864265)
- [YouTube — Solfate #33](https://www.youtube.com/watch?v=fahTUDvPpCw)
- [YouTube — Logan Jastremski #36](https://www.youtube.com/watch?v=57aXBTRBUew)
- [YouTube — Powering Solana's Onchain Economy](https://www.youtube.com/watch?v=k-6hkq4Ej4w)
- [YouTube — How Squads Secured $15B](https://www.youtube.com/watch?v=GfmHbuJZAa0)
- [YouTube — Breakpoint 2024 Squads keynote](https://www.youtube.com/watch?v=duEz_ePt6SU)
- [Altitude on X — built on Solana statement](https://x.com/tryaltitude/status/1971618113088008199)
- [Squads Bill Pay blog](https://squads.xyz/blog/introducing-altitude-bill-pay)
- [Web3.career — Squads roles](https://web3.career/web3-companies/squads)
- [bitcoinethereumnews — Squads response to Safe exploit](https://bitcoinethereumnews.com/tech/solana-multisig-provider-conducting-comprehensive-review-after-safe-exploit/)
- [PitchBook — Squads profile](https://pitchbook.com/profiles/company/469995-49)
