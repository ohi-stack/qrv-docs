# QR-V™ Documentation

Authoritative protocol, standards, architecture, verification, registry, issuer, API, security, and implementation documentation for the QR-V™ Global Verification Network.

## Documentation Role

This repository is a standards and implementation source, not a marketing blog.

Documentation must distinguish:

1. **Protocol** — QRVP-1 defines identifiers, resolution, verification, registry interaction, cryptographic validation, privacy modes, revocation, and responses.
2. **Standard** — QVS-1.0 defines operational rules and deterministic verification behavior.
3. **Implementation** — production APIs, database schemas, user interfaces, deployment, and operations.
4. **Commercial Product** — issuer portal, certificate verification, memberships, product authentication, and enterprise integrations.

## Canonical Public Access

Current consolidated public documentation entry:

```text
https://qrv.network/docs
```

Reserved dedicated documentation service:

```text
https://docs.qrv.network
```

Operational services remain separate:

- `https://verify.qrv.network`
- `https://api.qrv.network`
- `https://registry.qrv.network`
- `https://issuer.qrv.network`

## Authoritative Structure

```text
/overview
/protocol
/standards
/architecture
/verification
/registry
/issuers
/developers
/api-reference
/use-cases
/governance
/security
/resources
/legal
```

## Minimum Production Documentation

- What is QR-V™
- Problem with standard QR codes
- QRVP-1 introduction
- QRVID identifier formats
- Resolution and verification flow
- QVS-1.0 verification standard
- Deterministic status contract
- Registry data model
- Issuer onboarding and lifecycle
- Create, verify, and revoke API reference
- Privacy modes
- Cryptographic validation
- Threat model
- Deployment and operations guide
- Verification disclaimers

## Canonical Flow

```text
QR code
→ QR-V identifier
→ resolver
→ verification API
→ registry lookup
→ hash/signature validation
→ deterministic result
```

## Deterministic Statuses

```text
VERIFIED
REVOKED
EXPIRED
NOT_FOUND
INVALID_FORMAT
INVALID_SIGNATURE
SUSPENDED_ISSUER
UNAVAILABLE
```

See `VERIFICATION_STATUS_CONTRACT.md` for normative behavior.

## API Assets

- `openapi.yaml` — OpenAPI 3.1 contract for the production-facing core API.
- `VERIFICATION_STATUS_CONTRACT.md` — deterministic response and HTTP-mapping rules.

## Documentation Rules

- Use stable permanent URLs without dates.
- Use Gregorian/UTC timestamps as controlling operational timestamps.
- OneGodian Time™ may appear only as supplemental reference metadata where configured.
- Do not represent verification as legal adjudication, ownership adjudication, governmental approval, or independent validation of an issuer's underlying claim.
- State precisely what was checked: registry presence, issuer status, record status, hash integrity, signature validity, expiration, and revocation.
- Use current `qrv.network` service URLs; retain legacy domains only in clearly marked historical records.

## Production Completion Standard

A developer using this documentation must be able to:

1. authenticate as an approved issuer;
2. create a record;
3. receive a QRVID;
4. generate a verification QR;
5. retrieve a deterministic public result;
6. revoke the record;
7. observe the public result change to `REVOKED`;
8. interpret all errors and privacy modes without unpublished assumptions.
