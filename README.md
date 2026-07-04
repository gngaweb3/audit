# audit

Public specifications for the GNGA.WEB3 Protocol's audit and document certification system.

This repository contains the **sealed, canonical versions** of the specifications that define how the protocol records events and certifies documents. Both specs are cryptographically sealed on Hedera — the copies in this repo are byte-identical to the files that were hashed and pinned at the moment of sealing.

## What's in this repo

| Spec | What it defines |
|---|---|
| [`specs/audit-framework-v1.0.md`](./specs/audit-framework-v1.0.md) | The event system: how actors, subjects, domains, and actions are represented and published as immutable events on Hedera Consensus Service |
| [`specs/document-seals-v1.0.md`](./specs/document-seals-v1.0.md) | How individual documents (Whitepaper, Lite Paper, policies) are certified — hashed, pinned to IPFS, and sealed as a specific type of event under the framework above |

Document Seals is a specific application of the broader Audit Framework: every `DOCUMENT.SEALED` event follows the general event structure defined in the Audit Framework, with a document-specific payload (a SealRecord) defined in Document Seals.

## These files are not editable references

Both specs reached `SEALED` status under their own rules: once sealed, a document version is never modified — any change becomes a new version, sealed independently. **Do not reformat, correct typos in, or re-save these files.** Their published SHA-256 hash was calculated against the exact bytes in this repo; altering them, even cosmetically, breaks independent verification.

## How to verify these documents yourself

1. Download the spec file from this repo.
2. Calculate its SHA-256 hash.
3. Compare it against the sealed hash on [Document Seals](https://gnga.tech/document-seals).
4. Cross-check the corresponding `DOCUMENT.SEALED` event on the protocol's Hedera audit topic: [`0.0.10603515`](https://hashscan.io/mainnet/topic/0.0.10603515) via HashScan.

If all three match, the document in this repo is provably the exact version that was officially sealed.

## Where this fits

| Resource | What it is |
|---|---|
| [gnga.tech/audit](https://gnga.tech/audit) | Live Audit Framework — browse every sealed event in real time |
| [gnga.tech/document-seals](https://gnga.tech/document-seals) | Live Document Seals — browse every sealed document and its hash |
| [Hedera Topic `0.0.10603515`](https://hashscan.io/mainnet/topic/0.0.10603515) | The raw, immutable event ledger both pages read from |
| [`gngaweb3/the-vault`](https://github.com/gngaweb3/the-vault) | On-chain transparency layer for The Vault's backing assets |

## License

Released under the [MIT License](./LICENSE).

---

*GNGA.WEB3 Protocol*
