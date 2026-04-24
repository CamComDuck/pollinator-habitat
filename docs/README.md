# Pollinator Habitat — Documentation Index

Documentation is organized by audience. Find your role below and start there.

---

## For Conner Prairie Staff (Event Runners)

You run events, hand out QR codes, and look up party size data in the portal after events.

| Document | What it covers |
|---|---|
| [Client/CLIENT_GUIDE.md](Client/CLIENT_GUIDE.md) | What the game is, how to run an event, how to use the portal, FAQs |

---

## For IT / System Administrators

You deploy the system, manage the server, generate QR codes, and handle backups.

| Document | What it covers |
|---|---|
| [Admin/ADMIN_GUIDE.md](Admin/ADMIN_GUIDE.md) | Deployment, Docker, networking, session management, backups, troubleshooting, security |

---

## For Content Contributors

You update pollinator illustrations without writing code.

| Document | What it covers |
|---|---|
| [Contributor/UPDATING_POLLINATOR_IMAGES.md](Contributor/UPDATING_POLLINATOR_IMAGES.md) | Step-by-step guide for replacing a pollinator image in the spritesheet |

---

## For Software Developers

You write, test, and deploy code. Start with the Overview, then go to the specific guide for the area you're working in.

### Getting oriented
| Document | What it covers |
|---|---|
| [Developer/HANDOFF.md](Developer/HANDOFF.md) | **Start here if you're taking over** — current state, open work, gotchas, quick-start |
| [Developer/OVERVIEW.md](Developer/OVERVIEW.md) | All 3 apps, all pages, all API endpoints, game loop, JWT flow, how to run |
| [Developer/ENV_VARIABLES.md](Developer/ENV_VARIABLES.md) | Every environment variable across all services |

### Backend
| Document | What it covers |
|---|---|
| [Developer/backend-flow.md](Developer/backend-flow.md) | Every layer of the backend — startup, routing, handlers, services, Docker |
| [Developer/API_SPECIFICATION.md](Developer/API_SPECIFICATION.md) | All 34 endpoints — exact request/response schemas, auth, error codes |
| [Developer/DATABASE_SCHEMA.md](Developer/DATABASE_SCHEMA.md) | 7-table schema, ER relationships, migration history, seed data |
| [Developer/BACKEND_SERVICES.md](Developer/BACKEND_SERVICES.md) | game.service, route.service, utilities, DB operation classes |
| [Developer/NEXT_ROUTE_FLOW.md](Developer/NEXT_ROUTE_FLOW.md) | Deep trace of route deduplication — cycle algorithm, concurrency handling |

### Frontend
| Document | What it covers |
|---|---|
| [Developer/frontend-flow.md](Developer/frontend-flow.md) | Page-by-page flow, all services (jwtService, routeService, surveyStorageService), all 19 components |
| [Developer/SHARED_TYPES.md](Developer/SHARED_TYPES.md) | Route/RouteNode/FactNode interfaces, spritesheet coordinate system |
| [Developer/ACCESSIBILITY.md](Developer/ACCESSIBILITY.md) | localStorage schema, High Contrast CSS, TTS setting, Font Size Slider |

### Portal
| Document | What it covers |
|---|---|
| [Developer/PORTAL_FLOW.md](Developer/PORTAL_FLOW.md) | Portal state/logic, all components, fetch services, env vars, testing |

### Infrastructure
| Document | What it covers |
|---|---|
| [Developer/DOCKER_SETUP.md](Developer/DOCKER_SETUP.md) | All 4 compose files, all Dockerfiles, Nginx config, env vars, troubleshooting |

### Content & Routes
| Document | What it covers |
|---|---|
| [Developer/ADDING_ROUTES.md](Developer/ADDING_ROUTES.md) | Seed file structure, spritesheet coordinates, adding routes, re-seeding |

### Testing
| Document | What it covers |
|---|---|
| [Developer/TEST_DOCUMENTATION.md](Developer/TEST_DOCUMENTATION.md) | How to run tests; per-test documentation for all 37 test files |

### Route statistics
| Document | What it covers |
|---|---|
| [Developer/ROUTE_STATISTICS_SPEC.md](Developer/ROUTE_STATISTICS_SPEC.md) | Feature spec — 10 route metrics, 20 endpoints ✅ backend complete, portal UI ⏳ pending |
| [Developer/ROUTE_STATS_API_REFERENCE.md](Developer/ROUTE_STATS_API_REFERENCE.md) | API reference for all 20 statistics endpoints |

### Architecture decisions
| Document | What it covers |
|---|---|
| [Developer/MYSQL_LICENSE_ISSUE.md](Developer/MYSQL_LICENSE_ISSUE.md) | Why PostgreSQL is required for production deployment |

---

## Folder Structure

```
docs/
  README.md                    ← this file
  Developer/                   ← software developers
  Admin/                       ← IT / operations staff
  Client/                      ← Conner Prairie event staff
  Contributor/                 ← non-technical content editors
```
