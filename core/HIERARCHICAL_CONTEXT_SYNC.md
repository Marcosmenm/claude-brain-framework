# Hierarchical Context Synchronization

**Managing nested CLAUDE.md contexts across multi-level repository structures**

## 🎯 Problem Statement

Organizations with multi-team structures face context engineering challenges:

```
/company-root/                    ← Upper-level repository (you/lead)
  ├── CLAUDE.md                   ← Master context (potentially stale)
  ├── /backend-team/              ← Team 1 repository
  │   ├── CLAUDE.md               ← Team-specific context (actively updated)
  │   └── Documentation/          ← Team-specific docs (most current)
  ├── /frontend-team/             ← Team 2 repository
  │   ├── CLAUDE.md               ← Team-specific context (actively updated)
  │   └── Documentation/          ← Team-specific docs (most current)
  └── /mobile-team/               ← Team 3 repository
      ├── CLAUDE.md               ← Team-specific context (actively updated)
      └── Documentation/          ← Team-specific docs (most current)
```

### Key Challenges

1. **Stale Upper Context**: Opening root folder shows outdated context if teams updated their repos
2. **Documentation Drift**: Upper-level docs don't reflect lower-level reality
3. **Bidirectional Sync**: Need to push company-wide changes down AND pull team updates up
4. **Cross-Team Coordination**: Implementing features affecting multiple teams from upper level

## 🏗️ Solution Architecture

### Layer Detection System

**CLAUDE: When opening a folder, automatically detect context hierarchy:**

```bash
# Detection Algorithm
1. Check if current folder has CLAUDE.md
2. Scan subdirectories for nested CLAUDE.md files
3. Identify hierarchy level:
   - ROOT: Has CLAUDE.md + contains child CLAUDE.md files
   - TEAM: Has CLAUDE.md + no child CLAUDE.md files
   - STANDALONE: Has CLAUDE.md + isolated project
4. Apply appropriate behavior based on level
```

### Hierarchical Context Inheritance

**When opening UPPER-LEVEL (root) folder:**

```markdown
## 🚨 HIERARCHICAL CONTEXT DETECTED

**CLAUDE: This is a MULTI-LEVEL repository structure.**

### Detected Structure:
- **Level**: ROOT (Orchestration Layer)
- **Child Contexts**: 3 team repositories detected
  - /backend-team/ (Last updated: 2025-10-12)
  - /frontend-team/ (Last updated: 2025-10-13)
  - /mobile-team/ (Last updated: 2025-10-10)

### Automatic Behaviors:
1. ✅ **Context Awareness**: Load and reference child CLAUDE.md files for full context
2. ✅ **Documentation Aggregation**: Pull documentation from child repos for cross-team view
3. ✅ **Staleness Detection**: Alert if child contexts more recent than root context
4. ✅ **Coordinated Changes**: Enable multi-repo feature implementation from root
5. ✅ **Bidirectional Sync**: Propagate root-level changes to children when appropriate

**YOU ARE IN ORCHESTRATION MODE** - Changes can affect multiple teams.
```

## 🔄 Context Synchronization Mechanisms

### 1. **Upward Sync (Child → Root)**

**Purpose**: Keep root context aware of team-level changes

**CLAUDE Automatic Behavior:**

```
When opening ROOT folder:
1. Scan all child CLAUDE.md files
2. Extract key metadata:
   - Last updated timestamps
   - Technology stack changes
   - New critical workflows
   - Documentation updates
3. Alert if root context is stale:
   "⚠️ Child contexts have updates:
    - /backend-team/CLAUDE.md updated 2 days ago
    - New feature documented: Payment Gateway Integration
    - Suggest syncing root context with child updates"
4. Offer to sync:
   "Would you like me to:
    a) Show summary of child context changes
    b) Update root CLAUDE.md with child changes
    c) Continue with current root context"
```

**Context Refresh Command:**

```bash
# User can trigger manual sync
User: "Refresh context from child repos"
User: "Sync with team contexts"
User: "Update root context"

# Claude automatically:
1. Reads all child CLAUDE.md files
2. Generates change summary
3. Offers to update root CLAUDE.md
4. Updates root documentation index
```

### 2. **Downward Sync (Root → Child)**

**Purpose**: Propagate company-wide standards/changes to teams

**CLAUDE Automatic Behavior:**

```
When implementing changes at ROOT level that affect children:
1. Detect scope of change (which teams affected)
2. Alert about propagation need:
   "This change affects multiple teams:
    - /backend-team/ (API contract change)
    - /frontend-team/ (API integration update)

    I can create coordinated PRPs for each team."
3. Offer multi-team PRP generation
4. Track synchronization status
```

**Propagation Pattern:**

```bash
# User makes company-wide decision
User: "We're switching authentication from JWT to OAuth2"

# Claude in ROOT context:
"I'll help implement this cross-team change.

Detected Impact:
✓ /backend-team/ - Auth service implementation (HIGH)
✓ /frontend-team/ - Login flow changes (HIGH)
✓ /mobile-team/ - Auth flow changes (HIGH)

Propagation Strategy:
1. Generate master PRP at root level
2. Generate team-specific PRPs for each affected repo:
   - /backend-team/PRPs/active/AUTH-123-oauth2-migration.md
   - /frontend-team/PRPs/active/AUTH-123-oauth2-frontend.md
   - /mobile-team/PRPs/active/AUTH-123-oauth2-mobile.md
3. Each team PRP references root master PRP
4. Track implementation status across teams

Would you like me to generate these coordinated PRPs?"
```

### 3. **Cross-Team Feature Coordination**

**Purpose**: Implement features spanning multiple teams from root level

**Pattern: Orchestrated Multi-Repo Implementation**

```markdown
## Orchestrated Implementation Protocol

**CLAUDE: When implementing from ROOT affecting multiple teams:**

### Step 1: Context Aggregation
```bash
1. Load all relevant child CLAUDE.md contexts
2. Analyze documentation from affected teams:
   - Read /backend-team/.claude/documentation/
   - Read /frontend-team/.claude/documentation/
   - Read /mobile-team/.claude/documentation/
3. Build unified understanding of current architecture
4. Identify integration points and dependencies
```

### Step 2: Master Planning
```bash
1. Generate ROOT-level master PRP:
   - Location: /PRPs/active/[TICKET]-[feature]-MASTER.md
   - Contains: Overall strategy, team responsibilities, integration plan
2. Generate team-specific child PRPs:
   - Location: /[team]/PRPs/active/[TICKET]-[feature]-[team].md
   - Contains: Team-specific implementation, references master PRP
3. Define implementation sequence:
   - Phase 1: Backend API changes
   - Phase 2: Frontend/Mobile integration (parallel)
   - Phase 3: Testing and deployment
```

### Step 3: Sequential Implementation
```bash
1. Implement backend changes first:
   - Work in /backend-team/ context
   - Reference their CLAUDE.md patterns
   - Update their documentation
2. Implement frontend changes:
   - Work in /frontend-team/ context
   - Reference their CLAUDE.md patterns
   - Integrate with new backend APIs
3. Implement mobile changes:
   - Work in /mobile-team/ context
   - Reference their CLAUDE.md patterns
   - Integrate with new backend APIs
```

### Step 4: Documentation Propagation
```bash
1. Update each team's documentation:
   - /backend-team/Documentation/API/[new-endpoints].md
   - /frontend-team/Documentation/Features/[new-feature].md
   - /mobile-team/Documentation/Features/[new-feature].md
2. Update root-level documentation:
   - /Documentation/Cross_Team_Features/[feature].md
   - Links to team-specific docs
3. Update root CLAUDE.md if architecture changed
```
```

## 📋 Enhanced CLAUDE.md Structure

### Root-Level CLAUDE.md Template

```markdown
# Company Root - Multi-Team Context Engineering

## 🚨 HIERARCHICAL CONTEXT SYSTEM

**CLAUDE: This is a ROOT-LEVEL multi-team repository.**

### Context Hierarchy
```yaml
Repository_Type: Root Orchestration Layer
Child_Repositories:
  - Path: /backend-team/
    Type: Node.js + Express API
    CLAUDE_Context: /backend-team/CLAUDE.md
    Last_Synced: 2025-10-13

  - Path: /frontend-team/
    Type: React + TypeScript
    CLAUDE_Context: /frontend-team/CLAUDE.md
    Last_Synced: 2025-10-13

  - Path: /mobile-team/
    Type: React Native
    CLAUDE_Context: /mobile-team/CLAUDE.md
    Last_Synced: 2025-10-10
```

### 🔄 Context Synchronization Protocol

**CLAUDE: Always apply these rules when working in root context:**

#### 1. Context Loading Strategy
- **ALWAYS** scan child CLAUDE.md files before major implementations
- **REFERENCE** child documentation for team-specific patterns
- **DETECT** staleness and offer to refresh
- **AGGREGATE** understanding across all teams

#### 2. Change Impact Analysis
```bash
# Before any change, analyze scope:
1. Single team impact → Work in that team's context
2. Multi-team impact → Orchestrated implementation
3. Company-wide policy → Downward propagation to all teams
```

#### 3. PRP Coordination
```bash
# Multi-team features:
1. Master PRP at root: /PRPs/active/[TICKET]-[feature]-MASTER.md
2. Child PRPs per team: /[team]/PRPs/active/[TICKET]-[feature]-[team].md
3. Cross-reference between master and children
4. Track completion across all teams
```

#### 4. Documentation Strategy
```bash
# Root documentation = aggregation layer:
- High-level architecture across teams
- Integration points between teams
- Company-wide standards and policies
- Links to team-specific detailed docs

# Team documentation = detailed implementation:
- Team-specific patterns and conventions
- Detailed API documentation
- Component libraries and utilities
```

## 🎯 CROSS-TEAM WORKFLOWS

### Workflow: Implementing Multi-Team Feature

**Trigger:** User requests feature affecting multiple teams

**CLAUDE Response Pattern:**
```
"I'll implement [feature] affecting multiple teams.

Context Analysis:
✓ Loaded /backend-team/CLAUDE.md - Laravel API patterns
✓ Loaded /frontend-team/CLAUDE.md - React patterns
✓ Loaded /mobile-team/CLAUDE.md - React Native patterns

Impact Assessment:
- Backend: API endpoint creation, database migration
- Frontend: New component, API integration
- Mobile: New screen, API integration

Implementation Strategy:
1. Generate master PRP for overall coordination
2. Create team-specific PRPs:
   - FEAT-123-[feature]-MASTER.md (root)
   - FEAT-123-[feature]-backend.md (backend-team)
   - FEAT-123-[feature]-frontend.md (frontend-team)
   - FEAT-123-[feature]-mobile.md (mobile-team)
3. Sequential implementation:
   - Phase 1: Backend API (foundation)
   - Phase 2: Frontend + Mobile (parallel)
4. Coordinated documentation updates

Proceed with this strategy?"
```

## 📊 Child Team Context Template

### Team-Level CLAUDE.md Addition

```markdown
## 🔗 HIERARCHICAL CONTEXT

**CLAUDE: This is a TEAM-LEVEL repository within a multi-team structure.**

### Parent Context
- **Root Repository**: /company-root/
- **Root CLAUDE.md**: ../CLAUDE.md
- **Coordination**: Changes here may need root-level sync

### Sync Protocol

**CLAUDE: When making significant changes:**
1. ✅ Update this team's CLAUDE.md
2. ✅ Update team documentation
3. ✅ Suggest root sync if architectural changes:
   "This change updates our API architecture.
    Suggest syncing with root context:
    - Update root CLAUDE.md with new patterns
    - Update root documentation references"

**CLAUDE: When receiving root-level changes:**
1. ✅ Check for coordinated PRPs from root
2. ✅ Reference root master PRP for context
3. ✅ Implement team-specific portion
4. ✅ Update team documentation
```

## 🛠️ Synchronization Commands

### Automatic Detection

**CLAUDE automatically detects and prompts:**

```bash
# When opening root folder with outdated context:
"⚠️ Context Synchronization Notice:

 Child repositories have updates since last root sync:
 - /backend-team/: 3 documentation updates, 1 CLAUDE.md change
 - /frontend-team/: 2 documentation updates
 - /mobile-team/: No changes

 Would you like to:
 a) View summary of changes
 b) Sync root context now
 c) Continue with current root context"
```

### User-Triggered Sync

```bash
# Users can explicitly request sync:
User: "Sync context with child repos"
User: "Refresh team documentation"
User: "Update root context from teams"
User: "Show child context changes"

# Claude responds with aggregated summary and sync options
```

## 🎯 Implementation Workflow Examples

### Example 1: Single-Team Change (No Coordination Needed)

```
User: "Fix a bug in the backend login endpoint"

Claude: "I'll fix the backend login bug.

Context Analysis:
✓ This affects only /backend-team/
✓ Loading /backend-team/CLAUDE.md context
✓ Switching to team-level context

[Works within /backend-team/ context]

Implementation complete. This is team-isolated.
No root-level sync needed."
```

### Example 2: Multi-Team Feature (Coordination Needed)

```
User: "Add real-time notifications for order updates"

Claude: "I'll implement real-time order notifications.

Context Analysis:
✓ Multi-team feature detected
✓ Loading all team contexts:
  - /backend-team/: WebSocket server setup
  - /frontend-team/: Notification UI component
  - /mobile-team/: Push notification integration

Orchestrated Implementation:
1. Master PRP: /PRPs/active/NOTIF-456-realtime-notifications-MASTER.md
2. Backend PRP: /backend-team/PRPs/active/NOTIF-456-websocket-server.md
3. Frontend PRP: /frontend-team/PRPs/active/NOTIF-456-notification-ui.md
4. Mobile PRP: /mobile-team/PRPs/active/NOTIF-456-push-notifications.md

Implementation Sequence:
- Phase 1: Backend WebSocket server + event system
- Phase 2: Frontend notification component (parallel with Mobile)
- Phase 3: Mobile push notification integration

Proceeding with master PRP generation..."
```

### Example 3: Company-Wide Policy (Downward Propagation)

```
User: "We need to implement GDPR data export across all systems"

Claude: "I'll implement GDPR-compliant data export company-wide.

Cross-Team Impact Analysis:
✓ All teams affected (HIGH priority)
✓ Requires coordinated implementation
✓ Legal/compliance requirement

Propagation Strategy:
1. Root Master PRP:
   - Overall GDPR strategy
   - Company-wide data inventory
   - Export format specification

2. Team-Specific PRPs:
   - Backend: API endpoints for data export, user data aggregation
   - Frontend: Data export UI, privacy dashboard
   - Mobile: Data export feature, privacy settings

3. Documentation Requirements:
   - Legal: GDPR compliance documentation
   - Technical: Data export implementation guide
   - User-facing: Privacy policy updates

4. Implementation Timeline:
   - Week 1: Backend data export API
   - Week 2: Frontend + Mobile integration
   - Week 3: Testing + legal review

Generating coordinated PRPs for all teams..."
```

## ✅ Validation & Quality Assurance

### Root-Level Validation

```bash
# After multi-team implementation:
1. Validate each team's implementation:
   - cd /backend-team && npm test && npm run build
   - cd /frontend-team && npm test && npm run build
   - cd /mobile-team && npm test

2. Validate integration:
   - Backend + Frontend integration tests
   - Backend + Mobile integration tests
   - End-to-end workflow tests

3. Documentation check:
   - Root documentation updated
   - All team docs updated
   - Cross-references validated
```

## 📝 Best Practices

### For Root-Level (Orchestration) Work

1. **Always load child contexts** before major decisions
2. **Generate coordinated PRPs** for multi-team features
3. **Maintain master documentation** as aggregation layer
4. **Track synchronization state** with timestamps
5. **Respect team autonomy** - coordinate, don't dictate implementation details

### For Team-Level Work

1. **Update team documentation** regularly
2. **Sync with root context** for architectural changes
3. **Reference root policies** for company-wide standards
4. **Signal upward** when changes affect other teams
5. **Maintain team-specific patterns** while aligning with root standards

### For Context Synchronization

1. **Timestamp everything** - track last sync times
2. **Detect staleness automatically** - prompt for refresh
3. **Aggregate intelligently** - don't duplicate, reference
4. **Bidirectional awareness** - both up and down hierarchy
5. **Explicit coordination** - make multi-team impacts clear

## 🚨 Critical Rules

### Never Do These

1. ❌ **Never work at root without loading child contexts** for multi-team changes
2. ❌ **Never duplicate team documentation** at root (reference instead)
3. ❌ **Never assume root context is current** without checking child updates
4. ❌ **Never implement team-specific code at root** without switching context
5. ❌ **Never skip coordination** for changes affecting multiple teams

### Always Do These

1. ✅ **Always detect hierarchy** when opening folder
2. ✅ **Always check sync status** before major implementations
3. ✅ **Always generate coordinated PRPs** for multi-team features
4. ✅ **Always update relevant documentation** at appropriate levels
5. ✅ **Always validate across teams** for integrated features

---

**This hierarchical context synchronization system enables effective multi-team coordination while respecting team autonomy and avoiding context duplication.**

**Framework Enhancement Version:** 1.1.0 - Hierarchical Context Sync
**Created:** 2025-10-13
**Use Case:** Multi-team organizations with nested repositories
