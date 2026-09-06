# QR-V™ Documentation

## Executive Summary

- QR-V™ is registry-backed verification infrastructure that transforms QR codes from static links into verifiable, trust-aware identifiers.
- It exists to solve the core limitation of traditional QR codes: the inability to prove authenticity, issuer legitimacy, or record integrity.
- Every QR-V code resolves to a structured registry record that can be cryptographically verified in real time.
- It enables instant validation of certificates, identities, products, documents, and assets across distributed systems.
- The system introduces a global verification layer that confirms whether a record is valid, revoked, expired, or tampered with.
- QR-V replaces “scan and trust” with “scan and verify,” establishing a universal standard for QR-based trust infrastructure.
- Its core value proposition is eliminating fraud and ambiguity in QR-driven workflows through deterministic, registry-backed verification.

---

## Overview

### What is QR-V?

QR-V™ is registry-backed verification infrastructure for QR-based records, credentials, products, documents, and assets. A traditional QR code usually points to a static URL. QR-V changes that model by making the QR code point to a verifiable identifier that resolves through a registry, a verification service, and a structured response layer.

The purpose of QR-V is to answer the questions that ordinary QR codes do not answer: Is this record authentic? Who issued it? Is it still active? Has it been revoked or expired? Does the displayed information match the canonical registry record?

Under QRVP-1, a QR-V identifier functions as a verifiable reference pointer that resolves through a distributed network of verification nodes and registries. The protocol supports identity, documents, digital assets, physical products, financial instruments, and property records.

### Core concepts

The QR-V system is built around five core concepts: identifier, resolver, verification node, registry, and response.

A QR-V identifier is the encoded reference inside the QR code. The resolver determines where the identifier should be checked. The verification layer validates record status, cryptographic integrity, issuer authorization, and revocation state. The registry stores the authoritative record. The response layer returns a deterministic result to the user or application.

The QVS-1.0 standard defines QR-V as a registry-anchored verification model where a QR code contains a QR-V identifier that references a registry record instead of storing the full record directly in the QR image.

### Product scope

QR-V is not a general QR-code design tool. Its product scope is verification infrastructure.

The first production product is QR-V™ Verified Certificates. This use case demonstrates the full lifecycle: issuance, registry anchoring, QR code generation, public verification, and revocation. Certificates are the correct first implementation because they are easy to understand, commercially valuable, and technically exercise the entire QR-V system.

The broader product scope includes certificate verification, identity verification, membership verification, document authentication, product authentication, asset registration, financial record verification, property record verification, issuer portals, developer APIs, and white-label verification deployments.

---

## Protocol

### Identifier format

QRVP-1 defines the canonical identifier structure as:

```text
QRV://registry/type/objectID
```

Example:

```text
QRV://ino/member/M000000001
```

The identifier contains four core parts: the QRV scheme, the registry authority, the record type, and the object ID. QR-V identifiers may also be exposed through an HTTPS gateway such as:

```text
https://qrv.network/verify/{qrvid}
```

The HTTPS version is the public gateway for browsers and scanners. The QRV scheme is the protocol-level representation.

### Verification flow

The QR-V verification flow is deterministic:

```text
scan
→ resolve identifier
→ query verification node
→ lookup registry record
→ validate status and integrity
→ return verification result
```

QVS-1.0 defines the workflow as QR-V code issuance, registry record creation, code scan, identifier resolution, registry lookup, validation, and verification result.

A production certificate example follows the same lifecycle. An issuer creates the certificate, the system generates a QRVID, creates a cryptographic hash, stores the record in the registry, generates the QR-V code, and attaches the QR code to the certificate.

### Record states

QR-V verification states must be deterministic. The baseline states are:

```text
VERIFIED
REVOKED
EXPIRED
NOT_FOUND
INVALID_SIGNATURE
SUSPENDED_ISSUER
ERROR
```

The earlier QRVP-1 protocol materials define verified, revoked, expired, and unknown as core states, while later production specifications expand this into more precise operational states for invalid signatures, suspended issuers, and errors.

A public verification page must never return ambiguous language. It should clearly display whether the record is valid, revoked, expired, not found, or unavailable.

---

## Architecture

### Service topology

QR-V operates as a consolidated production platform under the root domain:

```text
qrv.network
```

The current production model uses two runtime boundaries:

```text
qrv.network       public platform and human-facing workflows
api.qrv.network   trusted backend, API, registry, cryptography, and audit authority
```

Historical service subdomains such as `verify.qrv.network`, `registry.qrv.network`, `issuer.qrv.network`, `docs.qrv.network`, `developers.qrv.network`, and `explorer.qrv.network` may remain as compatibility aliases, but new production routes should consolidate under `qrv.network`.

### Data flow

The data flow begins when an issuer creates a record. The issuer submits record data through the Issuer Portal. The API validates the request, creates the canonical record, generates or stores the hash and signature values, writes the record to the PostgreSQL registry, and returns a QRVID.

When a user scans the QR code, the verification page receives the QRVID, calls the API node, queries the registry, checks record status and integrity, and returns a verification response.

The documented network architecture follows this pattern:

```text
Client Scanner
→ QR-V Public Platform
→ Verification API
→ QR-V Registry
→ Verification Record
```

This architecture enables scalable verification across distributed infrastructure while keeping privileged data and cryptographic operations behind the API boundary.

### Trust boundaries

QR-V separates public, issuer, API, and registry responsibilities.

The public verifier is read-oriented. It should display deterministic verification results and public-safe metadata. The Issuer Portal is protected and allows authorized organizations to create, manage, and revoke records. The API is the controlled mutation and integration layer. The registry is the canonical source of truth.

The trust boundary is strongest at the API and registry layer. The registry stores issuer metadata, timestamps, cryptographic hashes, verification status, certificate records, and audit logs. Only authorized system services should write to this layer. Public users should verify records without receiving unauthorized private data.

---

## Registry

### Data model

The QR-V registry is the canonical datastore for verification records. QVS-1.0 identifies the core registry tables as:

```text
qr_objects
qr_hash_registry
qr_certificates
qr_issuers
qr_audit_log
```

These records form the verification ledger supporting QR-V operations.

A QR-V record should include the QRVID, record type, issuer, subject or owner, status, issued date, expiration date when applicable, hash, signature, timestamp, and privacy level. For certificates, additional fields include recipient name, certificate title, certificate number, course or credential metadata, issue date, and expiration date.

### Issuer model

An issuer is the organization or authorized entity that creates a QR-V record. The Issuer Portal is the operational interface where authorized issuers create records, generate QR-V codes, manage issued credentials, revoke or update records, and monitor verification activity.

Issuer records should include legal name, display name, issuer code, status, public key, website URL, contact email, approval timestamp, suspension timestamp, and audit history.

Only authorized issuers may create valid records. If an issuer is suspended, revoked, or not approved, the verification service should not treat its records as fully trusted.

### Audit log

The audit log records the lifecycle of QR-V activity. It should preserve issuer actions, verification events, record creation, record updates, revocations, authentication events, API-key events, administrative overrides, and system errors.

QVS-1.0 identifies verification audit logs as a core security protection and states that every verification event can be recorded.

A production audit entry should include event ID, event type, actor ID, issuer ID, record ID, request ID, IP address, user agent, timestamp, result, and metadata. Audit records should be append-oriented from the application layer.

---

## Developers

### Getting started

Developers integrate with QR-V by learning three flows first: verify a record, create a record, and revoke a record.

The minimum production integration should support:

```text
GET /healthz
GET /readyz
GET /version
GET /api/v1/verify/:qrvid
POST /api/v1/records
POST /api/v1/records/:qrvid/revoke
```

A developer should begin with the public verification API before using protected issuer routes. The verification API confirms that the QRVID resolves correctly and that the response format is deterministic.

The documentation sitemap identifies the Developers section as the integration layer and includes getting started, SDK overview, integration guides, verification integration, webhook events, environment setup, and testing sandbox.

### Authentication

Public verification endpoints may be read-only and unauthenticated, subject to rate limits. Issuer and registry mutation endpoints must require authentication.

Protected issuer routes should use bearer-token authentication, API keys, issuer identification, and role-based authorization. Issuer users may create records, view issuer-owned records, download QR codes, and revoke issuer-owned records. Platform administrators may approve issuers, suspend issuers, inspect audit logs, and perform documented administrative actions.

Authentication secrets, signing keys, database credentials, and issuer tokens must remain server-side. Frontend-safe URLs may be exposed, but private keys and API secrets must not be embedded in client code.

### API reference

The QR-V API should expose a clear machine-oriented contract.

Public verification:

```http
GET /api/v1/verify/:qrvid
```

Protected record creation:

```http
POST /api/v1/records
Authorization: Bearer <jwt>
x-issuer-id: <issuer-id>
x-api-key: <api-key>
```

Protected revocation:

```http
POST /api/v1/records/:qrvid/revoke
Authorization: Bearer <jwt>
```

For production, the API should return structured JSON with `ok`, `status`, `qrvid`, `recordType`, issuer details, issued timestamp, expiration timestamp, integrity result, and verification timestamp.

---

## Security

### Threat model

QR-V addresses threats that ordinary QR codes do not address. The protocol identifies QR cloning, forged documents, fake registries, and replay attacks as core threats. Security protections include cryptographic signatures, TLS encryption, revocation lists, and distributed verification nodes.

QVS-1.0 also identifies the major weaknesses of traditional QR codes: no authenticity validation, QR code cloning, no issuer identification, and no registry record.

Production controls should address malicious URL substitution, forged certificate data, fake issuers, stolen API keys, unauthorized revocation, record tampering, scraping, enumeration, denial of service, and privacy leakage.

### Key management

QRVP-1 requires cryptographic verification. The required hash algorithm is SHA-256 and the required signature algorithm is Ed25519, with RSA-4096 listed as optional.

The signing model should use issuer keypairs, canonical JSON serialization, record hashing, digital signatures, public-key verification, and key rotation. Private keys must never be exposed in browser code or public repositories.

Verification should follow this pattern:

```text
canonicalize record
→ hash with SHA-256
→ verify Ed25519 signature with issuer public key
→ check issuer status
→ check revocation and expiration
→ return deterministic result
```

### Privacy modes

QRVP-1 supports three privacy modes: public verification, restricted verification, and private verification. Public verification may display full permitted record data. Restricted verification returns limited metadata. Private verification returns only validity information.

Privacy mode must be enforced at response time. A public user should never receive restricted or private registry payloads simply because they know a QRVID. The verification service should filter fields based on record privacy level, issuer policy, and public-safe display rules.

Public pages should clearly indicate what is verified without exposing unnecessary personal or sensitive information.
