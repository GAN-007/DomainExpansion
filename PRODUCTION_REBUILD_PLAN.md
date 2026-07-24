# DomainExpansion Production Rebuild Plan

## Verified repository state

`GAN-007/DomainExpansion` currently contains documentation and engineering-assessment branches. It does not yet contain the executable DigitalPlat domain-management application.

The executable source of record is `DigitalPlatDev/Domain-OSS`, currently pinned for assessment at commit `7eac16f470a1890b6cdc70abe272771879665bb6`.

## Existing source capabilities

The source application is a Python 3.11+ self-hosted domain and DNS management platform with:

- Browser setup wizard and production Gunicorn runtime
- SQLite and MySQL support through SQLAlchemy
- Registration, authentication, account suspension, email verification, password recovery, sessions, TOTP, teams, and role-based permissions
- User and administrator domain-management interfaces
- Scoped, expiring API keys and versioned REST API
- OpenAPI documentation and Prometheus metrics
- A, AAAA, CNAME, MX, TXT, SRV, CAA, and NS records
- Cloudflare, PowerDNS, and BIND RFC 2136 provider integrations
- DNSSEC support through Cloudflare
- ACME DNS-01 challenge automation
- Durable DNS jobs, retries, webhooks, provider health, and background workers
- Terraform provider
- Internationalized server-rendered UI
- Docker and Compose deployment
- Pytest, Ruff, coverage, and Go provider tests

## Required source-preserving import

The complete `DigitalPlatDev/Domain-OSS` tree must be imported before production refactoring. The import must preserve:

- AGPL-3.0-only licensing and source-offer obligations
- Every Python module, HTML template, static asset, translation catalog, migration, test, integration, Docker file, workflow, and documentation file
- Existing runtime behavior and public API compatibility
- Git attribution and the pinned upstream revision
- Existing security controls and conservative network defaults

No production claim is valid until the complete source tree is present and reproducibly builds in this repository.

## Production architecture gaps to implement after import

### Persistence and tenancy

- PostgreSQL as the supported high-volume production database
- Explicit tenant and organization ownership on all business records
- Tenant-aware row-level security policies
- Online migrations, schema compatibility checks, and rollback tooling
- Read replicas for reporting and asynchronous read workloads
- Connection pooling and transaction-level timeouts

### Identity and authorization

- Organization SSO using OIDC and SAML
- SCIM provisioning and deprovisioning
- Policy-based authorization layered over roles
- Step-up authentication for destructive or privileged actions
- WebAuthn/passkeys and recovery-code lifecycle
- Session risk controls, device inventory, and forced revocation
- Fine-grained service accounts and workload identities

### Domain lifecycle

- Explicit state machine for requested, pending, active, suspended, expiring, expired, deleted, and restored domains
- Idempotent domain claims and provider reconciliation
- Conflict detection, drift reporting, and deterministic recovery
- Bulk domain operations with approvals and partial-failure reporting
- Scheduled expiration and renewal workflows
- Registrant contact and policy lifecycle where legally applicable

### DNS operations

- Provider capability negotiation and normalized error taxonomy
- Per-zone serial and revision tracking
- Change sets, previews, approvals, and atomic deployment where supported
- DNS propagation verification from independent resolvers
- DNSSEC lifecycle abstraction for all providers that support it
- Zone templates, record policies, and organization defaults
- Provider rate-limit coordination and adaptive retry budgets
- Queue partitioning by tenant, zone, and provider

### Reliability and scaling

- PostgreSQL-backed durable job leases or a supported queue such as Redis plus Celery/RQ with explicit delivery semantics
- Idempotency keys for every mutation
- Dead-letter handling, replay controls, and poison-message quarantine
- Horizontal web and worker scaling
- Backpressure and per-tenant quotas
- Circuit breakers and provider health-based routing
- Graceful shutdown and deployment draining
- Multi-region recovery architecture with tested RPO and RTO

### Security

- External secret-manager support
- Envelope encryption and versioned key rotation
- Content Security Policy without unsafe inline dependencies
- Strict SSRF controls for webhooks and provider endpoints
- Audit-event immutability and export
- Tamper-evident administrative logs
- Dependency, container, secret, and infrastructure scanning
- Software bill of materials and signed release artifacts
- Abuse-rate controls, CAPTCHA integration, and risk scoring

### APIs and integrations

- Stable pagination, filtering, sorting, and error contracts
- Request and response schemas with backward-compatibility tests
- Webhook delivery history, replay, endpoint verification, and secret rotation
- Event stream integration for enterprise consumers
- SDKs for Python, TypeScript, Go, and PHP
- Importers for common DNS providers and BIND zone files
- Export and portability guarantees

### Operations

- Kubernetes-compatible deployment manifests and Helm chart
- Terraform infrastructure modules
- Staging and production environment separation
- Automated database backup, restore verification, and disaster-recovery exercises
- Structured logs, traces, RED metrics, SLOs, alerts, and runbooks
- Canary or blue-green deployment support
- Independent penetration, load, accessibility, and restore testing

### Product and business expansion

- Managed SaaS mode with tenant isolation
- Reseller and white-label portals
- Usage metering, quotas, invoicing, and subscription management
- M-Pesa, bank transfer, Visa/Mastercard, and PayPal payment orchestration for paid plans
- Credits, refunds, reconciliation, tax, and accounting-ledger integration
- Enterprise support plans and SLA management
- Domain portfolio analytics and risk alerts
- Agency and developer collaboration workspaces
- Education and nonprofit plans
- API-first DNS automation product tier

## Market opportunities

The platform can serve niches beyond a conventional DNS panel:

- Community and nonprofit domain programs
- University and coding-bootcamp domain labs
- Managed subdomain platforms for SaaS products
- Internal developer-platform DNS self-service
- Agency portfolio management
- Multi-provider DNS resilience and migration tooling
- ACME challenge brokerage without broad DNS credentials
- Compliance-focused DNS change approval and evidence systems
- Disaster-recovery DNS control planes
- White-label domain communities and reseller networks

## Delivery gates

Production readiness requires all of the following evidence:

1. Complete source import and reproducible build.
2. Existing tests passing without behavior loss.
3. New architecture and security tests passing.
4. PostgreSQL migration and rollback verified on production-scale data.
5. Load tests meeting documented SLOs.
6. Penetration test and remediation.
7. Accessibility audit and remediation.
8. Backup restoration and regional recovery exercise.
9. Privacy, licensing, policy, abuse, and legal review.
10. Operational ownership, on-call procedures, and launch approval.

Until these gates are met, the repository must not be represented as a final production platform.
