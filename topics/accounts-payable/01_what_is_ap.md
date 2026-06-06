# 1 — What Accounts Payable Actually Is

*Vendor-neutral primer. Start here.*

## The one-sentence definition

**Accounts Payable (AP)** is the set of short-term obligations a business owes its suppliers/vendors for goods and services **already received but not yet paid for** — and also the *function/department* that receives, validates, approves, pays, and records those supplier bills.

AP is two things at once:
1. A **balance-sheet line item** — the aggregate amount owed (a current liability).
2. A **process/function** — the team and workflow that gets money out the door correctly.

## Why the function exists

Companies rarely pay cash-on-delivery. Suppliers extend **trade credit** ("Net 30" = pay within 30 days), creating a gap between *receiving value* and *paying for it*. AP manages that gap **with control**: paying the **right vendor, the right amount, for goods actually received, once, on time** — while preserving cash, capturing discounts, preventing fraud, and producing an auditable record.

## The accounting, in two journal entries

When the invoice is recorded:
```
Dr  Expense / Asset      $X     (the cost, or inventory received)
    Cr  Accounts Payable      $X (the obligation to pay the vendor)
```
When it's paid:
```
Dr  Accounts Payable     $X
    Cr  Cash                   $X
```
AP appears on the **balance sheet** under **current liabilities** (due within ~1 year). The expense side flows to the **income statement**; changes in the AP balance are an adjustment in **operating cash flow** (rising AP = a source of cash; paying it down = a use of cash).

## AP vs. the things it gets confused with

| Concept | What it is | Distinction from AP |
|---|---|---|
| **Accruals** | Costs incurred but **no invoice yet**; booked at period-end as an **estimate** | AP = invoice received, amount certain. When the invoice arrives, the accrual reverses → becomes AP. *Accrual → (invoice) → AP → (cash) → settled.* |
| **Accounts Receivable (AR)** | Money **owed to** you by customers | AP = money you **owe out** (liability); AR = money **owed in** (asset). Your AP is your supplier's AR — mirror images. |
| **General expense** | The P&L cost of doing business | An expense is the income-statement event; AP is the balance-sheet obligation that may accompany it. You can have expense with no AP (paid cash) and AP that isn't expense (inventory/asset). |
| **Payroll** | Compensation owed to **employees** | Own cycle/system, employment + tax-withholding rules, separate accrued-payroll liabilities — not third-party trade payables. |
| **Treasury** | Management of cash, liquidity, funding, bank relationships | AP decides *what is owed and when due*; Treasury decides *how/when cash actually leaves* and funds the payment run. AP feeds payment timing into Treasury's cash forecast. |

## Where AP sits in the finance stack

AP owns the **back half** of the broader purchasing cycle:

```
SOURCE-TO-PAY (S2P)
└── Sourcing / RFx / Contracting / Supplier onboarding
        └── PROCURE-TO-PAY (P2P / purchase-to-pay)
            └── Requisition → PO → Goods Receipt → [ AP: Invoice → Match → Approve → Pay ] → GL / Close
```

- **Procure-to-Pay (P2P):** requisition → PO → goods receipt → **invoice → payment → accounting**. AP owns invoice→payment→reconciliation.
- **Source-to-Pay (S2P):** the superset — adds upstream strategic sourcing, RFx (RFI/RFP/RFQ), contracting, supplier onboarding.

**Procurement** commits the spend (POs); **AP** is the **subledger** that records each invoice/payment in detail; the **General Ledger (GL)** holds a single summary **AP control account** that the AP subledger must always reconcile ("tie out") to. At **month-end close**, AP enforces cutoff, books accruals for received-but-unbilled items, and ties the AP aging to the GL control account before the books lock.

→ Next: [02_the_ap_lifecycle.md](./02_the_ap_lifecycle.md) — the full end-to-end workflow.
