# Multi-Repository E-Commerce Example

**Example demonstrating claude-brain-framework with multi-repository architecture**

## Overview

This example shows how to use the `CLAUDE_MD_MULTI_REPO_SYSTEM.md` template for a typical e-commerce platform split across multiple repositories:

- **Backend** (Node.js + Express + PostgreSQL)
- **Web Frontend** (React + TypeScript)
- **Mobile App** (React Native)

## Repository Structure

```
multi-repo-ecommerce/
├── CLAUDE.md                  # Multi-repo system context (uses CLAUDE_MD_MULTI_REPO_SYSTEM template)
├── backend/                   # API server repository
│   ├── src/
│   │   ├── controllers/
│   │   ├── services/
│   │   ├── models/
│   │   └── routes/
│   └── package.json
├── web-frontend/              # Customer-facing web app
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── api/
│   │   └── state/
│   └── package.json
├── mobile-app/                # Mobile application
│   ├── src/
│   │   ├── screens/
│   │   ├── components/
│   │   └── navigation/
│   └── package.json
└── .claude/
    └── documentation/         # Shared documentation for entire system
        ├── DOCUMENTATION_INDEX.md
        ├── Core_Systems/
        ├── Architecture/
        └── Workflows/
```

## Key Features Demonstrated

### 1. **Multi-Repository Context**
The [CLAUDE.md](CLAUDE.md) file uses the multi-repo template to provide:
- Unified context across all three repositories
- Cross-repository coordination guidelines
- Deployment sequence documentation
- API versioning strategy

### 2. **Documentation Index**
The [.claude/documentation/DOCUMENTATION_INDEX.md](.claude/documentation/DOCUMENTATION_INDEX.md) demonstrates:
- Central documentation catalog
- Status tracking (completed vs TODO)
- Priority-based organization
- Navigation paths for different user roles

### 3. **Incremental Documentation**
Shows how large systems can:
- Generate high-priority docs first
- Mark remaining docs as TODO
- Request additional docs incrementally
- Maintain quality without token exhaustion

## What Makes This Different

### Traditional Single-Repo Template
```
project/
├── CLAUDE.md (covers single codebase)
└── src/
```

### Multi-Repo Template
```
system/
├── CLAUDE.md (covers ALL repositories)
├── backend/ (separate repo in reality)
├── web-frontend/ (separate repo in reality)
└── mobile-app/ (separate repo in reality)
```

## Real-World Usage

In production, these would be separate Git repositories:

```bash
# Separate repositories
https://github.com/company/ecommerce-backend
https://github.com/company/ecommerce-web
https://github.com/company/ecommerce-mobile

# But shared CLAUDE.md approach:
# Each repo has a CLAUDE.md that references the multi-repo context
# Or a mono-repo contains all with single CLAUDE.md
```

## Use This Example When

✅ **Your project has:**
- Multiple interconnected repositories (backend + frontend(s))
- Different tech stacks per repository
- Coordinated deployment requirements
- Shared business domain across repos

❌ **Use single-repo template instead if:**
- Single codebase / monolith
- All code in one repository
- Simple architecture

## How to Apply to Your Project

1. **Copy the CLAUDE.md template:**
   ```bash
   cp templates/CLAUDE_MD_MULTI_REPO_SYSTEM.md your-project/CLAUDE.md
   ```

2. **Fill in your specifics:**
   - Repository names and tech stacks
   - User types and authentication methods
   - Business domain and workflows
   - Development commands

3. **Ask Claude to initialize:**
   ```
   "I have a multi-repository system. Please apply the claude-brain-framework
   initialization process for this architecture."
   ```

4. **Claude will:**
   - Analyze all repositories
   - Propose documentation structure
   - Generate DOCUMENTATION_INDEX.md
   - Create high-priority documentation
   - Leave remaining as incremental TODOs

## Learn More

- **Template:** [templates/CLAUDE_MD_MULTI_REPO_SYSTEM.md](../../templates/CLAUDE_MD_MULTI_REPO_SYSTEM.md)
- **Documentation Index:** [templates/DOCUMENTATION_INDEX_TEMPLATE.md](../../templates/DOCUMENTATION_INDEX_TEMPLATE.md)
- **Incremental Strategy:** See [core/INIT_PROCESS.md](../../core/INIT_PROCESS.md) Cycle 7

---

**This example demonstrates v1.1.0 features** added in October 2025
