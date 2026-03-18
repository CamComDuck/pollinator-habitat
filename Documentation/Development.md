# Development Environment Manual

## System Overview / Architecture

The Pollinator Habitat application is composed of six services that work together:

```
 User (Browser)                  Staff (Browser)
       │                                │
       ▼                                ▼
┌─────────────┐                ┌───────────────┐
│  Frontend   │                │    Portal     │
│  Next.js    │                │   Next.js     │
│  Port 3000  │                │   Port 3001   │
└──────┬──────┘                └──────┬────────┘
       │  REST API (JWT)              │  REST API
       └──────────────┬───────────────┘
                      ▼
             ┌────────────────┐
             │    Backend     │
             │  Node/Express  │
             │   Port 4000    │
             └──────┬─────────┘
                    │  Prisma ORM
                    ▼
             ┌────────────────┐
             │     MySQL      │
             │   Port 3306    │
             └────────────────┘

  (Production only)
  External Traffic → Nginx (Port 80) → Frontend / Backend
```

### Module Descriptions

- **Frontend** (Next.js, port 3000) — User-facing application. Guides visitors through an interactive pollinator route. Communicates with the backend via REST API, authenticated using JWT tokens that encode the session ID and a auto-generated PlayerID.

- **Portal** (Next.js, port 3001) — Staff-facing data collection portal. Allows staff to query and export visitor survey statistics. Communicates with the backend via REST API.

- **Backend** (Node.js/Express, port 4000) — Central REST API. Handles game logic, route progression, JWT authentication middleware, and visitor survey data. Uses Prisma ORM to read and write to MySQL.

- **MySQL** (port 3306) — Persistent database. Stores sessions, pollinator routes, route nodes, facts, player sessions, and survey data and it will soon store basic statistics about player engagements. Initialized via Prisma migrations and seeded on first startup.

- **Nginx** (port 80, production only) — Reverse proxy. Routes incoming external traffic to the frontend and backend services.

- **Shared package** (`/shared`) — Internal TypeScript types shared between the frontend and backend to ensure consistent interfaces across the application.

## Required Tools & Technologies
- Node.js (latest LTS recommended, minimum v20.19.0)
- Git
- VSCode
- Docker Desktop and engine
- Containers extension (Simplifies running Docker containers)
- Recommended to use VSCode with typescript/javascript extensions for ease of use

## Backend & Frontend

### Folder Structure Explanation and important files
```text
┣ 📂.devcontainer
┃ ┗ 📜devcontainer.json
┣ 📜.gitignore
┣ 📜Contributing.md
┣ 📂Documentation
┃ ┣ 📂pics
┃ ┃ ┣ 📜AccessibilitySettingsMenu.png
┃ ┃ ┣ 📜backendtests.png
┃ ┃ ┣ 📜CollectionCount.png
┃ ┃ ┣ 📜CollectionPage.png
┃ ┃ ┣ 📜dev_environment.png
┃ ┃ ┣ 📜DirectionBar.png
┃ ┃ ┣ 📜folders.png
┃ ┃ ┣ 📜FrontendTestingScreenshot.png
┃ ┃ ┣ 📜HomeButton.png
┃ ┃ ┣ 📜Pollinator_6_Legs.png
┃ ┃ ┣ 📜PollinatorArrivedAtLocation.png
┃ ┃ ┣ 📜PollinatorStart.png
┃ ┃ ┣ 📜Project1.png
┃ ┃ ┣ 📜Project2.png
┃ ┃ ┣ 📜RestartPrompt.png
┃ ┃ ┣ 📜RouteImageWorkers.png
┃ ┃ ┗ 📜StartScreenNew.png
┃ ┣ 📜Contributing.md
┃ ┣ 📜Deployment.md
┃ ┣ 📜Development.md
┃ ┣ 📜README.md
┃ ┗ 📜User.md
┣ 📂Pollinator-Habitat
┃ ┣ 📂backend
┃ ┃ ┣ 📂coverage
┃ ┃ ┣ 📂generated
┃ ┃ ┣ 📂JsonDataBackups
┃ ┃ ┃ ┣ 📜FactNodes.json
┃ ┃ ┃ ┣ 📜RouteNodes.json
┃ ┃ ┃ ┗ 📜Routes.json
┃ ┃ ┣ 📂prisma
┃ ┃ ┃ ┣ 📂migrations
┃ ┃ ┃ ┃ ┣ 📂20260224061121_init
┃ ┃ ┃ ┃ ┃ ┗ 📜migration.sql
┃ ┃ ┃ ┃ ┣ 📂20260316200703_add_survey_fields
┃ ┃ ┃ ┃ ┃ ┗ 📜migration.sql
┃ ┃ ┃ ┃ ┗ 📜migration_lock.toml
┃ ┃ ┃ ┣ 📜prisma-uml.png
┃ ┃ ┃ ┣ 📜schema.prisma
┃ ┃ ┃ ┗ 📜seed.js
┃ ┃ ┣ 📂src
┃ ┃ ┃ ┣ 📂api
┃ ┃ ┃ ┃ ┣ 📂interfaces
┃ ┃ ┃ ┃ ┃ ┗ 📜api.interfaces.ts
┃ ┃ ┃ ┃ ┣ 📂Utilities
┃ ┃ ┃ ┃ ┃ ┣ 📜api.utilities.ts
┃ ┃ ┃ ┃ ┃ ┗ 📜reshape.Utilites.ts
┃ ┃ ┃ ┃ ┗ 📜api.ts
┃ ┃ ┃ ┣ 📂Back-end_types
┃ ┃ ┃ ┃ ┗ 📜route.dto.ts
┃ ┃ ┃ ┣ 📂middleware
┃ ┃ ┃ ┃ ┗ 📜middleware.ts
┃ ┃ ┃ ┣ 📂services
┃ ┃ ┃ ┃ ┣ 📂db
┃ ┃ ┃ ┃ ┃ ┣ 📂DatabaseOperationsServices
┃ ┃ ┃ ┃ ┃ ┃ ┣ 📂Create
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┗ 📜getOrCreatePlayerSession.service.ts
┃ ┃ ┃ ┃ ┃ ┃ ┣ 📂Read
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getActiveRouteForPlayerSession.service.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getchildadultdatabystartandend.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getchildnumandadultdatetoforever.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getchildnumandadulttoenddate.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getChildrenandAdultsbySession.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜GetpolinatorNames.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getsessionandPlayeridbyAdultsize.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getsessionidsandplayeridsbyfamilysize.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜getSessionsandPlayeridsbyChildSize.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┣ 📜hassession.service.ts
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┗ 📜LoadRouteDTO.service.ts
┃ ┃ ┃ ┃ ┃ ┃ ┣ 📂Transactions
┃ ┃ ┃ ┃ ┃ ┃ ┃ ┗ 📜getNextRouteForPlayerSession.service.ts
┃ ┃ ┃ ┃ ┃ ┃ ┗ 📂Update
┃ ┃ ┃ ┃ ┃ ┃   ┗ 📜addChildrenadults.ts
┃ ┃ ┃ ┃ ┃ ┗ 📜prisma.ts
┃ ┃ ┃ ┃ ┣ 📂gameServiceUtils
┃ ┃ ┃ ┃ ┃ ┣ 📜CheckSession.service.ts
┃ ┃ ┃ ┃ ┃ ┗ 📜PlayeridTypeCheck.ts
┃ ┃ ┃ ┃ ┣ 📜game.service.ts
┃ ┃ ┃ ┃ ┣ 📜route.service.ts
┃ ┃ ┃ ┃ ┗ 📜statistics.service.ts
┃ ┃ ┃ ┣ 📜app.ts
┃ ┃ ┃ ┗ 📜index.ts
┃ ┃ ┣ 📂tests
┃ ┃ ┃ ┣ 📂integration
┃ ┃ ┃ ┃ ┗ 📜routes.test.ts
┃ ┃ ┃ ┣ 📂unit
┃ ┃ ┃ ┃ ┣ 📂campbell
┃ ┃ ┃ ┃ ┃ ┣ 📜api.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜api.utilities.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜CheckSession.service.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜game.service.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜getOrCreatePlayerSession.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜index.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜prisma.test.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜reshape.utilities.test.ts
┃ ┃ ┃ ┃ ┃ ┗ 📜route.service.test.ts
┃ ┃ ┃ ┃ ┗ 📜middleware.test.ts
┃ ┃ ┃ ┗ 📜tsconfig.json
┃ ┃ ┣ 📜.env
┃ ┃ ┣ 📜.gitignore
┃ ┃ ┣ 📜Dockerfile
┃ ┃ ┣ 📜dockerfile.dev
┃ ┃ ┣ 📜package.json
┃ ┃ ┣ 📜prisma.config.ts
┃ ┃ ┣ 📜tsconfig.json
┃ ┃ ┗ 📜vitest.config.ts
┃ ┣ 📂frontend
┃ ┃ ┣ 📂public
┃ ┃ ┃ ┣ 📂fonts
┃ ┃ ┃ ┃ ┗ 📜Antonio-Regular.ttf
┃ ┃ ┃ ┣ 📂images
┃ ┃ ┃ ┃ ┣ 📜CP_TTS_Button.png
┃ ┃ ┃ ┃ ┣ 📜CPLOGO.png
┃ ┃ ┃ ┃ ┣ 📜debug_spritesheet.png
┃ ┃ ┃ ┃ ┣ 📜minusarrow.svg
┃ ┃ ┃ ┃ ┣ 📜placeholder.png
┃ ┃ ┃ ┃ ┣ 📜plusarrow.svg
┃ ┃ ┃ ┃ ┣ 📜spritesheet_transparent.png
┃ ┃ ┃ ┃ ┗ 📜spritesheet.png
┃ ┃ ┃ ┗ 📜favicon.ico
┃ ┃ ┣ 📂src
┃ ┃ ┃ ┣ 📂app
┃ ┃ ┃ ┃ ┣ 📂accessibility
┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┃ ┣ 📂home
┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┃ ┣ 📂pollinator-collection
┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┃ ┣ 📂redirecting
┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┃ ┣ 📂route
┃ ┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┃ ┣ 📂services
┃ ┃ ┃ ┃ ┃ ┣ 📜jwtService.ts
┃ ┃ ┃ ┃ ┃ ┣ 📜routeService.ts
┃ ┃ ┃ ┃ ┃ ┗ 📜surveyStorageService.ts
┃ ┃ ┃ ┃ ┣ 📜components.tsx
┃ ┃ ┃ ┃ ┣ 📜globals.css
┃ ┃ ┃ ┃ ┣ 📜layout.tsx
┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┣ 📜global.d.ts
┃ ┃ ┃ ┗ 📜middleware.ts
┃ ┃ ┣ 📂testing
┃ ┃ ┃ ┣ 📂UAT
┃ ┃ ┃ ┃ ┣ 📜OneTimePartyASizeSurvey.test.tsx
┃ ┃ ┃ ┃ ┣ 📜PollinatorCollection.test.tsx
┃ ┃ ┃ ┃ ┗ 📜RepeatableRoutePlay.test.tsx
┃ ┃ ┃ ┣ 📜AccessibilityPage.test.tsx
┃ ┃ ┃ ┣ 📜HomePage.test.tsx
┃ ┃ ┃ ┣ 📜jwtService.test.tsx
┃ ┃ ┃ ┣ 📜Layout.test.tsx
┃ ┃ ┃ ┣ 📜Middleware.test.tsx
┃ ┃ ┃ ┣ 📜PollinatorCollectionPage.test.tsx
┃ ┃ ┃ ┣ 📜RedirectPage.test.tsx
┃ ┃ ┃ ┣ 📜RootPage.test.tsx
┃ ┃ ┃ ┣ 📜RootPageAPI.test.tsx
┃ ┃ ┃ ┣ 📜RoutePageFlow.test.tsx
┃ ┃ ┃ ┣ 📜routeService.test.tsx
┃ ┃ ┃ ┣ 📜setup.ts
┃ ┃ ┃ ┗ 📜surveyStorageService.test.tsx
┃ ┃ ┣ 📜.gitignore
┃ ┃ ┣ 📜Dockerfile
┃ ┃ ┣ 📜dockerfile.dev
┃ ┃ ┣ 📜eslint.config.mjs
┃ ┃ ┣ 📜next-env.d.ts
┃ ┃ ┣ 📜next.config.mjs
┃ ┃ ┣ 📜package.json
┃ ┃ ┣ 📜postcss.config.mjs
┃ ┃ ┣ 📜README.md
┃ ┃ ┣ 📜tsconfig.json
┃ ┃ ┗ 📜vitest.config.ts
┃ ┣ 📂mysql-init
┃ ┃ ┗ 📜create_shadow.sql
┃ ┣ 📂nginx
┃ ┃ ┗ 📜nginx.conf
┃ ┣ 📂portal
┃ ┃ ┣ 📂public
┃ ┃ ┃ ┣ 📂images
┃ ┃ ┃ ┃ ┣ 📜CP_Wordmark.png
┃ ┃ ┃ ┃ ┣ 📜CPLOGO.png
┃ ┃ ┃ ┃ ┗ 📜favicon.ico
┃ ┃ ┃ ┣ 📜minusarrow.svg
┃ ┃ ┃ ┗ 📜plusarrow.svg
┃ ┃ ┣ 📂src
┃ ┃ ┃ ┣ 📂app
┃ ┃ ┃ ┃ ┣ 📜components.tsx
┃ ┃ ┃ ┃ ┣ 📜globals.css
┃ ┃ ┃ ┃ ┣ 📜layout.tsx
┃ ┃ ┃ ┃ ┗ 📜page.tsx
┃ ┃ ┃ ┗ 📂services
┃ ┃ ┃   ┣ 📜fetchService.ts
┃ ┃ ┃   ┗ 📜inputValidator.ts
┃ ┃ ┣ 📂testing
┃ ┃ ┃ ┣ 📂UAT
┃ ┃ ┃ ┃ ┗ 📜ExportSearchResults.test.tsx
┃ ┃ ┃ ┣ 📜inputValidator.test.tsx
┃ ┃ ┃ ┣ 📜layout.test.tsx
┃ ┃ ┃ ┣ 📜portalFunction.test.tsx
┃ ┃ ┃ ┣ 📜portalStructure.test.tsx
┃ ┃ ┃ ┗ 📜setup.ts
┃ ┃ ┣ 📜.gitignore
┃ ┃ ┣ 📜Dockerfile
┃ ┃ ┣ 📜dockerfile.dev
┃ ┃ ┣ 📜eslint.config.mjs
┃ ┃ ┣ 📜next-env.d.ts
┃ ┃ ┣ 📜next.config.ts
┃ ┃ ┣ 📜package.json
┃ ┃ ┣ 📜postcss.config.mjs
┃ ┃ ┣ 📜README.md
┃ ┃ ┣ 📜tsconfig.json
┃ ┃ ┗ 📜vitest.config.ts
┃ ┣ 📂shared
┃ ┃ ┣ 📂data
┃ ┃ ┃ ┗ 📜Routes.json
┃ ┃ ┣ 📜index.js
┃ ┃ ┣ 📜tsconfig.json
┃ ┃ ┣ 📜types.js
┃ ┃ ┗ 📜types.ts
┃ ┣ 📜.dockerignore
┃ ┣ 📜docker-compose.dev.yml
┃ ┣ 📜docker-compose.yml
┃ ┣ 📜package.json
┃ ┗ 📜tsconfig.base.json
┗ 📜README.md


```
### Tech Stack
This project uses Next.JS and React for the frontend and Node/Express for the backend. This project uses Mysql and Prisma for the database operations. 

### Clone Repository

- Fork this repository first, then clone the copies: [https://github.com/campbell-r-e/Pollinator-Habitat-main-repo.git](https://github.com/campbell-r-e/Pollinator-Habitat-main-repo.git)
- Do not download the repository, it should be cloned using the command line, GitHub, or otherwise connected to Git
- Ensure the cloned repository is placed into an empty folder
- Command line command: ```git clone https://github.com/campbell-r-e/Pollinator-Habitat-main-repo.git```

### Install Dependencies

- Install Node.js, following the directions for the local OS: [https://nodejs.org/en/download](https://nodejs.org/en/download)
- Latest LTS is recommended; minimum v20.19.0
- After Node.js is installed, run ```npm install``` once from the root workspace folder:
    - ```/Pollinator-Habitat-Main-Repo/Pollinator-Habitat/```
- This installs all dependencies for the backend, frontend, portal, and shared packages via npm workspaces. No need to run `npm install` in each subfolder separately.



## Replicating the Development Environment with Docker

Docker allows for running the full development environment (frontend, backend,database and Data Collection Portal) without installing Node.js or configuring anything manually. The `docker-compose.dev.yml` file builds all services front and back ends and database and Portal. 

### Docker Dev Setup

- Refer to [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/) for how to setup and install Docker
- This project runs six services: frontend, backend, portal, MySQL database, a one-time migrate/seed container, and an nginx reverse proxy
- To open a Docker container, use the following commands:
    - ```cd Pollinator-Habitat```
    - ```docker compose -f docker-compose.dev.yml build --no-cache```
    - ```docker compose -f docker-compose.dev.yml up```
- To shutdown a Docker container, run the following command:
    - ```docker compose -f docker-compose.dev.yml down ```
- Docker desktop app must be open to run the containers
- To verify Docker is setup correctly, run the following command:
    - ```docker ps```

### How It Works
- **Frontend container:** runs on [http://localhost:3000](http://localhost:3000)
- **Backend container:** runs on [http://localhost:4000](http://localhost:4000)
- **Portal container:** runs on [http://localhost:3001](http://localhost:3001)
- Dependencies are installed inside the containers
- The local code is mounted into the containers so changes should update instantly

### To Access / See Session IDs

After running `docker compose -f docker-compose.dev.yml up`, wait a few moments for the backend to finish starting, then open a new terminal and run:

```
docker logs pollinator-backend-dev
```

The backend logs will print the session ID .

## Testing – How to Run Tests

### Test the Development Environment

The project can be locally viewed and interacted with at [http://localhost:3000](http://localhost:3000) on any web browser. All npm dependencies are chained properly so each command works across root, frontend, and backend. From the test commands terminal output, the test coverage percent is visible for all files. The table shows files that need more test coverage in yellow and files with little or no coverage in red. 

#### Run Frontend Tests

```
npm run test
```

#### Run All Tests With Coverage (Frontend + Backend + Portal)

```
npm run test:coverage
```

#### Target-Specific Test Commands

Run tests for a specific area of the project:

```
npm run test:frontend
npm run test:backend
npm run test:portal
```

Run coverage for a specific target:

```
npm run test:coverage:frontend
npm run test:coverage:backend
npm run test:coverage:portal
```
