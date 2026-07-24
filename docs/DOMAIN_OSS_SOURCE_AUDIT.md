# DigitalPlat Domain OSS Source Audit

## Verified source

- Repository: `DigitalPlatDev/Domain-OSS`
- Default branch: `main`
- Current inspected commit: `7eac16f470a1890b6cdc70abe272771879665bb6`
- Initial application commit: `a701d086dd8c8ee36e299c70f5da89b504736ab4`
- License: AGPL-3.0-only
- Runtime: Python 3.11+ / Python 3.12 container
- Application factory: `domain_oss:create_app`

## Existing implemented capability

The approved source is a real self-hosted domain and DNS management application. Existing behavior that must be preserved includes:

- Browser-based setup and administrator creation.
- SQLite default persistence and MySQL through `DATABASE_URL`.
- User registration, login, account suspension and per-user domain limits.
- Administrator interfaces for users, domains, settings, providers, zones, jobs, webhooks and audit events.
- Role-based teams, sessions, verification, password recovery and TOTP two-factor authentication.
- Scoped, expiring API keys and a versioned REST API.
- OpenAPI discovery and Prometheus metrics.
- DNS records for A, AAAA, CNAME, MX, TXT, SRV, CAA and NS.
- RFC 2136/BIND with TSIG, PowerDNS API and Cloudflare adapters.
- Cloudflare DNSSEC lifecycle controls and secondary DNS health checks.
- ACME DNS-01 challenge creation and cleanup.
- JSON import/export, CSV administration exports and a Go Terraform provider.
- Eight user-interface languages.
- Encrypted DNS credentials, CSRF controls, rate limits, password hashing and strict browser headers.
- Durable DNS jobs, retries, signed webhooks, SMTP delivery and provider health reporting.
- Docker, Docker Compose and a dedicated background worker.

## Verified repository-level files and components

The initial source commit proves the presence of at least the following top-level implementation assets:

- `.dockerignore`
- `.env.example`
- `.github/workflows/ci.yml`
- `.gitignore`
- `CONTRIBUTING.md`
- `Dockerfile`
- `LICENSE`
- `README.md`
- `domain_oss/`
- `integrations/terraform-provider-domainoss/`
- Python test and lint configuration
- Docker and database runtime configuration

The CI definition runs Python 3.12 installation, Ruff, pytest with coverage and Go tests for the Terraform provider.

## Architecture determination

The current platform is a server-rendered modular monolith with a separate background-worker process and provider integrations. This is an appropriate baseline for controlled growth. It should not be prematurely decomposed into microservices.

Production expansion should preserve the modular monolith while introducing explicit internal boundaries for:

1. Identity and organization tenancy.
2. Domain ownership and lifecycle.
3. DNS desired state and provider reconciliation.
4. Durable jobs and transactional outbox delivery.
5. Billing, invoices, payments and immutable ledgering.
6. Abuse cases, policy decisions and appeals.
7. Notifications and webhook delivery.
8. Audit, observability and compliance evidence.

## Material gaps relative to the requested final platform

The upstream README explicitly states that the existing application is not a registrar, registry, billing platform, abuse-handling service or authoritative DNS server. Those are therefore expansion areas, not existing features that may be claimed complete.

### Data and tenancy

- PostgreSQL is not documented as a supported production database.
- Database-enforced tenant row-level security is not established.
- Organization-wide quotas, billing ownership and data residency are not established.
- An immutable double-entry financial ledger is absent.
- Registry-grade append-only domain lifecycle evidence is absent.

### Domain lifecycle

- No registrar/registry protocol implementation is established.
- Availability, reservation, registration, renewal, expiration, grace, redemption, restoration and transfer workflows require implementation.
- Registry reconciliation, EPP adapters, contact validation and asynchronous command status require implementation.

### Payments and billing

- No M-Pesa, bank, card or PayPal implementation is established.
- Plans, subscriptions, invoices, taxes, credits, refunds and reconciliation require implementation.
- Provider callbacks must use signature validation, idempotency and independent settlement reconciliation.

### Enterprise and policy

- SAML, SCIM, enterprise session policy and delegated administration require verification or implementation.
- Policy-as-code, approval workflows and just-in-time privileged access require implementation.
- Abuse reporting, evidence handling, takedown, appeal and transparency workflows require implementation.

### Reliability and operations

- PostgreSQL HA, Redis, durable external queues, object storage and regional deployment are not established.
- SLOs, distributed tracing, alert routing and tested disaster recovery require implementation.
- Independent penetration, load, accessibility, privacy and legal validation remain launch gates.

## Migration integrity requirements

A valid import must preserve:

- Every tracked source file and directory.
- File modes, especially executable CLI scripts.
- AGPL-3.0 license and copyright notices.
- Source attribution and public source link.
- Templates, translations and static assets.
- Python dependency declarations and lock information when present.
- Go module files and Terraform-provider source.
- Migrations, tests, examples, CI and operational documentation.
- Existing routes, API behavior and database upgrade paths.

## Current migration blocker

The authenticated GitHub connector can inspect and write individual repository objects, but it does not expose a recursive cross-repository tree-copy/archive action. The execution container also cannot resolve `github.com`, so a native clone, test run and history-preserving push cannot be completed in this session.

Because a partial manually reconstructed application would violate migration integrity, no claim is made that the Domain-OSS source has been fully imported. The correct next repository operation is a complete Git object transfer or archive-based import followed by reproducible build and test validation.

## Required validation immediately after complete import

1. Compare source and destination file manifests and content hashes.
2. Verify executable modes and binary assets.
3. Install the Python development dependencies.
4. Run Ruff.
5. Run the complete pytest suite with coverage.
6. Run Go tests for the Terraform provider.
7. Build the production Docker image.
8. Start the web and worker processes.
9. Exercise setup, authentication, domain, DNS provider, API, webhook and worker flows.
10. Run migration upgrade and rollback tests against SQLite, MySQL and the proposed PostgreSQL production target.
