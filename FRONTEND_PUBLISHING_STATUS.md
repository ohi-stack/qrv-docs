# QR-V™ Frontend Publishing Status

**Status date:** September 6, 2026

QR-V documentation source remains maintained in `ohi-stack/qrv-docs`, while human-facing publication is consolidated under `https://qrv.network/docs` through `ohi-stack/qrv-node`.

## Current frontend convergence

The QR-V Sites/customer frontend is being imported into `qrv-node` in PR #17. This work changes presentation and publishing infrastructure only; it does not redefine protocol or verification semantics.

Canonical publication boundaries remain:

```text
qrv.network/docs              human-readable documentation
qrv.network/api-reference     human-readable API reference
api.qrv.network/api/v1        machine-facing API
```

## Publishing constraints

Documentation rendered through the consolidated frontend must preserve separation between:

- QRVP-1 protocol requirements;
- QVS-1.0 verification standard requirements;
- production implementation details;
- commercial/product messaging.

The frontend may improve navigation, visual design, accessibility, responsiveness, and conversion flows, but must not silently change protocol terminology or assert operational states unsupported by the live API/registry.

## Migration acceptance

Before the consolidated frontend becomes the only public publishing surface:

```text
[ ] docs routes remain addressable under qrv.network
[ ] API reference points to api.qrv.network/api/v1
[ ] protocol/standard content remains source-grounded
[ ] legacy docs.qrv.network redirects safely if retained
[ ] SEO/canonical metadata is correct
[ ] no production secret is exposed to browser code
[ ] public VERIFIED/Operational claims remain live-data-backed
```

`qrv-docs` remains a source-of-truth documentation repository even after frontend convergence is complete.
