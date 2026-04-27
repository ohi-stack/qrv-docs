# QR-V™ Full Platform Roadmap

Status: Active Development
Primary domain: `docs.qrv.network`

## Platform Boundary

QR-V™ is a registry-backed verification infrastructure platform. The documentation site defines how the network is built, integrated, operated, and verified.

| Service | Domain | Responsibility |
| --- | --- | --- |
| Marketing Site | `qrv.network` | Public positioning, use cases, calls to action |
| Verification Portal | `verify.qrv.network` | Public scan and QRVID result display |
| Issuer Portal | `issuer.qrv.network` | Issuer record creation and lifecycle management |
| Verification API | `api.qrv.network` | Resolver, validation, response normalization |
| Registry Service | `registry.qrv.network` | Canonical datastore and record lifecycle state |
| Developer Docs | `docs.qrv.network` | Protocol, API reference, guides, schemas, SDK docs |
| Developer Portal | `developers.qrv.network` | API keys, sandbox, usage, developer onboarding |
| Registry Explorer | `explorer.qrv.network` | Public registry search and transparency layer |
| Status Page | `status.qrv.network` | Health, uptime, incident reporting |

## Immediate Platform Priorities

1. Standardize `/health` and `/` service discovery across active Node services.
2. Connect `qrv-api` to `qrv-registry` through `REGISTRY_BASE_URL`.
3. Connect `qrv-verify` to `qrv-api` through `API_BASE_URL`.
4. Connect `issuer-qrv` to `qrv-api` for record creation.
5. Publish public documentation for QRVID format, verification states, registry schema, and integration flow.
6. Add smoke-test checklists for Hostinger deployments.
7. Add sample records and deterministic demo flows.

## Repository Map

| Repository | Role | Next Work |
| --- | --- | --- |
| `qrv-registry` | Canonical registry service | Confirm deployment, health endpoint, migrations, record lookup |
| `qrv-api` | Verification API | Add resolver integration with registry service |
| `qrv-verify` | Public verification portal | Render result states from API responses |
| `issuer-qrv` | Issuer UI | Submit record creation to API and show QRVID/verify URL |
| `qrv-docs` | Documentation | Build standards-style docs and API references |
| `qrv-sdk` | Developer SDK | Provide JS client for verify/create/revoke |
| `qrv-node` | Verification node runtime | Node deployment profile and federation model |
| `qrv-explorer` | Registry explorer | Public search UI and record transparency |
| `qrv-status` | Status page | Service uptime and operational metadata |
| `qrv-security` | Security documentation | Threat model, disclosure policy, controls |
| `qrv-billing` | Billing layer | Issuer plans, subscriptions, usage events |
| `qrv-developer-portal` | Developer portal | API keys, sandbox, account UX |

## Verification Lifecycle

```text
Issuer creates record
  ↓
API validates and normalizes payload
  ↓
Registry stores canonical record
  ↓
QRVID + hash + verification URL are returned
  ↓
Verifier scans QR-V code
  ↓
Verification portal calls API
  ↓
API resolves against registry
  ↓
Result is displayed with status, issuer, metadata, and hash
```

## Standard Status Model

| Status | Meaning |
| --- | --- |
| `VERIFIED` | Record exists, is active, and passes validation |
| `INVALID` | Request is malformed or cannot be validated |
| `NOT_FOUND` | QRVID does not map to a registry record |
| `REVOKED` | Record exists but was revoked by issuer or authority |
| `EXPIRED` | Record exists but is outside its valid date window |
| `UNAVAILABLE` | Registry or API service could not complete the lookup |

## Deployment Readiness Checklist

Each deployable service must expose:

- `GET /health`
- `GET /` service discovery response or landing UI
- environment variable documentation
- no hardcoded secrets
- consistent JSON error responses for API services
- smoke test instructions

## First Production Demonstration

The first complete platform demonstration should prove:

1. Create one certificate from `issuer.qrv.network`.
2. Persist it in `registry.qrv.network`.
3. Resolve it through `api.qrv.network`.
4. Display it at `verify.qrv.network`.
5. Document the flow at `docs.qrv.network`.

