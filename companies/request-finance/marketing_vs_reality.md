# Request Finance — Marketing vs Reality

*Claim audit + the crypto-AP category graveyard + competitive map + bear case*
*Compiled 2026-06-06*

Confidence: ✅ corroborated · 🟡 single/inferred · 🔴 dubious/contradicted.

---

## 1. Claim audit

| Claim | Verdict | Reality |
|---|---|---|
| ">$2B in crypto invoices" | 🔴 **inflated** | Request's own monthly "in Numbers" reports show **~$1.3B cumulative all-time (Jan 2026)**, after crossing $1B in Mar 2025. Run-rate ~$24–34M/month. The homepage's "~$300M" is stale/differently-scoped. A clean ">$2B" is not corroborated. |
| "43% of crypto finance teams use it" | 🔴 **misattributed** | The real 43% is **USDC's share of payments** on the platform (Aug 2025 data), not market share. "43% of teams" is a garbled version of a currency-mix stat. |
| "the Bill.com for crypto" | 🟡 **fair positioning, oversold parity** | Bill.com's core value is moving fiat + deep accounting integration; Request historically **didn't move fiat itself** and bolted accounting on via acquisition (Consola). The analogy is directionally right but overstates feature parity. |
| "~88–90% stablecoin share" | ✅ **checks out** | Consistent across Request's own monthly data; USDC the leader (~43%). |
| Marquee logo wall (Aave, Sandbox, etc.) | 🟡 **discount it** | Several logos overlap with seed investors; many "users" are really Safe-multisig users. Real independent commercial traction is smaller than the logos imply. |

## 2. The crypto-AP / treasury-ops category graveyard (the most important finding)

The "crypto-native treasury/AP/payroll tooling" category has **consolidated hard** — survivors are few, and the category increasingly belongs to *platform owners* (Safe, Coinbase, Squads), not scrappy peers:

| Player | 2026 status |
|---|---|
| **Request Finance** | ✅ Alive — leads crypto-native **AP/invoicing** (EVM-first) |
| **Toku** | ✅ Alive, strong — token/stablecoin **payroll + EOR + tax** ($1B+/yr) |
| **Rise** | ✅ Alive — **crypto payroll** (USDC, smart-contract payouts) |
| **Sphere (SpherePay)** | ✅ Alive — **Solana-first** stablecoin payments/billing API |
| **Den (Onchain Den)** | ✅ Alive — Safe-based multisig **ops/treasury**, ~130 DAOs |
| **Coinshift** | ✅ Alive but **pivoted** to csUSDL yield-bearing stablecoin (>$100M TVL) — no longer pure treasury-ops |
| **Liquifi** | 🟡 **Acquired by Coinbase (Jul 2025)** → token mgmt absorbed |
| **Multis** | 🔴 **Acquired by Safe (Apr 2024)** — dead as product |
| **Utopia Labs** | 🔴 **Wound down AP/payroll (Nov 2023)**, pivoted to a wallet |
| **Loop Crypto** | 🔴 **Shutting down ~Feb 2026** |
| **Parcel** | 🔴 Discontinued |

**Read:** Request is the clear leader of crypto-native AP/invoicing *specifically*, but standalone "crypto treasury ops" largely collapsed into Safe and Coinbase. Request increasingly competes with **platform owners** (Safe, Coinbase, **Squads/Altitude on Solana**), not peers.

## 3. Competitive map

**vs Bill.com / Tipalti (TradFi AP):** Bill.com/Tipalti win on fiat (ACH/wire/SEPA), normal SMB/mid-market businesses, deep ERP + tax-form machinery. Request wins when payments are tokens/stablecoins to wallets, counterparties are crypto-native, and you pay from a multisig — which Bill.com/Tipalti can't do natively. **The squeeze is real:** TradFi/B2B-payments players (Paystand USDb, Bridge, BVNK, Visa stablecoin settlement) are adding stablecoin rails with far larger distribution; ~$400B real-world stablecoin payment volume in 2025 normalizes the rail and narrows Request's "crypto-native" moat.

**vs Altitude (Squads, Solana):** Altitude is **account-led** (a stablecoin business *account* — cards, APY, ACH/SEPA + stablecoin, $200M+ processed, $42.9M raised). Request is **invoicing/AP-led and EVM-first**. Different centers of gravity: Altitude wants to *be the account*; Request wants to *be the AP/AR workflow on top of whatever account/multisig you have*. **On Solana, Altitude has home-field advantage.**

**vs other crypto-native:** Sphere (Solana-first payments API), Den (Safe ops), Toku/Rise (payroll) — see the graveyard table. Request leads invoicing/AP; others lead payments-API, ops, payroll respectively.

## 4. Bear case / strategic risks

1. **REQ token overhang** — economically irrelevant utility (~0.073% of supply ever burned), trades on speculation, decoupled from the business. A liability, not an asset.
2. **Narrow, cyclical TAM** — ~$1.3B all-time, ~$24M/month, tied to crypto-org headcount/grant budgets that contract in bear markets. The reason for the fiat+MiCA+Bpifrance pivot: escape the crypto-native ceiling.
3. **Two-sided squeeze** — TradFi-adding-stablecoins from above (distribution); Solana-native + platform-owners (Safe/Coinbase/Squads) from the side.
4. **Acquisition-dependent product** — accounting (Consola) and fiat rails (Pay.so) were *bought, not built* — integration risk + a signal the organic product wasn't enough to be a full CFO stack.
5. **Likely US tax-form gap** — native W-8/W-9/1099 unconfirmed; probably weaker than Tipalti/Trolley/Deel.

## 5. Honest one-liner

> Request Finance is the genuine category leader in crypto-native AP/invoicing (~$1.3B lifetime, real marquee logos) — but a modest, cyclical business whose headline numbers are inflated/misattributed, whose token is irrelevant, which is EVM-first (Solana peripheral), and which is buying its way toward a fiat+crypto CFO stack precisely because the pure crypto-native niche is no longer enough.

---

## What this means for Decimal

- **Request is the proof-of-concept and the cautionary tale.** It proves crypto-native AP works ($1B+, marquee logos) — and proves the TAM is small enough that you *will* be pulled toward fiat rails, accounting depth, and tax compliance. Plan for that gravity from day one.
- **Decimal's cleanest wedge vs Request is Solana-native depth.** Request is EVM-first; Solana is ~6% of its volume and absent from its API. Own the Solana-first orgs (Solana DeFi/infra/protocols already on Squads) where Request is weakest and Altitude is the only real rival.
- **The real two-front fight:** Altitude (Squads' own product) for the Solana stablecoin-finance accounts, and Request for the cross-chain crypto-native AP workflow. Decimal has to be **better than Altitude on AP-workflow depth** and **more Solana-native than Request** — that intersection is the defensible position.
- **Don't rebuild the hard compliance pieces.** Request bought them; Decimal should partner — off-ramp (Bridge/BVNK), tax/payee-reporting (Trolley/Toku) — and focus build effort on the Solana-native AP workflow + code-enforced multisig.
