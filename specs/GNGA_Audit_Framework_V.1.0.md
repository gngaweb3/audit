# GNGA.WEB3 Protocol — Audit Framework Specification

**Protocol Version:** 1.0
**Catalog Version:** 2026.02
**Schema Version:** 1.2
**Status:** Fully Auditable

---

Public documentation describing the event framework used by the protocol. This specification defines how actors, subjects, domains, actions, and events are represented, published, and interpreted within the protocol's immutable audit history.

**Documentation Status: v1.0 — Sealed**

This version defines the initial audit framework used to interpret protocol events. The specification is publicly accessible, immutable, and remains permanently available as a historical reference. Future versions may extend the framework, but they do not modify the meaning or integrity of events already published under this version.

---

## 01 · Introduction

This document defines the audit and transparency framework of the protocol. Its purpose is to provide a clear, verifiable, and immutable record of all relevant actions performed throughout the lifecycle of the protocol.

The system is designed around events. Every meaningful action is recorded as an event and published in a chronological sequence. Events are never modified or deleted once published.

This documentation explains the language, rules, and structure used to describe actors, subjects, and events, so that any observer can independently understand and verify what happened, when it happened, and who authorized it.

## 02 · Core Principles

- One protocol = one Topic
- One event = one actor
- One event = one subject
- The protocol has no privileged owner
- SYSTEM executes the rules
- The history defines the truth

> On-chain, truth is published. Off-chain, interpretation is published. Rules can live off-chain; the hash of the rules can live on-chain; the event always lives on-chain.

## 03 · Event Language

Every event follows a simple, fixed format:

```
DOMAIN.ACTION
```

Examples:

```
VAULT.CREATED
TOKEN.VERIFIED
TREASURY.MOVED
```

## 04 · Domain Catalog (v1.0)

The logical areas of the protocol:

`PROTOCOL` · `ASSET` · `TOKEN` · `VAULT` · `TREASURY` · `AUDIT` · `GOVERNANCE` · `DOCUMENT`

## 05 · Action Catalog (v1.0)

Universal actions, reusable across any domain:

`CREATED` · `UPDATED` · `CONFIGURED` · `VERIFIED` · `APPROVED` · `REVOKED` · `PROPOSED` · `MOVED` · `LINKED` · `UNLINKED` · `MINTED` · `BURNED` · `UPLOADED` · `ATTACHED` · `STARTED` · `COMPLETED` · `EXECUTED` · `SEALED`

## 06 · Actor Type Catalog (v1.0)

Defines who originates an event — not permissions, not ownership:

`SYSTEM` · `ADMIN` · `MULTISIG` · `DAO` · `USER`

Usage inside an event:

```json
"actor": {
  "type": "SYSTEM",
  "id": "protocol_core"
}
```

## 07 · Subject Type Catalog (v1.0)

Subject types define the category of entity that receives events throughout its lifecycle.

`VAULT_MASTER` · `VAULT` · `TOKEN` · `ASSET` · `TREASURY` · `AUDIT_RECORD` · `DOCUMENT`

> Subject types may evolve across protocol versions. Events remain immutable regardless of future subject classifications.

## 08 · Subject Rules (v1.0)

A subject is any persistent entity that can receive events and evolve over time — a vault, a token, an asset, a document.

- Subjects do not exist before events
- A subject is created by its first DOMAIN.CREATED event
- The first event assigns an immutable subject.id
- subject.type + subject.id must be globally unique
- Subjects have no ownership
- A subject cannot be deleted, only archived
- A subject may reach a final immutable state depending on its lifecycle

Subject IDs are generated automatically by SYSTEM, never by humans:

```
<subject_type>-<short_hash>

vault-7f3a9c
token-b91d02
asset-4caa11
```

> DOCUMENT subjects may reach a final immutable state through a DOCUMENT.SEALED event.

## 09 · JSON Base Event Structure (v1.0)

The only accepted format to write an event:

```json
{
  "version": "1.0",
  "event_type": "DOMAIN.ACTION",
  "timestamp": "ISO-8601",

  "subject": {
    "type": "SUBJECT_TYPE",
    "id": "subject_id"
  },

  "actor": {
    "type": "ACTOR_TYPE",
    "id": "actor_id"
  },

  "data": {},
  "refs": {},
  "hash": "sha256:..."
}
```

## 10 · Versioning

**Events never change. The rules around them can evolve.**

What is **NOT** versioned (immutable, sealed history):

`Event ID` · `Timestamp` · `Subject ID` · `Actor ID` · `Original payload` · `Topic`

What **IS** versioned:

`Event schema` · `Subject rules` · `Subject types` · `Event catalog` · `UI interpretation` · `Indexing logic`

---

*GNGA.WEB3 Protocol — Audit Framework Specification — v1.0*
