# Architecture overview

A simple monolith split into a React frontend and a FastAPI backend, backed by
MySQL. Docker Compose runs everything locally and in production.

```
Browser -> Caddy (HTTPS, static files, /media) -+-> React SPA (static build)
                                                +-> FastAPI (/api, /sitemap.xml, HTML with meta tags) -> MySQL
```

## Frontend

React, TypeScript, Vite, Tailwind. Extra libraries only where justified:
React Router (routing), TanStack Query (caching and loading states for the
catalog), react-hook-form + zod (admin forms only). Admin code is lazy-loaded
so public visitors never download it.

## Backend

FastAPI with lean layers: `api` (routers), `schemas` (Pydantic), `models`
(SQLAlchemy) and `services` (only where there is real logic, such as images and
SEO). No repository layer: it would add complexity without benefit at this size.
REST JSON under `/api/v1`; public endpoints are read-only.

## SEO with a SPA (ADR-003)

A pure SPA ships an empty HTML shell. Googlebot renders JavaScript with delay,
and WhatsApp/social scrapers do not run it at all, which matters for a store
whose links are shared on WhatsApp. FastAPI therefore serves the built
`index.html` with per-route `<title>`, description, Open Graph, canonical and
JSON-LD filled in (product, category, service). React takes over afterwards.

## Images (ADR-005)

Admin upload, validated by decoding with Pillow, EXIF removed, UUID file name,
WebP variants (400, 800 and 1600 px). Files live in a Docker volume served by
Caddy with long cache. The database stores path, alt text, position and
dimensions. A small storage interface allows moving to object storage later.

## Admin authentication (ADR-004)

Email and password, argon2id hash. JWT in an `HttpOnly`, `Secure`,
`SameSite=Strict` cookie plus a CSRF header check. Login is rate limited in
memory. The first admin is created by a CLI command; there is no registration
endpoint.

## Configuration

- Infrastructure: `.env` read by `pydantic-settings`; `.env.example` is
  versioned, `.env` is not.
- Store data (name, WhatsApp, phone, address, hours, social links): the
  `store_settings` table, editable in the admin and exposed by `GET /api/v1/settings`.
- The frontend builds every WhatsApp link through one function,
  `buildWhatsAppUrl(message)`.

## Routes

Public pages: `/`, `/catalogo`, `/catalogo/:categoria`, `/produtos/:slug`,
`/lista-de-interesse`, `/oficina`, `/oficina/:servico`, `/sobre`, `/contato`.

Admin pages: `/admin/login`, `/admin/produtos` (list, new, edit),
`/admin/categorias`, `/admin/marcas`, `/admin/servicos`, `/admin/configuracoes`.

Public API: `GET /api/v1/settings`, `/categories`, `/brands`, `/products`
(`q`, `category`, `brand`, `min_price`, `max_price`, `availability`, `featured`,
`sort`, `page`, `slugs`), `/products/{slug}`, `/services`, `/services/{slug}`;
plus `GET /sitemap.xml` and `GET /robots.txt`.

Admin API (`/api/v1/admin`): `POST /auth/login`, `POST /auth/logout`,
`GET /auth/me`; CRUD for `products`, `categories`, `brands`, `services`
(`PATCH` to activate/deactivate); image upload, reorder and delete;
`GET/PUT /settings`.

## Planned folder structure

```
<project>/
  backend/   app/{core,models,schemas,services,api/v1/{public,admin},seed}, alembic/, tests/
  frontend/  src/{app,pages,features,components,lib}, public/
  deploy/    Caddyfile
  docs/      architecture/, adr/, sprints/
  docker-compose.yml, docker-compose.prod.yml, .env.example
  .github/workflows/
```
