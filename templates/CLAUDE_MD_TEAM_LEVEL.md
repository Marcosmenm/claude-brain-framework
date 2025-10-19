# [Team Name] - Team-Level Context Engineering

**Team-specific context within multi-level repository structure**

> **Template Type:** TEAM_LEVEL
> **Use When:** Individual team repository within a parent root structure
> **Related:** HIERARCHICAL_CONTEXT_SYNC.md, CLAUDE_MD_ROOT_ORCHESTRATION.md

---

## 🚨 CRITICAL WORKFLOW ENFORCEMENT

**CLAUDE: Automatically apply context engineering for ANY development request.**

### Automatic Behaviors
1. ✅ Check documentation automatically
2. ✅ Assess complexity
3. ✅ Generate PRP for complex work (>3 files or significant logic)
4. ✅ Follow established patterns
5. ✅ Suggest relevant agents
6. ✅ Update documentation after changes
7. ✅ Signal root sync when needed

**User works naturally - methodology applies automatically.**

---

## 🔗 HIERARCHICAL CONTEXT

**CLAUDE: This is a TEAM-LEVEL repository within a multi-team structure.**

### Parent Context Integration

```yaml
Hierarchy_Level: Team
Team_Name: [Your Team Name, e.g., "Backend Team", "Frontend Team"]
Domain_Responsibility: [What this team owns, e.g., "API services", "Web application"]

Parent_Repository:
  path: ../
  root_claude_md: ../CLAUDE.md
  relationship: "Child repository within root orchestration structure"

Coordination_Protocol:
  when_to_sync_upward:
    - Architectural changes that affect other teams
    - New API endpoints or contracts
    - Changes to integration points
    - Significant pattern or standard updates

  when_to_sync_downward:
    - Receiving coordinated PRPs from root
    - Company-wide policy changes
    - Cross-team feature implementations
    - Shared infrastructure updates
```

### Sync Protocol

**CLAUDE: When making significant changes in this team context:**

#### Upward Sync (Team → Root)
```bash
# CLAUDE automatically detects when to suggest root sync:
IF (architectural_change OR integration_point_change OR new_patterns):
    Alert user:
    "✓ Implementation complete.

     ⚠️ This change affects team architecture:
     - [Specific change, e.g., 'New API endpoint structure']
     - [Impact, e.g., 'Affects frontend/mobile integration']

     Suggest syncing with root context:
     - Update ../CLAUDE.md with new patterns
     - Update root documentation references
     - Alert other teams if integration affected

     Would you like me to document this for root sync?"
```

#### Downward Sync (Root → Team)
```bash
# CLAUDE automatically checks for coordinated work:
1. Check for PRPs in /PRPs/active/ with "-MASTER" suffix referenced
2. Look for coordinated ticket numbers across parent PRP
3. Alert about multi-team coordination context:
   "📋 Coordinated Implementation Detected:

    This PRP is part of multi-team feature:
    - Master PRP: ../PRPs/active/[TICKET]-[feature]-MASTER.md
    - Team responsibility: [Specific scope]
    - Integration requirements: [What to coordinate]
    - Other teams involved: [team-2], [team-3]

    I'll implement following the coordinated plan..."
```

---

## 📋 PROJECT TYPE & CONTEXT

### Team Classification

```yaml
Team_Name: [Your Team Name]
Team_Type: [Backend / Frontend / Mobile / DevOps / Data]
Team_Size: [Number of developers]
Primary_Responsibility: [Core domain responsibility]

Technology_Stack:
  Primary_Language: [e.g., "TypeScript", "Python", "Go"]
  Framework: [e.g., "Express.js", "React", "Flutter"]
  Database: [e.g., "PostgreSQL", "MongoDB", "None (frontend)"]
  Key_Libraries:
    - [Library 1, e.g., "Prisma ORM"]
    - [Library 2, e.g., "Jest for testing"]
    - [Library 3, e.g., "Joi for validation"]
```

### Integration Points

**CLAUDE: Critical for understanding cross-team dependencies**

```yaml
Integrations:
  Provides:
    - type: [e.g., "REST API"]
      consumers: [[team-2-name], [team-3-name]]
      documentation: [Link to API docs]
      contact: [API endpoint or service URL]

  Consumes:
    - type: [e.g., "Authentication Service"]
      provider: [team-1-name]
      documentation: [Link to auth docs]
      contact: [Service endpoint]

  Shared_Resources:
    - type: [e.g., "Design System"]
      provider: [team-name]
      shared_with: [Other teams]
      documentation: [Link to design system]
```

---

## 🛠️ TECHNOLOGY STACK

### Core Technologies

```yaml
Runtime_Environment:
  platform: [e.g., "Node.js 18 LTS", "Python 3.11", "Browser"]
  package_manager: [e.g., "npm", "pip", "yarn"]

Framework:
  name: [e.g., "Express.js 4.18", "React 18", "FastAPI"]
  architecture: [e.g., "Layered", "Component-based", "Microservices"]

Database:
  system: [e.g., "PostgreSQL 15", "MongoDB", "N/A"]
  orm: [e.g., "Prisma", "Sequelize", "Mongoose", "N/A"]

Testing:
  framework: [e.g., "Jest", "Pytest", "Vitest"]
  coverage_tool: [e.g., "Istanbul", "Coverage.py"]
  e2e: [e.g., "Supertest", "Playwright", "N/A"]

Code_Quality:
  linter: [e.g., "ESLint", "Pylint"]
  formatter: [e.g., "Prettier", "Black"]
  type_checker: [e.g., "TypeScript", "mypy", "N/A"]
```

---

## ⚙️ DEVELOPMENT COMMANDS

### Environment Setup
```bash
# Installation
[e.g., "npm install", "pip install -r requirements.txt"]

# Environment configuration
[Copy .env.example to .env and configure]
```

### Development
```bash
# Start development server
[e.g., "npm run dev", "python main.py", "npm start"]

# Build for production
[e.g., "npm run build", "docker build"]
```

### Testing
```bash
# Run all tests
[e.g., "npm test", "pytest"]

# Run with coverage
[e.g., "npm run test:coverage", "pytest --cov"]

# Run specific test
[e.g., "npm test -- auth.test.js", "pytest tests/test_auth.py"]

# E2E tests
[e.g., "npm run test:e2e", "playwright test"]
```

### Validation (run after changes)
```bash
# CLAUDE: Always run after implementation
[e.g., "npm run lint && npm test && npm run build"]
[e.g., "pylint src && pytest && python -m build"]
```

---

## 🏗️ PROJECT ARCHITECTURE

### Directory Structure

```
/[team-repo-root]/
├── CLAUDE.md                    # This file (team context)
├── .claude/
│   ├── documentation/           # Team-specific documentation
│   ├── chat-history/            # Conversation logs
│   └── agents/                  # Custom agents (optional)
├── PRPs/
│   ├── active/                  # Current feature PRPs
│   └── completed/               # Finished PRPs
├── [src/app/code folder]/       # Source code
│   ├── [folder 1]/              # [e.g., controllers, components]
│   ├── [folder 2]/              # [e.g., services, hooks]
│   ├── [folder 3]/              # [e.g., repositories, utils]
│   └── ...
├── [tests/test folder]/         # Test files
├── [config files]               # [e.g., package.json, tsconfig.json]
└── README.md                    # Public project readme
```

### Architecture Patterns

**CLAUDE: Follow these established patterns**

```yaml
Code_Organization:
  pattern: [e.g., "Layered architecture", "Feature-based", "Atomic design"]
  description: |
    [Brief description of how code is organized, e.g.,
    "Controllers handle requests, Services contain business logic,
    Repositories handle data access"]

Key_Patterns:
  - name: [Pattern name, e.g., "Dependency Injection"]
    usage: [When/where used, e.g., "For all services and repositories"]
    example_file: [Path to example]

  - name: [Pattern name, e.g., "Repository Pattern"]
    usage: [When/where used]
    example_file: [Path to example]
```

---

## 🎯 DOMAIN KNOWLEDGE

### Team Domain

```yaml
Primary_Domain: [e.g., "API Services", "User Interface", "Mobile Experience"]

Core_Responsibilities:
  - [Responsibility 1, e.g., "User authentication and authorization"]
  - [Responsibility 2, e.g., "Product catalog management"]
  - [Responsibility 3, e.g., "Order processing"]

Key_Entities:
  - name: [Entity, e.g., "User"]
    description: [What it represents]
    location: [e.g., "src/models/User.ts"]

  - name: [Entity, e.g., "Product"]
    description: [What it represents]
    location: [e.g., "src/models/Product.ts"]
```

### Critical Workflows

**CLAUDE: Reference these for understanding feature context**

```yaml
Workflows:
  - name: [Workflow, e.g., "User Registration"]
    trigger: [What starts it, e.g., "User submits registration form"]
    steps:
      - [Step 1, e.g., "Validate email and password"]
      - [Step 2, e.g., "Create user in database"]
      - [Step 3, e.g., "Send verification email"]
    key_files:
      - [File 1, e.g., "src/controllers/auth.controller.ts"]
      - [File 2, e.g., "src/services/user.service.ts"]
    documentation: [Link to detailed workflow doc]
```

---

## 📚 DOCUMENTATION

### Team Documentation Structure

**CLAUDE: ALWAYS check relevant documentation before implementation**

```
/.claude/documentation/
├── DOCUMENTATION_INDEX.md       # Team documentation index
├── Core_Systems/
│   ├── [System_1].md            # [e.g., Authentication_System.md]
│   ├── [System_2].md            # [e.g., Database_Design.md]
│   └── ...
├── Features/
│   ├── [Feature_1].md           # [e.g., User_Management.md]
│   ├── [Feature_2].md           # [e.g., Product_Catalog.md]
│   └── ...
└── Patterns/
    ├── [Pattern_1].md           # [e.g., Error_Handling.md]
    ├── [Pattern_2].md           # [e.g., Testing_Patterns.md]
    └── ...
```

**Quick Access:**
- **📑 Start Here:** [DOCUMENTATION_INDEX.md](.claude/documentation/DOCUMENTATION_INDEX.md)
- **🏗️ Architecture:** [Link to key architecture doc]
- **🔒 Authentication:** [Link to auth doc if relevant]
- **💾 Database:** [Link to database doc if relevant]

---

## 🔄 FEATURE DEVELOPMENT WORKFLOW

### Simple Changes (<3 files, no business logic)

1. **Check documentation** - Review relevant team docs
2. **Follow team patterns** - Match existing code style
3. **Implement** - Make the change
4. **Validate** - Run tests and build
5. **Update docs** - If behavior changed

### Complex Features (>3 files, business logic, integrations)

**CLAUDE AUTO-GENERATES PRP:**

1. **Ask for ticket number** (e.g., TEAM-XXX, JIRA-XXX)
2. **Check coordinated context**:
   ```bash
   IF (part_of_multi_team_feature):
       Look for master PRP in parent: ../PRPs/active/[TICKET]-*-MASTER.md
       Reference master PRP in team PRP
       Follow coordinated implementation plan
   ```
3. **Create team PRP**: `/PRPs/active/[TICKET]-[feature].md`
4. **Clarify business/technical decisions** specific to team
5. **Implement systematically** following team patterns
6. **Validate thoroughly**: Tests + build + integration checks
7. **Update team documentation**
8. **Check if root sync needed** - Alert if architectural changes

---

## ✅ VALIDATION PROTOCOLS

### Team-Level Validation

```bash
# CLAUDE: Run after every implementation
1. Linting: [e.g., "npm run lint"]
2. Type checking: [e.g., "tsc --noEmit"]
3. Unit tests: [e.g., "npm test"]
4. Integration tests: [e.g., "npm run test:integration"]
5. Build: [e.g., "npm run build"]
6. Coverage check: [e.g., "npm run test:coverage"]
```

### Integration Validation (when applicable)

```bash
# When changes affect integration points:
1. Test against dependent team's contracts
2. Verify API compatibility
3. Check shared resource usage
4. Run cross-team integration tests (if available)
5. Update integration documentation
```

---

## 🚨 CRITICAL TEAM RULES

### Never Do These

1. ❌ **Never skip documentation check** before implementation
2. ❌ **Never break integration contracts** without coordinating with dependent teams
3. ❌ **Never commit untested code** - always run validation
4. ❌ **Never duplicate root documentation** - reference it instead
5. ❌ **Never ignore coordinated PRPs** from root level

### Always Do These

1. ✅ **Always check team documentation** before implementing
2. ✅ **Always follow team patterns** and architecture
3. ✅ **Always generate PRP** for complex features
4. ✅ **Always run validation** before completing
5. ✅ **Always update team documentation** after changes
6. ✅ **Always check for coordinated context** from root
7. ✅ **Always signal upward** when integration points change

---

## 🔗 CROSS-TEAM COORDINATION

### Working in Coordinated Context

**CLAUDE: When this team is part of multi-team feature:**

```
Detection:
1. Check PRPs for master references: ../PRPs/active/[TICKET]-*-MASTER.md
2. Check for same ticket number in other team folders
3. Look for coordination notes in team PRP

Response Pattern:
"📋 Coordinated Feature Implementation Detected

This is part of multi-team feature: [Feature Name]
- Master PRP: ../PRPs/active/[TICKET]-[feature]-MASTER.md
- Team responsibility: [What this team implements]
- Dependencies: [What this team needs from others]
- Integration: [How this connects with other teams]

Other teams involved:
- [team-2-name]: [Their part]
- [team-3-name]: [Their part]

Implementation sequence:
- [If backend]: Implement first (API contracts)
- [If frontend/mobile]: Wait for backend, then integrate

I'll implement this team's portion following the coordinated plan..."
```

### Signaling to Root

**CLAUDE: Auto-suggest root sync when appropriate:**

```bash
# After implementation, check if root needs update:
IF (integration_point_changed OR
    new_api_endpoint OR
    architectural_change OR
    new_shared_pattern):

    Suggest:
    "✓ Team implementation complete.

     ⚠️ Root sync recommended:
     - [What changed, e.g., 'New REST API endpoint structure']
     - [Impact, e.g., 'Frontend/mobile need to update integration']
     - [Documentation, e.g., 'API docs updated at [link]']

     Would you like me to prepare root sync documentation?"
```

---

## 🎭 AGENT COORDINATION (Optional)

### Team-Specific Agents

```yaml
Available_Agents:
  - [agent-name]:
      purpose: [What it does, e.g., "Review security in API endpoints"]
      triggers: [When to use, e.g., "New API endpoint", "Auth changes"]

  - [agent-name]:
      purpose: [What it does, e.g., "Optimize database queries"]
      triggers: [When to use, e.g., "New DB query", "Performance issue"]
```

---

## 📝 TEAM CONVENTIONS

### Code Style

```yaml
Style_Guide: [e.g., "Airbnb JavaScript Style Guide"]
Naming_Conventions:
  - files: [e.g., "kebab-case for files"]
  - functions: [e.g., "camelCase"]
  - classes: [e.g., "PascalCase"]
  - constants: [e.g., "UPPER_SNAKE_CASE"]

Comment_Standards:
  - [e.g., "JSDoc for all public functions"]
  - [e.g., "Inline comments for complex logic only"]
  - [e.g., "TODO comments with ticket numbers"]
```

### Git Workflow

```yaml
Branch_Strategy: [e.g., "Git Flow", "GitHub Flow", "Trunk-based"]
Branch_Naming: [e.g., "feature/TICKET-description", "fix/TICKET-description"]
Commit_Messages: [e.g., "Conventional Commits format"]
PR_Requirements:
  - [e.g., "All tests pass"]
  - [e.g., "Code review approved"]
  - [e.g., "No merge conflicts"]
```

---

**Context Engineering Framework Version:** 1.1.0
**Template Version:** 1.0.0
**Template Type:** TEAM_LEVEL
**Last Updated:** [YYYY-MM-DD]
**Team:** [Your Team Name]

---

## 📖 Quick Start Checklist

**When first setting up this team-level context:**

- [ ] Fill in all `[bracketed placeholders]` with actual team details
- [ ] Document team-specific technology stack
- [ ] List integration points with other teams
- [ ] Set up team documentation structure
- [ ] Document team conventions and patterns
- [ ] Link to parent root CLAUDE.md
- [ ] Create initial team documentation
- [ ] Set up validation commands

**For more details:** See [HIERARCHICAL_CONTEXT_SYNC.md](../core/HIERARCHICAL_CONTEXT_SYNC.md)
