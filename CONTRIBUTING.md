# Contributing to DomainExpansion

## Repository state

The repository currently contains documentation and engineering planning, not a complete executable platform. Contributions must preserve that distinction and must not claim production readiness without reproducible evidence.

## Development rules

1. Work in a dedicated branch and submit a pull request.
2. Keep upstream attribution and the complete applicable license notices.
3. Do not commit credentials, private keys, tokens, customer data, payment data, registry credentials, or production exports.
4. Add tests for every executable behavior introduced.
5. Use database migrations for schema changes; never depend on manual production edits.
6. Make mutating API operations idempotent and authorization-aware.
7. Keep tenant ownership explicit on every tenant-controlled record.
8. Record externally visible state changes in an immutable audit trail.
9. Document operational impact, rollback, observability, and failure handling.
10. Do not merge incomplete placeholder implementations into a release branch.

## Pull-request evidence

Every implementation pull request must state:

- the problem and affected users;
- architecture and security impact;
- database and migration impact;
- API compatibility impact;
- tests executed and results;
- observability added;
- rollback procedure;
- remaining risks or launch gates.

## Definition of done

A change is complete only when code, migrations, tests, documentation, authorization, telemetry, error handling, and operational procedures are included and validated. A successful local happy path alone is not production evidence.
