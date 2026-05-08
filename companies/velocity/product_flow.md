# Velocity - Product Flow

Date: 2026-05-07

## Flow 1: Customer onboarding

1. Business applies to Velocity.
2. Velocity collects KYB/KYC, ownership, risk, and compliance information.
3. Compliance reviews the business.
4. Approved customer gets portal/API access.
5. Customer creates API keys and starts integration.

Evidence: docs landing says customers create a Velocity account, complete onboarding, and once approved access the dashboard and APIs. Job listings emphasize KYC, EDD, UBO analysis, and transaction monitoring.

## Flow 2: Create wallets and accounts

1. Customer creates stablecoin wallets.
2. Customer links or creates bank/payment endpoints.
3. Velocity records these as account/wallet objects.
4. Compliance and custody policies attach to those objects.

Evidence: docs landing lists "Create wallets", "Add beneficiary wallets", and transfer flows. Homepage sample includes `wallet_id` and `bank_account_id`.

## Flow 3: Make a transfer

1. Customer chooses source: wallet or bank account.
2. Customer chooses destination: wallet, bank account, or beneficiary.
3. Customer requests quote.
4. Velocity prices the route.
5. Customer confirms.
6. Velocity executes using stablecoin and/or fiat rails.
7. Customer receives status and reporting.

Evidence: docs landing lists "Make a Transfer" and homepage sample quote endpoint.

## Flow 4: Stablecoin-to-fiat route

Example: pay EUR from USDC.

1. Customer holds USDC balance.
2. Customer requests `USDC-EUR` quote.
3. Velocity routes through liquidity/FX partners.
4. Stablecoin leg settles on-chain or within custody network.
5. Fiat leg pays out through bank/payment partner.
6. Velocity updates ledger and audit records.

Evidence: homepage sample uses `currency_pair: USDC-EUR`, `side: BUY`, `wallet_id`, and `bank_account_id`.

## Flow 5: Fiat-to-stablecoin route

Example: receive customer funds and get funded in stables.

1. Customer receives fiat through a bank/payment partner.
2. Velocity converts or settles into stablecoin balance.
3. Stablecoin balance becomes usable for treasury, settlement, or payouts.

Evidence: homepage mentions "Get funded in stables", "Fiat transfers powered by stables", and stablecoin payment accounts.

## Flow 6: Treasury and reporting

1. Customer sees balances across fiat/stablecoins.
2. Customer moves liquidity where needed.
3. Customer applies approval/policy controls.
4. Data syncs to TMS/ERP.
5. Finance team reconciles from one operating layer.

Evidence: homepage mentions TMS/ERP integrations, unified payments/balances/liquidity, programmatic payments, and reporting/controls.

## Flow 7: Compliance and monitoring

1. Customer and beneficiary are screened.
2. Transfer is checked against risk policies.
3. Crypto/fiat transactions are monitored.
4. Suspicious activity is investigated/escalated.
5. Travel Rule requirements are handled where applicable.

Evidence: docs include Travel Rule; job listings mention crypto and fiat transaction monitoring, KYC/EDD, suspicious activity escalation, Chainalysis, Sumsub, and Notabene.

## The product in one sentence

Velocity lets an enterprise finance team treat stablecoin rails like a controlled, compliant, API-accessible treasury network instead of a crypto wallet.
