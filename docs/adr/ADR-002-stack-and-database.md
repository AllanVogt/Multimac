# ADR-002: Stack and database

- **Status:** Accepted
- **Date:** 2026-10-05

## Context

The stack is reused from Absurd Market. Its docs are inconsistent about the database: README, ARCHITECTURE and its decisions list say PostgreSQL, while AI_CONTEXT, PROJECT and ROADMAP say MySQL. The brief for this project explicitly asks for MySQL.

## Decision

Backend: Python, FastAPI, SQLAlchemy, Alembic. Frontend: React, TypeScript, Vite, Tailwind CSS. Database: MySQL 8. Infrastructure: Docker and Docker Compose. Extra frontend libraries only where justified: React Router, TanStack Query, react-hook-form + zod (admin only). No Redis, microservices or Kubernetes.

## Consequences

A simple monolith split into frontend and backend. Any new technology requires a documented need and approval.
