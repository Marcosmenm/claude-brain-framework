# Multi-Team Company Example

**Practical example of hierarchical context synchronization**

This example demonstrates exactly your scenario: A company with three teams (backend, frontend, mobile), each working on their own repositories, with a parent root-level repository for orchestration.

## 📁 Structure

```
/multi-team-company/                    ← You work here (root orchestration)
├── CLAUDE.md                           ← Root context (orchestration layer)
├── /backend-team/                      ← Backend team repository
│   ├── CLAUDE.md                       ← Backend team context
│   └── .claude/documentation/          ← Backend docs (actively updated)
├── /frontend-team/                     ← Frontend team repository
│   ├── CLAUDE.md                       ← Frontend team context
│   └── .claude/documentation/          ← Frontend docs (actively updated)
└── /mobile-team/                       ← Mobile team repository
    ├── CLAUDE.md                       ← Mobile team context
    └── .claude/documentation/          ← Mobile docs (actively updated)
```

## 🎯 Your Scenario Addressed

### Problem 1: Stale Upper Context
**Solution:** Root CLAUDE.md automatically detects and alerts when child contexts are more recent

```
When you open /multi-team-company/:
✓ Claude scans for child CLAUDE.md files
✓ Compares last_synced timestamps
✓ Alerts: "⚠️ Child contexts updated:
  - /backend-team/ updated 2 days ago
  - New feature: Payment Gateway Integration"
✓ Offers to sync root context
```

### Problem 2: Documentation Drift
**Solution:** Root context references (not duplicates) child documentation

```
Root documentation = Aggregation layer:
- High-level architecture
- Integration points
- Company-wide standards
- LINKS to child team docs (never duplicates)

Team documentation = Source of truth:
- Detailed implementation patterns
- API documentation
- Team-specific guides
```

### Problem 3: Bidirectional Sync
**Solution:** Upward and downward sync mechanisms

**Upward (Team → Root):**
```
Backend team implements new API pattern:
1. Backend updates their CLAUDE.md
2. Next time you open root, Claude alerts:
   "Backend team updated API patterns - suggest reviewing"
3. You can choose to:
   - View summary of changes
   - Update root context with new patterns
   - Continue with current context
```

**Downward (Root → Teams):**
```
You decide: "Switch to OAuth2 authentication company-wide":
1. Claude generates master PRP at root
2. Claude generates child PRPs for each team:
   - /backend-team/PRPs/active/AUTH-123-oauth2-backend.md
   - /frontend-team/PRPs/active/AUTH-123-oauth2-frontend.md
   - /mobile-team/PRPs/active/AUTH-123-oauth2-mobile.md
3. Each team PRP references master PRP
4. Implementation coordinated across all teams
```

### Problem 4: Multi-Team Features
**Solution:** Orchestrated implementation from root

```
You: "Implement real-time notifications"

Claude:
"This affects all three teams.

Orchestrated Implementation:
1. Master PRP at root: NOTIF-456-notifications-MASTER.md
2. Backend PRP: WebSocket server implementation
3. Frontend PRP: Notification UI component
4. Mobile PRP: Push notification integration

Implementation sequence:
- Phase 1: Backend (foundation)
- Phase 2: Frontend + Mobile (parallel, after backend)

Generating coordinated PRPs..."
```

## 🚀 Quick Start

### Step 1: Set Up Root Context

1. Copy `CLAUDE_MD_ROOT_ORCHESTRATION.md` template to `/multi-team-company/CLAUDE.md`
2. Fill in your company details:
   - Company name
   - Team names and paths
   - Integration points
3. Update `last_synced` timestamps

### Step 2: Set Up Team Contexts

For each team (backend, frontend, mobile):

1. Copy `CLAUDE_MD_TEAM_LEVEL.md` template to team folder
2. Fill in team-specific details:
   - Team name and tech stack
   - Domain responsibilities
   - Integration points with other teams
3. Create team documentation structure

### Step 3: Initial Sync

1. Open root context
2. Say: "Sync with child team contexts"
3. Claude will scan all teams and build unified understanding

## 📋 Common Workflows

### Workflow 1: You Working at Root Level

```bash
# Scenario: Fix bug in backend
cd /multi-team-company/
# Open Claude

You: "Fix authentication bug in backend"

Claude:
"This affects backend team only.
Loading /backend-team/CLAUDE.md context...
[Switches to backend team patterns]
[Implements fix]
No root sync needed (isolated change)."
```

### Workflow 2: Multi-Team Feature Implementation

```bash
# Scenario: Add new feature affecting all teams
cd /multi-team-company/
# Open Claude

You: "Add user profile customization"

Claude:
"Multi-team feature detected.
Loading all team contexts...

Impact:
- Backend: API endpoints for profile data
- Frontend: Profile customization UI
- Mobile: Profile screen updates

Generating orchestrated PRPs...
[Creates master + 3 team PRPs]
[Implements sequentially across teams]"
```

### Workflow 3: Backend Team Works Independently

```bash
# Scenario: Backend team opens their folder directly
cd /multi-team-company/backend-team/
# Open Claude

Backend Dev: "Optimize database queries"

Claude:
"Team-level context detected.
Working in backend-team context...
[Implements optimization]
[Updates backend documentation]

✓ Complete. Root sync suggested:
  - New query optimization pattern
  - May benefit other teams
  Would you like to document for root?"
```

### Workflow 4: Company-Wide Policy Change

```bash
# Scenario: Implement GDPR across all systems
cd /multi-team-company/
# Open Claude

You: "Implement GDPR data export"

Claude:
"Company-wide requirement - all teams affected.

Downward Propagation:
1. Root master PRP: Legal requirements, data format
2. Backend PRP: Export API implementation
3. Frontend PRP: Export UI in settings
4. Mobile PRP: Export feature in app

Coordinated timeline:
- Week 1: Backend
- Week 2: Frontend + Mobile
- Week 3: Testing

Generating coordinated PRPs for all teams..."
```

### Workflow 5: Refreshing Root Context

```bash
# Scenario: You haven't opened root in a week
cd /multi-team-company/
# Open Claude (automatically detects staleness)

Claude:
"⚠️ Context Synchronization Notice:

Child repositories have updates:
- /backend-team/: Updated 3 days ago
  - New feature: Payment webhook handling
  - 2 documentation updates
- /frontend-team/: Updated 1 day ago
  - New component library pattern
- /mobile-team/: No changes

Would you like to:
a) View detailed change summary
b) Sync root context now
c) Continue with current context"

You: "Sync now"

Claude:
"Syncing with child contexts...
✓ Loaded backend updates
✓ Loaded frontend updates
✓ Root context refreshed
✓ Integration points validated

Summary of changes:
- Backend now handles payment webhooks
- Frontend has new component pattern
- Update root timestamp: 2025-10-13

You're now up to date with all teams."
```

## 🎯 Key Benefits

### For You (Root Level)

1. **Always Aware**: Claude alerts when child contexts updated
2. **Coordinated Features**: Easily implement multi-team features
3. **Policy Propagation**: Push company-wide changes to all teams
4. **No Duplication**: Root docs reference child docs (never duplicate)
5. **Intelligent Context**: Claude loads all relevant team contexts automatically

### For Teams (Team Level)

1. **Autonomy**: Teams work in their own context with their patterns
2. **Awareness**: Claude alerts when part of coordinated feature
3. **Standards**: Receive company-wide policy updates from root
4. **Documentation**: Maintain their own detailed docs
5. **Integration**: Clear integration points with other teams

## 🔧 Maintenance

### Weekly Sync (Recommended)

```bash
cd /multi-team-company/
# Say to Claude:
"Refresh context from all teams"

# Claude will:
1. Scan all child CLAUDE.md files
2. Show summary of changes
3. Update root context
4. Update integration documentation
```

### After Major Features

```bash
# When a team completes major feature:
# At root level, say:
"Sync [team-name] updates to root"

# Claude will:
1. Read team's updated CLAUDE.md
2. Read team's new documentation
3. Suggest root documentation updates
4. Update root context if architectural changes
```

## 📖 Templates Used

- **Root**: [CLAUDE_MD_ROOT_ORCHESTRATION.md](../../templates/CLAUDE_MD_ROOT_ORCHESTRATION.md)
- **Teams**: [CLAUDE_MD_TEAM_LEVEL.md](../../templates/CLAUDE_MD_TEAM_LEVEL.md)
- **Core Concepts**: [HIERARCHICAL_CONTEXT_SYNC.md](../../core/HIERARCHICAL_CONTEXT_SYNC.md)

## ✅ Success Indicators

**You'll know it's working when:**

- Opening root folder shows staleness alerts if teams updated
- Multi-team features automatically generate coordinated PRPs
- Company-wide changes propagate to all team PRPs
- Root documentation stays high-level (no team detail duplication)
- Teams signal upward when integration points change
- Claude switches context appropriately (root vs team)

---

**This example directly addresses your three-team scenario with practical, actionable patterns for hierarchical context management.**
