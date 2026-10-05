# ADR-003: SEO through server-side head injection

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

A React SPA delivers an empty HTML shell. Googlebot renders JavaScript with delay and WhatsApp/social scrapers do not run it, but product links are shared on WhatsApp constantly.

## Decision

FastAPI serves the built `index.html` with per-route title, description, Open Graph, canonical and JSON-LD filled in for products, categories and services, plus a dynamic `sitemap.xml` and `robots.txt`. React takes over in the browser.

## Consequences

Link previews and indexing work without leaving the agreed stack. The body is still client-rendered; moving to full SSR (for example Next.js) would be a stack change and is not recommended now. Needs a small template step and tests.
