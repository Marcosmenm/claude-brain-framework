# Version Detection Protocol

**MANDATORY: Claude MUST check version BEFORE any framework action**

## 🚨 The Rule

**CLAUDE: Before doing ANYTHING framework-related:**

1. **Check if project already uses framework** (look for CLAUDE.md)
2. **Identify current version** (check CLAUDE.md footer)
3. **Read CHANGELOG** to see what's changed
4. **Apply ONLY missing changes** (never redo everything)
5. **Update in-place** (never create "_Enhanced" duplicates)

## 🔍 Quick Detection

```bash
# Step 1: Does project have framework?
test -f CLAUDE.md && echo "Framework detected" || echo "No framework"

# Step 2: What version?
tail -10 CLAUDE.md | grep -E "Version|Framework"

# Step 3: Check framework CHANGELOG
cat /path/to/claude-brain-framework/CHANGELOG.md | head -50
```

## 📊 Decision Tree

```
User asks to apply framework
    ↓
Check for CLAUDE.md
    ↓
├─ NO CLAUDE.md → NEW PROJECT
│   └─ Run INIT_PROCESS.md (full initialization)
│
└─ CLAUDE.md EXISTS → EXISTING PROJECT
    ↓
    Check version in footer
    ↓
    ├─ No version listed → v1.0.0 (first release)
    ├─ v1.0.0 → Apply v1.0.1 + v1.1.0 changes
    ├─ v1.0.1 → Apply v1.1.0 changes
    └─ v1.1.0+ → Up to date, no action
```

## ✅ Correct Behavior Examples

### Example 1: New Project
```
User: "Apply claude-brain-framework"

Claude checks: ls CLAUDE.md → file not found

Claude: "No framework detected. I'll initialize from scratch.
        Running full initialization interview..."

[Proceeds with INIT_PROCESS.md]
```

### Example 2: Existing v1.0.0 Project
```
User: "Update framework"

Claude checks:
- CLAUDE.md exists ✓
- Footer says: "Framework Version: 1.0.0"
- CHANGELOG shows: v1.0.1 and v1.1.0 available

Claude: "Current version: v1.0.0
        Latest: v1.1.0

        Changes to apply:

        v1.0.1 (Migration):
        - Move Documentation/ → .claude/documentation/
        - Move PRPs/ → .claude/prps/

        v1.1.0 (Features):
        - Add Documentation Index
        - Add hierarchical context templates

        I'll apply these now..."

[Applies migrations from CHANGELOG]
[Updates version to 1.1.0]

Claude: "✓ Updated to v1.1.0
        ✓ Directories migrated
        ✓ New templates available"
```

### Example 3: Already Up-to-Date
```
User: "Update framework"

Claude checks: Footer says "Framework Version: 1.1.0"

Claude: "You're on v1.1.0 (latest). No updates needed.
        Want me to review your setup or enhance something specific?"
```

## ❌ Wrong Behaviors to Avoid

### Wrong: Re-initializing Existing Project
```
❌ WRONG:
User: "Apply framework updates"
Claude: [Doesn't check for CLAUDE.md]
Claude: "I'll set up context engineering..." [starts from scratch]
Result: Overwrites existing customizations

✅ CORRECT:
Claude: [Checks CLAUDE.md first]
Claude: "Framework detected (v1.0.0). Applying updates..."
```

### Wrong: Creating Duplicate Files
```
❌ WRONG:
.claude/prps/_TEMPLATE.md (existing)
.claude/prps/_TEMPLATE_Enhanced.md (new - WRONG!)

✅ CORRECT:
.claude/prps/_TEMPLATE.md (updated in-place)
<!-- Updated 2025-10-13: v1.1.0 improvements applied -->
```

### Wrong: Not Reading CHANGELOG
```
❌ WRONG:
Claude: "I'll compare your files to latest templates..."
[Wastes tokens, might miss official migration steps]

✅ CORRECT:
Claude: "Reading CHANGELOG for v1.0.1 → v1.1.0...
        Official migration: mv Documentation .claude/documentation
        Applying..."
```

## 🔄 Integration with Other Processes

**This protocol is the FIRST STEP for:**

- **User says "apply framework"** → Version Detection → INIT or UPDATE
- **User says "update framework"** → Version Detection → UPDATE_PROCESS
- **User says "check updates"** → Version Detection → Report status

**Process Flow:**
```
VERSION_DETECTION.md (you are here)
    ↓
    ├─ New project? → INIT_PROCESS.md
    └─ Existing project? → UPDATE_PROCESS.md
                              ↓
                         CHANGELOG.md (migration steps)
```

## 📝 Version Tracking Format

**CLAUDE: Always add/update this in CLAUDE.md footer:**

```markdown
---

**Context Engineering Version:** 1.1.0
**Framework:** claude-brain-framework v1.1.0
**Last Updated:** 2025-10-13
```

**For projects with update history:**
```markdown
**Update History:**
- 2025-10-13: v1.0.0 → v1.1.0 (directory migration + new features)
- 2025-10-10: Initial setup v1.0.0
```

## 🎯 Critical Rules Summary

1. **Always check CLAUDE.md first** before any framework action
2. **Never re-initialize** existing projects (update them instead)
3. **Read CHANGELOG** for migration steps (don't improvise)
4. **Update in-place** (no "_Enhanced" or "_v2" files)
5. **Track version** in CLAUDE.md footer after every change
6. **Preserve customizations** when updating files

---

**This protocol prevents duplicate work, lost customizations, and inconsistent updates.**

**Framework Version:** 1.1.0+
**Status:** MANDATORY
**Integration:** Required before INIT_PROCESS.md or UPDATE_PROCESS.md
