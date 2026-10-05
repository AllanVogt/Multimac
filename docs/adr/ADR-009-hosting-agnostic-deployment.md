# ADR-009: Hosting-agnostic deployment, decision deferred

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

No domain or server exists yet. Hosting must not complicate development, but the project must be publishable later without rework.

## Decision

Build production-ready from the start (environment configuration, multi-stage Dockerfiles, dev and prod compose files, health endpoint, same-origin routing, `SITE_URL` and `ALLOW_INDEXING`). Choose and provision hosting in Sprint 8. The recommended target is a single VPS with Docker Compose. Validate the production setup locally before any server exists.

## Consequences

No provider lock-in and no early cost. See docs/architecture/deployment.md.
