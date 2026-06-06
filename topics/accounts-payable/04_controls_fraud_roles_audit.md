# 4 — Roles, Controls, Fraud & Audit

*AP is the point where money leaves the company — so it is the most control-intensive, fraud-exposed function in finance.*

## The people / roles

**Inside AP:**
- **AP clerk / specialist / processor** — the "maker." Receives, codes, matches, routes, resolves discrepancies, schedules payments. Should **never** also approve or release payment.
- **AP manager / supervisor** — owns the function, policy, KPIs, exceptions; often the "checker" on higher-value items.

**Up the chain:**
- **Controller** — owns GL integrity + financial statements; designs the AP control framework; owns the close; primary interface to auditors. In SOX, the control owner who must evidence controls operated.
- **CFO / VP Finance** — sets policy (incl. Delegation of Authority), owns working-capital strategy; in public companies, **certifies** statements + control effectiveness (SOX 302/404); top-of-matrix approver.

**Adjacent:**
- **Procurement / buyers** — source suppliers, raise/approve POs (the demand side; PO creator ≠ PO approver).
- **Approvers / budget owners** — confirm a purchase was legitimate, received, in-budget, up to their DoA limit.
- **Treasury** — *funds* the payments, releases the bank files, manages liquidity + positive-pay. Separating Treasury (moves money at the bank) from AP (decides what to pay) is itself a control.
- **External auditors** — independent CPAs testing balances + controls.
- **The vendor** — counterparty; also the vector for the most damaging modern fraud (BEC/bank-change).

**How it scales:** 1-person shop (one person does all → SoD impossible → rely on compensating controls like owner reviewing the bank statement) → mid-market (clerk + manager + Controller oversight) → enterprise **Shared-Services Center** (fragmented sub-teams: intake/OCR, matching/exceptions, **a dedicated vendor-master team**, payments, helpdesk — fragmentation is both efficiency and deliberate control design).

## Internal controls

Mapped to the **COSO** framework. The goal: only **valid, accurate, authorized, properly recorded** obligations get paid, **once**.

- **Segregation of Duties (SoD)** — the foundational control. The four AP duties — **(1) processing/recording, (2) approval, (3) payment execution, (4) reconciliation** — must be split. Canonical example: the same person must never be able to *set up a vendor + approve an invoice + release payment* (else they create a fake vendor, approve a fake invoice, pay themselves). Highest-risk conflicts: vendor-master + payments; PO creation + PO approval; goods receipt + invoice verification; invoice posting + payment execution. **The most-cited control in audit findings** (often missed in ERP role assignment).
- **Delegation of Authority (DoA) / approval matrix** — who approves what, up to what amount, under what conditions (tiered thresholds, escalating hierarchies, out-of-policy escalation). ~90% of companies have one; only ~71% consider theirs effective (usually because it's enforced manually, not in workflow).
- **Three-way match** — the signature preventive control (PO + receipt + invoice agree on qty/price/item before payment). Catches overbilling, duplicate billing, phantom deliveries, inflated/fake invoices.
- **Vendor master controls** — the most fraud-sensitive data store (holds bank details). Only a restricted team can add/edit; **bank-detail changes = high-risk event requiring out-of-band verification** (call a known number, not one from the request); full audit trail; periodic review for duplicate/dormant/suspicious vendors; match vendor bank/address against the employee master.
- **Maker-checker / dual authorization** ("four-eyes") — the maker can never be sole approver; high-risk items (large payments, new vendors, bank changes) need two independent approvals; bank disbursements above thresholds need dual release.
- **SOX (Sarbanes-Oxley)** — §302 (CEO/CFO certify accuracy) + §404 (management documents + tests ICFR; auditor attests for accelerated filers). Because AP feeds expenses/liabilities into the statements, AP controls are **squarely in SOX 404 scope** — documented, tested that they *operated*, deficiencies remediated (deficiency → significant deficiency → material weakness).
- **Audit trails** — every control depends on an immutable log of who-did-what-when (entry, approvals, vendor changes, payment release, **overrides** — a red flag auditors examine).

## AP fraud — the major types + the numbers

**Benchmark stats:** ACFE 2024 *Report to the Nations* — orgs lose ~**5% of revenue/yr** to occupational fraud, median **$145K/case**, **89% asset misappropriation**; **billing schemes ~$100K median**. AFP 2025 — **79% of orgs** faced payments fraud in 2024. FBI IC3 2024 — **BEC ~$2.8B in 2024** (~$8.5B cumulative 2022–24).

- **Business Email Compromise (BEC) / vendor impersonation / bank-change fraud** — a fraudster spoofs a vendor/exec and requests a payment redirect ("update our bank details"). **#1 fraud avenue (63% of orgs, 2024)**; vendor-imposter fraud hit 45% (+11 pts YoY); wires the top target. *Defense:* out-of-band callback, locked vendor master, dual approval, DMARC/SPF/DKIM, positive pay.
- **Duplicate payments** (error or fraud) — same invoice paid twice; tweaked invoice number/date/vendor variant. *Defense:* ERP duplicate detection (incl. fuzzy matching), three-way match, recovery audits.
- **Fictitious / shell vendor schemes** — insider creates a fake vendor + bills for nothing delivered. *Defense:* vendor-master SoD, verified tax IDs/bank details, employee-file cross-match, dormant-vendor review, three-way match (no PO/receipt → fails).
- **Invoice fraud / inflated invoices / billing schemes** — inflated qty/price, pass-through markup. *Defense:* three-way match, tolerance checks, independent budget-owner approval.
- **Check fraud & ACH fraud** — checks remain **most-defrauded (63%)** yet 75%+ have no plan to stop using them; ACH fraud rising. *Defense:* positive pay, ACH debit blocks/filters, payee-name verification, dual control.
- **Internal collusion** — two+ insiders defeat SoD (the "second pair of eyes" is in on it). *Defense:* job rotation/mandatory vacations, continuous monitoring, **whistleblower hotlines (tips are the #1 detection method per ACFE)**.

## Audit & assurance

Auditors test management **assertions**:
- **Existence/occurrence** — recorded payables are real.
- **Completeness** — *all* payables that should be recorded *are* — **the highest-risk AP assertion** (natural risk is *understatement* to flatter the balance sheet).
- **Cutoff** — recorded in the correct period (did a Dec invoice land in Dec?).
- **Valuation / rights & obligations** — amounts correct, obligation truly the entity's.

**Key procedures:** **Search for Unrecorded Liabilities (SURL)** — examine post-year-end payments and trace back to see if the liability belonged in the prior period (*the* completeness test); **AP confirmations** (often with *active vendors showing small/zero balances*, where understatement hides); cutoff testing; AP↔GL + vendor-statement reconciliations; tests of controls (re-perform three-way match, approvals, SoD, override logs); analytical procedures (AP turnover, DPO trends).

## Record retention / audit-readiness

Keep invoices, POs, receipts, approvals, contracts, W-9s + bank verification, payment records, remittance, and the audit trail. **US baseline:** IRS general rule 3 years, but AP/AR records commonly **7 years** for safety (6 if income under-reported >25%; indefinite for fraud/non-filing; employment tax ≥4 years). Electronic records OK if they reproduce originals and stay accessible. **Audit-readiness** = complete, indexed, retrievable documentation + intact audit trail + current reconciliations + preserved control evidence.

→ Next: [05_automation_ai_metrics_market.md](./05_automation_ai_metrics_market.md)
