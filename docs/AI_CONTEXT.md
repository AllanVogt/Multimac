# AI Context

Read this first when continuing the project in a new conversation.

## Project

**Multimac** — digital catalog for a physical store and workshop specialized in two-stroke
equipment, connected to the workshop and to WhatsApp. **Not an e-commerce.**
Purchases and pick-ups are in person only. See [requirements](requirements.md).

## Working rules

- Never write code before the current sprint's plan is agreed.
- Before each step: explain what will be done, identify dependencies,
  implement, validate, review, update docs.
- Do not silently change an agreed architecture; explain the reason first and
  record it as an ADR.
- Never add anything from the "out of scope" list in requirements.md without
  the owner's approval.
- Add a technology only when a real need exists.
- Explain important decisions objectively (why, not academic theory).
- Do not invent business facts or product data; use placeholders and
  `is_demo` records.
- Code, commits and docs in English; site content in pt-BR.
- Small commits following Conventional Commits.

## Stack

Python, FastAPI, SQLAlchemy, Alembic, MySQL 8; React, TypeScript, Vite,
Tailwind CSS; Docker Compose; Caddy in production. Details in
[architecture](architecture/overview.md) and the [ADRs](adr/README.md).

## Current state

Sprint 0 — Discovery and requirements, done. Sprint 1 (UX/UI and visual
identity) started: name, logo and palette received, see
[ADR-010](adr/ADR-010-visual-identity.md). A static home prototype lives in
`prototype/index.html`. Still missing: store/workshop/product photos.
See [sprints/ROADMAP.md](sprints/ROADMAP.md).
