# QR-V™ Documentation — Authoritative Content Source

This repository remains the authoritative source for QR-V protocol, standards, architecture, verification, registry, issuer, API, security, and implementation documentation.

It is **not** a required standalone production node after consolidation.

## Canonical public documentation

```text
https://qrv.network/docs
https://qrv.network/docs/overview
https://qrv.network/docs/protocol
https://qrv.network/docs/verification
https://qrv.network/docs/registry
https://qrv.network/docs/issuers
https://qrv.network/docs/developers
https://qrv.network/api-reference
```

## Two-node architecture

```text
qrv.network
  human-facing documentation and application routes
      ↓
api.qrv.network
  machine-facing API and registry authority
```

`docs.qrv.network` is now a legacy compatibility hostname, not a required independent application. If retained, point it to `qrv-node` so it redirects to `qrv.network/docs`.

## Documentation role

Continue to maintain standards-quality source material here, including:

- QRVP-1;
- QVS-1.0;
- identifier and resolution rules;
- verification status contract;
- registry data model;
- issuer lifecycle;
- API reference;
- security and threat model;
- deployment and operations guidance;
- changelog and versioning.

## Publishing rule

Production-facing human documentation is published through `ohi-stack/qrv-node`. Machine-facing API behavior is implemented by `ohi-stack/qrv-api`.

Do not delete this repository; it is a source-of-truth documentation repository, not a runtime dependency.
