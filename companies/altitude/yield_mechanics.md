# Altitude — Yield Mechanics (How the ~5% Actually Works)

*Compiled 2026-06-06. Resolves the open question flagged in `marketing_vs_reality.md` ("the actual yield issuer is never named") and sharpens the yield-routing claims in `on_chain_truth.md`.*

Confidence: ✅ verified (primary/multiple sources) · 🟡 inferred/single source · 🔴 marketing-only / unverified.

---

## The headline finding

Altitude markets **"5.00% APY backed by short-term US Treasuries custodied with BlackRock"** (homepage currently shows **3.25%** — an unexplained discrepancy). But the marketing **blurs two distinct yield paths**, and the headline number is mostly the *low-risk, non-DeFi* one:

- **Path A — Reserve-interest pass-through ("rewards").** The user holds plain, liquid **USDC**. The Treasury yield is earned **upstream at the stablecoin-reserve level** (Circle's USDC reserves + Bridge reserves, held in short-term Treasuries; the BlackRock-managed reserve fund is the source of "custodied with BlackRock"). Squads/Altitude collects "incentives" tied to those holdings and pays a **discretionary slice back to the user as "rewards."** This is why it can claim **"instant liquidity"** — the user never holds a redemption-gated T-bill token, just USDC. ✅
- **Path B — Self-custodial DeFi lending ("DeFi integrations").** The optional on-chain path where the smart account lends into a protocol while retaining custody (mechanism below). 🟡 real integrations; the explicit Altitude→specific-vault link is partly inferred.

**The clever part is the legal wrapper, not the technology.**

## The custody mechanism (how a self-custodial multisig earns yield)

This is the technically important bit, and it's directly relevant to anything built on Squads v4:

> The Squads **smart account signs a cross-program invocation (CPI)** into the yield protocol, and the **receipt/position token returns to the *same* smart account.** Custody never leaves — only the user's multisig keys/policy can withdraw.

This is the public **SquadsX → Kamino** pattern (SquadsX = Squads' smart-account browser extension that lets a multisig interact with Solana DeFi while retaining custody). It's how "self-custodial" and "earning in a protocol" coexist: funds enter a lending market, but the position is owned by the user's smart account, not transferred to Altitude. ✅ (mechanism) / 🟡 (that Altitude's headline rewards run through this — they likely do NOT; Path A is reserve pass-through).

For **Path A**, the user does *not* hold a fund token — they hold USDC, and "earning" = receiving reward payouts. The Treasury allocation generating the underlying yield is controlled by the issuer/reserve manager (Circle/Bridge/BlackRock), not the user.

## The named protocols (and what's actually confirmed)

In the Squads/Altitude stack:
- **Kamino** — USDC lending; the **Gauntlet USDC Prime** curated vault exists on Kamino. ✅ integration real (via SquadsX) · 🔴 Gauntlet curating *Altitude's* funds specifically is **unconfirmed** (likely conflation from the shared Kamino venue).
- **Lulo** — yield *aggregator* that rebalances USDC across ~5 Solana lending markets. ✅ (Squads treasury docs)
- **Maple** `syrupUSDC` (~6.5%) — reachable via Kamino. 🟡
- **Save (Solend)** — named in Squads treasury docs. ✅
- **Plume Nest RWA vaults** — tokenized real-world-yield on Solana (5 Nest vaults launched Dec 4, 2025); our prior `on_chain_truth.md` had Altitude routing here. 🟡 integration real; Altitude-specific routing inferred.

**Unverified / corrected:**
- 🔴 **"BlackRock via BUIDL" is NOT confirmed.** Altitude only says "custodied with BlackRock" — equally consistent with plain Circle/Bridge *reserve* interest. BUIDL/Ondo/Securitize are never named.
- 🔴 **Gauntlet-curated Altitude strategy** — unconfirmed.
- The earlier `on_chain_truth.md` framing (Plume Nest + Kamino USDC Prime as *the* yield rails) is **more confident than the public sourcing supports** — treat those as *available DeFi integrations*, not the confirmed source of the headline rewards.

## Who earns what

Per the Altitude Supplemental Terms ([squads.xyz/legal/altitude](https://squads.xyz/legal/altitude)): the account *"does not itself earn interest,"* rewards are *"incentives from providers of Third-Party Services,"* paid at Squads' *"sole discretion,"* *"variable,"* and *"may be eliminated entirely."* → **Altitude earns the gross yield, passes a discretionary/revocable slice to the user, and keeps the spread.** ✅

## The regulatory structure (why it's "rewards," never "interest")

The **GENIUS Act (2025)** bars *payment-stablecoin issuers* from paying yield. Altitude's workaround:
- **It isn't the issuer** (Circle/Bridge are) — it's a *third party* paying a usage "reward," which the Act is silent on. ✅
- ToS use deliberate GENIUS-defensive language: *"Rewards are not interest and the Altitude Account is not an interest-bearing or yield-generating product."* ✅
- **Geofenced out of the EEA, Singapore, and Japan** (MiCA/MAS/JFSA exposure); not geofenced from the US in the disclosures found — the legally riskiest part. 🟡
- **Contested:** the OCC has proposed extending the yield ban to affiliates/third parties; a 2026 CLARITY-Act compromise reportedly preserves *usage-driven* rewards while banning passive bank-style interest. So the structure is real but fragile. 🟡

## What's genuinely NOT disclosed

- The exact instrument behind the headline rate (direct reserve interest vs a tokenized-T-bill fund vs Maple Cash).
- Whether the headline rewards touch DeFi at all, or are purely reserve pass-through.
- Any instant-liquidity-buffer vs yield-tranche architecture for Altitude specifically.
- Why homepage (3.25%) and X (5.00%) disagree.

## Implications for a Squads-based competitor (e.g., Decimal)

- **Path B (DeFi lending) is permissionlessly replicable today** on the same Squads v4 rails — CPI from a customer's smart account into Kamino/Lulo/Plume, receipt token stays in their account, custody retained. The SquadsX pattern is public.
- **Path A (the "BlackRock Treasuries" branding) is NOT easily replicable** — it needs scale/relationships to share stablecoin-reserve income, or holding tokenized T-bills directly. The BlackRock name does brand work that can't be borrowed.
- **The hard parts are not code** — they're (1) the **legal wrapper** ("rewards-not-interest," discretionary, geofenced, run through a purpose-built entity — Squads uses *Selimor Investments Ltd*, BVI), and (2) **risk**: Path B puts customer *payables* money into Kamino lending (smart-contract, oracle [Pyth/Switchboard], liquidation/utilization risk) — a different risk animal than reserve pass-through, hidden behind "instant liquidity, backed by Treasuries."

## Sources

- [Altitude on X — "5.00% APY, backed by short-term U.S. Treasuries custodied with BlackRock"](https://x.com/altitude/status/2009641526549467407)
- [Altitude Supplemental Terms (rewards/custody/jurisdiction)](https://squads.xyz/legal/altitude)
- [altitude.xyz](https://altitude.xyz/) (3.25% APY; "rewards are not interest")
- [Squads — Introducing Altitude](https://squads.xyz/blog/introducing-altitude-and-a-strategic-investment-from-haun-ventures) ("stablecoin rewards and DeFi integrations, with instant liquidity")
- [Blockworks — Squads launches Altitude](https://blockworks.com/news/squads-launches-altitude-stablecoins-funding-huan) (Circle + Bridge issuers, 1:1 Treasury reserves)
- [Squads — Grid: a stablecoin API for accounts, payments, cards and yield](https://squads.xyz/blog/grid-a-stablecoin-api-for-accounts-payments-cards-and-yield) ("RWA and high yield DeFi strategies," "guardrails")
- [Squads — SquadsX × Kamino](https://squads.xyz/blog/squadsx-kamino)
- [Squads treasury management overview](https://docs.squads.so/main/getting-started/treasury-management-overview) (Lulo, Save/Solend, Maple T-Bills)
- [Gauntlet — Vaults on Kamino (USDC Prime / SOL Balanced)](https://www.gauntlet.xyz/resources/gauntlet-vaults-on-kamino-sol-usdc) (no Altitude link)
- [Plume — Real-World Yield Layer on Solana / Nest vaults](https://plume.org/blog/building-solanas-real-world-yield-layer-with-plume)
- [GENIUS Act (S.1582) text — issuer yield prohibition](https://www.congress.gov/bill/119th-congress/senate-bill/1582/text)
- [CoinDesk — stablecoin rewards vs interest / OCC proposal](https://www.coindesk.com/policy/2026/03/01/stablecoin-yield-rewards-likely-won-t-be-banned-under-occ-proposal-state-of-crypto)
- [Perkins Coie — OCC proposes extending yield ban to affiliates/third parties](https://perkinscoie.com/insights/update/stablecoin-interest-yield-and-rewards-occ-proposes-sweeping-regulations-under)
- [Maple — syrupUSDC on Kamino (~6.5%)](https://maple.finance/insights/syrupusdc-and-syrupusdt-built-for-scale)
