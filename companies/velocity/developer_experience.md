# Velocity - Developer Experience

Date: 2026-05-07

## Public developer surface

Velocity has a developer posture, but it is gated.

Publicly visible:

- Docs landing page at `velocity.xyz/velocity-docs`.
- API topics: onboarding, API keys, fees, Travel Rule, beneficiary wallets, wallet creation, transfers, beneficiaries.
- API/portal domains referenced in Trust Centre: `api.velocity.xyz` and `portal.velocity.xyz`.
- Homepage sample `transfers/quote` request with bearer auth.

Not publicly visible:

- Full API reference.
- Sandbox instructions.
- Auth details.
- Webhook payloads.
- SDKs.
- Rate limits.
- Error model.
- Pricing.
- Supported countries/currencies/networks.

Docs pages redirect to a password page, so developer experience cannot be audited deeply without access.

Sources: [docs landing](https://www.velocity.xyz/velocity-docs), [password-protected docs page](https://docs.velocity.xyz/docs/getting-started), [homepage](https://www.velocity.xyz/), [Trust Centre](https://trust.velocity.xyz/).

## API shape inferred from public pages

Visible concepts:

- `entity_id`
- `wallet_id`
- `bank_account_id`
- `currency_pair`
- quote creation
- transfers
- wallets
- beneficiaries
- fees and charges
- Travel Rule

This implies a standard fintech API model:

1. Create/approve business entity.
2. Create wallets or bank endpoints.
3. Create beneficiaries.
4. Request quote.
5. Create transfer.
6. Monitor transaction status.
7. Receive webhooks.
8. Reconcile through portal/API exports.

## Developer maturity score

Score: 5/10 publicly, likely higher privately.

Why not higher:

- Docs are gated.
- No self-serve sandbox visible.
- No public OpenAPI spec found.
- No SDKs found.
- No pricing visible.
- No public integration examples beyond one quote snippet.

Why not lower:

- They clearly have an API-first product story.
- They expose concrete objects and endpoints.
- Trust Centre references `api.velocity.xyz`.
- Enterprise customer posture makes gated docs normal.

## Compare to Bridge, BVNK, Altitude/Grid

- Bridge: clearer public docs and API surface.
- BVNK: mature payments API posture, enterprise sales led.
- Altitude/Grid: public API spec and Solana-native smart account primitives.
- Velocity: more gated, but potentially broader enterprise treasury scope.

## What we can learn

For our product, public developer experience can be a wedge. If we build anything API-driven, we should have:

- Public docs.
- OpenAPI spec.
- Sandbox.
- Webhooks.
- Idempotency.
- Clear object model.
- Runnable examples.
- Test credentials or demo mode.

Velocity may win enterprise relationships, but a clearer public developer experience can help us win builders and early adopters.
