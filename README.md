# Pollinator Habitat

## Summary

Pollinator Habitat is an interactive web application built for **Conner Prairie's** *Food, Farm, and Energy Experience*. The app digitizes and improves Conner Prairie's existing paper-based pollinator activity, guiding visitors through a dichotomous key route walk on their own mobile device — no app store install required. At the end of each route, visitors discover which pollinator they were secretly assigned and learn facts about it.

A companion **Admin Portal** lets Conner Prairie staff search, review, and export visitor participation data and survey results for grant reporting and program analysis, without collecting any personally identifiable information.

---

## Team Members

| Name | GitHub |
|---|---|
| Camden Hovell | [@CamComDuck](https://github.com/CamComDuck) |
| Campbell Reed | [@campbell-r-e](https://github.com/campbell-r-e) |
| C.J. Fulciniti | [@cjfulciniti](https://github.com/cjfulciniti) |
| Evan Kiser | [@EvanKiser](https://github.com/EvanKiser) |

## Client Partner

**Company:** Conner Prairie  
**Contact:** Ronda Hamm

---

## Source Code Repository

| Repository | Description |
|---|---|
| [Pollinator-Habitat-main-repo](https://github.com/campbell-r-e/Pollinator-Habitat-main-repo) | Full application source code — frontend, portal, backend, database, Docker setup |

---

## Project Overview Documents

| Document | Description |
|---|---|
| [Project Description](ProjectDescription.md) | High-level feature list, requirements, and constraints |
| [For Future Teams](For%20Future.md) | Known issues and improvement opportunities left for future teams |

---

## Documentation

High-level guides for users, developers, and administrators.

| Document | Description |
|---|---|
| [User Documentation](Documentation/User.md) | End-user guide and admin portal usage walkthrough |
| [Development Setup](Documentation/Development.md) | Developer environment, folder structure, tech stack, and test commands |
| [Deployment Guide](Documentation/Deployment.md) | Production deployment, Docker setup, environment variables, troubleshooting |

---

## Technical Documentation

Detailed source code documentation organized by audience. Full index: [docs/README.md](docs/README.md)

### For Conner Prairie Staff

| Document | Description |
|---|---|
| [Client Guide](docs/Client/CLIENT_GUIDE.md) | What the game is, how to run an event, how to use the portal, FAQs |

### For IT / System Administrators

| Document | Description |
|---|---|
| [Admin Guide](docs/Admin/ADMIN_GUIDE.md) | Deployment, Docker, networking, backups, troubleshooting, security |

### For Content Contributors

| Document | Description |
|---|---|
| [Updating Pollinator Images](docs/Contributor/UPDATING_POLLINATOR_IMAGES.md) | Step-by-step guide for replacing pollinator artwork in the spritesheet |

### For Developers

| Document | Description |
|---|---|
| [Handoff](docs/Developer/HANDOFF.md) | **Start here** — current state, open work, gotchas, quick-start |
| [Overview](docs/Developer/OVERVIEW.md) | All 3 apps, all pages, all API endpoints, JWT flow |
| [API Specification](docs/Developer/API_SPECIFICATION.md) | All 34 endpoints with request/response schemas, auth, error codes |
| [Database Schema](docs/Developer/DATABASE_SCHEMA.md) | 7-table schema, ER relationships, migration history |
| [Docker Setup](docs/Developer/DOCKER_SETUP.md) | All 4 compose files, Dockerfiles, nginx config, troubleshooting |
| [Environment Variables](docs/Developer/ENV_VARIABLES.md) | Every environment variable across all services |
| [Backend Flow](docs/Developer/backend-flow.md) | Backend architecture — startup, routing, handlers, services |
| [Frontend Flow](docs/Developer/frontend-flow.md) | Frontend pages, services, and all 19 components |
| [Portal Flow](docs/Developer/PORTAL_FLOW.md) | Portal state, logic, components, fetch services |
| [Accessibility](docs/Developer/ACCESSIBILITY.md) | localStorage schema, high contrast CSS, TTS, font size slider |
| [Adding Routes](docs/Developer/ADDING_ROUTES.md) | How to add new pollinator routes to the database |
| [Shared Types](docs/Developer/SHARED_TYPES.md) | Route/RouteNode/FactNode interfaces, spritesheet coordinate system |
| [Backend Services](docs/Developer/BACKEND_SERVICES.md) | Service layer — game, route, statistics, DB operations |
| [Next Route Flow](docs/Developer/NEXT_ROUTE_FLOW.md) | Route deduplication algorithm and concurrency handling |
| [Route Statistics Spec](docs/Developer/ROUTE_STATISTICS_SPEC.md) | Feature spec for 10 route metrics and 20 endpoints |
| [Route Stats API Reference](docs/Developer/ROUTE_STATS_API_REFERENCE.md) | API reference for all 20 statistics endpoints |
| [Test Documentation](docs/Developer/TEST_DOCUMENTATION.md) | How to run tests; per-test docs for all 37 test files |
| [MySQL License Issue](docs/Developer/MYSQL_LICENSE_ISSUE.md) | Why PostgreSQL is required for non-academic production deployment |

---

## Presentations

| File | Description |
|---|---|
| [Design Day](Presentations/DesignDay.pdf) | Design Day presentation |
| [Iteration 1](Presentations/IterationDay_1.pdf) | First iteration day presentation |
| [Iteration 2](Presentations/IterationDay_2.pdf) | Second iteration day presentation |
| [Final Poster](Presentations/FinalPoster.pdf) | Final design day poster |

---

## Design Documents

| Document | Description |
|---|---|
| [Architecture](Design/Architecture.md) | Back-end and front-end software architecture overview |
| [Business Requirements](Design/BusinessRequirements.md) | BR1 and BR2 — how the project meets Conner Prairie's organizational goals |
| [Domain Model](Design/DomainModel.md) | Class diagram of project entities, attributes, and relationships |
| [Use Cases](Design/UseCases.md) | UC1–UC5 — how each type of user interacts with the system |
| [Requirements](Design/Requirements.md) | Full functional and non-functional requirements by priority |
| [Tech Stack](Design/TechStack.md) | Languages and frameworks used and their roles |
| [Prototype](Design/Prototype.md) | Interactive digital mock-up of the front-end game |

---

## Discovery

| Document | Description |
|---|---|
| [Initial Discovery Meeting](Discovery/2025-09-23.md) | Summary of first meeting with Ronda Hamm at Conner Prairie |
| [Discovery Meeting Notes](Discovery/Discovery_Meeting_Notes) | Handwritten notes from each team member digitized |

---

## Meeting Minutes

### Client Partner Meetings

| Date | Notes |
|---|---|
| [2025-09-29](MeetingMinutes/ClientPartner/2025-09-29.md) | |
| [2025-10-27](MeetingMinutes/ClientPartner/2025-10-27.md) | |
| [2025-12-01](MeetingMinutes/ClientPartner/2025-12-01.md) | |
| [2026-01-29](MeetingMinutes/ClientPartner/2026-01-29.md) | |
| [2026-03-13](MeetingMinutes/ClientPartner/2026-03-13.md) | |
| [2026-04-16](MeetingMinutes/ClientPartner/2026-04-16.md) | Final client meeting — deployment feedback and handoff |

### Team Meetings

| Date | Notes |
|---|---|
| [2025-09-26](MeetingMinutes/Team/2025-09-26.md) | |
| [2025-09-30](MeetingMinutes/Team/2025-09-30.md) | |
| [2025-10-09](MeetingMinutes/Team/2025-10-09.md) | |
| [2025-10-16](MeetingMinutes/Team/2025-10-16.md) | |
| [2025-10-23](MeetingMinutes/Team/2025-10-23.md) | |
| [2025-10-30](MeetingMinutes/Team/2025-10-30.md) | |
| [2025-11-04](MeetingMinutes/Team/2025-11-04.md) | |
| [2025-11-06](MeetingMinutes/Team/2025-11-06.md) | |
| [2025-11-06 (in-class)](MeetingMinutes/Team/2025-11-06_during-class-time.md) | |
| [2025-11-20](MeetingMinutes/Team/2025-11-20.md) | |
| [2025-11-25](MeetingMinutes/Team/2025-11-25.md) | |
| [2025-11-25 (in-class)](MeetingMinutes/Team/2025-11-25_during-class-time.md) | |
| [2025-12-02 (in-class)](MeetingMinutes/Team/2025-12-02_during-class-time.md) | |
| [2026-01-13](MeetingMinutes/Team/2026-01-13.md) | |
| [2026-01-20](MeetingMinutes/Team/2026-01-20.md) | |
| [2026-01-27](MeetingMinutes/Team/2026-01-27.md) | |
| [2026-01-29](MeetingMinutes/Team/2026-01-29.md) | |
| [2026-02-03](MeetingMinutes/Team/2026-02-03.md) | |
| [2026-02-10](MeetingMinutes/Team/2026-02-10.md) | |
| [2026-02-17](MeetingMinutes/Team/2026-02-17.md) | |
| [2026-02-26](MeetingMinutes/Team/2026-02-26.md) | |
| [2026-03-10](MeetingMinutes/Team/2026-03-10.md) | |
| [2026-03-17](MeetingMinutes/Team/2026-03-17.md) | |
| [2026-03-24](MeetingMinutes/Team/2026-03-24.md) | |
| [2026-03-31](MeetingMinutes/Team/2026-03-31.md) | |
| [2026-04-07](MeetingMinutes/Team/2026-04-07.md) | |
| [2026-04-16](MeetingMinutes/Team/2026-04-16.md) | |
| [2026-04-21](MeetingMinutes/Team/2026-04-21.md) | Final team meeting |
