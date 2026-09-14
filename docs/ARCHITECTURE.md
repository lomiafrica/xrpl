# Architecture

Custodial hop only. One operator omnibus signs. Merchants never hold XRPL keys.

```
Wave / MTN / card / bank  ->  lomi. ledger  ->  XRPL tagged Payment  ->  last mile (Wave / MTN / SPI)
```

1. Merchant payout exists in the internal ledger (`payout_id` UUID).
2. Omnibus submits a Payment to the merchant receive account.
3. `DestinationTag` is a uint32 derived from sha256(`payout_id`).
4. MemoData carries the full UUID so reconcile can join exactly.
5. Last mile is still local rails. XRPL is the correspondent hop, not a customer checkout.

This lab stops at step 4 on Testnet. Next in this repo: payout-shaped HTTP (`POST /payouts` analogue), last-mile stubs, then a later private-API wire if the hop is real.
