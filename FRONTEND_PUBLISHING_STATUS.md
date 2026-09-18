# QR-V™ Frontend Publishing & Multi-Builder Status

**Status date:** September 18, 2026

QR-V documentation source remains maintained in `ohi-stack/qrv-docs`, while human-facing publication is consolidated under `https://qrv.network/docs` through `ohi-stack/qrv-node`.

## Current implementation state

Frontend runtime convergence is complete on `qrv-node/main`.

```text
Runtime convergence: eaac061efd4c03d8d90714409414832682e3fec0
Multi-builder baseline: 4e9dd06e7c164b61ec586c54f2c3578192ef5bb3
Production sitemap baseline: 0949815c020e7f27f388f48f696bd931a6504b0a
```

Canonical publishing boundaries remain:

```text
qrv.network/docs              human-readable documentation
qrv.network/api-reference     human-readable API reference
api.qrv.network/api/v1        machine-facing API
```

## Sitemap and route authority

The canonical public-platform route contract is maintained in `ohi-stack/qrv-node`:

```text
config/routes.manifest.json
  machine-readable route/tier contract

docs/PRODUCTION_SITEMAP.md
  human-readable full production sitemap
```

The exact API endpoint contract must come from the normative OpenAPI specification in `qrv-api`; documentation must not create a second conflicting API specification.

The public header contract is:

```text
Products · Solutions · Developers · Documentation · Pricing · About
```

Actions:

```text
Verify Record · Issuer Login · Get Started
```

## Multi-builder publishing workflow

```text
work/chatgpt-sites
  documentation UI, navigation, typography, diagrams, responsive presentation

work/google-ai-studio
  interactive examples, developer tooling, Gemini-assisted prototypes

integration/multi-builder
  reconcile and validate both lanes

main
  production publication only
```

Documentation content remains governed by `qrv-docs`; frontend builders may change presentation but must not silently rewrite protocol or standard semantics.

## Publishing constraints

Published documentation must preserve separation between:

- QRVP-1 protocol requirements;
- QVS-1.0 verification standard requirements;
- production implementation details;
- commercial/product messaging.

Builders may improve navigation, visual design, accessibility, responsiveness, examples, and conversion flows. They must not assert operational states unsupported by the live API/registry.

A defined route is not automatically a production capability. Product/workflow claims require implementation, integration, documentation, testing, and repeatability.

## Promotion gate

Before documentation changes reach `main`:

```text
[ ] source terminology remains accurate
[ ] links use qrv.network + api.qrv.network
[ ] no production secrets enter browser code
[ ] operational claims are live-data-backed
[ ] public routes match config/routes.manifest.json
[ ] API examples match normative OpenAPI
[ ] npm run check:sitemap passes
[ ] npm run check:lanes passes
[ ] npm run validate:prod passes
[ ] integration/multi-builder review completed
```

`qrv-docs` remains the source-of-truth documentation repository for normative and explanatory content after frontend convergence.
