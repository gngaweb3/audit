# GNGA.WEB3 Protocol — Document Seals Specification

**Specification Version:** 1.0
**Seal Format:** SealRecord v1
**Verification:** Public
**Status:** Active

---

Cryptographic document certification and immutable publication records.

---

## 01 · Introduction

The protocol certifies documents through cryptographic proofs published as immutable events.

Documents themselves are not stored on-chain. Instead, the protocol publishes verifiable references and integrity proofs that allow anyone to independently verify authenticity, integrity, and publication history.

Document Seals provide a transparent and auditable method for certifying protocol documentation, governance records, reports, specifications, and other public resources.

## 02 · Core Principles

`Immutable` · `Verifiable` · `Hash-Based` · `Storage-Agnostic` · `Publicly Auditable`

- A seal certifies a specific document version.
- A seal never modifies a document.
- A sealed document remains verifiable indefinitely.
- Verification is independent of the issuer.
- The seal proves document integrity, not authorship.

## 03 · Document Lifecycle

Documents may progress through multiple states before becoming permanently sealed.

**States:** `DRAFT` · `BETA` · `RELEASED` · `SEALED`

**Events:** `DOCUMENT.CREATED` · `DOCUMENT.UPDATED` · `DOCUMENT.SEALED`

**Lifecycle:**

```
DRAFT
  ↓
BETA
  ↓
RELEASED
  ↓
SEALED
```

> Once a document reaches SEALED status, no further modifications are permitted under the same document version. Any subsequent revision must be published as a new document version and sealed independently.

## 04 · Seal Record Structure

The seal information is stored inside the `data` field of a `DOCUMENT.SEALED` event.

```json
{
  "document_id": "whitepaper-v1",
  "document_title": "GNGA.WEB3 Protocol — Whitepaper v1.0",
  "document_version": "1.0",

  "document_type": "whitepaper",
  "document_category": "whitepaper",

  "document_hash": "sha256:...",
  "hash_algorithm": "SHA-256",

  "storage_uri": "ipfs://...",
  "storage_type": "IPFS",

  "file_name": "whitepaper.pdf",
  "mime_type": "application/pdf",
  "file_size": 2549831,

  "previous_hash": null,

  "status": "SEALED",

  "sealed_at": "2026-06-16T12:00:00Z",

  "seal_version": "1.0"
}
```

`document_type` defines the broad category of the document (`specification`, `policy`, `whitepaper`, `marketing`). `document_category` defines the specific identifier within that category (e.g. `audit_framework`, `document_seals`, `treasury_policy`). This two-level classification allows the protocol to add new specific documents over time without ever needing to redefine the broad type catalog.

The SealRecord contains all information necessary to independently verify a document and reconstruct its publication history.

## 05 · Verification Process

Document verification follows a deterministic process:

1. Retrieve the document from its published location.
2. Calculate the document hash using the specified algorithm.
3. Compare the calculated hash with the published seal.
4. Verify the corresponding DOCUMENT.SEALED event.
5. Confirm document integrity and publication history.

> If the calculated hash matches the published hash, the document is verified.

## 06 · Storage Independence

The protocol does not store documents directly on-chain.

Documents may be stored using different storage systems:

`IPFS` · `Arweave` · `HTTPS` · `Private Storage`

Only cryptographic proofs and references are published through protocol events.

> Storage systems may evolve over time without affecting the validity of previously published seals.

## 07 · Versioning

`SealRecord v1` — Active

**Published seals never change.**

Verification methods and documentation standards may evolve through future specification updates while preserving compatibility with previously sealed documents.

> Future versions may extend the specification without altering the validity or integrity of existing seals.

---

*GNGA.WEB3 Protocol — Document Seals Specification — v1.0*
