# MySQL Licensing Issue and PostgreSQL Migration

**Date:** 2026-04-01

---

## The Problem — MySQL's License

MySQL Community Server is distributed under the **GNU General Public License v2 (GPL v2)**.

The GPL is a "copyleft" license. This means: **any software that links against or distributes MySQL must also be released under the GPL**, or must obtain a separate commercial license from Oracle (who owns MySQL).

For this project, that creates a conflict:

- If the project is deployed commercially, distributed to clients, or kept proprietary, Oracle technically requires a **paid commercial license** for MySQL.
- The GPL's copyleft clause can propagate to the application itself — meaning the backend Express app could be considered a derivative work.
- Oracle actively enforces MySQL's commercial license for production software that is not itself open-sourced under GPL.

### Why MariaDB Doesn't Fully Escape This

MariaDB is a fork of MySQL and is also GPL-licensed. It has the same copyleft problem for proprietary/commercial use. It does not resolve the licensing concern — it only removes Oracle as the licensor.

---

## The Solution — PostgreSQL

PostgreSQL is released under the **PostgreSQL License**, a permissive open-source license similar to BSD/MIT.

Key properties:
- No copyleft — using PostgreSQL does **not** require your application to be open source.
- No commercial license required — you can deploy PostgreSQL in any commercial or proprietary product for free.
- No Oracle involvement.

Switching to PostgreSQL eliminates the licensing concern entirely.

---

## When You Need to Switch

You **must** switch to PostgreSQL (or another permissive-licensed database) if any of the following are true:

| Scenario | Action required |
|---|---|
| The project is deployed outside a personal/academic context | Switch to PostgreSQL |
| The app is distributed to clients or the public | Switch to PostgreSQL |
| The app is used by a business that does not want to open-source their code | Switch to PostgreSQL |
| The project is submitted for commercial evaluation or grant funding | Switch to PostgreSQL |
| Your institution's legal team flags GPL contamination | Switch to PostgreSQL |

For a **purely academic, non-distributed course project** where no one outside the class runs it, GPL enforcement risk is low — but it is still technically non-compliant if the application itself is not also GPL.

---

## What's Already in This Repo

A full PostgreSQL stack is already implemented and ready to use. No Prisma schema changes are required — the Prisma adapter handles the MySQL → PostgreSQL switch transparently.

### Files Added for PostgreSQL Support

| File | Purpose |
|---|---|
| [`backend/prisma/postgresql/schema.prisma`](Pollinator-Habitat/backend/prisma/postgresql/schema.prisma) | PostgreSQL-flavored Prisma schema |
| [`backend/prisma/seed.pg.js`](Pollinator-Habitat/backend/prisma/seed.pg.js) | PostgreSQL-compatible seed script |
| [`backend/prisma.config.pg.ts`](Pollinator-Habitat/backend/prisma.config.pg.ts) | Prisma config pointing at the PostgreSQL schema |
| [`backend/Dockerfile.pg`](Pollinator-Habitat/backend/Dockerfile.pg) | Multi-stage Docker build for the PostgreSQL backend |
| [`docker-compose.prod.pg.yml`](Pollinator-Habitat/docker-compose.prod.pg.yml) | Full production stack using `postgres:17` |
| [`docker-compose.dev.pg.yml`](Pollinator-Habitat/docker-compose.dev.pg.yml) | Development stack with hot reload and exposed port 5432 |

---

## How to Run with PostgreSQL

### Development

```bash
docker compose -f docker-compose.dev.pg.yml up
```

Dev credentials (hardcoded):
- User: `pollinator`
- Password: `pollinatorpw`
- Database: `pollinator`
- Port exposed to host: `5432`

`DATABASE_URL` inside the container: `postgresql://pollinator:pollinatorpw@postgres:5432/pollinator`

### Production

1. Copy `.env.pg.example` to `.env.pg` and fill in your credentials.
2. Run:

```bash
docker compose -f docker-compose.prod.pg.yml up
```

The `migrate` service runs `prisma migrate deploy` + `seed.pg.js` automatically on first start, then exits. The `backend` service waits for both `postgres` (healthy) and `migrate` (complete) before starting.

---

## What Does Not Change

- All application code (Express handlers, Prisma queries, frontend, portal) is identical.
- The Prisma client is generated from the PostgreSQL schema but the query API is the same.
- Seed data is identical: session IDs `18429`, `57243`, `90618`, `34790`, `62851`, all 11 pollinators.
- The original `docker-compose.yml` and `docker-compose.dev.yml` (MySQL/MariaDB) remain in the repo and still work for local development where licensing is not a concern.
