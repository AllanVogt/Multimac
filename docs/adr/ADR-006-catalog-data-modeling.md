# ADR-006: Catalog data modeling

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

Absurd Market modeled products with many-to-many categories, brand as text and specifications deferred. This project is a catalog without orders or customers.

## Decision

One category per product; `Brand` as an entity; specifications as label/value pairs; `availability` as an enum; nullable price for on-request items; `is_demo` flag for mock data; no customer, cart or order tables.

## Consequences

Simple URLs, breadcrumbs and canonical; easy admin. No filtering by specification. See docs/architecture/data-model.md.
