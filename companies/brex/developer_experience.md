# Brex - Developer Experience

Date: 2026-05-09

## Public developer surface

Brex has a strong public developer surface relative to most finance platforms in this research set.

Publicly visible:

- Developer portal at [developer.brex.com](https://developer.brex.com/).
- REST APIs.
- OpenAPI descriptions.
- JSON over HTTPS.
- Production base URL: `https://api.brex.com`.
- Bearer token authentication.
- API categories for accounting, budgets, expenses, fields, onboarding, payments, team, transactions, travel, and webhooks.
- API status page.
- Slack community link.
- Examples in cURL, JavaScript, Node.js, Python, Ruby, and Java on endpoint pages.

Not fully visible:

- Self-serve sandbox with test credentials.
- Complete embedded-finance partnership path.
- Pricing for API usage.
- Enterprise approval/KYB requirements for partner use.
- Whether all endpoints are available to all customer tiers.

Source: [Developer Portal](https://developer.brex.com/).

## Authentication

Brex developer authentication is user-token based for customer integrations:

1. Sign in to the Brex dashboard as an account admin or card admin.
2. Go to Developer settings.
3. Accept the developer API agreement if needed.
4. Create a token and choose scopes.
5. Pass it as a bearer token:

```http
Authorization: Bearer <YOUR_TOKEN_HERE>
```

Brex says user tokens expire if unused for 90 days and stop working if the associated user becomes inactive.

Source: [Authentication guide](https://developer.brex.com/guides/authentication).

## API catalog

Public API categories:

| API | What it exposes | Why it matters |
|---|---|---|
| Accounting | Accounting data and export workflows | Close automation and ERP sync |
| Budgets | Budgets and budget programs | Pre-spend controls |
| Expenses | Card expenses, receipt match, receipt upload, expense records | Expense automation and reconciliation |
| Fields | Custom fields and field options | Company-specific accounting metadata |
| Onboarding | Referrals and signup prefill | Partner/channel motion |
| Payments | Vendors, incoming transfers, outgoing transfers, linked accounts | AP and money movement |
| Team | Users, locations, departments, titles, cards, legal entities, company | Org graph and card administration |
| Transactions | Card/cash transactions, accounts, statements | Reconciliation and ledger sync |
| Travel | Trips made in Brex Travel | Travel expense data |
| Webhooks | Event subscriptions and event notifications | Real-time workflow integrations |

Source: [Developer Portal](https://developer.brex.com/).

## Expenses API

The Expenses API exposes card expense and expense records. The public docs show:

- Production server: `https://api.brex.com`.
- Staging server: `https://api-staging.brex.com`, with a warning that it is not a sandbox and does not work with customer tokens.
- OAuth2 scopes such as `expenses.card.readonly` and `expenses.card`.
- Expense filters by user, budget, spending entity, status, payment status, purchased dates, updated dates, and more.
- Expense types including card, bill pay, reimbursement, clawback, and unset.
- Receipt match endpoint: `/v1/expenses/card/receipt_match`.

The important read: Brex exposes enough expense/accounting metadata for internal tools to automate close workflows, dashboards, and exception review.

Source: [Expenses API](https://developer.brex.com/openapi/expenses_api/expenses/listexpenses).

## Payments API

The Payments API lets customers initiate and manage payments and vendors from Brex business accounts. Public docs expose:

- Vendor endpoints: create, list, update, delete vendors.
- Transfer endpoints: incoming transfers, outgoing transfers, transfer status.
- Linked account endpoints.
- ACH, domestic wire, and check payment support is named in the developer portal overview.

This is not the same as a stablecoin on/off-ramp API. It is an AP/payment workflow API over Brex business accounts and supported fiat rails.

Source: [Payments API](https://developer.brex.com/openapi/payments_api/).

## Team and card APIs

The Team API lets customers manage users, departments, locations, titles, cards, legal entities, and company metadata. Public docs show endpoints for:

- Users.
- Locations.
- Departments.
- Titles.
- Cards.
- Legal entities.
- Company.

This matters because spend controls depend on org context. You cannot automate finance well if the API only exposes transactions. You need users, roles, entities, departments, and cards.

Source: [Team API](https://developer.brex.com/openapi/team_api).

## Transactions and accounts APIs

The Transactions API exposes:

- Card transactions.
- Cash account transactions.
- Card accounts.
- Cash accounts.
- Statements.

This supports reconciliation, internal dashboards, month-end close, treasury monitoring, and custom controls.

Source: [Transactions API](https://developer.brex.com/openapi/transactions_api).

## Webhooks

Brex webhooks send real-time notifications when events happen in managed accounts. Public docs show webhook subscriptions, webhook groups, webhook secrets, and event types such as:

- Accounting record ready for export.
- Expense payment updated.
- Transfer processed.
- Transfer failed.
- User updated.
- Referral events.
- Embedded card/account events.

This is a meaningful developer primitive because finance automations should be event-driven, not cron-driven exports.

Source: [Webhooks API](https://developer.brex.com/openapi/webhooks_api/).

## Sandbox reality

Brex documents a staging server, but the Expenses API page explicitly warns that staging is not a sandbox and will not work with customer tokens. That is a real limitation for third-party developers.

Practical implication:

- Existing Brex customers can build internal automations with production access.
- Partners may get a deeper partner-auth flow.
- Independent developers cannot easily play with a fake company, fake cards, fake bills, and fake transactions the way they can with a strong sandbox product.

This is fine for an enterprise spend platform, but weaker than a developer-first infrastructure company.

## Developer maturity score

Score: 8/10 for customer/internal-tool developers, 5/10 for open platform builders.

Why high:

- Public docs.
- OpenAPI.
- REST/JSON.
- Broad API surface.
- Auth docs.
- Webhooks.
- Real payment/vendor/card/account objects.

Why not perfect:

- No obvious public sandbox.
- API usage is tied to being a Brex customer/partner.
- Not an embedded stablecoin/card/banking platform.
- Some docs imply partner flows are gated.

## Compare to Bridge, BVNK, Altitude/Grid

- Bridge: better for embedded stablecoin on/off-ramp and issuing flows; more infrastructure-native.
- BVNK: better for merchant/payment processing and fiat/stablecoin orchestration.
- Altitude/Grid/Squads: better for Solana-native smart account/control-plane logic.
- Brex: much deeper in business finance workflows, accounting context, expenses, AP, and enterprise operations.

Brex is the model for workflow APIs; Bridge/BVNK are the model for money-movement APIs.

## What we can learn

If we build a stablecoin CFO product, our developer API should copy Brex's object discipline:

- Users.
- Roles.
- Legal entities.
- Departments.
- Cards/wallets/accounts.
- Budgets.
- Vendors.
- Bills.
- Payments/transfers.
- Expenses.
- Accounting exports.
- Webhooks.

The API should not start and end with "send USDC." Serious business customers need the operating context around the payment.
