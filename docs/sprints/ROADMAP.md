# Roadmap

Each sprint follows the same order: explain, identify dependencies,
implement, validate, review, update documentation, commit.

| Sprint | Goal | Main deliverables |
|---|---|---|
| 0 | Discovery and requirements | Requirements, architecture, data model, ADRs 001-009, repository |
| 1 | UX/UI and visual identity | Mobile-first wireframes, palette from the logo, typography, component list |
| 2 | Architecture, database and Docker | ERD, Alembic baseline, Dockerfiles, dev/prod compose skeleton, `.env.example`, `/health` |
| 3 | Backend / API | Public read-only API, demo seed (`is_demo`), settings, head injection and sitemap |
| 4 | Frontend / catalog | Home, catalog with filters, product page, per-route meta tags |
| 5 | WhatsApp / interest list | `buildWhatsAppUrl`, contextual messages, interest list |
| 6 | Admin panel | Authentication, product/category/brand/service CRUD, image upload, settings |
| 7 | SEO, performance, accessibility | Audit of structured data, Lighthouse, WCAG checks, security headers |
| 8 | Tests, deploy, documentation | Choose hosting, first deploy, backups, CI/CD, runbook, go-live checklist |

Changes from the original brief: Docker and MySQL running move to Sprint 2
("Docker before application"), and head injection moves to Sprints 3-4
because it is architecture rather than polish.
