# Project Structure Standards

**Critical guidelines for maintaining consistent context engineering structure**

## 🚨 CRITICAL PRINCIPLE: Directory Structure Consistency

### The Standard Structure

**ALL projects using claude-brain-framework MUST use this structure:**

```
your-project/
├── CLAUDE.md (Project brain)
├── /.claude/
│   ├── /documentation/        # NOT /Documentation/ - lowercase, in .claude/
│   │   ├── /Core_Systems/
│   │   ├── /Architecture/
│   │   ├── /Workflows/
│   │   └── DOCUMENTATION_INDEX.md
│   ├── /prps/                 # NOT /PRPs/ - lowercase, in .claude/
│   │   ├── /active/
│   │   ├── /completed/
│   │   └── _TEMPLATE.md
│   ├── /agents/               # Specialized Claude instances
│   │   ├── README.md
│   │   └── [agent-name].md
│   └── /chat-history/         # Optional: conversation tracking
└── [your source code]
```

### Why This Matters

**Consistency enables:**
- ✅ Universal tooling and automation
- ✅ Easy project switching (developers know where things are)
- ✅ Framework updates can be applied predictably
- ✅ Cross-project knowledge transfer
- ✅ AI agents can locate files reliably

**Inconsistency causes:**
- ❌ Confusion when switching between projects
- ❌ Framework updates break things
- ❌ Custom scripts for each project
- ❌ Wasted time searching for files
- ❌ Documentation references fail

---

## 📋 Directory Structure Rules

### Rule 1: Everything in `.claude/` Directory

**ALL context engineering artifacts MUST live in `.claude/`:**

```
✅ CORRECT:
/.claude/documentation/
/.claude/prps/
/.claude/agents/
/.claude/chat-history/

❌ WRONG:
/Documentation/
/PRPs/
/docs/
/prps/
```

**Why:**
- Clean separation from source code
- Easy to `.gitignore` if needed (except DOCUMENTATION_INDEX.md)
- Clear ownership (this is Claude's working directory)
- Prevents conflicts with existing project folders

### Rule 2: Use Lowercase for Directory Names

**Directory names inside `.claude/` use lowercase:**

```
✅ CORRECT:
/.claude/documentation/
/.claude/prps/
/.claude/agents/
/.claude/chat-history/

❌ WRONG:
/.claude/Documentation/
/.claude/PRPS/
/.claude/Agents/
```

**Exception:** Files and subdirectories that follow their own conventions:
- `Core_Systems/` (uses PascalCase with underscore - established pattern)
- `DOCUMENTATION_INDEX.md` (all caps for high visibility)
- `README.md` (standard convention)

### Rule 3: Preserve Existing Project Structure

**If a project already has different structure, MIGRATE it:**

```bash
# Example migration:
mv /Documentation /.claude/documentation
mv /PRPs /.claude/prps
mv /Agents /.claude/agents

# Update all file references:
# - In CLAUDE.md
# - In documentation files
# - In PRPs
# - In agent configurations
```

**Never:** Keep duplicate or parallel structures

### Rule 4: File Naming Conventions

**Templates:**
```
✅ CORRECT:
/.claude/prps/_TEMPLATE.md
/.claude/prps/_TEMPLATE_ProjectSpecific.md

❌ WRONG:
/.claude/prps/template.md
/.claude/prps/TEMPLATE_Enhanced.md (don't add "Enhanced", "New", "Updated")
```

**Agent Files:**
```
✅ CORRECT:
/.claude/agents/code-reviewer.md
/.claude/agents/security-auditor.md
/.claude/agents/laravel-api-tester.md

❌ WRONG:
/.claude/agents/Code-Reviewer.md (no caps)
/.claude/agents/code_reviewer.md (no underscores)
```

**Documentation:**
```
✅ CORRECT:
/.claude/documentation/Core_Systems/User_Management_Documentation.md
/.claude/documentation/Architecture/Backend_Architecture.md

❌ WRONG:
/.claude/documentation/core-systems/user-management.md (lowercase folders OK, but inconsistent with established pattern)
```

---

## 🔧 Migration Guide

### Migrating Existing Projects

**When applying claude-brain-framework to existing project with wrong structure:**

#### Step 1: Assess Current State
```bash
# Check what exists
ls -la | grep -iE "(documentation|docs|prps|agents)"
ls -la .claude/
```

#### Step 2: Create Correct Structure
```bash
# Create .claude if doesn't exist
mkdir -p .claude/{documentation,prps,agents,chat-history}
mkdir -p .claude/documentation/{Core_Systems,Architecture,Workflows}
mkdir -p .claude/prps/{active,completed}
```

#### Step 3: Move Existing Content
```bash
# Move documentation
if [ -d "Documentation" ]; then
  cp -r Documentation/* .claude/documentation/
  # Verify, then remove old:
  # rm -rf Documentation
fi

# Move PRPs
if [ -d "PRPs" ]; then
  cp -r PRPs/* .claude/prps/
  # Verify, then remove old:
  # rm -rf PRPs
fi

# Move agents
if [ -d "agents" ] || [ -d "Agents" ]; then
  cp -r agents/* .claude/agents/ 2>/dev/null || cp -r Agents/* .claude/agents/ 2>/dev/null
  # Verify, then remove old
fi
```

#### Step 4: Update All References

**Files to update:**
1. `CLAUDE.md` - Update all file paths
2. `/.claude/documentation/DOCUMENTATION_INDEX.md` - Update links
3. All documentation files - Update cross-references
4. All PRPs - Update documentation references
5. All agent files - Update context references

**Find and replace patterns:**
```bash
# Find old references
grep -r "/Documentation/" . --include="*.md"
grep -r "/PRPs/" . --include="*.md"

# Replace with:
# /Documentation/ → /.claude/documentation/
# /PRPs/ → /.claude/prps/
```

#### Step 5: Verify and Test

```bash
# Check all markdown files for broken links
find .claude -name "*.md" -exec grep -l "@.*/" {} \;

# Verify structure
tree .claude -L 2
```

---

## 🎯 Framework Application Protocol

### For New Projects (Clean Slate)

When applying framework to project without existing context engineering:

```bash
# 1. Create structure (automated by Claude during init)
mkdir -p .claude/{documentation,prps,agents}
mkdir -p .claude/documentation/{Core_Systems,Architecture,Workflows}
mkdir -p .claude/prps/{active,completed}

# 2. Generate CLAUDE.md
# 3. Generate documentation
# 4. Configure agents
# 5. Create templates
```

### For Existing Projects (Migration Required)

When applying framework to project with existing structure:

```
✅ CORRECT APPROACH:
1. Acknowledge existing structure
2. Create correct .claude/ structure
3. MIGRATE existing content (don't duplicate)
4. UPDATE all references
5. VERIFY everything works
6. REMOVE old structure

❌ WRONG APPROACH:
1. Create new structure alongside old ❌
2. Keep both Documentation/ and .claude/documentation/ ❌
3. Add "Enhanced" or "New" to file names ❌
4. Mix structures ❌
```

### For Projects Being Updated

When updating projects already using framework:

```
✅ CORRECT APPROACH:
1. Review current structure against standards
2. Identify deviations
3. Plan migration (if needed)
4. Update in-place (don't create new versions)
5. Preserve git history

❌ WRONG APPROACH:
1. Create parallel "updated" versions ❌
2. Rename with "v2" or "enhanced" ❌
3. Keep old versions around ❌
```

---

## 📝 Update Protocol

### Updating Templates

**When framework introduces better template:**

```
✅ CORRECT:
1. Read existing template
2. Identify improvements from framework
3. UPDATE existing template in-place
4. Preserve project-specific customizations
5. Document changes in template comments

❌ WRONG:
1. Create new "_TEMPLATE_Enhanced.md" ❌
2. Keep both old and new ❌
3. Lose project-specific customizations ❌
```

**Example:**
```markdown
# In template file:
<!-- Updated 2025-10-13: Added @import syntax for documentation references -->
<!-- Updated 2025-10-13: Added agent invocation section -->
```

### Updating Documentation Structure

**When framework adds new documentation categories:**

```
✅ CORRECT:
1. Add new folders/files to existing structure
2. Update DOCUMENTATION_INDEX.md
3. Create navigation from existing docs to new
4. Maintain consistency

❌ WRONG:
1. Create parallel structure ❌
2. Rename old structure to "legacy" ❌
3. Break existing links ❌
```

---

## 🚨 CLAUDE INITIALIZATION MANDATE

### When Initializing Framework on Project

**CLAUDE: You MUST follow this sequence:**

1. **ASSESS CURRENT STATE:**
   ```
   "I'll check if you already have context engineering structure...
   [checks for Documentation/, PRPs/, .claude/, etc.]"
   ```

2. **IF EXISTING STRUCTURE FOUND:**
   ```
   "I found existing structure at [locations].
   To maintain consistency with claude-brain-framework standards,
   I'll migrate this to the standard .claude/ structure.

   Current structure:
   - Documentation/ → will move to .claude/documentation/
   - PRPs/ → will move to .claude/prps/

   This ensures:
   - Consistency across all projects
   - Framework updates work smoothly
   - Easy navigation for developers

   Proceed with migration?"
   ```

3. **MIGRATE, DON'T DUPLICATE:**
   ```
   "Migrating existing content to standard structure...
   ✓ Moved Documentation/ → .claude/documentation/
   ✓ Moved PRPs/ → .claude/prps/
   ✓ Updated all references in CLAUDE.md
   ✓ Updated cross-references in documentation
   ✓ Verified all links work

   Old directories can now be removed safely."
   ```

4. **NEVER:**
   - Create both `/Documentation/` and `/.claude/documentation/`
   - Add "Enhanced", "New", "v2" to filenames
   - Keep multiple versions of same structure
   - Leave broken references

---

## ✅ Verification Checklist

### After Applying Framework

**Verify correct structure:**
```bash
# Check structure exists
[ -d ".claude/documentation" ] && echo "✓ documentation" || echo "✗ documentation"
[ -d ".claude/prps" ] && echo "✓ prps" || echo "✗ prps"
[ -d ".claude/agents" ] && echo "✓ agents" || echo "✗ agents"

# Check no old structure remains
[ ! -d "Documentation" ] && echo "✓ No old Documentation/" || echo "✗ Old Documentation/ still exists"
[ ! -d "PRPs" ] && echo "✓ No old PRPs/" || echo "✗ Old PRPs/ still exists"

# Check file references
grep -r "/Documentation/" CLAUDE.md && echo "✗ Old references" || echo "✓ References updated"
```

**Verify links work:**
```bash
# Check documentation index
[ -f ".claude/documentation/DOCUMENTATION_INDEX.md" ] && echo "✓ Index exists"

# Check templates
[ -f ".claude/prps/_TEMPLATE.md" ] || [ -f ".claude/prps/_TEMPLATE_"*.md ] && echo "✓ PRP template"

# Check agents
[ -f ".claude/agents/README.md" ] && echo "✓ Agents configured"
```

---

## 📊 Common Violations and Fixes

### Violation 1: Parallel Structures
```
❌ PROBLEM:
/Documentation/
/.claude/documentation/

✅ FIX:
1. Compare content
2. Merge any differences
3. Keep only /.claude/documentation/
4. Update all references
5. Remove /Documentation/
```

### Violation 2: Inconsistent Naming
```
❌ PROBLEM:
/.claude/PRPS/
/.claude/Agents/

✅ FIX:
1. Rename to lowercase:
   mv .claude/PRPS .claude/prps
   mv .claude/Agents .claude/agents
2. Update references
```

### Violation 3: Enhanced/New Versions
```
❌ PROBLEM:
/.claude/prps/_TEMPLATE_Enhanced.md
/.claude/prps/_TEMPLATE_Old.md

✅ FIX:
1. Merge improvements into single template
2. Keep only /.claude/prps/_TEMPLATE_ProjectName.md
3. Remove others
4. Document updates in template comments
```

---

**This standard ensures every project using claude-brain-framework maintains consistent, predictable structure that enables cross-project developer productivity and framework evolution.**

**Framework Version:** 1.1.0+
**Standard Established:** 2025-10-13
**Status:** MANDATORY for all framework applications
