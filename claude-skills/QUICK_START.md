# 🚀 Anthropic Skills Integration - Quick Start

**10-minute practical guide to using skills in the framework**

---

## What You'll Learn

- Verify skills installation
- Understand when to load specific skills
- Use skills in project recommendations
- Create custom skills

**Time:** 10 minutes

---

## Step 1: Verify Installation (1 minute)

```bash
cd claude-brain-framework/claude-skills/anthropic
ls
```

**Should see:** 13 skill directories (mcp-builder, document-skills, etc.)

**If not installed:**
```bash
cd claude-brain-framework
git clone https://github.com/anthropics/skills claude-skills/anthropic
```

---

## Step 2: Understand Skill Structure (2 minutes)

**Every skill:**
```
skill-name/
├── SKILL.md          # Load this when you need the skill
└── Optional: scripts/, references/, assets/
```

**Example - Read a skill:**
```bash
cat anthropic/mcp-builder/SKILL.md
```

**Key point:** Skills are loaded WHEN NEEDED, not upfront.

---

## Step 3: Know When to Load Skills (3 minutes)

### Tech Stack → Skill Mapping

**See [README.md#when-to-load-skills](README.md#when-to-load-skills) for complete list.**

Quick examples:
- User building MCP server → Load `anthropic/mcp-builder/SKILL.md`
- User generating PDFs → Load `anthropic/document-skills/pdf/SKILL.md`
- User creating custom skill → Load `anthropic/skill-creator/SKILL.md`

### Skill Details

**Don't memorize - reference when needed:**
- Full skill catalog: [ANTHROPIC_SKILLS_CATALOG.md](ANTHROPIC_SKILLS_CATALOG.md)
- Selection guide: [ANTHROPIC_SKILLS_CATALOG.md#skill-selection-guide](ANTHROPIC_SKILLS_CATALOG.md#skill-selection-guide)

---

## Step 4: Use in Project Recommendations (2 minutes)

When initializing a project with the framework, recommend relevant skills in the project's CLAUDE.md:

```markdown
## 🎯 RECOMMENDED SKILLS

**Framework location:** /path/to/claude-brain-framework/claude-skills/anthropic/

### When Working On:
- **API integration** → Load mcp-builder/SKILL.md
- **PDF generation** → Load document-skills/pdf/SKILL.md
- **Testing workflows** → Load webapp-testing/SKILL.md
```

**Pattern:** Point to skill locations, load when needed.

---

## Step 5: Create Custom Skills (2 minutes)

### Quick Method
```bash
cd claude-skills/anthropic
cat skill-creator/SKILL.md  # Read the guide
```

### 6-Step Process Summary
1. Gather concrete examples
2. Plan reusable contents
3. Initialize skill structure
4. Develop resources
5. Package and validate
6. Iterate

**Full details:** Load `anthropic/skill-creator/SKILL.md` when creating custom skills.

---

## Common Patterns

### Pattern 1: User Asks to Build MCP Server
```
1. Load anthropic/mcp-builder/SKILL.md
2. Follow 4-phase workflow in skill
3. Use language-specific guides from references/
```

### Pattern 2: User Asks to Generate PDFs
```
1. Load anthropic/document-skills/pdf/SKILL.md
2. Use pypdf examples from skill
3. Apply formatting recommendations
```

### Pattern 3: Project Uses Multiple Skills
```markdown
# In project's CLAUDE.md

## 🎯 RECOMMENDED SKILLS
Framework: /path/to/framework/claude-skills/anthropic/

- mcp-builder/ - API development
- document-skills/pdf/ - Invoice generation
- webapp-testing/ - Test automation
```

---

## Maintenance

**Update skills:**
```bash
cd claude-skills/anthropic && git pull origin main
```

**Custom skills location:**
```bash
claude-skills/custom/my-skill/
```

---

## Next Steps

1. **Browse catalog:** [ANTHROPIC_SKILLS_CATALOG.md](ANTHROPIC_SKILLS_CATALOG.md)
2. **Read integration strategy:** [../core/SKILLS_INTEGRATION.md](../core/SKILLS_INTEGRATION.md)
3. **Try a skill:** Load any skill's SKILL.md and follow its guidance
4. **Create custom skill:** Follow `anthropic/skill-creator/SKILL.md`

---

## FAQ

**Q: Do I load all skills upfront?**
A: No. Load specific skill's SKILL.md when needed for a task.

**Q: Where are skill details?**
A: [ANTHROPIC_SKILLS_CATALOG.md](ANTHROPIC_SKILLS_CATALOG.md) - reference when needed, don't memorize.

**Q: How do I know which skill to use?**
A: Check [README.md#when-to-load-skills](README.md#when-to-load-skills) or the catalog's selection guide.

**Q: Can I modify official skills?**
A: No - create custom skills in `claude-skills/custom/` instead.

**Q: What if I need help with a specific skill?**
A: Load that skill's SKILL.md file - it contains complete instructions.

---

**Version:** 2.0.0 (Token-Optimized)
**Words:** ~450 (was 1,405)
**Token Savings:** 68%
**Approach:** Procedural steps + pointers to authority sources
