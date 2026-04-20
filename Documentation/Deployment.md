# Deploying the Pollinator Habitat Application

## Prerequisites 
### Server Requirements
- **Operating System:** Linux (any supported LTS), macOS, or Windows 10/11 with WSL2 and Docker Desktop  
- **CPU:** Dual-core or better  
- **RAM:** Minimum 4 GB (8 GB recommended for Docker)  
- **Storage:** 30 GB free disk space  
- **Network:** Internet access to pull Docker images and npm packages  
- **Docker:** Docker Engine or Docker Desktop with Compose v2  
- **Database:** MySQL 8.4 or PostgreSQL 18 — both run as Docker containers; no separate installation needed  
- **Node.js:** >= 24.0.0 (only required for running outside Docker)  
- **npm:** >= 10.0.0 (only required for running outside Docker)  

Firewall ports **80** and **3001** must be open for production. In development, ports **80** (frontend), **3001** (portal), and **4000** (backend API) must be reachable from localhost. The backend is **not** exposed externally in production — nginx proxies all traffic.

## Docker Memory Allocation (macOS & Windows)

Docker Desktop limits the RAM available to containers.

Recommended:
- Minimum: 4 GB allocated to Docker
- Preferred: 8 GB or higher 

How to change memory settings in Docker Desktop:

macOS / Windows:
1. Open Docker Desktop
2. Go to Settings (or Preferences on macOS)
3. Select Resources
4. Increase Memory slider to 4–8 GB
5. Apply & Restart

## Environment Variables

Before running any compose file, create a `.env` file in the project root (next to the compose files) with at minimum:

```env
JWT_SECRET=your-secret-here
```

For production MySQL, also set:
```env
MYSQL_ROOT_PASSWORD=...
MYSQL_DATABASE=pollinator
MYSQL_USER=pollinator
MYSQL_PASSWORD=...
DATABASE_URL=mysql://pollinator:<password>@mysql:3306/pollinator
SHADOW_DATABASE_URL=mysql://pollinator:<password>@mysql:3306/pollinator_shadow
```

For production PostgreSQL, copy and edit `.env.pg.example` in the project root.

Development compose files use hardcoded credentials and do not require a `.env` file, except that `JWT_SECRET` must still be set.

> Never modify files inside `node_modules`. All environment-dependent variables are set in the compose files or `.env` and do not need to be changed for local development beyond setting `JWT_SECRET`.

## Building and Compiling

### File and Folder Placement
Clone the repository into `/opt/pollinator-habitat` (Linux) or `~/Documents/Pollinator-Habitat` (macOS/Windows). This may require `sudo` on Linux and admin rights on Windows.  
Do **not** move `frontend`, `backend`, `portal`, or `shared` out of the project root — Docker volume mounts depend on this structure.

### Compose Files Overview

All compose commands must be run from the project root (the folder containing the compose files).

| File | Purpose | Database |
|---|---|---|
| `docker-compose.dev.yml` | Development with hot reload | MySQL |
| `docker-compose.dev.pg.yml` | Development with hot reload | PostgreSQL |
| `docker-compose.yml` | Production build | MySQL |
| `docker-compose.prod.pg.yml` | Production build | PostgreSQL |

On first startup, a `migrate` service runs automatically to apply Prisma migrations and seed the database. This runs once and exits before the backend starts.

## Installing and Setting Up Docker

Follow these steps to install and configure **Docker Desktop** or **Docker Engine**.

### Check for Existing Installation

```bash
docker --version
docker compose version
```

## Docker Development Container Setup 

### MySQL (default)

```sh
docker compose -f docker-compose.dev.yml build
docker compose -f docker-compose.dev.yml up
```
Or rebuild and run in one step:
```sh
docker compose -f docker-compose.dev.yml up --build
```

### PostgreSQL

```sh
docker compose -f docker-compose.dev.pg.yml build
docker compose -f docker-compose.dev.pg.yml up
```
Or rebuild and run in one step:
```sh
docker compose -f docker-compose.dev.pg.yml up --build
```

**Development service URLs:**

| Service | URL |
|---|---|
| Frontend | http://localhost:80 |
| Portal | http://localhost:3001 |
| Backend API | http://localhost:4000 |

To stop containers:
```sh
docker compose -f docker-compose.dev.yml down
# or for PostgreSQL:
docker compose -f docker-compose.dev.pg.yml down
```

## Docker Production Container Setup 

In production, an **nginx** reverse proxy sits in front of all services. The backend is not exposed directly — nginx routes `/api/` requests to the backend and all other traffic to the frontend or portal.

### MySQL (default)

```sh
docker compose -f docker-compose.yml build
docker compose -f docker-compose.yml up
```
Or rebuild and run in one step:
```sh
docker compose -f docker-compose.yml up --build
```

### PostgreSQL

```sh
docker compose -f docker-compose.prod.pg.yml build
docker compose -f docker-compose.prod.pg.yml up
```
Or rebuild and run in one step:
```sh
docker compose -f docker-compose.prod.pg.yml up --build
```

**Production service URLs (via nginx):**

| Service | URL |
|---|---|
| Frontend | http://\<host\>:80 |
| Portal | http://\<host\>:3001 |
| Backend API | http://\<host\>/api/ (proxied by nginx) |

To stop containers:
```sh
docker compose -f docker-compose.yml down
# or for PostgreSQL:
docker compose -f docker-compose.prod.pg.yml down
```

## Errors, Troubleshooting, and Maintenance Guide

### Common Issues

#### Missing Dependencies
If you see errors like "module not found" or "cannot find module":
```bash
npm install
```

#### Port Already in Use
If a container fails to start with `Error: listen EADDRINUSE`, something is already using that port. Stop the containers and check:
```bash
docker compose -f docker-compose.dev.yml down
lsof -i :80
lsof -i :3001
lsof -i :4000
```

To kill stray node processes:
```bash
sudo pkill -f node
```

#### What Are the Most Critical Pieces That Can Fail
- Database (MySQL or PostgreSQL container not healthy)
- Missing or incorrect `.env` / `JWT_SECRET`
- `migrate` service failing (check logs before backend starts)
- Backend API crash
- Frontend or portal build errors
- Docker image build failures
- nginx misconfiguration (production only)

#### Failing Builds

Rebuild without cache:
```bash
# Development (MySQL)
docker compose -f docker-compose.dev.yml build --no-cache
# Development (PostgreSQL)
docker compose -f docker-compose.dev.pg.yml build --no-cache
# Production (MySQL)
docker compose -f docker-compose.yml build --no-cache
# Production (PostgreSQL)
docker compose -f docker-compose.prod.pg.yml build --no-cache
```

If a specific package fails to install:
- Frontend: delete `frontend/node_modules` then run `npm install --prefix frontend`
- Backend: delete `backend/node_modules` then run `npm install --prefix backend`
- Portal: delete `portal/node_modules` then run `npm install --prefix portal`

#### Check If Services Are Running
```bash
docker ps
```

### Production Start/Stop
```sh
# MySQL
docker compose -f docker-compose.yml up -d
docker compose -f docker-compose.yml down
# PostgreSQL
docker compose -f docker-compose.prod.pg.yml up -d
docker compose -f docker-compose.prod.pg.yml down
```

### Quick Health Check

- Frontend: [http://localhost:80](http://localhost:80)  
- Portal: [http://localhost:3001](http://localhost:3001)  
- Backend (dev only): [http://localhost:4000](http://localhost:4000)

### Where Logs Are Found

#### Docker Logs

Development (MySQL):
```bash
docker compose -f docker-compose.dev.yml logs -f
docker compose -f docker-compose.dev.yml logs -f backend
docker compose -f docker-compose.dev.yml logs -f frontend
docker compose -f docker-compose.dev.yml logs -f portal
docker compose -f docker-compose.dev.yml logs -f migrate
```

Development (PostgreSQL):
```bash
docker compose -f docker-compose.dev.pg.yml logs -f
```

Production (MySQL):
```bash
docker compose -f docker-compose.yml logs -f
```

Production (PostgreSQL):
```bash
docker compose -f docker-compose.prod.pg.yml logs -f
```
