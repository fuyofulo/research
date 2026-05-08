# KAST - On-Chain Truth

Date: 2026-05-08

## Short verdict

KAST uses on-chain rails, but the public product is mostly a custodial app/ledger. Without official wallet addresses, USDKY/USDK token addresses, reserve attestations, or public dashboards, most company-level claims cannot be independently verified on-chain.

## What is publicly on-chain-ish

KAST publicly supports stablecoin deposits on multiple networks:

- Ethereum.
- Tron.
- Solana.
- Polygon.
- Arbitrum.
- BNB Chain.
- Stellar.
- XRP Ledger.

It supports withdrawals on fewer networks:

- Ethereum.
- Tron.
- Solana.
- Arbitrum.

Source: [supported stablecoins](https://concierge.kast.xyz/hc/en-us/articles/11784729022863-Which-Stablecoins-Are-Supported-on-the-KAST-App).

## KAST Dollar / USDKY

KAST announced a partnership with M0 to build two digital dollars on Solana. M0 said KAST would use M0 to build two digital dollars: one initially for tokenizing deposits/payments and one for savings. KAST Earn now describes USDKY as a stablecoin backed 1:1 by short-term U.S. Treasury Bill reserves, powered by M0, held in a user's Privy wallet on Solana.

Sources: [M0 announcement](https://www.m0.org/press-releases/m-0-launches-on-solana-bringing-the-first-programmable-stablecoin-infrastructure-to-one-of-cryptos-fastest-growing-ecosystem), [KAST Earn](https://www.kast.xyz/earn).

## What cannot be verified yet

Missing public data:

- USDKY token mint address.
- USDK/payment stablecoin token mint address.
- KAST treasury/reserve wallets.
- KAST omnibus deposit wallets.
- Proof of reserves for KAST Cash.
- On-chain supply of KAST-issued stablecoins.
- Wallet count attributable to KAST.
- Transaction volume attributable to KAST.
- Card volume, obviously off-chain.
- Fiat payout volume, off-chain.

## Important legal distinction

Even though KAST supports on-chain deposits, ordinary account balances are not necessarily on-chain assets owned by the user. Terms say transferred virtual assets are sold to KAST and KAST records a USD-denominated reference balance. That means on-chain deposits may disappear into KAST-controlled custody/liquidity/ledger systems.

KAST Earn is different: the Earn page says USDKY and Gauntlet vault shares are held in the user's own Privy wallet on Solana/Base.

Sources: [Terms](https://www.kast.xyz/legal/terms-and-conditions-of-service), [Earn](https://www.kast.xyz/earn).

## How to verify later

If KAST publishes token addresses or reserve dashboards:

1. Pull USDKY and USDK mint addresses.
2. Check supply on Solscan.
3. Check holder concentration.
4. Identify M0 wrapper/reserve mechanics.
5. Compare supply to KAST-reported deposits/Earn AUM.
6. Check whether transfer restrictions exist.
7. Pull largest holders and inspect whether they are KAST/Privy/user wallets.
8. Look for Wormhole/M0 cross-chain movement.
9. Compare on-chain volume to claimed app transaction volume.
10. Record reserve attestations and update this file.

## Bottom line

KAST's product uses blockchains, but KAST itself is not transparently analyzable like a DeFi protocol today. Most diligence must focus on legal terms, partner structure, ledger/reserve practices, and published support docs rather than explorer data.
