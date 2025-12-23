# CLAUDE.md - [Project Name] (Token-Optimized)

**[Brief 1-sentence project description]**

## Project Structure
- **Component A**: [Technology] ([path/to/component/](path/to/component/))
- **Component B**: [Technology] ([path/to/component/](path/to/component/))
- **Database**: [Database type] @ [connection details]

## Quick Start
```bash
# Component A: [start command]
# Component B: [start command]
# Tests: [test command]
```

---

## 🚨 Critical Rules

### Database Safety
- ❌ NEVER run destructive commands: `[list specific commands for your stack]`
- ✅ Database changes are [manual migrations / specific process]

### Server Interaction
- ❌ NEVER execute SSH/deployment commands without explicit approval
- ✅ Always ask first and explain why

### Git Commits
- ❌ NO "Generated with Claude Code" footers
- ✅ Keep commits clean and professional

### Chat History
- ✅ SAVE to `.claude/chat-history/[TICKET]_YYYYMMDD_HHMM_chat.md`
- ✅ Use BASH with `>>` to append (silent operation)

---

## 📚 Documentation Index

**CLAUDE: Fetch documentation only when needed. Don't load everything upfront.**

**Core Systems** (`.claude/documentation/Core_Systems/`):
- `System_A_Documentation.md` - [Brief description]
- `System_B_Documentation.md` - [Brief description]
- `Feature_X_Documentation.md` - [Brief description]

**Specialized Features** (`.claude/documentation/Specialized_Features/`):
- `Feature_Y_Documentation.md` - [Brief description]

**Component Guides:**
- [ComponentA/CLAUDE.md](ComponentA/CLAUDE.md) - [Technology-specific patterns]
- [ComponentB/CLAUDE.md](ComponentB/CLAUDE.md) - [Technology-specific patterns]

**When to Fetch:**
- **System A questions** → Read `System_A_Documentation.md`
- **Feature X work** → Read `Feature_X_Documentation.md`
- **Component A patterns** → Read `ComponentA/CLAUDE.md`

---

## 🧠 Framework Philosophy

**CLAUDE: Read `.claude/FRAMEWORK_PRINCIPLES.md` on session start**

Daily development standards (Claude-to-Claude protocol):
- Documentation: Pointer-based, token-optimized
- Code comments: Simple, semantic (no decoration)
- Quality checks: Auto-execute before creating docs
- PRPs: Auto-generate for >3 files or business logic
- Integration: Enhance existing, never create parallel systems

**Framework reference:** `/Users/marcosm/Documents/dev/claude-brain-framework/`

---

## 🚀 Methodology References

**CLAUDE: Fetch these only when working on complex features:**

### For Complex Features (>3 files or business logic):
- **PRP Workflow**: Read `CLAUDE_FULL_METHODOLOGY.md` lines [X-Y]
- **Development Approach**: Read `CLAUDE_FULL_METHODOLOGY.md` lines [X-Y]

### For Database Work:
- **Migration Guide**: Read `.claude/documentation/Database_Guidelines.md`

### For Deployment:
- **Deployment Process**: Read `README-DEPLOYMENT.md`

---

## 🎯 Architecture Quick Reference

### Authentication
- **System**: [Auth technology]
- **Details**: Read `User_Management_Documentation.md` when needed

### Key Integrations
- **Integration A**: [Technology/service]
- **Integration B**: [Technology/service]

### Tech Stack
- **Backend**: [Framework + version]
- **Frontend**: [Framework + version]
- **Database**: [Database + version]
- **Other**: [Key libraries/tools]

---

## 📊 Token Optimization

This CLAUDE.md uses on-demand documentation loading:
- Minimal upfront context (~5-8k tokens vs ~40-50k traditional)
- Documentation fetched only when relevant to task
- Expected token savings: 25-35% average

**Full methodology available in:** `CLAUDE_FULL_METHODOLOGY.md`

---

**Framework:** claude-brain-framework v1.4.0
**Template:** Token-Optimized
**Last Updated:** YYYY-MM-DD