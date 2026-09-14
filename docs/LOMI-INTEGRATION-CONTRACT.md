# lomi. payout mapping (XRPL lab)

Isolated XRPL Testnet only. No live API, no merchant keys, no XRP on merchant `accounts`.

| Lab | Production analogue |
| --- | --- |
| Omnibus classic account | Custodial treasury |
| Merchant classic account | Internal receive address |
| Payment 10 XRP | Correspondent hop |
| `DestinationTag` from sha256(payout_id) | Numeric filter on the Payment |
| MemoType `payout_id` / MemoData UUID | Exact payout join |
| `data/testnet-proof.json` | Future webhook `xrpl_transaction_id` |
| Mock last mile | Wave / MTN / SPI |

There is no `rail: 'xrpl'` on the live API.
