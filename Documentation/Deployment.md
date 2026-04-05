# Deploying the Pollinator Habitat Application

## Valid Session Codes

To retrieve valid session IDs:
1. Start the containers with docker compose up
2. Wait a few moments for the server to finish starting
3. Open a new terminal and navigate to the backend folder:
```bash
cd backend
```
4. Run:

Development:
```bash
docker logs pollinator-backend-dev
```
Production:
```bash
docker logs pollinator-backend
```
    
## Prerequisites 
### Server Requirements
- **Operating System:** Linux (Any Linux LTS that is still supported) or macOS  
- **CPU:** Dual-core or better  
- **RAM:** Minimum 4 GB (8 GB recommended for Docker)
- **Storage:** 30 GB free disk space  
- **Network:** Internet access to install Node modules and Docker images
- **Database:** MySQL or MariaDB (used via Prisma ORM)

Firewall ports 80, 3000, 3001, and 4000 need to be open. Recommended deployment environment is a machine running this in Docker. 

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

## Building and Compiling

- Set Any Environment Dependent Variables Before Deploying
    - Never modify inside node_modules. Environment variables (e.g. DATABASE_URL) are set in the docker-compose files and do not need to be changed for local development.
- Authentication API Endpoint
    - JWT is Used for Authentication and it is by a SessionId in the JWT. 
- API Base Url
    - http://localhost:4000

### File and Folder Placement
Clone the repository into `/opt/pollinator-habitat` (Linux) or `~/Documents/Pollinator-Habitat` (macOS/Windows).  Might require sudo in Linux and Unix like Systems and Admin rights on Windows.
Do NOT move the frontend, backend, or portal out of the Pollinator-Habitat folder — it will cause it not to work with Docker.

## Installing and Setting Up Docker

Run docker compose files from the root of the project. There are two compose files:

- **`docker-compose.dev.yml`** — for development. Supports hot reload and mounts source files as volumes. Accessible via localhost only.
- **`docker-compose.yml`** — for production. Builds optimized containers intended for deployment. Accessible over the network or via localhost.

Follow these steps to install and configure **Docker Desktop** or **Docker Engine**.

### Check for Existing Installation

Before installing, check if Docker is already installed:

```bash
docker --version
docker compose version
```

### Docker Development Container Setup 


To build and run containers issue this command from the root of the project 

```sh
docker compose -f docker-compose.dev.yml build
docker compose -f docker-compose.dev.yml up
```
Or to rebuild automatically on changes:
```sh
docker compose -f docker-compose.dev.yml up --build
```

Frontend runs on → http://localhost:3000
Backend runs on → http://localhost:4000
Portal runs on → http://localhost:3001
to stop containers

```sh
docker compose -f docker-compose.dev.yml down
```

### Docker Production Container Setup 

To build and run containers issue this command from the root of the project 

```sh
docker compose -f docker-compose.yml build
docker compose -f docker-compose.yml up
```
Or to rebuild automatically on changes:
```sh
docker compose -f docker-compose.yml up --build
```

Frontend runs on → http://localhost:3000
Backend runs on → http://localhost:4000
Portal runs on → http://localhost:3001
to stop containers

```sh
docker compose -f docker-compose.yml down
```
## Errors, Troubleshooting, and Maintenance Guide

This short guide explains how to fix the most common problems and keep the Pollinator Habitat web application running smoothly.

### Common Issues

#### Missing Dependencies
If you see errors like “module not found” or “cannot find module”:
```bash
npm install
```
If a container fails to start and you see:
Error: listen EADDRINUSE
It means something is already using that port. Stop the containers and check what is using the port:
```bash
docker compose -f docker-compose.dev.yml down
lsof -i :4000
```

#### Common Issues
- Incorrect folder structure
- Port already in use
- Backend cannot bind to port 4000
- Frontend cannot reach backend API

Fix port issues:
sudo pkill -f node
lsof -i :3000
lsof -i :3001
lsof -i :4000

#### What are the most critical pieces that can fail
- Database
- Environment variables when used
- Backend API crash
- Frontend build errors
- Docker image build failures


#### Failing Builds

- Rebuild (Development) without cache: ```docker compose -f docker-compose.dev.yml build --no-cache```
- Rebuild and run (Development): ```docker compose -f docker-compose.dev.yml up --build```
- Rebuild (Production) without cache: ```docker compose -f docker-compose.yml build --no-cache```
- Rebuild and run (Production): ```docker compose -f docker-compose.yml up --build```
- If frontend fails:
    - Delete “node_modules” inside /frontend
    - Run: ```npm install --prefix frontend```
- If backend fails:
    - Delete “node_modules” inside /backend
    - Run: ```npm install --prefix backend```
- If portal fails:
    - Delete “node_modules” inside /portal
    - Run: ```npm install --prefix portal```

#### Check If Services Are Actually Running
```docker ps```


### Production Start/Stop
```sh
docker compose -f docker-compose.yml up
docker compose -f docker-compose.yml down
```

### Quick Health Check

Frontend, Open in browser: [http://localhost:3000](http://localhost:3000)

####  Where Logs Are Found
##### 1. Docker Logs

Development containers:
```docker compose -f docker-compose.dev.yml logs -f```

Production containers:
```docker compose -f docker-compose.yml logs -f```

Specific service:
```docker compose -f docker-compose.dev.yml logs -f backend```
```docker compose -f docker-compose.dev.yml logs -f frontend```
```docker compose -f docker-compose.dev.yml logs -f portal```

