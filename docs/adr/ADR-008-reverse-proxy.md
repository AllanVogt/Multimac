# ADR-008: Caddy as reverse proxy

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

Production needs HTTPS, static file serving, `/media` and proxying to the API on a single VPS.

## Decision

Use Caddy: automatic HTTPS, simple configuration, security headers.

## Consequences

One small config file replaces an nginx and certbot setup. The team is less familiar with it than with nginx.
