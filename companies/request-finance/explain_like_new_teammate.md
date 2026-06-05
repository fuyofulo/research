# Request Finance — Explain Like a New Teammate

## One sentence

Request Finance is the crypto-native "Bill.com": a non-custodial AP/AR/invoicing/payroll app that lets a DAO, protocol, or crypto startup invoice, approve, and pay vendors & contributors in stablecoins straight from their own wallet or Safe multisig — and keep the books — built on the open-source Request Network protocol.

## What problem it solves

Before it, a DAO paying 80 contributors in USDC did it as raw multisig transactions: no invoices, no approval trail, no GL coding, no audit record, reconciliation by hand. Request turned "pay people in crypto" into a Bill.com-style workflow: contributor submits an invoice → finance approves → pays from the Safe → the books update automatically.

## How it's different from Bill.com / Tipalti

The big one: **custody.** Bill.com pulls your money into its own accounts and earns float; Tipalti makes you pre-fund a non-interest account. Request (on the crypto side) **holds nothing** — the payer signs from their own wallet and funds go wallet-to-wallet on-chain. No float, no pre-funding, no middleman holding your money. *(Caveat: since 2024 Request added custodial fiat rails — off-ramp, a Global USD Account, cards — so on the fiat side it's now more fintech-like.)*

## How a payment works

1. Contributor/vendor submits an invoice (or you upload a bill; AI OCR captures it).
2. It routes to approvers (email-notified), who approve in Request or in the Safe app.
3. You batch-pay from your Safe multisig — many transfers bundled into one transaction, across chains/currencies.
4. Funds move wallet-to-wallet on-chain; Request watches the chain and marks invoices paid.
5. Paid bills sync to QuickBooks/Xero/NetSuite (or Request's own crypto accounting).

## Who buys it

Crypto-native finance leads ("Web3 CFOs") at DAOs, protocols, foundations, and crypto startups. Marquee logos: Aave, The Sandbox, The Graph, MakerDAO/Sky, OpenZeppelin, Arbitrum, Ledger (discount the wall — several are also investors).

## The honest read

It's the real leader of crypto-native AP/invoicing — but a **small, cyclical business** (~$1.3B lifetime volume, ~$24M/month), its headline stats are inflated (not "$2B"; "43%" was USDC's payment share, not market share), its REQ token is economically irrelevant, and it's **EVM-first — Solana is ~6% of volume and not in its API.** It's buying its way into fiat + accounting + MiCA because the pure crypto-native niche is too small.

## Why it matters for Decimal

Request is Decimal's **workflow-twin** (Altitude is the account-twin). It proves the model works — and previews Decimal's roadmap pressures (fiat off-ramp, accounting, US tax forms). **Decimal's clearest opening: be genuinely Solana-native**, the rail position Request only peripherally serves. The defensible spot is the intersection — *better than Altitude on AP-workflow depth, more Solana-native than Request.*

## Related files
- [deep_dive.md](./deep_dive.md) · [architecture.md](./architecture.md) · [use_cases_and_examples.md](./use_cases_and_examples.md) · [marketing_vs_reality.md](./marketing_vs_reality.md)
