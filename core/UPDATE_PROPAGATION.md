# Framework Update Propagation Protocol

**Automated system for propagating framework updates to all projects**

## Version Tracking System

### Source of Truth
- Framework version: `claude-brain-framework/CHANGELOG.md`
- Project version: Footer of each project's `CLAUDE.md`
- Format: `Framework: claude-brain-framework v[X.Y.Z]`

### Version Detection
```
claude-brain-framework/CHANGELOG.md → Latest: v1.4.0
project/CLAUDE.md footer → Current: v1.2.0
Gap detected: v1.3.0, v1.4.0 missing
```

## Propagation Triggers

### 1. Session Start (Proactive)
**CLAUDE: Auto-check on first interaction in any project**
1. Read project CLAUDE.md footer → extract version
2. Read framework CHANGELOG.md → extract latest version
3. If gap exists → notify user immediately with delta
4. Offer update options before proceeding with user request

### 2. Explicit Request
User: "Update framework" / "Apply latest framework updates"
→ Execute full propagation process

### 3. Multi-Project Scan
User: "Update framework across all projects"
→ Scan parent directory, apply to all projects with framework

## Propagation Process

### Step 1: Detect Projects
```bash
# Scan for projects with framework integration
find /Users/marcosm/Documents/dev -name "CLAUDE.md" -type f
# Filter: Contains "Framework: claude-brain-framework"
```

### Step 2: Version Gap Analysis
For each project:
1. Extract current version from CLAUDE.md footer
2. Compare with framework CHANGELOG.md
3. List missing version updates
4. Categorize update types: behavioral, template, structural

### Step 3: Apply Updates

**For each missing version:**

#### Behavioral Updates
- Modify `.claude/FRAMEWORK_PRINCIPLES.md`
- Update based on new principles in CHANGELOG
- Example: v1.4.0 adds stricter token optimization rules

#### Template Updates
- Add new templates to `.claude/documentation/Workflows/`
- Example: New language-specific coding standards

#### Structural Updates
- Create new directories if required
- Add new framework reference files
- Example: New `.claude/agents/` directory

#### CLAUDE.md Updates
- Add new sections if framework template changed
- Update framework reference section
- Update version footer

### Step 4: Validation
1. Verify FRAMEWORK_PRINCIPLES.md updated
2. Verify CLAUDE.md footer version matches latest
3. Create update log in `.claude/update-history/YYYYMMDD_vX.Y.Z_update.md`
4. Confirm all projects synchronized

## Update Types

### Type 1: Additive Behavioral Rules
**Impact:** `.claude/FRAMEWORK_PRINCIPLES.md`
**Action:** Append new rules, preserve existing
**Example:** New documentation consolidation rule

### Type 2: New Templates
**Impact:** `.claude/documentation/Workflows/`
**Action:** Add new template files
**Example:** Python coding standards template

### Type 3: Structural Changes
**Impact:** Directory structure
**Action:** Create new directories, move files
**Example:** New `.claude/skills/` integration

### Type 4: CLAUDE.md Enhancements
**Impact:** Project CLAUDE.md
**Action:** Add sections, update references
**Example:** New framework philosophy section

## Backward Compatibility

### Non-Breaking Updates Only
- Never remove existing rules (only add/refine)
- Additive changes preserve project customizations
- Migration path if breaking change unavoidable

### Project Customization Preservation
- Detect custom sections in CLAUDE.md → preserve
- Detect custom documentation → don't overwrite
- Only update framework-controlled sections

## User Control

### Update Options
1. **Apply all updates** → Full synchronization
2. **Apply specific version** → Selective update
3. **Skip for now** → Track as pending
4. **Review changes first** → Show diff before applying

### Tracking Skipped Updates
- Record in `.claude/pending-updates.md`
- Remind on future session starts
- Allow delayed application

## Propagation Log

### Update History Tracking
**Location:** `.claude/update-history/`

**Log Format:**
```markdown
# Framework Update: v1.3.0 → v1.4.0
**Date:** 2025-11-23
**Applied by:** Claude Code

## Changes Applied
- Updated FRAMEWORK_PRINCIPLES.md: Added token optimization rules
- Updated CLAUDE.md: Added framework philosophy section
- Updated version footer: v1.4.0

## Files Modified
- .claude/FRAMEWORK_PRINCIPLES.md
- CLAUDE.md

## Validation
✓ Version synchronized
✓ Framework principles current
✓ No breaking changes
```

## Multi-Project Propagation

### Batch Update Process
```
User: "Update framework across all projects"

Claude:
1. Scans /Users/marcosm/Documents/dev/
2. Detects: TagMyLink (v1.2.0), JokerPoker (v1.3.0), claude-web-builder (v1.1.0)
3. Lists missing updates per project
4. Offers: "Apply v1.4.0 to all 3 projects?"
5. Executes propagation in parallel
6. Reports completion status per project
```

### Parallel vs Sequential
- **Parallel:** Independent projects (TagMyLink, JokerPoker)
- **Sequential:** Dependencies exist (backend then frontend)

## Error Handling

### Conflict Detection
- Custom FRAMEWORK_PRINCIPLES.md modifications detected
- Prompt user: merge or preserve custom version
- Create backup before overwriting

### Rollback Capability
- Backup pre-update state in `.claude/update-history/backup/`
- Allow rollback if update causes issues
- Restore from backup with version downgrade

## Framework Evolution

### Breaking Changes (Rare)
1. Announce in CHANGELOG.md with migration guide
2. Require explicit user confirmation before applying
3. Provide automated migration script when possible
4. Document in UPDATE_PROPAGATION.md

### Deprecation Path
1. Mark feature deprecated in version N
2. Provide migration in version N+1
3. Remove in version N+2
4. Always 2-version deprecation window

## Implementation Commands

### Check for Updates
```
CLAUDE: On session start, auto-execute:
1. Read {project}/CLAUDE.md footer
2. Extract version: v[X.Y.Z]
3. Read /Users/marcosm/Documents/dev/claude-brain-framework/CHANGELOG.md
4. Compare versions
5. If gap: "Framework update available: v{X.Y.Z} → v{latest}. Apply now?"
```

### Apply Single Project Update
```
CLAUDE: When user confirms update:
1. Read CHANGELOG.md delta (missing versions)
2. Apply behavioral updates to FRAMEWORK_PRINCIPLES.md
3. Apply template updates to .claude/documentation/Workflows/
4. Update CLAUDE.md sections
5. Update version footer
6. Create update log
7. Confirm completion
```

### Apply Multi-Project Update
```
CLAUDE: When user requests "update all projects":
1. Scan parent directory for CLAUDE.md files
2. Filter: contains framework version footer
3. Analyze version gaps
4. Present summary with update plan
5. On confirmation, execute per-project updates
6. Report aggregate status
```

## Best Practices

### When to Propagate
- Major framework version releases (v1.X.0 → v2.0.0)
- New behavioral rules added
- New universal templates created
- Bug fixes in framework principles

### When NOT to Propagate
- Project-specific customizations
- Experimental framework features
- User explicitly opted out

### Communication
- Always notify user of available updates
- Show what changed in each version
- Allow review before applying
- Provide rollback option

---

**Version:** 1.0.0
**Framework:** claude-brain-framework v1.4.0
**Date:** 2025-11-23
