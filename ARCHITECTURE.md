# architecture // the machine without the keys

ONE4ALL runs on a lean event graph. Public facts enter through allowlisted
readers. Plain code checks identity, freshness, duplicates, policy and limits
before a model ever sees an event, and Omni only writes about what survived.

```text
Solana / RevShare / site event
               │
               ▼
            watcher
   parse · dedupe · timestamp
               │
               ▼
      deterministic policy
      ╱        │        ╲
  ignore     stage     escalate to owner
               │
               ▼
             OMNI
   writes the words, reasoning shown
               │
               ▼
           verifier
   facts · limits · duplicate check
               │
               ▼
  public post / chat answer / receipt
               │
               ▼
         durable audit
```

## public signal contract

This is a **schema example**, not a live event or transaction receipt:

```json
{
  "schema": "one4all.signal.v1",
  "id": "example_public_signal",
  "observedAt": "2026-01-01T00:00:00.000Z",
  "source": {
    "kind": "public-chain-reader",
    "network": "solana-mainnet"
  },
  "event": {
    "name": "reward.distribution.confirmed",
    "status": "verified"
  },
  "evidence": {
    "publicUrl": "https://explorer.solana.com/",
    "confirmation": "finalized"
  }
}
```

Collectors, private endpoints, prompts, deployment controls, policy internals,
databases and credentials are deliberately left out of this repository.

## why it stays lean

- Reads and policy still work when model providers are offline.
- Models write language. They never do accounting or grant permission.
- Omni runs inside a fixed monthly spending cap and posts only when something
  real changed.
- Retries keep the same idempotency key, so nothing is posted twice.
- Public outputs keep their evidence, timestamps and receipts.
- Anything risky stops at the owner.

Autonomy with a seatbelt: Omni can watch and speak without becoming a wallet.
