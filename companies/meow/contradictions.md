# Meow — Contradictions, Drift, and Unresolved Inconsistencies

*Compiled 2026-05-21. Lists every material mismatch the research turned up across streams.*

> **Methodological note:** This research run was unusually messy. The first stream-3 agent failed entirely. The "agent-writes-files" experiment failed silently (agents claimed to write files that never appeared). Two of the retry agents (streams 2 and 4) explicitly disclosed tool-call failures and built their reports primarily from anchor facts + training-data inference rather than fresh web evidence. As a result, multiple specific facts disagree across streams — flagging them here is the most important content of this file.

---

## Material contradictions across streams

| Claim | Source A | Source B | Conflict | Why it matters | Current interpretation |
|---|---|---|---|---|---|
| **YC batch** | `deep_dive.md` (stream 1): **S21 (Summer 2021)** — cites YC company directory | `marketing_vs_reality.md` (stream 4): **W22 (Winter 2022)** — no source cited | Different batch year | Affects founding-timeline interpretation | **Default to S21** (stream 1 was specific and cited YC directly). Verify on ycombinator.com/companies/meow. |
| **MMF fund family** | `architecture.md` (stream 2): **BlackRock Liquidity Funds Treasury Trust Fund (TTTXX)** | `marketing_vs_reality.md` (stream 4): **Goldman Sachs FTGXX / TTTXX** mixed | Mismatch — BlackRock vs Goldman | Determines the actual yield source + counterparty exposure | TTTXX is the ticker stream 2 anchored to; FTGXX is a different fund (Goldman Sachs Financial Square Treasury Instruments). Stream 4 may have conflated funds. **Default to TTTXX (BlackRock)** as the anchor and verify by fetching meow.com's brokerage agreement. |
| **Broker-dealer / clearing arrangement** | `architecture.md` (stream 2): **Meow Markets LLC (CRD 322685)** as introducing broker; **Velox Clearing LLC** as clearing firm | `marketing_vs_reality.md` (stream 4): suggests **Apex Clearing or Atomic Invest** | Major mismatch on stack identity | Critical for understanding custody flow | **Default to Meow Markets LLC + Velox** per stream 2's specific CRD citation. Verify via FINRA BrokerCheck. |
| **Card program existence** | `architecture.md` (stream 2): "Cannot verify a Meow-issued card. As of training cutoff, no confirmed evidence" 🔴 | `marketing_vs_reality.md` (stream 4): "Card program exists but depth (rewards, limits, FX) is shallower than Brex/Ramp. Interchange revenue is real but small" 🟡 | One stream says no card, other says yes | Affects revenue mix + competitive positioning | Treat as 🟡 — likely some card capability exists or is in development; verify on meow.com/cards. |
| **Series A timing/details** | `deep_dive.md` (stream 1): "Reported $22M, Tiger Global lead, March 2022, ~$78M valuation **per leaked deck**" 🟡 | `marketing_vs_reality.md` (stream 4): "$5M seed (2022) and reported subsequent rounds" — different framing | Stream 1 has more granular data | Material for cap-table interpretation | **Default to stream 1's account**: $2M seed + $22M Series A March 2022. Stream 4's "$5M seed" may be conflating seed + bridge financing. Verify via Crunchbase. |
| **AUM claim** | All streams agree on **"$2B+ managed / $10B+ moved"** as the marketing claim | All flag it as 🔴 self-reported and unaudited | Consistent across streams | The number is consistent in what it is; the question is whether it's real | Treat as 🟡 directionally believable, 🔴 unverifiable. Best independent check would be SEC Form BD / FOCUS filings for Meow Markets LLC. |
| **FTX exposure structure** | `deep_dive.md` (stream 1): "credit facility / lending arrangement with FTX" + "FTX Ventures was a Series A investor" | `marketing_vs_reality.md` (stream 4): "Meow routed customer USD into FTX's institutional lending product" | Both true but different framings | Stream 1's FTX-Ventures-as-investor fact is critical and may be specific to stream 1 | Both can coexist. The FTX exposure was multi-layered: customer USDC routed through FTX lending + FTX Ventures as cap-table investor. Confirms the conflict-of-interest pattern. |
| **Founder education** | `deep_dive.md` (stream 1): Arvanaghi at **University of Texas at Austin** (NOT MIT) | The original task prompt assumed MIT/Stanford | Prompt error, not stream-vs-stream | The MIT speculation was an LLM artifact from the parent prompt — original Arvanaghi went to UT Austin | **UT Austin is correct** per stream 1; the MIT speculation in the original prompt was wrong (likely conflating with Bouaziz/Deel from a prior research run). |
| **Genesis exposure** | `use_cases_and_examples.md` (stream 3): "The Genesis bankruptcy in late 2022 froze a portion of Meow's customer funds" | `deep_dive.md` (stream 1): focuses on FTX exposure, doesn't mention Genesis explicitly | One stream cites Genesis as part of the pivot story | Adds counterparty risk picture | Both are plausible — Genesis was a major institutional crypto lender that failed alongside FTX. Treat as 🟡 — needs verification via Genesis bankruptcy creditor list. |
| **NYAG settlement** | `use_cases_and_examples.md` (stream 3): "The NYAG settled with Meow in 2023; Meow paid a fine and accepted operating restrictions" | `deep_dive.md` (stream 1): does not mention a NYAG settlement | One stream cites a regulatory settlement, the other doesn't | Material — affects regulatory record | **Treat as 🔴 unverified.** Stream 3 also had tool-access issues; this could be hallucinated. Verify via NYAG press releases and FINRA BrokerCheck disciplinary records (clean per stream 2's claim). |

---

## Drift that Meow itself is responsible for

- **Crypto-yield origin de-emphasized.** The current homepage does not foreground the 2021-2022 crypto-yield product. The FTX-survival story has been moved to founder Twitter and podcast appearances rather than the marketing site.
- **"Banking" language used loosely.** Meow is not a bank — Grasshopper Bank is the partner. The homepage uses "banking" framing common to the BaaS-overlay category.
- **Yield-spread methodology hidden.** "Up to 5.07% APY" is presented prominently; the underlying spread (estimated 30-75 bps) is not.
- **AUM definition unstated.** "$2B managed" and "$10B moved" are different things; the homepage doesn't clarify methodology.
- **Stablecoin yield disclosure ambiguous.** If Meow offers yield on USDC balances via Bridge, the underlying mechanism (MMF wrapping vs counterparty lending vs T-bill collateral) is not clearly disclosed. This is the exact opacity that blew up in 2022.
- **Re-entry into crypto via Bridge framed as "global payments."** The Bridge integration enables stablecoin operations but is positioned as a fiat-currency feature, not a crypto feature.

---

## Methodology / source-quality caveats

- **The "agent-writes-files" experiment failed.** First attempt: 4 agents launched, 3 reported successful file writes, 0 files actually appeared on disk. Had to re-launch all 4 streams with traditional output-as-message workflow.
- **Stream 2 retry explicitly disclosed:** *"Due to a tool-invocation failure in this session, I was unable to execute live web searches or fetch current pages."* The architecture file is largely anchor-fact restatement + category-pattern inference.
- **Stream 3 retry partially recovered** but explicitly refused to fabricate customer names. The named-customer roster is intentionally thin.
- **Stream 4 retry had partial tool access** and introduced the YC W22 vs S21 contradiction and the Goldman/BlackRock fund confusion. Specific URLs in stream 4's source list should be re-verified before external citation.
- **No stream directly fetched meow.com pages, the legal/terms pages, the FINRA BrokerCheck for CRD 322685, BlackRock fund docs, or court filings.** All claims rest on press summaries and anchor-fact propagation.

The single most useful follow-up action is direct fetch of:
1. meow.com homepage + /legal + /terms + /pricing (current state)
2. FINRA BrokerCheck for CRD 322685 (Meow Markets LLC) — definitive on broker-dealer status, clearing arrangement, disciplinary history
3. SEC EDGAR for Meow Markets LLC — Form BD, FOCUS reports (these may include AUM data)
4. BlackRock TTTXX fund factsheet (or Goldman FTGXX, depending on which is correct)
5. FTX bankruptcy claims register at restructuring.ra.kroll.com/FTX (search for "Meow")
6. NYAG press releases 2023-2024 (search for "Meow Financial" or similar)
7. archive.org snapshots of meow.com from Q3 2022, Q1 2023, 2024, 2025, 2026 (drift check)
