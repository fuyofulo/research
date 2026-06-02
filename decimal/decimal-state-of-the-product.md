# Decimal — State of the Product

A factual snapshot of what Decimal is today, what's been built, and the direction taken to get here. Written so it can be cross-referenced against research on other companies in the space. Not opinionated about what to build next — that comes after the cross-check.

---

## 1. What Decimal is

**Decimal is a team-based B2B finance operator for stablecoin payouts on Solana.**

A team connects (or creates) a Squads multisig treasury wallet, invites coworkers as members with signing wallets, and operates the treasury as a shared finance surface: pay invoices from a single source-of-truth treasury, route every payout through multisig approval, run batch payment runs over CSVs or AI-extracted invoice PDFs, see every payout's full proposal-to-settlement lifecycle.

Live at https://decimal.finance. Submitted to Colosseum Frontier hackathon.

Original thesis (`product_direction.md`, dated 2026-05-05):

> An AI finance ops copilot for Solana teams that reads invoices, builds payment queues, flags risks, creates Squads payment proposals, and generates weekly cash reports.

Positioned as **"Monk for stablecoin-native businesses, starting with Solana treasuries."**

---

## 2. Who Decimal is for

**Decimal is built for teams, not individuals.** Every primitive in the system — organizations, memberships, invites, multisig, signing wallets, proposal voting — is team-shaped. There is no single-user mode.

### Personas inside a team

Within a Decimal organization, the same person may wear multiple hats, but the *roles* the product is built around are:

- **Initiator / proposer** — the operations person who creates payouts. Drafts payment orders from invoice extraction, CSV imports, or manual entry. Submits proposals into the approval flow. *They are the heaviest day-to-day user.*
- **Approver / voter** — Squads member with `vote` permission. Reviews pending proposals and signs off (or doesn't). May or may not be the same person as the initiator.
- **Executor** — Squads member with `execute` permission. Lands approved proposals on-chain. Often automated or co-located with the approver in practice.
- **Org admin** — manages members, invites, treasury creation, Squads configuration changes. Can be the same as initiator.

The team-shaped surface is what makes Decimal *not* a single-user tool. The multisig and proposal flow is the entire point — it exists *because* finance ops at a real company requires more than one person on the loop.

### Target customer (per original thesis)

Teams that already have:
- USDC treasury on Solana
- Squads multisig (or willingness to use Squads)
- Global contractors / vendors
- Invoices arriving in Gmail / Slack / Drive / Notion / PDF
- Manual payment operations today
- No mature in-house finance team

Best early users named in the original plan:
- Solana hackathon teams
- Small protocols
- Solana agencies
- Stablecoin / payment startups
- Infra / tooling teams
- DAOs with recurring contributors

Explicitly avoided as early users:
- Non-crypto businesses (need banking education)
- Companies needing payroll compliance
- Companies needing ACH / wire / SEPA on day one
- Enterprises requiring SOC2, ERP depth, procurement portals, or legal review

---

## 3. Tech stack

| Layer | Choice |
|---|---|
| Frontend | React + Vite, deployed on Vercel as an SPA |
| Backend | Node.js + TypeScript (Fastify-style API), deployed locally and tunneled to prod via Cloudflare |
| Database | PostgreSQL 15+ in Docker (single shared instance across prod-mainnet, prod-devnet, local) |
| Auth | Email + password, Google OAuth 2.0, session tokens |
| Wallet provider | Privy embedded wallets for Solana signing |
| Email | Resend (transactional outbound) |
| AI | OpenRouter (free tier) for doc-to-proposal invoice extraction |
| Solana | `@solana/web3.js`, Squads v4 SDK, USDC SPL token |
| Treasury provider (additive) | Squads Grid SDK (Phase 1 backend wired, sandbox key pending) |
| Network | Toggle between `mainnet` and `devnet` via `SOLANA_NETWORK` env |
| Observability | Manual logs; no APM in place |

Hosting model: SPA on Vercel + API on the founder's laptop tunneled to `api.decimal.finance` via Cloudflare. No cloud bill. Postgres + ClickHouse run in local Docker.

The Yellowstone worker (a gRPC chain-data indexer using ClickHouse) was retired from the core product runtime. Code remains in the repo for possible future use, but it is not assumed by the main payment workflow.

---

## 4. Data model

Source: `postgres/init/001-control-plane.sql`. Tables grouped by concern:

### Identity & access
- `users` — email + Google subject, verification, password hash
- `organizations` — the team unit
- `organization_memberships` — user × org, with `role` (admin / member)
- `organization_invites` — email-bound invite tokens
- `auth_sessions` — session tokens
- `idempotency_records` — request idempotency for write endpoints

### Wallets
- `user_wallets` — personal signing wallets (Privy-backed embedded, or external)
- `wallet_challenges` — sign-a-nonce ownership proofs for external wallets
- `treasury_wallets` — organization-owned wallets. Carries `source` (`manual`, `squads`, or `grid`), `address` (vault PDA for Squads), `usdc_ata_address`, and `properties_json` for provider-specific metadata
- `organization_wallet_authorizations` — explicit bridge linking personal wallets to treasury wallets with a role (signer / approver / etc.)

### Counterparties (vendors / payees / payers — direction-agnostic)
- `counterparties` — display name + category (vendor / customer / etc.)
- `counterparty_wallets` — labeled Solana wallets with a `trust_state` (trusted / unreviewed / restricted / blocked). One wallet per row; the same wallet can be used as both a destination and a collection source

### Payment inputs (intake)
- `payment_requests` — incoming requests for the team to pay (manual entry, CSV import, or invoice extraction)
- `payment_orders` — promoted, payable rows with `state` (draft → submitted → approved → ...)
- `payment_runs` — a batch container; one run holds many `payment_orders`
- `transfer_requests` — the lowest-level intent: "send N USDC from treasury X to counterparty wallet Y"
- `transfer_request_events`, `transfer_request_notes` — full event log per transfer

### Execution
- `execution_records` — submission state per transfer
- `decimal_proposals` — generic proposal surface. Carries `provider` (`squads_v4`), `proposal_type` (`config_transaction` / `vault_transaction`), `semantic_type` (`add_member` / `change_threshold` / `send_payment`), Squads PDAs, signatures, and the original intent JSON. Links to `payment_order_id` and `payment_run_id` so a single vault proposal can settle N transfers
- `payment_order_events` — full event log per payment order

### Collections (A/R — the inbound mirror of payments)
- `collection_requests` — expected inbound payments
- `collection_runs` — batched expected inbounds
- `collection_request_events`

Note: collections exists at the data layer but is not the wedge today. It was unified with the destination model into `counterparty_wallets` (commit `5143b0b`), so the same address book serves both directions.

### Cross-cutting
- `organization_id` is the tenant key on every operational table. Strict org-scoped queries everywhere.
- `external_reference` / `invoice_number` carry the bookkeeper-relevant identifiers.
- `metadata_json` / `properties_json` are flexible side-channels on most tables for provider-specific fields.

---

## 5. Implemented features — backend

### Auth
- Email + password registration (with Resend-delivered verification codes; dev fallback returns the code in the response)
- Google OAuth 2.0 sign-in
- Session cookie auth on every protected route
- Email verification + resend
- Logout

### Organizations & membership
- Create organization (becomes admin)
- List organizations for current user
- Organization summary (lightweight counts for shell navigation)
- List members
- Invite-only joining: organization invites are email-bound, single-use, token-hashed in DB. Direct `POST /organizations/:id/join` is deprecated and returns a forbidden response — joining requires an invite token
- Create invite (admin only), revoke invite, accept invite, preview invite (public route via token)

### Personal (signing) wallets
- List personal wallets for current user
- Connect external wallet (sign-a-challenge flow with nonce hash)
- Register embedded wallet metadata
- Create managed Privy embedded wallet (the API creates a new Privy Solana wallet for the user)
- Delete a Privy embedded wallet (archives the local record)
- Sign a Squads v4 versioned transaction with a Privy-backed personal wallet (server-side signing for embedded wallets)

### Wallet authorizations
- List, create, revoke. Explicit linkage between a personal wallet and a treasury wallet with a role (`owner` / `admin` / `signer` / `approver`)

### Treasury wallets — generic
- List treasury wallets for an org
- List treasury wallets with live SOL + USDC balances pulled from RPC
- Manually add an existing treasury address (`source = 'manual'`)
- Update treasury wallet (display name, notes)

### Treasury wallets — Squads v4 (the main flow)
- **Create Squads treasury intent** — backend prepares a signable v4 multisig creation transaction. Returns serialized transaction for the client to sign with the creator's Privy wallet
- **Confirm Squads treasury** — verifies the on-chain Squads multisig creation, derives the vault PDA, persists the vault PDA as the treasury wallet address with the multisig PDA stored as metadata
- **Squads treasury detail** — full viewer payload including on-chain config (threshold, members, transaction index) joined with local member linkage
- **Squads treasury status** — live multisig status
- **Sync members** — pulls the on-chain member list and reconciles with `organization_wallet_authorizations`

### Treasury wallets — Squads Grid (additive, sandbox-pending)
- **Create Grid signers account** — calls Grid SDK with policy spec (signers + permissions + threshold + timelock), persists the resulting account as a `treasury_wallets` row with `source = 'grid'` and metadata in `properties_json.grid`
- **Grid status** — live account state from Grid
- **Grid balances** — live balances from Grid
- All Grid routes 404 cleanly if a treasury wasn't created via Grid

### Squads config proposals (member management)
- List config proposals across an entire org (every treasury the user is a member of) — supports the "Proposals" page
- List config proposals for one treasury
- Get one config proposal (gated to actual on-chain Squads members)
- Create add-member proposal intent — returns signable transaction
- Create change-threshold proposal intent
- Approve config proposal intent (vote)
- Execute config proposal intent (land it on-chain)

### Squads vault proposals (payment proposals)
- **Single payment proposal** — wraps one `payment_order` in a Squads vault proposal
- **Payment run proposal** — wraps an entire `payment_run` (N payment orders) in **one** Squads vault transaction with N USDC transfer instructions. This is the batch-payouts feature, and it's a single signed transaction, not N separate ones
- After client-side signing + submission, the API confirms via Solana RPC (Yellowstone is no longer in this path)

### Decimal proposals (the generic proposal surface)
- List org-wide proposals (mixes config + vault)
- Get one proposal with live Squads voting state when on-chain data is available
- Confirm submission signature (client tells API the proposal was submitted)
- Confirm execution signature
- Approve / reject / execute intent endpoints (delegate to the underlying Squads flow)

### Payment inputs
- Payment requests: create, import from CSV, preview CSV, get one, promote to payment order, cancel
- Payment orders: list, create, get, update, submit, cancel
- Payment runs: list, get, delete, cancel, close (when fully settled)
- **Import payment run from CSV** — bulk import preserving unreviewed counterparties
- **Import payment run from document (PDF / image)** — the AI doc-to-proposal pipeline. Hits OpenRouter, extracts structured payment rows page-by-page, auto-creates unreviewed counterparties, returns a draft payment run. Wallet addresses are extracted when present
- Prepare payment order execution (signer-ready Solana transfer packet)
- Attach payment order / payment run signature

### Counterparties
- List counterparties + counterparty wallets
- Create / update counterparties + wallets
- `trust_state` gates whether transfers actually execute (`trusted` is the green path; `unreviewed` requires manual review before payment)

### Collections (A/R — present but de-emphasized)
- List, create, preview-csv-import, get, cancel
- Collection runs: same pattern as payment runs

### Proof / export (per individual or batch)
- `GET /payment-orders/:id/proof` — JSON proof for a single payment order
- `GET /payment-runs/:id/proof?detail=summary|compact|full` — proof packet for a batch
- `GET /collections/:id/proof`, `GET /collection-runs/:id/proof`
- Output: structured JSON capturing the full lifecycle (proposal, signatures, settlement)

### Ops
- `GET /audit-log` — org-scoped audit log
- `GET /ops-health` — Postgres + RPC health metrics

### System
- `GET /health`, `GET /capabilities` (machine-readable feature map), `GET /openapi.json`

---

## 6. Implemented features — frontend

### Public surface
- **Landing page** (`Landing.tsx`) — Monk-style design with pink orb, scroll-driven product demo, "Built on" marquee showing Squads / Solana / USDC / Privy logos. Refreshed multiple times during the hackathon push
- **Sign in / sign up** — email + password and Google OAuth
- **Invite accept** — public route for opening an org invite link

### Authenticated app
- **Overview / Command Center** — lands here after sign-in. Onboarding checklist that auto-hides once a multisig exists. Stats and recent activity
- **Wallets** — personal signing wallets + treasury wallets in one view
- **Treasury wallet detail** — full view of one treasury, including Squads viewer (threshold, members, on-chain state)
- **Members** — invite, list, revoke, see roles
- **Payments** — list of payment orders (single payouts)
- **Payment detail** — one payment order with full lifecycle
- **Payment run detail** — a batch payout with all its rows
- **Counterparties** — address book
- **Collections** — A/R view (de-emphasized)
- **Collection detail** + **Collection run detail**
- **Proposals** (`OrganizationProposals.tsx`) — org-wide view of every Squads proposal across every treasury the user is a member of. Filter bar with status / type / search, stats bar with counts. Has been the focus of recent UX work
- **Proposal detail** — one proposal with voting state, signers, execute / approve / reject actions

### UI primitives & polish
- `RdEmptyState` primitive with `EmptyIcon` set — used across Wallets, Counterparties, Payments, Collections, Members
- `RdPageHeader` + `RdPrimaryCard` chrome for detail pages
- `RdFilterBar` extracted from the proposals page and used on every list page
- Stats bar primitive on Proposals
- Solscan link copy buttons everywhere
- Sidebar with Profile + Sign out as static buttons (the in-app tour was ripped out)
- Live invoice import via the doc-to-proposal pipeline

### Notable UX decisions in the recent commits
- After sign-in / login / org creation, lands on Overview (not Wallets) — establishes the team-shaped mental model immediately
- Empty states across the app have explicit CTAs pointing the user to the next correct action
- The Proposals page is the org-wide rallying point — every member can see every proposal across every treasury they're a member of

---

## 7. Infrastructure & deployment

### Production runtime architecture
- **Frontend:** static SPA built with Vite, deployed to Vercel via `vercel.json` rewrites for SPA deep-link routing
- **API:** runs as a Node process on the founder's laptop via `make prod-backend` (or `make prod-backend-devnet` / `prod-backend-mainnet`)
- **Public access to API:** Cloudflare tunnel from `api.decimal.finance` to the local process
- **Database:** PostgreSQL in local Docker, same instance for mainnet / devnet / local dev — there is no `network` column on `users` or `organizations`, so the chain distinction only appears at the wallet level
- **ClickHouse:** runs in local Docker but is not in the active product path
- **Yellowstone worker:** retired from core, still in repo

### Environments
- `SOLANA_NETWORK=mainnet` or `devnet` flag controls USDC mint, Squads program, and the network advertised to the frontend via `/capabilities`
- The frontend reads the network from `/capabilities` and switches its Solscan / RPC URLs accordingly

### Operational
- `Makefile` with `infra-up`, `dev`, `prod-backend-mainnet`, `prod-backend-devnet`, `backup-db`, `list-backups`, `restore-db`, `reset-prod-data`
- `db-queries.txt` at repo root holds a comprehensive set of Postgres queries for inspecting users / orgs / wallets / treasuries / proposals across environments

---

## 8. The direction taken — chronological arc

Early Decimal (then Axoria) was conceived as a chain-data indexer + reconciliation product. The arc since has been: drop the indexing wedge, focus on Squads-backed team treasury operations, layer AI on top of invoice intake, then double down on multisig UX and proposals as the centerpiece. Approximate timeline from the git log:

### Pre-pivot (Axoria-era)
- Yellowstone gRPC indexer + ClickHouse for chain analytics
- Reconciliation-first thesis
- Initial frontend was reconciliation/indexing-flavored

### Pivot 1 — Squads-first product
- Yellowstone retired from core runtime (`rpc-confirmation-and-squads-lifecycle-handoff.md`, now deleted)
- Lifecycle simplified to Squads' 5-stage shape (`745f468 Collapse single + batch lifecycle rails to the Squads 5-stage shape`)
- Direct-sign batch flow dropped; runs route through Squads multisig only (`8dd63ad`)
- Settlement confirmation moved to direct Solana RPC

### Pivot 2 — Brand + positioning
- Renamed from Axoria to Decimal
- Landing page rebuilt in Monk style with pink orb + scroll demo (`e3c95c9 Rebuild landing page in Monk style with pink orb and scroll-driven demo`)
- Brand colors / fonts / logo refreshed (Bricolage Grotesque + Geist, pink `#ff3d8a`)
- Decimal favicon, pink n-arch sidebar logo, real Squads / Solana / USDC / Privy SVGs

### Pivot 3 — Invite-only org model
- Direct `POST /organizations/:id/join` deprecated
- Email-bound invite tokens become the only path into an organization (closes a multi-tenancy hole and matches enterprise expectations)

### Pivot 4 — Address book unification
- `Destination` (outbound) and `CollectionSource` (inbound) collapsed into a single `CounterpartyWallet` entity (`5143b0b`)
- Removes a direction-coupled model that was making the address book harder to use
- Cleanup pass removed all dead code (`3c9b6f4 Frontend dead-code cleanup post address-book unification`)

### Pivot 5 — AI invoice intake
- Spike: invoice PDF → structured payment rows via OpenRouter (`bf8ad5b`)
- Wired into the product (`c310694`)
- CSV's auto-create-unreviewed flow mirrored for doc imports (`8ccdb28`)
- Iterations on multi-page PDFs, page markers, max_tokens, missed-pages debugging
- Result: the team can upload an invoice and get a draft proposal in seconds

### Pivot 6 — Voting hygiene
- Auto-approve dropped from proposal creation (`remove-auto-approve-handoff.md`, since deleted) — every voter, including the proposer, casts their vote as a separate, deliberate action
- Rationale: in a 2-of-2 with auto-approve, the proposer's vote happens invisibly. Removing it keeps the proposal in `Active` longer and gives the proposer a moment to reconsider before signing

### Pivot 7 — Proposals as the rallying surface
- Org-wide proposals page added (across every treasury a member belongs to)
- `RdFilterBar` extracted and used on every list page
- Stats bar + search added to Proposals
- Inline approve / cancel controls on batch run rows

### Hackathon push (Colosseum Frontier)
- Pitch deck (`deliverables/pitch-deck/`) — 9 slides, brand-consistent, print-to-PDF support
- Remotion product demo video — friction hook, brand intro, onboarding, AI invoice extraction, multi-sig approval, outro. 53-second runtime with ElevenLabs voiceover + background music
- Submitted to Colosseum Frontier in the last 7 seconds of the deadline
- Removed inaccurate "100% Self-custodial" marketing claim from landing
- Removed "$0.0008 Avg fee per payout" claim (swapped for "AI · Invoice extraction")

### Most recent (post-hackathon, current)
- **Grid integration Phase 1 backend wired** — `@sqds/grid` SDK installed, three endpoints under `/treasury-wallets/grid/*`, `source = 'grid'` discriminator on `treasury_wallets`. Sandbox key pending (Carlos DM sent)
- **Outputs folder cleanup** — nine shipped handoff specs deleted
- **Runtime contract refreshed** — `outputs/production-env-contract.md` brought current with the actual `api/.env.example` (Privy, Resend, OpenRouter, Grid, SOLANA_NETWORK), Yellowstone references dropped
- **Feature catalog and AP-intake spec written** for grant planning

---

## 9. What's in flight right now

- **Grid Phase 1 → Phase 2 transition.** Phase 1 (account create / status / balances) is shipped and unblocked locally. Phase 2 (managed account operations, spending limits, standing orders) waits on Grid sandbox API key access. Carlos DM sent.
- **Grant application prep** for Solana Foundation India. Feature catalog written. AP intake + counterparty / vendor intelligence specs written. QuickBooks integration spec pending the research that just landed.
- **Open architectural questions** captured in `feature-spec-ap-intake.md` under each section.

---

## 10. What's deliberately not built

Recorded so it's not re-litigated:

- **Fiat rails** (ACH / wire / SEPA / on-ramp / off-ramp). USDC-only.
- **Cards.** Not in scope.
- **Payroll compliance.** Not in scope.
- **Full accounting system.** QuickBooks integration is on the roadmap; building a competing GL is not.
- **Autonomous payments.** AI never auto-pays. All payouts pass through human approval and multisig.
- **Multi-chain.** Solana-only until PMF.
- **Cash flow / treasury insight dashboard, copilot, conversational layer.** Cut from grant scope.
- **Onboarding wizard as a marketing feature.** UX investment, not a sold feature.
- **Webhook / public API surface for third-party integrations.** No customers asking for it yet.
- **Recurring billing / subscription extraction.** Different product wedge; depended on contract extraction which is also cut.
- **Contract extraction.** Monk's core; deep compliance / legal expertise required; weak alignment with payouts wedge.
- **A/R / collections as a wedge.** Data model exists (`collection_requests`, `collection_runs`) but the product is A/P-focused.
- **Vendor risk scoring + sanctions screening.** No external reputation data, no compliance ownership.
- **Audit packet export as a sold feature.** Falls out of clean reconciliation; treated as expected hygiene, not a flex.

---

## 11. What sits next to Decimal (the gravity)

Decimal's unique surface area, when stacked against incumbents, comes from:

- **Multisig as the choke point.** Every outflow passes through Squads. This is a *structural* property of the product — no traditional fintech has this gate.
- **On-chain settlement evidence.** Every payment has a public, verifiable signature. Audit trail is automatic at the protocol layer.
- **Wallet address as the canonical vendor identifier.** Counterparty deduplication and BEC detection benefit directly. Traditional fintech doesn't have this signal.
- **AI invoice extraction wired all the way through to multisig proposals.** Upload a PDF, get a signed-by-the-team payout. Most incumbents stop at "extracted data in a UI."
- **Team-first from the data model up.** Organizations, memberships, invites, signer roles, voting permissions, proposal voting — none of this is bolted on. The product literally cannot operate as a single user.

These are the levers a competitor (Bill.com / Ramp / Brex / Mercury) can't easily copy without rebuilding their custody and approval primitives.

---

## 12. Useful reference points in the repo

- `product_direction.md` — the original MVP plan (2026-05-05)
- `system_explained/` — older docs explaining the system at a snapshot
- `outputs/grid-integration-plan.md` — current Grid phasing
- `outputs/decimal-feature-catalog.md` — full feature survey from competitor research
- `outputs/feature-spec-ap-intake.md` — detailed specs for §1, §2 + cut decisions for §3-§11
- `outputs/quickbooks-research.md` — QuickBooks integration research brief
- `outputs/production-env-contract.md` — current runtime env contract
- `db-queries.txt` — query reference for inspecting any environment
- `api/src/api-contract.ts` — authoritative list of every API endpoint
- `postgres/init/001-control-plane.sql` — authoritative data model
