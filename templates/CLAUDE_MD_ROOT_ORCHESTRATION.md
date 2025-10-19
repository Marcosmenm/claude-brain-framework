# [Company/Project Name] - Root Orchestration Context

**Multi-team repository orchestration with hierarchical context engineering**

> **Template Type:** ROOT_ORCHESTRATION
> **Use When:** Managing multiple team repositories from a parent/root folder
> **Related:** HIERARCHICAL_CONTEXT_SYNC.md, CLAUDE_MD_TEAM_LEVEL.md

---

## 🚨 HIERARCHICAL CONTEXT SYSTEM

**CLAUDE: This is a ROOT-LEVEL multi-team repository structure.**

### Automatic Hierarchical Context Behaviors

**CLAUDE: When you open this folder, automatically:**

1. ✅ **Detect hierarchy** - Scan for child CLAUDE.md files in subdirectories
2. ✅ **Check sync status** - Compare timestamps between root and child contexts
3. ✅ **Load child contexts** - Reference team-specific CLAUDE.md files for full understanding
4. ✅ **Alert staleness** - Notify if child contexts updated more recently than root
5. ✅ **Enable orchestration** - Support multi-team feature coordination from root level

**YOU ARE IN ORCHESTRATION MODE** - Changes can affect multiple teams.

---

## 📋 CONTEXT HIERARCHY

### Repository Structure

```yaml
Repository_Type: Root Orchestration Layer
Organization: [Your Company/Organization Name]
Purpose: [Multi-team coordination, shared infrastructure, etc.]

Child_Repositories:
  - path: /[team-1-name]/
    type: [Tech stack - e.g., "Node.js + Express API"]
    domain: [Domain responsibility - e.g., "Backend services"]
    claude_context: /[team-1-name]/CLAUDE.md
    last_synced: [YYYY-MM-DD]
    status: [active/maintenance]

  - path: /[team-2-name]/
    type: [Tech stack - e.g., "React + TypeScript"]
    domain: [Domain responsibility - e.g., "Web frontend"]
    claude_context: /[team-2-name]/CLAUDE.md
    last_synced: [YYYY-MM-DD]
    status: [active/maintenance]

  - path: /[team-3-name]/
    type: [Tech stack - e.g., "React Native"]
    domain: [Domain responsibility - e.g., "Mobile apps"]
    claude_context: /[team-3-name]/CLAUDE.md
    last_synced: [YYYY-MM-DD]
    status: [active/maintenance]
```

### Integration Points

**Cross-team dependencies and integration points:**

```yaml
Integration_Points:
  - type: [e.g., "REST API"]
    provider: [team-1-name]
    consumers: [[team-2-name], [team-3-name]]
    documentation: [Link to API docs]

  - type: [e.g., "Shared authentication"]
    provider: [team-1-name]
    consumers: [[team-2-name], [team-3-name]]
    documentation: [Link to auth docs]

  - type: [e.g., "Design system"]
    provider: [team-2-name]
    consumers: [[team-2-name], [team-3-name]]
    documentation: [Link to design system docs]
```

---

## 🔄 CONTEXT SYNCHRONIZATION PROTOCOL

### CLAUDE: Synchronization Rules

**Always apply these rules when working in root context:**

#### 1. Context Loading Strategy

```bash
# Before ANY major implementation:
1. Scan child CLAUDE.md files for current state
2. Read relevant child documentation:
   - /[team-1-name]/.claude/documentation/
   - /[team-2-name]/.claude/documentation/
   - /[team-3-name]/.claude/documentation/
3. Build unified understanding across all teams
4. Identify integration points and dependencies
5. Alert if any child context is more recent than root
```

#### 2. Change Impact Analysis

```bash
# Before implementing any change:
IF (affects_single_team):
    → Switch to team-level context
    → Work within team's patterns
    → Update team documentation

ELSE IF (affects_multiple_teams):
    → Orchestrated multi-team implementation
    → Generate master + child PRPs
    → Coordinate across teams

ELSE IF (company_wide_policy):
    → Downward propagation to all teams
    → Update all team contexts
    → Generate PRPs for each affected team
```

#### 3. PRP Coordination for Multi-Team Features

```bash
# When feature spans multiple teams:
1. Generate MASTER PRP at root:
   Location: /PRPs/active/[TICKET]-[feature]-MASTER.md
   Content:
   - Overall strategy and business context
   - Team responsibilities breakdown
   - Integration plan and dependencies
   - Timeline and milestones

2. Generate CHILD PRPs per affected team:
   Location: /[team-name]/PRPs/active/[TICKET]-[feature]-[team].md
   Content:
   - Team-specific implementation details
   - Reference to master PRP
   - Team-specific acceptance criteria
   - Integration requirements with other teams

3. Cross-reference:
   - Master PRP links to all child PRPs
   - Child PRPs link back to master PRP
   - Track completion status across all teams
```

#### 4. Documentation Strategy

```yaml
Root_Documentation:
  purpose: "Aggregation and coordination layer"
  location: /.claude/documentation/
  contains:
    - High-level architecture across teams
    - Integration points between teams
    - Company-wide standards and policies
    - Cross-team workflows
    - Links to team-specific detailed docs
  update_when:
    - Architecture changes
    - New integration points
    - Policy changes
    - Multi-team features completed

Team_Documentation:
  purpose: "Detailed implementation documentation"
  location: /[team-name]/.claude/documentation/
  contains:
    - Team-specific patterns and conventions
    - Detailed API documentation
    - Component libraries and utilities
    - Team workflow documentation
  managed_by: "Individual teams"
  referenced_by: "Root documentation (no duplication)"
```

### Context Refresh Commands

**CLAUDE: User can trigger these explicitly:**

```bash
# Sync commands (user can say naturally):
"Refresh context from child repos"
"Sync with team contexts"
"Update root context"
"Show child context changes"
"Check team documentation updates"

# When user triggers, Claude:
1. Reads all child CLAUDE.md files
2. Scans child documentation directories
3. Generates change summary since last sync
4. Offers to update root CLAUDE.md if needed
5. Updates "last_synced" timestamps
```

---

## 🎯 COMPANY-WIDE CONTEXT

### Technology Stack Overview

**CLAUDE: Reference for understanding overall architecture**

```yaml
Primary_Technologies:
  Backend:
    - [Framework/Language, e.g., "Node.js + Express"]
    - [Database, e.g., "PostgreSQL 15"]
    - [Key libraries]

  Web_Frontend:
    - [Framework, e.g., "React 18 + TypeScript"]
    - [State management, e.g., "Zustand"]
    - [Key libraries]

  Mobile:
    - [Platform, e.g., "React Native + Expo"]
    - [Navigation, e.g., "React Navigation"]
    - [Key libraries]

Shared_Infrastructure:
  - [Cloud provider, e.g., "AWS"]
  - [Services used, e.g., "S3, RDS, CloudFront"]
  - [CI/CD, e.g., "GitHub Actions"]
  - [Monitoring, e.g., "Datadog"]

Development_Tools:
  - [Version control, e.g., "Git + GitHub"]
  - [Project management, e.g., "Jira"]
  - [Communication, e.g., "Slack"]
```

### Business Domain

```yaml
Industry: [e.g., "E-commerce", "SaaS", "FinTech"]
Primary_Product: [Description of what you build]

Core_Entities:
  - [Entity 1]: [Description, e.g., "User - Customer accounts"]
  - [Entity 2]: [Description, e.g., "Product - Items for sale"]
  - [Entity 3]: [Description, e.g., "Order - Purchases"]

Critical_Workflows:
  - name: [Workflow name, e.g., "Purchase flow"]
    teams_involved: [[team-1], [team-2], [team-3]]
    documentation: [Link to workflow docs]
```

---

## 🛠️ DEVELOPMENT COMMANDS

### Root-Level Commands

```bash
# Validation across all teams
./scripts/validate-all-teams.sh

# Run all tests
./scripts/test-all.sh

# Build all projects
./scripts/build-all.sh

# Start all services (development)
docker-compose up -d
```

### Team-Specific Commands

```bash
# Backend Team
cd [team-1-name] && npm install && npm run dev
cd [team-1-name] && npm test

# Frontend Team
cd [team-2-name] && npm install && npm run dev
cd [team-2-name] && npm test

# Mobile Team
cd [team-3-name] && npm install && npm start
cd [team-3-name] && npm test
```

---

## 📚 DOCUMENTATION

### Root Documentation Structure

**CLAUDE: ALWAYS check documentation before implementation**

```
/.claude/documentation/
├── DOCUMENTATION_INDEX.md          # Master index (links to all docs)
├── Architecture/
│   ├── System_Overview.md          # Overall architecture
│   ├── Integration_Points.md       # How teams integrate
│   └── Data_Flow.md                # Cross-team data flows
├── Standards/
│   ├── API_Standards.md            # Company-wide API conventions
│   ├── Security_Standards.md       # Security policies
│   └── Code_Standards.md           # Shared coding standards
└── Workflows/
    ├── Multi_Team_Workflows.md     # Cross-team processes
    └── Deployment_Strategy.md      # Deployment coordination
```

**Quick Access:**
- **📑 Start Here:** [DOCUMENTATION_INDEX.md](.claude/documentation/DOCUMENTATION_INDEX.md)
- **🏗️ Architecture:** [System_Overview.md](.claude/documentation/Architecture/System_Overview.md)
- **🔗 Integration:** [Integration_Points.md](.claude/documentation/Architecture/Integration_Points.md)

### Team Documentation (Reference Only)

**CLAUDE: DO NOT duplicate team docs at root - reference them:**

```
/[team-1-name]/.claude/documentation/  ← Managed by Team 1
/[team-2-name]/.claude/documentation/  ← Managed by Team 2
/[team-3-name]/.claude/documentation/  ← Managed by Team 3
```

---

## 🎯 ORCHESTRATED WORKFLOWS

### Workflow 1: Single-Team Change

**CLAUDE: When change affects only one team**

```
User: "Fix bug in backend API endpoint"

Claude Response Pattern:
"I'll fix the backend API bug.

Context Analysis:
✓ Single-team scope (backend only)
✓ Loading /[team-1-name]/CLAUDE.md context
✓ Switching to team-level work

[Works within team context using team patterns]

Implementation complete.
✓ Team documentation updated
✓ No root-level sync needed (isolated change)"
```

### Workflow 2: Multi-Team Feature

**CLAUDE: When feature spans multiple teams**

```
User: "Add real-time notifications for [event]"

Claude Response Pattern:
"I'll implement real-time notifications for [event].

Context Analysis:
✓ Multi-team feature detected
✓ Loading all team contexts:
  - /[team-1-name]/: WebSocket server implementation
  - /[team-2-name]/: Notification UI component
  - /[team-3-name]/: Push notification integration

Orchestrated Implementation Plan:
1. Master PRP Generation:
   /PRPs/active/[TICKET]-notifications-MASTER.md
   - Overall strategy
   - Team responsibilities
   - Integration architecture

2. Team PRPs:
   - /[team-1-name]/PRPs/active/[TICKET]-websocket-server.md
   - /[team-2-name]/PRPs/active/[TICKET]-notification-ui.md
   - /[team-3-name]/PRPs/active/[TICKET]-push-notifications.md

3. Implementation Sequence:
   Phase 1: Backend WebSocket infrastructure
   Phase 2: Frontend + Mobile (parallel)
   Phase 3: Integration testing

4. Documentation Updates:
   - Root: /.claude/documentation/Features/Notifications.md
   - Teams: Each team updates their specific docs

Proceed with this orchestrated approach?"
```

### Workflow 3: Company-Wide Policy Change

**CLAUDE: When policy affects all teams**

```
User: "Implement GDPR data export across all systems"

Claude Response Pattern:
"I'll implement company-wide GDPR data export.

Cross-Team Impact Analysis:
✓ ALL teams affected
✓ Regulatory/compliance requirement
✓ Requires coordinated rollout

Downward Propagation Strategy:
1. Root Master PRP:
   /PRPs/active/[TICKET]-gdpr-export-MASTER.md
   - Legal requirements
   - Company-wide data inventory
   - Standardized export format

2. Propagate to all teams:
   - /[team-1-name]/PRPs/active/[TICKET]-gdpr-backend.md
     → API endpoints, data aggregation
   - /[team-2-name]/PRPs/active/[TICKET]-gdpr-web.md
     → Export UI, privacy dashboard
   - /[team-3-name]/PRPs/active/[TICKET]-gdpr-mobile.md
     → Export feature, privacy settings

3. Coordinated Timeline:
   Week 1: Backend implementation
   Week 2: Frontend + Mobile integration
   Week 3: Testing + legal review
   Week 4: Deployment

4. Documentation Requirements:
   - Root: Legal compliance documentation
   - Root: Technical implementation guide
   - Teams: Team-specific implementation docs

Generating coordinated PRPs for all teams..."
```

---

## ✅ VALIDATION PROTOCOLS

### Multi-Team Validation

**CLAUDE: After orchestrated implementation:**

```bash
# Step 1: Validate each team individually
cd [team-1-name] && npm test && npm run build
cd [team-2-name] && npm test && npm run build
cd [team-3-name] && npm test

# Step 2: Integration testing
./scripts/integration-tests.sh

# Step 3: End-to-end workflows
./scripts/e2e-tests.sh

# Step 4: Documentation verification
./scripts/validate-docs.sh

# Step 5: Cross-team review
# Ensure all PRPs completed
# Verify all documentation updated
# Check all teams synced
```

---

## 🚨 CRITICAL ORCHESTRATION RULES

### NEVER Do These at Root Level

1. ❌ **Never implement team-specific code at root** without switching to team context
2. ❌ **Never work multi-team without loading all child contexts** first
3. ❌ **Never duplicate team documentation at root** (reference instead)
4. ❌ **Never assume root context is current** without checking sync status
5. ❌ **Never skip coordination** for changes affecting multiple teams

### ALWAYS Do These at Root Level

1. ✅ **Always detect hierarchy** and load child contexts
2. ✅ **Always check sync status** before major implementations
3. ✅ **Always generate coordinated PRPs** for multi-team features
4. ✅ **Always analyze impact** before implementing (single vs multi-team)
5. ✅ **Always update root documentation** for architectural changes
6. ✅ **Always propagate standards** to child teams when needed
7. ✅ **Always validate across all teams** for integrated features

---

## 📝 SYNC STATUS TRACKING

### Last Synchronization Record

```yaml
Last_Full_Sync: [YYYY-MM-DD HH:MM]

Team_Sync_Status:
  - team: [team-1-name]
    last_synced: [YYYY-MM-DD]
    changes_since: [Number or "none"]
    status: [up-to-date / needs-sync / unknown]

  - team: [team-2-name]
    last_synced: [YYYY-MM-DD]
    changes_since: [Number or "none"]
    status: [up-to-date / needs-sync / unknown]

  - team: [team-3-name]
    last_synced: [YYYY-MM-DD]
    changes_since: [Number or "none"]
    status: [up-to-date / needs-sync / unknown]
```

**CLAUDE: Check this before any major work - prompt sync if needed**

---

## 🎭 AGENT COORDINATION (Optional)

### Root-Level Agents

```yaml
Available_Agents:
  - orchestrator-agent:
      purpose: "Coordinate multi-team implementations"
      triggers: ["multi-team feature", "cross-team change"]

  - architecture-reviewer:
      purpose: "Review cross-team architectural decisions"
      triggers: ["integration point changes", "new team added"]

  - documentation-aggregator:
      purpose: "Sync documentation across teams"
      triggers: ["doc sync request", "team doc updates"]
```

---

**Context Engineering Framework Version:** 1.1.0
**Template Version:** 1.0.0
**Template Type:** ROOT_ORCHESTRATION
**Last Updated:** [YYYY-MM-DD]
**Organization:** [Your Company/Organization]

---

## 📖 Quick Start Checklist

**When first setting up this root orchestration context:**

- [ ] Fill in all `[bracketed placeholders]` with actual team names and details
- [ ] Update child repository paths and tech stacks
- [ ] Document integration points between teams
- [ ] Set up initial sync timestamps
- [ ] Create root-level documentation structure
- [ ] Ensure all teams have their own CLAUDE.md (use CLAUDE_MD_TEAM_LEVEL.md template)
- [ ] Document company-wide standards and policies
- [ ] Set up validation scripts for multi-team testing

**For more details:** See [HIERARCHICAL_CONTEXT_SYNC.md](../core/HIERARCHICAL_CONTEXT_SYNC.md)
