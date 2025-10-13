# [Project Name] - Context Engineering

**Multi-repository system: [Backend + Frontend(s)] architecture**

## 🚨 CRITICAL WORKFLOW ENFORCEMENT

**CLAUDE: Automatically apply context engineering for ANY development request.**

### Automatic Behaviors
1. ✅ Check documentation automatically
2. ✅ Assess complexity
3. ✅ Generate PRP for complex work (>3 files or significant logic)
4. ✅ Follow established patterns
5. ✅ Suggest relevant agents
6. ✅ Update documentation

**User works naturally - methodology applies automatically.**

---

## 📋 PROJECT TYPE & CONTEXT

### Project Classification
**Primary Type:** [Multi-Repository System / Microservices / Monorepo with multiple apps]

**Domain:** [Business domain - e.g., E-commerce, CRM, SaaS Platform]

**Scale:** [Startup / SMB / Enterprise]

**Organization:** [Company/Team Name]

### Repository Structure

This is a **multi-repository system** containing [X] interconnected applications:

```
/[project-root]/
├── [backend-repo]/        → [Backend Tech Stack] (e.g., Spring Boot, Node.js, Django)
├── [web-frontend-repo]/   → [Web Tech Stack] (e.g., React, Vue, Angular)
├── [mobile-frontend-repo]/ → [Mobile Tech Stack] (e.g., React Native, Flutter, Swift) [OPTIONAL]
├── [admin-panel-repo]/    → [Admin Tech Stack] [OPTIONAL]
└── [shared-libs]/         → [Shared code/utilities] [OPTIONAL]
```

**IMPORTANT:** All repositories share the same business domain but serve different user types:
- **Backend**: Single source of truth API for all frontends
- **Web Frontend**: [Description - e.g., Customer-facing web application]
- **Mobile Frontend**: [Description - e.g., Customer mobile app] [OPTIONAL]
- **Admin Panel**: [Description - e.g., Internal admin dashboard] [OPTIONAL]

### User Types & Access

**[User Type 1] ([Repository]):**
- **Users:** [Who uses this - e.g., Internal staff, Customers, Admins]
- **Purpose:** [What they do]
- **Authentication:** [Auth method - e.g., Azure AD, OAuth2, JWT]

**[User Type 2] ([Repository]):**
- **Users:** [Who uses this]
- **Purpose:** [What they do]
- **Authentication:** [Auth method]

---

## 🛠️ TECHNOLOGY STACK

### Backend ([repo-name])

**Framework & Core:**
- **[Framework]:** [Version] ([Language] [Version])
- **Architecture:** [Pattern - e.g., Microservices, DDD, Layered, MVC]
- **Web Server:** [e.g., Tomcat, Undertow, Nginx]
- **ORM/Database Access:** [e.g., JPA + Hibernate, Sequelize, Prisma, SQLAlchemy]
- **Database:** [e.g., PostgreSQL 14, MySQL 8, MongoDB 5]
- **API Documentation:** [e.g., Swagger/OpenAPI, Postman Collections]

**Key Dependencies:**
- [Dependency]: [Purpose]
- [Dependency]: [Purpose]

**Cloud/Infrastructure:**
- **Provider:** [AWS, Azure, GCP, On-premise]
- **Services Used:**
  - [Service]: [Purpose - e.g., S3 for file storage]
  - [Service]: [Purpose - e.g., SQS for message queuing]

**Real-time Communication (if applicable):**
- **Technology:** [e.g., WebSocket, Server-Sent Events, Socket.io]
- **Use cases:** [e.g., Live chat, notifications, real-time updates]

**Security:**
- **Authentication:** [Method]
- **Authorization:** [Pattern - e.g., RBAC, ABAC]
- **Secrets Management:** [e.g., Environment variables, Vault, Key Management Service]

**Testing:**
- **Framework:** [e.g., JUnit, Jest, pytest]
- **Test DB:** [e.g., H2 in-memory, TestContainers]

### Web Frontend ([repo-name])

**Framework & Core:**
- **[Framework]:** [Version] (e.g., React 18, Vue 3, Angular 15)
- **Language:** [e.g., TypeScript 5, JavaScript ES6+]
- **Build Tool:** [e.g., Vite, Webpack, Create React App]
- **State Management:** [e.g., Redux Toolkit, Zustand, Pinia, NgRx]
- **Data Fetching:** [e.g., TanStack Query, RTK Query, Apollo Client]
- **Routing:** [e.g., React Router, Vue Router, Angular Router]

**UI Framework:**
- **Primary:** [e.g., Material-UI, Ant Design, Tailwind CSS, Bootstrap]
- **Component Library:** [Custom or third-party]

**Authentication:**
- **Provider:** [e.g., Auth0, Azure MSAL, Firebase Auth, Custom JWT]
- **Flow:** [e.g., OAuth2, JWT, Session-based]

**Testing:**
- **Framework:** [e.g., Jest + React Testing Library, Vitest, Cypress]
- **E2E:** [e.g., Playwright, Cypress, Selenium]

### Mobile Frontend ([repo-name]) [OPTIONAL]

**Framework & Core:**
- **Platform:** [e.g., React Native, Flutter, Native iOS/Android]
- **Framework:** [Version]
- **Language:** [e.g., TypeScript, Dart, Swift, Kotlin]
- **Build System:** [e.g., Expo, Gradle, Xcode]

**Navigation:**
- **Library:** [e.g., React Navigation, Flutter Navigator]

**State Management:**
- **Library:** [Same or different from web]

**Platform-Specific:**
- **iOS:** [Min version supported]
- **Android:** [Min version supported]
- **App Store Info:** [Bundle ID, App Name]

---

## ⚙️ DEVELOPMENT COMMANDS

### Backend ([repo-name])

```bash
# Environment Setup
cd [repo-name]
[install dependencies command]  # e.g., npm install, pip install -r requirements.txt, ./mvnw install

# Development
[dev server command]             # e.g., npm run dev, python manage.py runserver, ./mvnw spring-boot:run
[build command]                  # e.g., npm run build, ./mvnw clean package

# Testing
[test command]                   # e.g., npm test, pytest, ./mvnw test
[test coverage command]          # e.g., npm run test:coverage

# Database
[migration command]              # e.g., npm run migrate, python manage.py migrate, flyway migrate
[seed command]                   # e.g., npm run seed, python manage.py loaddata
```

### Web Frontend ([repo-name])

```bash
# Environment Setup
cd [repo-name]
[install dependencies]           # e.g., npm install, yarn install

# Development
[dev server command]             # e.g., npm start, npm run dev, yarn dev
# Typically runs on port [XXXX]

# Build
[build command]                  # e.g., npm run build, yarn build
# Output: [build folder name]

# Testing
[test command]                   # e.g., npm test, yarn test
[e2e test command]               # e.g., npm run test:e2e
```

### Mobile Frontend ([repo-name]) [OPTIONAL]

```bash
# Environment Setup
cd [repo-name]
[install dependencies]

# Development
[start dev server]               # e.g., npm start, expo start
[run iOS]                        # e.g., npm run ios, flutter run
[run Android]                    # e.g., npm run android

# Build
[build iOS command]              # e.g., eas build --platform ios
[build Android command]          # e.g., eas build --platform android

# Testing
[test command]
```

### Validation (run after changes)

```bash
# Backend
cd [backend-repo] && [test command] && [build command]

# Web Frontend
cd [web-repo] && [test command] && [build command]

# Mobile Frontend
cd [mobile-repo] && [test command]
```

---

## 🏗️ PROJECT ARCHITECTURE

### Multi-Repository Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                        │
├─────────────────────────┬───────────────────────────────────┤
│   [Web Frontend]        │   [Mobile Frontend] [OPTIONAL]    │
│   [Tech Stack]          │   [Tech Stack]                    │
│   For: [User Type]      │   For: [User Type]                │
└─────────────────────────┴───────────────────────────────────┘
                             ↓
                     [API Protocol - HTTP REST, GraphQL, gRPC]
                             ↓
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                         │
│              [Backend] ([Framework])                         │
│              [Architecture Pattern]                          │
│              [API Versioning Strategy if applicable]         │
└─────────────────────────────────────────────────────────────┘
                             ↓
                     [Database Protocol]
                             ↓
┌─────────────────────────────────────────────────────────────┐
│                        DATA LAYER                            │
│                    [Database System]                         │
│              [Schema Organization]                           │
└─────────────────────────────────────────────────────────────┘
```

### API Versioning Strategy [If Applicable]

**Why Multiple API Versions?**
[Explain if you have different API versions for different frontends]

**API v1 (`/api/v1/*`) - [Frontend Name]:**
- [Purpose]
- [Key characteristics]

**API v2 (`/api/v2/*`) - [Frontend Name]:**
- [Purpose]
- [Key characteristics]

### Directory Structure

**Backend:**
```
/[backend-repo]/
├── [source folder]/          # e.g., src/, app/
│   ├── [layer 1]/           # e.g., controllers/, routes/, views/
│   ├── [layer 2]/           # e.g., services/, business logic/
│   ├── [layer 3]/           # e.g., models/, repositories/, data access/
│   └── [layer 4]/           # e.g., utils/, config/, middleware/
├── [test folder]/            # e.g., tests/, __tests__/
├── [config files]            # e.g., package.json, pom.xml, requirements.txt
└── [deployment files]        # e.g., Dockerfile, docker-compose.yml
```

**Web Frontend:**
```
/[web-repo]/
├── [source folder]/          # e.g., src/, app/
│   ├── [components]/        # Reusable components
│   ├── [pages or views]/    # Page-level components
│   ├── [state management]/  # Redux, Zustand, etc.
│   ├── [services or api]/   # API client, business logic
│   ├── [routing]/           # Route configuration
│   └── [utils]/             # Helper functions
├── [public or static]/       # Static assets
├── [config files]
└── [deployment files]
```

**Mobile Frontend:** [OPTIONAL]
```
/[mobile-repo]/
├── [source folder]/
│   ├── [screens]/           # App screens
│   ├── [components]/        # Reusable components
│   ├── [navigation]/        # Navigation setup
│   ├── [state]/             # State management
│   └── [services]/          # API and business logic
├── [assets]/                # Images, fonts, etc.
├── [config files]           # app.json, eas.json, etc.
└── [platform-specific]/     # ios/, android/
```

---

## 🎯 DOMAIN KNOWLEDGE

### Business Domain

**Primary Business:** [Describe what the system does]

**Core Business Entities:**
[List 5-10 main domain entities with brief descriptions]
1. **[Entity Name]** - [Description]
2. **[Entity Name]** - [Description]

### Critical Workflows

**[Workflow Name 1]:**
- **Trigger:** [What starts this workflow]
- **Steps:** [High-level steps]
- **Success Criteria:** [What defines success]
- **Involved Repositories:** [Which repos are affected]
- **Key Files:** [Important files]

**[Workflow Name 2]:**
- **Trigger:** [What starts this workflow]
- **Steps:** [High-level steps]
- **Success Criteria:** [What defines success]
- **Involved Repositories:** [Which repos are affected]
- **Key Files:** [Important files]

---

## 📚 DOCUMENTATION

### System Documentation
**Location:** `/.claude/documentation/`

**CLAUDE: ALWAYS check relevant documentation before implementation.**

**Quick Access:**
- **📑 Start Here:** [@.claude/documentation/DOCUMENTATION_INDEX.md](/.claude/documentation/DOCUMENTATION_INDEX.md) - Complete documentation catalog
- **🏗️ Architecture:** [@.claude/documentation/Architecture/Multi_Repository_Architecture.md](/.claude/documentation/Architecture/Multi_Repository_Architecture.md) - System overview

**Available Documentation:**

**Core Systems ([X] created, [Y] planned):**
- ✅ [@.claude/documentation/Core_Systems/System_Name.md](/.claude/documentation/Core_Systems/System_Name.md) - Brief description
- 📝 System_Name.md - Brief description (TODO)

**Architecture ([X] created, [Y] planned):**
- ✅ [@.claude/documentation/Architecture/Multi_Repository_Architecture.md](/.claude/documentation/Architecture/Multi_Repository_Architecture.md) - Multi-repo overview
- 📝 Component_Name.md - Brief description (TODO)

**Workflows ([X] planned):**
- 📝 Workflow_Name.md - Brief description (TODO)

### External References

**Backend:**
- [Framework Documentation]: [Link]

**Web Frontend:**
- [Framework Documentation]: [Link]

**Mobile Frontend:** [OPTIONAL]
- [Framework Documentation]: [Link]

---

## 🤖 AGENT RECOMMENDATIONS

### Essential Agents (Recommended for this stack)

**1. [agent-name]**
- **Purpose:** [What it does]
- **Use Cases:** [When to use]
- **Applies to:** [Which repos]

**2. [agent-name]**
- **Purpose:** [What it does]
- **Use Cases:** [When to use]
- **Applies to:** [Which repos]

### Agent Location
`.claude/agents/[agent-name].md`

**Invocation:** Automatic based on task, or manual: "Use [agent] for [task]"

---

## ✅ VALIDATION & QUALITY

### Quality Standards

**Backend:**
- [Standard 1]
- [Standard 2]

**Web Frontend:**
- [Standard 1]
- [Standard 2]

**Mobile Frontend:** [OPTIONAL]
- [Standard 1]
- [Standard 2]

### Validation Checklist

```bash
# Backend Validation
cd [backend-repo]
- [ ] Tests pass: [test command]
- [ ] Build succeeds: [build command]
- [ ] [Other checks]

# Web Frontend Validation
cd [web-repo]
- [ ] Tests pass: [test command]
- [ ] Build succeeds: [build command]
- [ ] [Other checks]

# Mobile Frontend Validation [OPTIONAL]
cd [mobile-repo]
- [ ] App runs on [platform]: [command]
- [ ] [Other checks]
```

---

## 🔒 SECURITY & COMPLIANCE

### Security Practices

**Backend:**
- [Practice 1 - e.g., Authentication method]
- [Practice 2 - e.g., Data protection]

**Web Frontend:**
- [Practice 1 - e.g., Token storage]
- [Practice 2 - e.g., XSS prevention]

**Mobile Frontend:** [OPTIONAL]
- [Practice 1 - e.g., Secure storage]
- [Practice 2 - e.g., Biometric auth]

### Sensitive Data

**NEVER commit:**
- [File type 1 - e.g., .env files]
- [File type 2 - e.g., API keys]
- [File type 3 - e.g., Credentials]

**Git ignore patterns verified:**
- Backend: [.gitignore covers what]
- Web: [.gitignore covers what]
- Mobile: [.gitignore covers what]

---

## 🚀 DEPLOYMENT & OPERATIONS

### Environments

**Development:**
- Backend: [How/where it runs]
- Web: [How/where it runs]
- Mobile: [How/where it runs]
- Database: [Dev database setup]

**Staging:**
- Backend: [Staging environment]
- Web: [Staging environment]
- Mobile: [Staging/TestFlight/Internal Testing]
- Database: [Staging database]

**Production:**
- Backend: [Production environment]
- Web: [Production environment]
- Mobile: [App Store + Google Play]
- Database: [Production database]

### Deployment Process

**Backend CI/CD:**
- [CI/CD tool - e.g., GitHub Actions, GitLab CI, Jenkins]
- [Deployment target]
- Manual steps: [Any manual interventions needed]
- Health checks: [How to verify deployment]

**Web Frontend CI/CD:**
- [Build process]
- [Deployment target]
- Manual steps: [Any manual interventions]
- Health checks: [How to verify]

**Mobile Frontend CI/CD:** [OPTIONAL]
- [Build service - e.g., EAS Build, Fastlane]
- [App store deployment process]
- Manual steps: [Version bumps, release notes]

### Cross-Repository Deployment Coordination

**When features span multiple repos:**

1. **Backend deployed first:**
   - Ensure backward compatibility
   - Deploy during [time window]
   - Monitor [health check endpoints]

2. **Web frontend deployed second:**
   - Deploy within [time window] of backend
   - Test immediately after deployment

3. **Mobile submitted to app stores:** [OPTIONAL]
   - Submit to [platform] ([typical review time])
   - Coordinate release timing with backend features

### Monitoring & Observability

**Metrics:**
- Backend: [What metrics are tracked]
- Web: [What metrics are tracked]
- Mobile: [What metrics are tracked]

**Logging:**
- Backend: [Where logs go]
- Web: [Where logs go]
- Mobile: [Where logs go]

**Alerting:**
- [Alert conditions and notification channels]

---

## 💡 PROJECT-SPECIFIC NOTES

### Known Issues & Gotcas

**Backend:**
- [Issue 1]: [Description and solution]

**Web Frontend:**
- [Issue 1]: [Description and solution]

**Mobile Frontend:** [OPTIONAL]
- [Issue 1]: [Description and solution]

### Performance Considerations

**Backend:**
- [Consideration 1]

**Web Frontend:**
- [Consideration 1]

**Mobile Frontend:** [OPTIONAL]
- [Consideration 1]

---

## 🔄 FEATURE DEVELOPMENT WORKFLOW

### Simple Changes (Single repo, <3 files)

1. **Check documentation:** Review relevant `@.claude/documentation/` files
2. **Identify repository:** Backend, web frontend, or mobile frontend
3. **Implement following patterns:** Match existing code style
4. **Run validation:** Tests + build for affected repository
5. **Update docs if needed:** Document new behavior

### Complex Features (Multi-file, business logic, >1 repository)

1. **CLAUDE AUTO-GENERATES PRP** (Product Requirements Prompt)
   - Asks for ticket number (e.g., [PROJECT]-XXX)
   - Creates `/.claude/prps/active/[TICKET]-[feature].md`
   - Documents requirements, acceptance criteria, affected repos

2. **Clarify business/technical decisions**
   - Which repositories affected (backend/web/mobile)?
   - API changes required?
   - Database schema changes?
   - Real-time features needed?
   - Cloud services involved?

3. **Implement systematically**
   - Backend first (API contracts)
   - Web/Mobile frontend integration
   - Real-time events (if needed)
   - Update all repositories in sync

4. **Full validation**
   - Backend: [validation command]
   - Web: [validation command]
   - Mobile: [validation process]

5. **Agent review if appropriate**
   - Security: Use `security-auditor` for auth/payment features
   - Performance: Use `performance-analyzer` for heavy features
   - Code Quality: Use appropriate reviewer agent

6. **Update documentation**
   - Add/update `@.claude/documentation/` files
   - Update CLAUDE.md if architecture changed
   - Document new API endpoints

7. **Move PRP to completed**
   - Move `/.claude/prps/active/[TICKET]-[feature].md` → `/.claude/prps/completed/`

### Multi-Repository Feature Coordination

**When feature spans multiple repos:**

1. **Backend changes first:**
   - Create/modify API endpoints
   - Update database schema
   - Deploy to staging

2. **Frontend integration (parallel for web + mobile if applicable):**
   - Update API clients
   - Add UI components
   - Update state management
   - Test against staging backend

3. **Deployment sequence:**
   - Backend deployed first (backward compatible)
   - Web frontend deployed second
   - Mobile submitted to app stores (if applicable)

**Breaking Changes Protocol:**
- Version API endpoints (e.g., `/api/v2/...`)
- Maintain backward compatibility
- Coordinate deployment timing across teams

---

## 🗂️ REPOSITORY-SPECIFIC QUICK REFERENCE

### When working on Backend ([repo-name]):
- **Primary Language:** [Language]
- **Build Tool:** [Tool]
- **Architecture:** [Pattern]
- **Key Patterns:** [List key patterns]
- **Testing:** [Test framework]
- **Main Config:** [Config file path]

### When working on Web Frontend ([repo-name]):
- **Primary Language:** [Language]
- **Build Tool:** [Tool]
- **Architecture:** [Pattern]
- **Key Patterns:** [List key patterns]
- **Testing:** [Test framework]
- **Main Config:** [Config file path]

### When working on Mobile Frontend ([repo-name]): [OPTIONAL]
- **Primary Language:** [Language]
- **Build Tool:** [Tool]
- **Architecture:** [Pattern]
- **Key Patterns:** [List key patterns]
- **Testing:** [Testing approach]
- **Main Config:** [Config file path]

---

**Context Engineering Version:** 1.0.1
**Last Updated:** [YYYY-MM-DD]
**Project Type:** Multi-Repository [System Type]
**Organization:** [Organization Name]

---

**This CLAUDE.md provides unified context across all repositories of the [Project Name] system. Claude will automatically reference this file for all development tasks, ensuring consistent patterns and architectural decisions across the entire tech stack.**
