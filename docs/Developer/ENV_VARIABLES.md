# Environment Variables Reference

This document lists every environment variable used across all three apps and their containers.

For production deployment, all variables are set in `.env.pg` (PostgreSQL stack) or `.env` (MySQL stack). See [DOCKER_SETUP.md](DOCKER_SETUP.md) for how to create these files.

---

## Backend Variables

Set in the `backend` and `migrate` services in the compose file.

| Variable | Required | Default | Description |
|---|---|---|---|
| `DATABASE_URL` | Yes | — | Full database connection string. Prefix determines adapter: `postgresql://...` or `mysql://...` |
| `SHADOW_DATABASE_URL` | MySQL only | — | Shadow DB for Prisma migrations with MariaDB. Not needed for PostgreSQL. |
| `JWT_SECRET` | Yes | — | Secret key for signing/verifying JWT tokens. **Must be changed from default.** Generate with `openssl rand -hex 32`. |
| `NODE_ENV` | Yes | — | `production` or `development`. Affects logging and error output. |

**`DATABASE_URL` formats:**

PostgreSQL:
```
postgresql://<user>:<password>@<host>:<port>/<database>
postgresql://pollinator:pollinatorpw@postgres:5432/pollinator
```

MySQL/MariaDB:
```
mysql://<user>:<password>@<host>:<port>/<database>
mysql://pollinator:pollinatorpw@mysql:3306/pollinator
```

The hostname (`postgres` or `mysql`) is the Docker service name. Do not use `localhost` in Docker — containers communicate by service name on the shared network.

**Port:** The backend listens on port 4000. This is hardcoded in [`backend/src/index.ts`](Pollinator-Habitat/backend/src/index.ts) and is not configurable via environment variable. The port is internal to Docker and not exposed to the host.

---

## Frontend Variables

Set in the `frontend` service in the compose file or in `frontend/.env.local` for local development outside Docker.

| Variable | Required | Default | Description |
|---|---|---|---|
| `NEXT_PUBLIC_API_URL` | Yes | `""` | Base URL for API calls. **Must be empty string in production** so Nginx proxies `/api/...` correctly. Set to `http://localhost:4000` for direct-to-backend local dev (outside Docker). |
| `NODE_ENV` | Yes | — | `production` or `development`. |

**Why `NEXT_PUBLIC_API_URL` is empty in production:**
In the Docker stack, the frontend makes requests to `/api/...` (a relative path). Nginx intercepts these and proxies them to `backend:4000`. If `NEXT_PUBLIC_API_URL` is set to a full URL, requests bypass Nginx and will fail if the backend isn't directly accessible.

**Development exception:** When running the portal outside Docker (e.g., `npm run dev` on your machine while the backend runs separately), set `NEXT_PUBLIC_API_URL=http://localhost:4000` to reach the backend directly.

---

## Portal Variables

Same pattern as frontend.

| Variable | Required | Default | Description |
|---|---|---|---|
| `NEXT_PUBLIC_API_URL` | Yes | `""` | Base URL for API calls. Empty in production (Nginx proxy on port 3001). Set to `http://localhost:4000` for direct local dev. |
| `NODE_ENV` | Yes | — | `production` or `development`. |

---

## Database Container Variables

### PostgreSQL

Set via `env_file: .env.pg` in `docker-compose.prod.pg.yml`.

| Variable | Required | Description |
|---|---|---|
| `POSTGRES_DB` | Yes | Database name. Default in example: `pollinator` |
| `POSTGRES_USER` | Yes | Database user. Default in example: `pollinator` |
| `POSTGRES_PASSWORD` | Yes | Database password. **Change from default.** |

These three must be consistent with the `DATABASE_URL` in the same `.env.pg` file:
```
DATABASE_URL=postgresql://${POSTGRES_USER}:${POSTGRES_PASSWORD}@postgres:5432/${POSTGRES_DB}
```

### MySQL/MariaDB (development)

Hardcoded in [`docker-compose.dev.yml`](Pollinator-Habitat/docker-compose.dev.yml) — not configurable without editing the compose file.

| Variable | Value (hardcoded) | Description |
|---|---|---|
| `MYSQL_ROOT_PASSWORD` | `rootpw` | MySQL root password (dev only) |
| `MYSQL_DATABASE` | `pollinator` | Database name |
| `MYSQL_USER` | `pollinator` | App user |
| `MYSQL_PASSWORD` | `pollinatorpw` | App user password |

For production MySQL, use `docker-compose.yml` (not `.dev.yml`) and provide these via an env file.

---

## Environment Files

| File | Used by | Notes |
|---|---|---|
| [`.env.pg.example`](Pollinator-Habitat/.env.pg.example) | PostgreSQL stack | Template — copy to `.env.pg` and fill in secrets. **Do not commit `.env.pg`.** |
| `.env` | MySQL production stack | Not included — create from `docker-compose.yml` variable references |
| `frontend/.env.local` | Frontend dev (outside Docker) | Not committed. Set `NEXT_PUBLIC_API_URL=http://localhost:4000` |
| `portal/.env.local` | Portal dev (outside Docker) | Same as frontend |

---

## Variable Matrix

| Variable | Backend | Frontend | Portal | MySQL DB | PostgreSQL DB |
|---|---|---|---|---|---|
| `DATABASE_URL` | ✅ | | | | |
| `SHADOW_DATABASE_URL` | MySQL only | | | | |
| `JWT_SECRET` | ✅ | | | | |
| `NODE_ENV` | ✅ | ✅ | ✅ | | |
| `NEXT_PUBLIC_API_URL` | | ✅ | ✅ | | |
| `POSTGRES_DB/USER/PASSWORD` | | | | | ✅ |
| `MYSQL_ROOT_PASSWORD/DATABASE/USER/PASSWORD` | | | | ✅ | |
