# 🧠 Claude Skills Integration

**13 official Anthropic skills for specialized capabilities**

---

## What This Is

Official skills from Anthropic providing specialized workflows for development, documents, creative work, and enterprise tasks.

**Repository:** https://github.com/anthropics/skills
**Location:** `claude-skills/anthropic/`
**Last Synced:** 2025-11-11

---

## Quick Navigation

| Resource | Purpose |
|----------|---------|
| **[ANTHROPIC_SKILLS_CATALOG.md](ANTHROPIC_SKILLS_CATALOG.md)** | Complete skills reference - read for skill details |
| **[QUICK_START.md](QUICK_START.md)** | 10-minute practical getting started guide |
| **[../core/SKILLS_INTEGRATION.md](../core/SKILLS_INTEGRATION.md)** | Integration strategy for framework developers |
| **`anthropic/[skill]/SKILL.md`** | Actual skill instructions - load when needed |

---

## Available Skills

**Read `anthropic/[skill-name]/SKILL.md` when you need the skill. Details in [ANTHROPIC_SKILLS_CATALOG.md](ANTHROPIC_SKILLS_CATALOG.md)**

| Category | Skills |
|----------|--------|
| **Development** | mcp-builder, artifacts-builder, webapp-testing |
| **Documents** | pdf, docx, xlsx, pptx (in `document-skills/`) |
| **Creative** | algorithmic-art, canvas-design, theme-factory |
| **Enterprise** | brand-guidelines, internal-comms, slack-gif-creator |
| **Meta** | skill-creator, template-skill |

---

## When to Load Skills

### By Tech Stack
- **Laravel/PHP** → mcp-builder, pdf, webapp-testing
- **React** → artifacts-builder, canvas-design, webapp-testing
- **Python** → mcp-builder, xlsx, pdf

### By Task
- **"Generate PDF"** → Load `anthropic/document-skills/pdf/SKILL.md`
- **"Build MCP server"** → Load `anthropic/mcp-builder/SKILL.md`
- **"Create custom skill"** → Load `anthropic/skill-creator/SKILL.md`

**Complete selection guide:** [ANTHROPIC_SKILLS_CATALOG.md#skill-selection-guide](ANTHROPIC_SKILLS_CATALOG.md#skill-selection-guide)

---

## Directory Structure

```
claude-skills/
├── anthropic/           # Official skills (git cloned)
│   ├── mcp-builder/
│   ├── document-skills/ (pdf, docx, xlsx, pptx)
│   ├── skill-creator/
│   └── ...
├── custom/              # User-created skills
└── skills-manifest.json # Version tracking (not implemented yet)
```

**Skill structure:**
```
skill-name/
├── SKILL.md          # YAML + instructions
└── Optional: scripts/, references/, assets/
```

---

## Usage in Projects

Projects using the framework can list recommended skills in their CLAUDE.md:

```markdown
## 🎯 RECOMMENDED SKILLS

**Location:** /path/to/framework/claude-skills/anthropic/

When working on:
- API integration → Load mcp-builder/SKILL.md
- PDF generation → Load document-skills/pdf/SKILL.md
```

---

## Maintenance

**Update skills:**
```bash
cd claude-skills/anthropic
git pull origin main
```

**Create custom skill:**
```bash
mkdir -p claude-skills/custom/my-skill
# Follow: anthropic/skill-creator/SKILL.md
```

---

## Implementation Status

### ✅ Phase 1: Foundation (Complete)
- Official skills repository cloned
- Directory structure established
- Documentation created

### 📅 Planned Phases
- **Phase 2:** Auto-discovery by tech stack
- **Phase 3:** Permission system (enabled-skills.json)
- **Phase 4:** Update automation scripts
- **Phase 5:** Project templates with skills
- **Phase 6:** Custom skill marketplace

**Detailed roadmap:** [../core/SKILLS_INTEGRATION.md](../core/SKILLS_INTEGRATION.md)

---

## Not Implemented Yet

- ❌ Automatic skill discovery/recommendations
- ❌ skills-manifest.json (version tracking)
- ❌ Update automation scripts (check-skill-updates.sh, etc.)
- ❌ Permission system (project-level skill enablement)
- ❌ Usage analytics
- ❌ Custom skill templates beyond skill-creator

**These are documented in SKILLS_INTEGRATION.md for future implementation.**

---

## For Framework Developers

**When to read SKILLS_INTEGRATION.md:**
- Implementing discovery engine (Phase 2)
- Building permission system (Phase 3)
- Creating update automation (Phase 4)
- Understanding integration architecture

**When to read ANTHROPIC_SKILLS_CATALOG.md:**
- Understanding available skills and capabilities
- Creating project recommendations
- Building skill selection logic

---

**Version:** 2.0.0 (Token-Optimized)
**Lines:** ~150 (was 415)
**Words:** ~350 (was 1,414)
**Token Savings:** 75%
