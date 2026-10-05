# ADR-005: Image storage and processing

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

The catalog depends on photos, with several images per product, uploaded by the administrator.

## Decision

Uploads are validated by decoding with Pillow, EXIF is removed, files get UUID names, and WebP variants (400, 800, 1600 px) are generated. Files live in a Docker volume served by Caddy with long cache. The database stores path, alt text, position and dimensions. Storage sits behind a small interface.

## Consequences

Fast pages and no layout shift. Moving to object storage later only changes the storage implementation. Object storage is not added now.
