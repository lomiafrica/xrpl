# xrpl

Testnet lab from [lomi.](https://lomi.africa) for a tagged XRPL Payment.

lomi.africa S.A.R.L. (Abidjan) builds payment infrastructure:

- **lomi.** ([lomi.africa](https://lomi.africa)): live PSP for francophone West Africa. Merchants collect XOF over Wave, MTN, cards, and bank rails.
- **Rill** ([userill.com](https://userill.com)): agent payment control plane. Humans fund; agents pay APIs that accept MPP and x402.

This repo is the XRP Ledger correspondent hop: custodial omnibus, `DestinationTag` plus memo = `payout_id`, last mile stays Wave / MTN / SPI. Merchants never hold keys. We do not issue a token. We do not run a crypto checkout.

It is a standalone lab. It is not wired to live payouts.

**Payout mapping:** [docs/LOMI-INTEGRATION-CONTRACT.md](./docs/LOMI-INTEGRATION-CONTRACT.md)  
**Shape:** [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md)

## What is in here

- XRPL Testnet faucet bootstrap for an omnibus account and a merchant receive account
- Omnibus to merchant Payment of 10 XRP with `DestinationTag` from the payout id and MemoData = the payout UUID
- Reconcile helper that prints explorer links from `data/testnet-proof.json`

Not in this repo yet: payout-shaped HTTP, last-mile adapters, HSM / KMS, or mainnet keys. Those come next in this same repo.

## Setup

```bash
pnpm install
cp .env.example .env
pnpm bootstrap
pnpm settle
pnpm proof
```

Bootstrap uses the XRPL Testnet faucet (`https://faucet.altnet.rippletest.net/accounts`). Settle submits 10 XRP omnibus to merchant with `DestinationTag` = first 32 bits of sha256(`payout_id`) and MemoData = the UUID.

Explorer: [testnet.xrpl.org](https://testnet.xrpl.org)

Current testnet accounts:

- Omnibus: `rGXEzo42vrv2skGp9KkJS4mr3u4APqSkha`
- Merchant: `rJSZYQmB7KFryR5Xs3wXV38KYnNnyX3FGN`

Settled hop: [8DD8D6B11B8E8E35176CF587764647DE825CD14D10D0FFD6B626745ACC853D4F](https://testnet.xrpl.org/transactions/8DD8D6B11B8E8E35176CF587764647DE825CD14D10D0FFD6B626745ACC853D4F)

Do not send mainnet XRP to these addresses.

## Checks

```bash
pnpm typecheck
pnpm test
```

## Local data (gitignored)

| Path | Purpose |
| --- | --- |
| `keys/` | Testnet signing keys (never commit) |
| `.env` | Same secrets as `keys/` |

Committed public addresses and explorer tx ids (no secrets): `data/testnet-proof.json`.

## License

MIT. See [LICENSE](./LICENSE).
