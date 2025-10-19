# Quick Setup Guide - Multi-Team Hierarchical Context

**Get your multi-team context engineering running in 15 minutes**

## 🎯 Your Goal

Set up hierarchical context engineering for:
```
/your-company-root/
├── /backend-team/      ← Team 1 with their own CLAUDE.md
├── /frontend-team/     ← Team 2 with their own CLAUDE.md
└── /mobile-team/       ← Team 3 with their own CLAUDE.md
```

## ⚡ 15-Minute Setup

### Step 1: Root Context Setup (5 minutes)

```bash
# 1. Copy root template
cd /your-company-root/
cp /path/to/claude-brain-framework/templates/CLAUDE_MD_ROOT_ORCHESTRATION.md CLAUDE.md

# 2. Open CLAUDE.md and fill in (replace [bracketed] values):
#    - Company name
#    - Team paths and names
#    - Tech stacks
#    - Integration points
```

**Minimal required changes:**
```yaml
# In CLAUDE.md, update this section:
Child_Repositories:
  - path: /backend-team/              # ← Your actual folder name
    type: Node.js + Express           # ← Your actual tech
    domain: API Services              # ← What they do
    claude_context: /backend-team/CLAUDE.md
    last_synced: 2025-10-13           # ← Today's date
    status: active

  # Repeat for each team...
```

### Step 2: Team Contexts Setup (3 minutes per team)

```bash
# For EACH team folder:
cd /your-company-root/backend-team/
cp /path/to/claude-brain-framework/templates/CLAUDE_MD_TEAM_LEVEL.md CLAUDE.md

# Open CLAUDE.md and fill in:
#    - Team name
#    - Tech stack
#    - Integration points with other teams
```

**Minimal required changes:**
```yaml
# In each team's CLAUDE.md, update:
Team_Name: Backend Team               # ← Your team name
Primary_Responsibility: API Services  # ← What they own

Technology_Stack:
  Primary_Language: TypeScript        # ← Your stack
  Framework: Express.js               # ← Your framework
  Database: PostgreSQL                # ← Your database

Integrations:
  Provides:
    - type: REST API                  # ← What you provide
      consumers: [frontend, mobile]   # ← Who uses it
```

### Step 3: Initialize Documentation (3 minutes)

```bash
# At ROOT level:
cd /your-company-root/
mkdir -p .claude/documentation/Architecture
mkdir -p .claude/documentation/Standards
mkdir -p .claude/documentation/Workflows

# For EACH team:
cd backend-team/  # Repeat for each team
mkdir -p .claude/documentation/Core_Systems
mkdir -p .claude/documentation/Features
mkdir -p .claude/documentation/Patterns
```

### Step 4: Test Setup (1 minute)

```bash
# Open Claude at root level and say:
"Test hierarchical context detection"

# Claude should respond with:
# ✓ Root orchestration mode detected
# ✓ Found 3 child repositories
# ✓ Context hierarchy initialized
# ✓ Ready for multi-team coordination
```

## ✅ Verification Checklist

After setup, verify these work:

```bash
# 1. Staleness Detection
# - Open root, Claude should check child timestamps
# - If child updated, Claude alerts

# 2. Multi-Team Feature
# Open root and say: "Implement [multi-team feature]"
# Claude should:
#   ✓ Detect it affects multiple teams
#   ✓ Offer to generate coordinated PRPs
#   ✓ Load all relevant team contexts

# 3. Team Isolation
# Open a team folder and say: "Fix [team-specific bug]"
# Claude should:
#   ✓ Work in team context only
#   ✓ Not involve other teams
#   ✓ Use team-specific patterns

# 4. Context Sync
# At root, say: "Sync with child contexts"
# Claude should:
#   ✓ Scan all team CLAUDE.md files
#   ✓ Report any changes since last sync
#   ✓ Offer to update root context
```

## 🎯 Common Issues & Fixes

### Issue 1: Claude doesn't detect hierarchy

**Fix:** Ensure each team folder has `CLAUDE.md` file (exact name, not `claude.md` or `Claude.md`)

```bash
# Check:
ls /your-company-root/*/CLAUDE.md
# Should show all team CLAUDE.md files
```

### Issue 2: Staleness not detected

**Fix:** Ensure `last_synced` timestamps are set in root CLAUDE.md

```yaml
# In root CLAUDE.md:
Child_Repositories:
  - path: /backend-team/
    last_synced: 2025-10-13  # ← Must be present
```

### Issue 3: Multi-team features not coordinated

**Fix:** Ensure integration points are documented

```yaml
# In root CLAUDE.md:
Integration_Points:
  - type: REST API
    provider: backend-team
    consumers: [frontend-team, mobile-team]  # ← Must list dependencies
```

### Issue 4: Teams don't reference root

**Fix:** Ensure team CLAUDE.md has parent reference

```yaml
# In each team CLAUDE.md:
Parent_Repository:
  path: ../
  root_claude_md: ../CLAUDE.md  # ← Must be present
```

## 🚀 Next Steps

### Immediate (Today)

1. ✅ Set up root + team CLAUDE.md files
2. ✅ Test hierarchical detection
3. ✅ Try one multi-team feature implementation

### This Week

1. Document your current architecture
2. Add team-specific documentation
3. Run full context sync
4. Train teams on signaling upward for changes

### Ongoing

1. Weekly context sync at root level
2. Update team contexts as they evolve
3. Document new integration points
4. Refine cross-team workflows

## 💡 Usage Examples

### Example 1: Daily Work (Single Team)

```bash
# Backend team member opens their folder
cd /company-root/backend-team/

# In Claude:
Dev: "Optimize user query performance"

Claude:
"Working in backend team context...
[Implements optimization using backend patterns]
[Updates backend documentation]
No multi-team impact - done."
```

### Example 2: Weekly Planning (Root Level)

```bash
# You plan new feature at root
cd /company-root/

# In Claude:
You: "We need to add social login"

Claude:
"Multi-team feature affecting:
- Backend: OAuth integration
- Frontend: Login button UI
- Mobile: Native social auth

Generating coordinated PRPs:
- SOCIAL-123-social-login-MASTER.md (root)
- SOCIAL-123-oauth-backend.md (backend team)
- SOCIAL-123-login-ui-frontend.md (frontend team)
- SOCIAL-123-native-auth-mobile.md (mobile team)

Implementation sequence:
1. Backend OAuth setup (Week 1)
2. Frontend + Mobile integration (Week 2)

Ready to generate PRPs?"
```

### Example 3: Context Refresh (Root Level)

```bash
# You haven't checked in for a few days
cd /company-root/

# In Claude (automatically):
Claude:
"⚠️ Child context updates detected:

- /backend-team/: Updated 2 days ago
  - New webhook handling system
  - Database optimization patterns

- /frontend-team/: Updated yesterday
  - New component library structure

Would you like to sync root context?"

You: "Yes"

Claude:
"Syncing...
✓ Backend updates loaded
✓ Frontend updates loaded
✓ Root context refreshed
You're now up to date."
```

## 📚 Templates Reference

**Use these templates:**

- **Root Setup**: `templates/CLAUDE_MD_ROOT_ORCHESTRATION.md`
- **Team Setup**: `templates/CLAUDE_MD_TEAM_LEVEL.md`
- **Full Guide**: `core/HIERARCHICAL_CONTEXT_SYNC.md`
- **Example**: `examples/multi-team-company/README.md`

## 🆘 Getting Help

If something isn't working:

1. **Check CLAUDE.md files exist** in all locations
2. **Verify timestamps** are set correctly
3. **Review integration points** are documented
4. **Test with simple request** first

**Common question:** "Do I need to run any init commands?"

**Answer:** No! Once CLAUDE.md files are in place, Claude automatically detects hierarchy when you open the folder. Just start working naturally.

---

**You're ready! Open your root folder in Claude and start with:** "Test hierarchical context detection"
