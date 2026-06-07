# Stage 2 — Matching → Exception Handling → Approval

*The verification-and-authorization gate between "an invoice arrived" and "money is allowed to leave." This is where the crypto-native model is most differentiated.*

## The problem

- **Matching:** 2-way (PO+invoice, for services), 3-way (+goods receipt — the workhorse for goods), 4-way (+inspection). A **data-hygiene problem**: only works if PO, GRN, and invoice exist, are linked, and have comparable line granularity. The non-PO long tail (utilities, SaaS, pro-fees) has *no PO to match* → manual review. Most "AP automation" is really non-PO invoice routing, not true 3-way.
- **Exception handling:** ~14% average exception rate; "high exceptions" is the #1 AP-leader complaint. Resolved via credit memo / PO amendment, loops back to match.
- **Approval:** routed per a **Delegation of Authority (DoA)** matrix (thresholds, hierarchies, delegation) under **segregation of duties** (entry ≠ approve ≠ pay ≠ reconcile). ~90% of firms have a DoA matrix; only ~71% consider it effective — *"because it's enforced manually, not in workflow."* **That gap — policy-on-paper vs policy-enforced-in-code — is the entire strategic axis of this stage.**

## How each company solves it

| Company | Matching | Exception UX | Approval model |
|---|---|---|---|
| **Bill.com** | no true 3-way (PO *reference* only) | exception queue (~10–30% of bills); **no auto-escalation** | rules: thresholds, caps, category limits, approver chains |
| **Tipalti** | **genuine 2/3-way, header+line** (PO Matching Agent + Approve.com) | clerk queue | rules + multi-stage + Bill Approvers Agent |
| **Stampli** | limited; adding via P2P (2025) | **collaboration ON the invoice** (best-in-class) | collaboration-first routing + Billy |
| **Vic.ai** | **Autopilot PO match** (2/3-way) | continuous correction loop | autonomous routing (weakness: mistakes go *into payments*, software-only) |
| **Ramp** | PO match via Procurement (Venue); caught >$50M overbilling | agent flags ~3% | **policy-at-swipe** (out-of-policy blocked preventively, 94% in-policy) |
| **Request Finance** | **no PO/3-way** | thin; on-chain audit trail | **Gnosis Safe multisig** — approval & payment split; batch via MultiSend; m-of-n = the DoA |
| **Altitude** | **none** | thin | **Squads multisig + on-chain `SpendingLimit` PDAs + time-lock + policy hooks** |

## The crypto-native angle — multisig AS approval (the central contrast)

In traditional AP, **approval and execution are decoupled**: the approver clicks "Approve" (a DB row + audit log), and *later, separately*, a payment system moves money. Nothing structurally stops the software — or an insider with DB access, or a compromised account — from paying something unapproved. SoD/DoA are enforced by the **application layer** (the "enforced manually, not in workflow" weakness).

In the crypto-native model, **the approval IS the payment authorization, cryptographically and atomically:**

| | Traditional software approval | Multisig code-enforced |
|---|---|---|
| What approval *is* | DB row + audit log | on-chain signature (the authorization) |
| Enforcement layer | application code | smart contract / SVM |
| Platform can override? | yes (DB write) | no (needs threshold sigs) |
| Insider/DB-compromise SoD bypass | possible | **structurally impossible** |
| Spending limits | app-checked | **SVM-enforced (`SpendingLimit` PDA)** |
| Approval ↔ execution gap | decoupled (FBO/pre-fund) | atomic / same tx |

- **Request** uses Gnosis Safe: the Safe's m-of-n *is* the DoA; approve/pay split so signers see the exact payload; batch via MultiSend.
- **Altitude** goes further (built by Squads): `threshold` on the Settings PDA = the DoA; **`SpendingLimit` PDAs** ("$5k/week" enforced by the SVM, not a backend) = DoA-as-code with delegation; **time-locks** up to 3 months; **pre/post-CPI policy hooks** for sanctions/allow-list at the execution boundary. Jupiter walkthrough: upload invoice → Squads requests 2-of-3 → signer approves in Phantom → executes → auto-reconciles.

The punchline: Vic.ai's autonomy makes agent mistakes go *into payments* with only software controls; the multisig model makes agent/insider mistakes **structurally un-executable** — the agent can *draft*, but code *executes*.

## Spectrum

**Authorization enforcement (weak→strong binding):** rules-routing (BILL/Tipalti/Melio, app-enforced) → policy-at-swipe (Ramp/Brex, preventive but app-layer) → autonomous routing (Vic.ai, *weakens* control) → **multisig code-enforcement** (Request/Altitude, can't be faked/overridden; cost = m-of-n rigidity + signer-availability friction).

**Exception resolution:** queue (BILL/Ramp/Tipalti/Vic.ai — resolved *off* the document) → **collaboration-on-invoice** (Stampli, cleanest UX) → crypto-native (Request/Altitude — thinnest; they innovate on the gate, not on resolving mismatches).

**Where 3-way is genuinely hard:** line-item granularity mismatch; no PO exists (the whole non-PO tail); the GRN dependency lives in an ERP/WMS the AP tool doesn't own (why Tipalti needed Approve.com, Ramp needed Venue, and pure-payments players don't do it at all). **For crypto-native buyers (DAOs/protocols = almost all non-PO services spend), 3-way matching is largely irrelevant** — not doing it is a *fit* decision, not purely a gap.

## Build implication

- **Don't build a 3-way matching engine first** — needs PO+GRN systems you won't own, and early crypto-native customers are non-PO. Start with non-PO capture + coding + duplicate detection. 2-way covers most need; 3-way only for goods-heavy customers (needs a GRN feed).
- **Make the approval the on-chain signature.** Build on **Squads Smart Account Program** — inherit OtterSec+Certora formal verification rather than rolling your own multisig. Implement **DoA-as-code via `SpendingLimit` PDAs** (routine spend within an SVM-enforced limit needs no human; above it escalates to threshold). Use **policy hooks** for un-skippable sanctions screening. **Split approve-from-execute and show signers the exact payload.** Batch via Squads transaction-buffer.
- **The underbuilt opportunity:** pair the **code-enforced multisig gate** (which neither Stampli nor Tipalti has) with a **Stampli-grade collaboration/exception UX** (which neither Request nor Altitude has). *That intersection is open.*
- **The hard part:** not the on-chain auth (Squads gives it) — it's (1) the non-PO exception/collaboration UX + time-to-value (Stampli wins on 4–6wk deploy, not rails), (2) getting matchable PO/GRN data, and (3) **signer-availability friction** (m-of-n is strong but brittle when a signer is unreachable — the crypto analog to "approver-not-responding," worse because you can't override). Mitigate with SpendingLimit delegation + time-locks + escalation, not by weakening the gate.

*Gaps: Stampli's exact approval-rule mechanics, Altitude matching/exception engine (none documented — likely genuine gap), Routable's "PO-matching" depth, and tolerance-band specifics all under-documented locally.*
