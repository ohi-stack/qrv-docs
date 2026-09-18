# QR-V™ Global Verification Network — Production Sitemap

**Effective date:** 2026-09-17  
**Public platform:** https://qrv.network  
**Trusted API/data plane:** https://api.qrv.network

## Authority

Documentation follows:

1. QRVP-1
2. QVS-1.0
3. QR-V™ Platform — Full Developer Build Specification
4. Canonical Production Sitemap
5. Normative OpenAPI specification
6. Repository implementation
7. Deployment and operations runbooks

## Canonical route families

Public browser routes are consolidated under `qrv.network`:

- `/about`
- `/verify`
- `/registry`
- `/issuer`
- `/products`
- `/solutions`
- `/developers`
- `/docs`
- `/protocol`
- `/security`
- `/enterprise`
- `/pricing`
- `/resources`
- `/network`
- `/status`
- `/company`
- `/support`
- `/legal`

The full machine-readable route inventory is maintained in:

`ohi-stack/qrv-node/config/routes.manifest.json`

## Documentation hierarchy

Canonical documentation URLs are:

- `/docs/overview`
- `/docs/protocol`
- `/docs/verification`
- `/docs/registry`
- `/docs/issuers`
- `/docs/developers`
- `/docs/api-reference`
- `/docs/deployment`
- `/docs/examples`
- `/docs/changelog`

The dedicated `/protocol` route family presents protocol/standard material to platform users; `/docs/protocol` remains the deeper documentation hierarchy.

## API documentation rule

The authoritative machine contract lives in:

`ohi-stack/qrv-api/openapi.yaml`

Human-readable API reference content may be rendered under `qrv.network/docs/api-reference` or `qrv.network/api-reference`, but it must be generated from or reconciled against the normative OpenAPI contract.

Do not maintain a competing manual API contract.

## Status rule

Documentation must distinguish:

- LIVE
- IMPLEMENTED BUT NOT DEPLOYED
- PARTIALLY IMPLEMENTED
- DEVELOPMENT
- PLANNED
- BLOCKED
- DEPRECATED

A documented route or planned product does not establish that the workflow is operational.

## Release tiers

### Tier 1

Release-critical routes:

`/`, `/verify`, `/verify/{qrvid}`, `/issuer`, `/issuer/onboarding`, `/issuer/dashboard`, `/issuer/records`, `/registry`, `/developers`, `/docs`, `/products`, `/pricing`, `/security`, `/status`, `/support`, `/legal`.

### Tier 2

Product, solution, developer, protocol, issuer-management, analytics, API-key, webhook, enterprise and integration surfaces.

### Tier 3

Deep guides, tutorials, examples, downloads, resource libraries and educational expansion.

## Publishing rule

This repository remains the standards-quality documentation source. Runtime publication is through `ohi-stack/qrv-node`. API behavior is owned by `ohi-stack/qrv-api`.
