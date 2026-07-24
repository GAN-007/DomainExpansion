# Security Policy

## Current security status

DomainExpansion does not yet contain an executable application. The current repository consists of a migrated documentation baseline and engineering assessment. No deployment should be described as production-ready until the application source, infrastructure, identity, data, registry integrations, payment integrations, and operational controls are implemented and independently verified.

## Supported versions

No production version is currently supported. Security support begins only after a tagged release passes the launch gates in `docs/ENGINEERING_REPORT.md`.

## Reporting a vulnerability

Do not open a public issue containing credentials, personal data, exploit details, registry secrets, payment data, or tenant information.

Report suspected vulnerabilities privately to the repository owner through GitHub Security Advisories. Include:

- affected commit or release;
- affected component and endpoint;
- reproduction steps;
- impact assessment;
- logs or screenshots with secrets and personal data removed;
- proposed remediation when available.

## Required security controls before production

- OIDC/OAuth 2.1 identity with MFA, passkeys, recovery, session revocation, and service-account controls.
- Deny-by-default organization authorization and PostgreSQL row-level security.
- Secrets stored in a managed secret service; no production secrets in Git, images, logs, CI output, or client bundles.
- Input validation, output encoding, CSRF defense, SSRF controls, secure file handling, rate limiting, and bot mitigation.
- Signed, replay-protected webhooks and idempotent provider callbacks.
- Immutable audit events and independently reconciled financial ledger entries.
- Dependency review, SBOM generation, signed artifacts, provenance, container scanning, and protected deployments.
- Penetration, tenant-isolation, load, accessibility, backup-restore, and disaster-recovery testing.
- Privacy, abuse, registrant, payment, and legal approval.

## AGPL compliance

Covered network deployments must satisfy the GNU Affero General Public License version 3 source-availability obligations. Legal review is required before combining AGPL-covered components with differently licensed proprietary components.
