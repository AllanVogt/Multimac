# ADR-004: Admin authentication

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

Only administrators authenticate. There are no customer accounts. Absurd Market planned JWT for all users.

## Decision

Email and password with argon2id hashing. JWT stored in an `HttpOnly`, `Secure`, `SameSite=Strict` cookie with a CSRF header check. Login is rate limited in memory (no Redis). The first admin is created by a CLI command; no registration endpoint exists.

## Consequences

Safer than a token in `localStorage`. Requires same-origin deployment, which is already planned (ADR-008).
