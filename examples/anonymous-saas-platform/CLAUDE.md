# Anonymous SaaS Platform - Context Engineering

**Team productivity and workflow automation platform**

## 🚨 CRITICAL WORKFLOW ENFORCEMENT

**CLAUDE: Automatically apply context engineering for ANY development request.**

---

## 📋 PROJECT CONTEXT

### Tech Stack
**Backend:**
- Framework: Express.js 4.18
- Language: Node.js 18 LTS with TypeScript 5.2
- Database: PostgreSQL 15
- ORM: Prisma 5.3
- Authentication: JWT + Passport.js

**Frontend:**
- Framework: React 18.2
- Language: TypeScript 5.2
- Build: Vite 4.5
- Styling: Tailwind CSS 3.3
- State: Zustand + React Query

**Infrastructure:**
- Hosting: AWS (ECS + RDS)
- CI/CD: GitHub Actions
- Monitoring: DataDog

### Development Commands
```bash
# Backend
npm run dev              # Start API server
npm test                # Run tests
npm run db:migrate      # Run migrations (manual only)

# Frontend
npm run dev             # Start dev server
npm run build           # Production build
npm test               # Run tests

# Validation
npm test && npm run lint && npm run build
```

---

## 🏗️ ARCHITECTURE

### Project Structure
```
/backend/
├── /src/
│   ├── /controllers/   # Request handlers
│   ├── /services/      # Business logic
│   ├── /models/        # Prisma models
│   └── /middleware/    # Auth, validation
/frontend/
├── /src/
│   ├── /components/    # React components
│   ├── /pages/         # Page components
│   ├── /hooks/         # Custom React hooks
│   └── /services/      # API clients
/Documentation/         # System docs (@import these)
/PRPs/                  # Feature blueprints
/.claude/               # Framework config
```

### API Communication
- **Style:** REST API
- **Auth:** JWT tokens in Authorization header
- **Base URL:** `http://localhost:3000/api`

---

## 🎯 BUSINESS DOMAIN

### Core Entities
**Project:**
- Purpose: Container for tasks and workflows
- Key Fields: name, description, owner_id, team_id
- File: `backend/src/models/project.ts`

**Task:**
- Purpose: Individual work items
- Key Fields: title, status, assigned_to, project_id
- File: `backend/src/models/task.ts`

**Workflow:**
- Purpose: Automated task sequences
- Key Fields: trigger_event, actions, project_id
- File: `backend/src/models/workflow.ts`

### Critical Workflows
1. **Task Assignment:**
   - Trigger: Task created or reassigned
   - Steps: Validate permissions → Update DB → Notify user → Log activity
   - Files: `TaskController`, `NotificationService`

2. **Workflow Automation:**
   - Trigger: Specified event occurs
   - Steps: Check conditions → Execute actions → Update state
   - Files: `WorkflowEngine`, `ActionExecutor`

---

## 📚 DOCUMENTATION

### System Documentation
- `@Documentation/Core_Systems/Project_Management.md`
- `@Documentation/Core_Systems/Workflow_Automation.md`
- `@Documentation/Core_Systems/User_Authentication.md`

**CLAUDE: Always check relevant docs before implementation.**

---

## 🤖 RECOMMENDED AGENTS

**Essential:**
- `typescript-validator` - Type safety and patterns
- `api-tester` - Endpoint validation
- `security-auditor` - Auth and permissions

**Location:** `.claude/agents/[agent-name].md`

---

## ✅ VALIDATION

```bash
# After implementation
npm test && npm run lint && npm run type-check && npm run build
```

**Checklist:**
- [ ] Tests pass
- [ ] TypeScript compiles
- [ ] No linting errors
- [ ] Build succeeds
- [ ] Documentation updated

---

**Context Engineering Version:** 1.0.0
**Last Updated:** 2025-10-10
