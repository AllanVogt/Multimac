# Deployment strategy

Principle: **production-ready, hosting-agnostic**. Development stays
`docker compose up`; hosting is chosen and provisioned only in Sprint 8.

## Built in from the start

- All configuration through environment variables; `.env.example` versioned.
- Multi-stage Dockerfiles for `api` and `web`.
- `docker-compose.yml` (dev, hot reload, demo seed) and
  `docker-compose.prod.yml` (built images).
- Stateless API: state lives only in MySQL and the media volume.
- Same origin in production (`/api`, `/media` behind one domain); in dev the
  Vite proxy imitates it.
- `GET /health` and logs to stdout.
- Alembic migrations run as a separate command during deploy.
- `SITE_URL` (canonical, sitemap, Open Graph) and `ALLOW_INDEXING`
  (`noindex` by default outside production).
- Image storage behind an interface; no provider-specific code.

## Deliberately not done now

Server, domain, certificate, Terraform/Kubernetes, automated deploy pipeline,
monitoring stack, separate staging. Instead, the production compose file is run
locally to validate the real build, Caddy and migrations.

## Production target

One VPS running Caddy (automatic HTTPS, static files, `/media`), the API and
MySQL 8 with a persistent volume. Only ports 80/443 and key-based SSH are open;
the database is never exposed; containers run as non-root. Prefer a region in
Brazil for latency. Shared hosting is not viable (no FastAPI/Docker).

## Deploy flow

1. First manual: GitHub Actions builds images and pushes to GHCR; on the
   server, `docker compose pull && docker compose up -d`; migrations run as a
   deploy step. Rollback = previous image tag.
2. Later automated by tag or merge to `main`, once the manual flow is stable.

## Operations

- Daily `mysqldump` plus media volume copy, off-server, with retention and a
  **tested restore**.
- External uptime ping on `/health`.
- Dependabot and `pip-audit` in CI.
- Domain `.com.br`; Google Search Console (sitemap) and Google Business Profile.

## Go-live checklist

- [ ] `is_demo` data removed
- [ ] Real `store_settings` and photos with alt text
- [ ] Admin created through CLI, strong password, unique `SECRET_KEY`
- [ ] `SITE_URL` correct; `ALLOW_INDEXING=true` only in production
- [ ] Security headers active in Caddy
- [ ] Backup running and restore tested
- [ ] Lighthouse and accessibility checks passed
- [ ] Sitemap submitted; `robots.txt`, favicon and 404 page checked
- [ ] WhatsApp links tested on a phone
