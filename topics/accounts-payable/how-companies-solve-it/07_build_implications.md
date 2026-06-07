# Build Implications — Assembling Your Own AP Pipeline

*The synthesis: for someone building the full AP pipeline, what to build vs buy/partner at each stage, the hard part, and where the open white space is. Distilled from the six stage teardowns.*

## The three laws that fall out of every stage

1. **The rail is not the moat.** Routable bolting stablecoin on via Brale (2025) proves rails are swappable. Moving USDC on Solana is the *easy* part.
2. **Extraction is commoditized.** Frontier LLM + RAG matches incumbents in ~6 months. Don't build proprietary OCR; don't pitch extraction as the edge.
3. **The moat is the boring middleware + the un-overridable gate:** onboarding + tax + deep ERP sync + agent orchestration + code-enforced execution. **No incumbent has all of it.**

## Build vs buy/partner — the decision per stage

| Stage | BUILD (differentiation) | BUY / PARTNER (commodity or regulated) | The hard part |
|---|---|---|---|
| **1 Intake/Capture/Code** | GL-coding via RAG-over-customer-history + confidence gate (the correction-loop flywheel) | Extraction = vision-LLM (Claude/GPT/Gemini) + OCR fallback | Coding novel/non-PO spend; reconciling cleanly into the ERP |
| **2 Match/Exception/Approval** | **Code-enforced approval on Squads** (DoA-as-code via SpendingLimit PDAs) + collaboration-on-invoice exception UX | Multisig primitive itself = **inherit Squads SAP** (don't roll your own — get OtterSec+Certora for free) | Signer-availability friction; getting matchable PO/GRN data; exception UX + time-to-value |
| **3 Pay/Rails/Float** | The orchestration + payee-choice (fiat *or* USDC behind one API) | USDC rail (Solana) + **fiat off-ramp partner (Bridge/BVNK)** | Vendor acceptance of stablecoin (the same limiter as virtual cards); regulatory (MTL/MSB/OFAC) |
| **4 Onboarding/Tax/Compliance** | Onboarding portal + bank/wallet validation + **fraud-locked vendor master** (out-of-band callback, dual approval) | **Tax filing → Trolley/Toku; KYB → Sumsub/Persona; OFAC → screening vendor; e-invoicing → Sovos/Pagero** | Liability, not features — strict-liability OFAC, IRS penalties, lost VAT, per-country mandate wave |
| **5 ERP Sync/Close** | Hand-build the 2–3 ERPs your ICP runs (NetSuite first) + **active sync monitoring + recon dashboards** | Long-tail ERPs via aggregator (**Merge/Codat/Rutter**) | Master-data mapping, period locks, the double-write balance guarantee — *the chain doesn't reconcile your customer's NetSuite for you* |
| **6 AI/Architecture** | **Agent-with-tools + tool registry**, per-org memory; the convenience↔security separation | Frontier models (via an LLM-proxy so you can swap) | Keeping "agent" (probabilistic) and "code" (deterministic, un-overridable) cleanly separated |

## The architecture, in one sequence

> **agent drafts → human approves → code enforces → multisig executes**

- **Agent** (probabilistic, agent-with-tools, no execution authority): reads invoices/email/CSV, looks up vendor history, suggests GL codes, drafts payment proposals.
- **Human** approves (the trust contract).
- **Code** enforces the rules that *cannot be overridden* — spend caps, required signers, approval chains, sanctions hooks — as on-chain Squads PDAs (SVM-enforced, not backend-enforced).
- **Multisig executes** atomically; the approval *is* the on-chain signature.

This is the combination no incumbent has: Ramp-grade agent orchestration **+** code-enforced execution that makes agent/insider mistakes *structurally un-executable* (directly defeating BEC, the #1 fraud vector). It also lets you safely give the agent more autonomy than TradFi can, because the gate is deterministic.

## Where the open white space is

From the matrix, two intersections nobody occupies:
1. **Code-enforced multisig gate (Altitude/Request have it) + Stampli-grade collaboration/exception UX (they don't) + Tipalti/Trolley-grade tax & ERP depth (crypto-native lacks entirely).** That full stack, Solana-native, is unbuilt.
2. **Solana-native AP at all.** Request is EVM-first (Solana ~6%, not in API); Altitude is account-led with no real AP workflow (no matching, no ERP sync, no tax). The Solana AP-workflow position is genuinely open.

## The honest sequencing (what's hard, in order)

1. **Easy / solved:** moving USDC; invoice extraction. Buy/commodity.
2. **Medium / inherit:** the multisig gate (Squads SAP, formally verified — don't rebuild).
3. **Hard / build:** GL-coding flywheel; the agent-with-tools orchestration; the exception/collaboration UX + time-to-value (Stampli wins deals on 4–6 week deploy, not rails).
4. **Hardest / liability — partner, don't build:** tax filing (W-8/9→1099/1042-S), OFAC, e-invoicing, multi-entity ERP sync depth. This is the table-stakes layer that makes crypto-native AP products thin today; closing it (by *partnering*) is the unlock.

## The one-line build thesis

> Build the **agent-with-tools + code-enforced multisig** core on Solana/Squads (the defensible, un-copyable part), nail **onboarding + ERP sync + exception UX** (the boring moat + the quality opening against Tipalti's flaky sync), and **partner the regulated liability layer** (tax via Trolley/Toku, KYB via Sumsub, off-ramp via Bridge, e-invoicing via Sovos). The rail is swappable; the moat is everything wrapped around it.

→ Back to the [master matrix](./00_master_matrix.md) · the [AP primer](../README.md)
