# Crypto Wallets

The common crypto-wallet vocabulary -- the wallets that hold digital assets, the addresses that receive them, the balances held, the transactions and transfers that move them and the tokens they hold -- distilled from the APIs that already exist. Market prices belong to the market-data context and orders to trading. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Wallets, Digital Assets, Stablecoins, Custody, Crypto, Cryptocurrency, Crypto Wallet, Wallet Infrastructure in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| wallet | 75 | 70 | id 51% | wallets 44, wallet 31, vaults 12, accounts 1 |
| wallet_address | 7 | 6 | address 100%, chain 50%, format 50%, id 50% | addresses 5, deposit_addresses 1, deposit-addresses 1 |
| wallet_balance | 17 | 14 | asset 50%, total 50% | balances 10, balance 7 |
| wallet_transaction | 54 | 52 | status 67%, id 64%, direction 60%, tx_hash 54% | transactions 41, transfers 19, transfer 14, transaction 10 |
| token | 27 | 22 | symbol 64%, name 59% | tokens 17, token 15, assets 3, supported_assets 1 |

Cohort: 345 providers with harvested OpenAPI, 75 crosswalks. Of the providers exposing a wallet: 52% create, 76% list, 45% fetch, 11% update, 5% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A wallet transaction agrees on id, status, direction and the transaction hash -- the hash is the one identifier every crypto API shares, because the chain assigns it.
- A wallet agrees only on an id: custodians, MPC wallet platforms and exchanges each model the wallet as a vault, an account or a key set.
- A token agrees on its symbol and name; contract address and decimals sit just below core.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Blockchain and Web3 are not cohort tags: they cover node, RPC and chain-data infrastructure more than wallets.
- A wallet covers vaults and vault accounts in custody platforms, but not DeFi yield or staking vaults, which are investment products.
- Wallet balances and transactions are `/wallets/{wallet_id}/balances` and `/wallet-transactions`: banking owns the bare words.
- Deposits, withdrawals and transfers are wallet transactions, told apart by `direction`.
- Duplicates merged: Seshat, LootRush, M0, Massive into Polygon, Mesh, MyStars.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
