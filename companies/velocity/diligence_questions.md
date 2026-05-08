# Velocity - Diligence Questions

Date: 2026-05-07

## Questions before treating Velocity as a direct competitor

1. Which customer segments are actually live: payment companies, global businesses, or financial institutions?
2. How many live customers exist?
3. What is monthly payment/settlement volume?
4. Which geographies are live today?
5. Which currencies are live today?
6. Which stablecoins are supported: USDC, USDT, USDG, EURC, others?
7. Which blockchains are supported?
8. Are they chain-agnostic or prioritizing one network?
9. Is AI a real product surface or just future automation language?
10. Which workflows do customers use most: payout, settlement, treasury, liquidity, yield, or reconciliation?

## Technical diligence

1. Is there a public or private OpenAPI spec?
2. Is there a sandbox?
3. Do they support webhooks?
4. Do they support idempotency keys?
5. What are the rate limits?
6. Is the ledger double-entry?
7. Can customers export full transaction/audit logs?
8. How are wallet addresses generated and controlled?
9. What custody model is used: direct custody, sub-custody, customer-owned custody, omnibus, segregated?
10. What exactly do Fireblocks and Zodia each handle?
11. How do they handle Travel Rule payloads?
12. What compliance tools are integrated?
13. What is the reconciliation model for fiat/stablecoin mixed flows?
14. Do they have ERP/TMS integrations live or planned?

## Regulatory diligence

1. Which licenses does Velocity itself hold?
2. Which licenses are held only by partners?
3. Who is the legal counterparty to the customer?
4. Who holds customer funds at each step?
5. Are customer funds safeguarded, segregated, insured, or held in trust?
6. Which jurisdictions are excluded?
7. How is yield/rewards offered legally?
8. What disclosures are given to customers about stablecoin risk?
9. How do they manage sanctions and chain-risk exposure?
10. What is the complaint/dispute process?

## Business diligence

1. What is the pricing model: SaaS, bps, FX spread, wallet fees, transfer fees, or enterprise contract?
2. What is gross margin by flow?
3. What is the main revenue driver?
4. What is CAC if selling to enterprise CFOs?
5. How long is sales cycle?
6. Do they have a repeatable wedge or mostly founder-led enterprise deals?
7. Is Dragonfly investment strategic for distribution or purely financial?
8. Are Fireblocks/Zodia exclusive or standard vendor relationships?
9. What is their biggest bottleneck: licenses, bank partners, liquidity, engineering, compliance, or sales?

## Questions for our own MVP

1. Which customer problem can we solve without building Velocity's entire banking network?
2. Can we use Bridge for fiat rails and focus on AI workflow intelligence?
3. Can we use Squads/Grid/Privy for wallet control instead of building custody?
4. What finance workflow is painful enough that customers do not care that we are not a full bank?
5. Can we provide better reconciliation, approvals, exception handling, and treasury insight than Velocity's generic platform?
6. Can we win Solana-native teams first, where Velocity is broader but less specialized?
