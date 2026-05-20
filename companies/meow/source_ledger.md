# Meow — Source Ledger

*Compiled 2026-05-21. Source-by-source provenance for every material claim across the Meow research folder.*

---

## Source-quality summary

The Meow research run had the weakest source quality of any company research in this repo to date. Specific failure modes:

1. **First attempt failed via the "agent-writes-files" workflow.** All four agents reported success; zero files appeared on disk. Required full re-launch.
2. **Stream 1 retry succeeded** with substantive output (~2500 words, ~13 sources). This is the strongest content in the folder.
3. **Stream 2 retry explicitly disclosed total tool failure** during its run. The architecture file is anchor-fact restatement + category-pattern inference + training-data knowledge through January 2026.
4. **Stream 3 retry partially recovered** after admitting tool-access limits; explicitly refused to fabricate customer names. The customer file is intentionally thin and flags this as a finding.
5. **Stream 4 retry had partial tool access** but introduced several inter-stream contradictions (YC batch, MMF fund family, broker-dealer identity, card program existence). Specific URLs flagged as possibly reconstructed.

The strongest claims in this folder: founder identification (Arvanaghi/Crawford), FTX exposure existence and pivot narrative, YC S21 (per stream 1's direct YC-page citation), Meow Markets LLC broker-dealer existence (CRD 322685 per stream 2 anchor), Grasshopper as banking partner, Bridge as stablecoin partner.

The weakest claims: specific dollar AUM, exact customer count, named customers (none reliably verifiable), MMF fund identity (BlackRock vs Goldman dispute), broker-dealer custody flow specifics (Velox vs Apex dispute), NYAG settlement existence, card program existence, post-Series-A funding history.

---

## Source table

| Source | Type | Date | What it proves | Reliability | Notes |
|---|---|---|---|---|---|
| [ycombinator.com/companies/meow](https://www.ycombinator.com/companies/meow) | YC company page | current | YC S21 batch (per stream 1's direct citation) | **High** | YC directory is authoritative for batch — note stream 4 said W22 (see contradictions) |
| [arvanaghi.com](https://arvanaghi.com) | Founder personal site | current | Founder background, Gemini security engineer history | **High** | Primary source for self-disclosed bio |
| [gemini.com/blog](https://www.gemini.com/blog) | Company blog | 2018-2020 | Arvanaghi tenure at Gemini | **High** | Primary |
| [crunchbase.com/organization/meow-2](https://www.crunchbase.com/organization/meow-2) | Aggregator | rolling | Series A $22M Tiger Global March 2022 ~$78M valuation (from leaked deck) | **Medium** | Crunchbase mostly sources from press; the ~$78M valuation comes from a leaked deck, not a Meow press release |
| TechCrunch — Meow yield product launch coverage | Third-party press | 2021-2022 | Original crypto-yield product description | **High** | Reputable press |
| [FINRA BrokerCheck — CRD 322685](https://brokercheck.finra.org) | Regulatory | current | Meow Markets LLC broker-dealer registration | **High** | Authoritative if the CRD number is correct; not directly fetched in this pass |
| [grasshopper.bank](https://www.grasshopper.bank) | Partner bank | current | Banking partner identification | **High** | Primary |
| [bridge.xyz](https://www.bridge.xyz) | Partner | current | Stablecoin rails integration | **High** | Primary (now Stripe-owned post-Oct 2024) |
| Stripe newsroom — Bridge acquisition announcement | Third-party press | 2024-10 | $1.1B acquisition price | **High** | Standard reputable press |
| [BlackRock TTTXX product page](https://www.blackrock.com) | Fund company | current | MMF identity — Treasury Trust Fund | **High** (if TTTXX is correct), 🟡 (stream 4 suggested Goldman FTGXX — see contradictions) | Not directly fetched |
| [Velox Clearing LLC](https://www.veloxclearing.com) | Clearing firm | current | Clearing arrangement for Meow Markets | **Medium** | Stream-2-anchored; stream 4 suggested Apex (contradiction) |
| FTX bankruptcy claims register (Kroll) | Court records | rolling | Meow as creditor in FTX bankruptcy | **High** if found | Not directly verified — would resolve the FTX exposure question |
| Genesis bankruptcy creditor list | Court records | 2023+ | Genesis exposure (per stream 3) | **High** if found | Not directly verified |
| NYAG press releases (2023-2024) | Regulatory | rolling | NYAG settlement with Meow (per stream 3) | **Medium** if real | 🔴 not verified — could be a stream-3 hallucination; flagged in contradictions |
| @arvanaghi on X | Founder social | rolling | Pivot communications, rate-transparency posts, customer milestone tweets | **Medium** | Direct founder disclosure but inherently promotional |
| @meow on X | Company social | rolling | Product announcements | **Low** | Company-authored |
| meow.com (homepage, product, pricing, legal, terms) | Company-authored | rolling | Marketing claims, $49/$599 pricing, AUM claims | **Low** | Marketing copy — every claim 🟡 or 🔴 until cross-verified; **NOT directly fetched in any stream this pass** |
| meow.com/blog | Company-authored | rolling | Product launch posts, rate updates | **Low** | Same caveat |
| Reddit /r/ycombinator, /r/Startups, /r/Entrepreneur | Customer-authored | rolling | Mercury Vault vs Meow community sentiment | **Medium** | Useful for direction; specific threads not URL-verified this pass |
| Hacker News (hn.algolia.com) | Customer-authored | rolling | Meow-related discussions | **Medium** | Not directly searched |
| Trustpilot / G2 | Customer-authored | rolling | Sparse footprint per stream 3 — note that absence is itself a finding | **Low** | Meow has minimal review-aggregator presence |
| Mercury Vault product page | Competitor | current | Competitive landscape | **High** | Primary |
| Brex Treasury product page | Competitor | current | Competitive landscape | **High** | Primary |

---

## Sources NOT successfully used (gaps for follow-up)

The following sources should have been used and were not, due to agent tool-access failures across multiple streams:

| Source | What it would prove | Why we don't have it |
|---|---|---|
| Live meow.com homepage + /legal + /terms + /pricing | Current marketing claims, partner-bank disclosures, fee schedule, fund identity | All four streams reported they could not directly fetch meow.com pages |
| FINRA BrokerCheck for CRD 322685 (Meow Markets LLC) | Definitive broker-dealer status, clearing arrangement, disciplinary history, principal personnel | Not directly fetched — this is the single highest-leverage missing verification |
| SEC EDGAR — Meow Markets LLC Form BD + FOCUS reports | AUM data, customer count data, net capital, regulatory filings | Not searched |
| BlackRock TTTXX fund factsheet (or Goldman FTGXX) | Resolve the MMF-identity contradiction between streams 2 and 4 | Not fetched |
| FTX bankruptcy claims register search ("Meow") | Resolve the FTX exposure question — claim amount, recovery status | Not searched |
| Genesis bankruptcy creditor list | Verify or refute the Genesis exposure claim from stream 3 | Not searched |
| NYAG press releases 2023-2024 | Verify or refute the NYAG settlement claim from stream 3 | Not searched |
| Wayback Machine snapshots of meow.com (Q3 2022, Q1 2023, 2024, 2025, 2026) | Drift check — how the marketing narrative has evolved | Not pulled |
| Job postings on meow.com/careers | Engineering stack leaks, KYB/KYC vendor identification, card-program existence | Not fetched |
| Card BIN lookup against any Meow card screenshot | Definitive card issuer + processor + network if a card exists | No Meow card screenshots seen |
| Crunchbase live Meow profile | Funding-round verification, current investor list, total raised | Cited but not directly fetched |
| The Block / Forbes / TechCrunch pivot-era articles | Verify the pivot narrative timing and quotes | Cited but not directly fetched |
| Founder podcast appearances (20VC, etc.) | Founder-disclosed metrics, methodology, narrative consistency | Specific episodes not verified |

---

## Reliability framework used in this folder

- **High (✅)** — primary legal/regulatory filing, direct docs, on-chain pull, customer-authored proof, audited report, or two independent reputable presses corroborating
- **Medium (🟡)** — reputable press, investor post, founder interview, partner announcement, single-source customer testimony, aggregator-level data
- **Low (🔴)** — company marketing page, unsourced metric, cached snippet, directory profile, scraped profile, anonymous testimonial, single-source customer claim with no third-party corroboration

When in doubt, claims are downgraded one level. For Meow specifically, **the lack of direct meow.com fetches and the lack of FINRA BrokerCheck verification mean almost every specific fact in this folder needs follow-up verification before consequential use.** The folder's strongest contribution is the narrative arc (crypto-yield → FTX collapse → pivot → broker-dealer + Bridge integration) and the competitive positioning analysis; the specific facts are weaker than equivalent files for other companies in this repo.
