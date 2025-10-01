# Architecture Overview #
This document serves as a critical, living template designed to equip agents with a rapid and comprehensive understanding of the codebase's architecture, enabling efficient navigation and effective contribution from day one. Update this document as the codebase evolves.

## 1. Project Structure ##
The Pollinator Habitat project will be using a Monolith architecture to keep hosting costs low and keep the project structure simple. This project has four folders under the root one 
for the Front End and one for the Back end code and a folder for documentation and a folder for scripts that will hold database seeds and other needed scripts and files. 


## Project Structure

```text
[Project Root]/
├── backend/              # Contains all server-side code and APIs
│   ├── src/              # Main source code for backend services
│   │   ├── api/          # API endpoints and controllers
│   │   ├── services/     # Business logic and service implementations
│   │   ├── models/       # Database models/schemas
│   │   └── utils/        # Backend utility functions
│   ├── config/           # Backend configuration files
│   ├── tests/            # Backend unit and integration tests
│   
├── frontend/             # Contains all client-side code for user interfaces
│   ├── src/              # Main source code for frontend applications
│   │   ├── components/   # Reusable UI components
│   │   ├── pages/        # Application pages/views
│   │   ├── assets/       # Images, fonts, and other static assets
│   │   ├── services/     # Frontend services for API interaction
│   │   └── store/        # State management (e.g., Redux, Vuex, Context API)
│   ├── public/           # Publicly accessible assets (e.g., index.html)
│   ├── tests/            # Frontend unit and E2E tests
│   └── package.json      # Frontend dependencies and scripts
|
│   
│   
├── docs/                 # Project documentation (e.g., API docs, setup guides)
├── scripts/              # Automation scripts (e.g., deployment, data seeding)
|
├── .github/              # GitHub Actions or other CI/CD configurations
├── .gitignore            # Specifies intentionally untracked files to ignore
├── README.md             # Project overview and quick start guide
|
```


## 2. High-Level System Diagram ##
Provide a simple block diagram (e.g., a C4 Model Level 1: System Context diagram, or a basic component diagram) or a clear text-based description of the major components and their interactions. Focus on how data flows, services communicate, and key architectural boundaries.
 
[User] <--> [Frontend Application] <--> [Backend Service 1] <--> [Database 1]
[Administrator] <--> [Frontend Application] <--> [Backend Service 2] <--> [Database 2]    

User → Frontend: sessionIdCode, player actions

Frontend → Backend: cardId, game state
Frontend → Backend: StatsUser,statsPassword
Backend → DB: pollinator facts, statistics, admin credentials  
Backend → Frontend: pollinator facts, statistics


## 3. Core Components ##


### 3.1. Frontend ###

Name: [Polinattor Habitat Webapp game]

Description: The Front End will allow the players to play the Pollinator Habitat game as well as have a route for Admins to be able to download the game statistics and it will allow team leads to create sessions of the game and generate QR codes for the players to join with. 

Technologies: [React and Next.js]

Deployment: [TBD] Client is unsure. 

### 3.2. Backend Services



#### 3.2.1. [Service Name 1]

Name: [Pollinator Habitat Card generator]

Description: [Generate random cards for users and feed card data from database to the user]

Technologies: [Node.js,Express js,Typescript,Prisma]

Deployment: [(TBD)]

#### 3.2.2. [Service Name 2]

Name: [Create Sessions]

Description: [Create sessions and generate qr codes for the users to play]

Technologies: [Typescript,prisma,node.js(Express)]

Deployment: [TBD]

## 4. Data Stores


### 4.1. [Data Store Type 1]

Name: [Game database]

Type: [MySql Relational Database]

Purpose: [To store card data for the users and game stats as well as account management]

Key Schemas/Collections: [Pollinator,pollinator facts,Pollinator questions,Statistics,Accounts,Permissions]

## 5. External Integrations / APIs



Service Name 1: None yet

Purpose: None yet

Integration Method: None yet

## 6. Deployment & Infrastructure

Cloud Provider: [TBD]

Key Services Used: [Static Website,Mysql Database,Node.js instance]

CI/CD Pipeline: [GitHub Actions]

Monitoring & Logging: [e.g., Prometheus, Grafana, CloudWatch, Stackdriver, ELK Stack]

## 7. Security Considerations

(Highlight any critical security aspects, authentication mechanisms, or data encryption practices.)

Authentication: [JWT]

Authorization: [RBAC]

Data Encryption: [TLS in transit]

Key Security Tools/Practices: [regular security audits]

## 8. Development & Testing Environment

Local Setup Instructions:[Setup Directions]( https://github.com/campbell-r-e/Pollinator-Habitat-main-repo/blob/main/Contributing.md )

Testing Frameworks: [Jest]

Code Quality Tools: [ESLint]

## 9. Future Considerations / Roadmap

(Briefly note any known architectural debts, planned major changes, or significant future features that might impact the architecture.)

[e.g., "Migrate from monolith to microservices."]

[e.g., "Implement event-driven architecture for real-time updates."]

## 10. Project Identification

Project Name: [Pollinator Habitat]

Repository URL: [https://github.com/campbell-r-e/Pollinator-Habitat-main-repo]

Primary Contact/Team: [Camden Hovell]

Date of Last Update: [2025-09-30]

## 11. Glossary / Acronyms

Define any project-specific terms or acronyms.)

[Acronym]: [Full Definition]

[Term]: [Explanation]
