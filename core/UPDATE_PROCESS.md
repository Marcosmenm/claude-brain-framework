# Framework Update Process

**How to propagate Claude Brain Framework updates to your projects**

## 🔄 Update Philosophy

When the framework evolves, your projects should benefit from improvements while preserving your customizations.

## 📊 Version Management

### Semantic Versioning
- **Major (2.0.0):** Breaking changes - requires migration
- **Minor (1.5.0):** New features - safe auto-update
- **Patch (1.5.1):** Bug fixes - always safe

### Checking for Updates

**User asks Claude:**
```
"Check for claude-brain-framework updates"
```

**Claude automatically:**
1. Reads `CHANGELOG.md` from framework repo
2. Compares with project's current version
3. Explains what changed
4. Offers to update if beneficial

## 🎯 Update Detection

### CLAUDE: How to Check for Updates

When user requests update check:

```bash
# 1. Check framework repo CHANGELOG
curl https://raw.githubusercontent.com/Marcosmenm/claude-brain-framework/main/CHANGELOG.md

# 2. Compare versions
# Project version in: [PROJECT]/CLAUDE.md (last line)
# Latest version in: CHANGELOG.md (top entry)

# 3. Present findings
"Framework Update Available:
 - Current: v1.0.0
 - Latest: v1.5.0
 - Type: Minor (safe to update)
 
 Changes:
 - [Feature 1]
 - [Feature 2]
 
 Would you like me to update your project?"
```

## 🔧 Update Types

### Patch Updates (1.0.0 → 1.0.1)
**What:** Bug fixes, documentation improvements
**Impact:** Zero breaking changes
**Process:** Automatic, no user action needed

**CLAUDE Process:**
1. Download updated templates
2. Apply fixes to project files
3. Preserve all customizations
4. Update version number
5. Notify completion

### Minor Updates (1.0.0 → 1.5.0)
**What:** New features, enhanced templates
**Impact:** Backward compatible additions
**Process:** Safe auto-update with review

**CLAUDE Process:**
1. Download new features/templates
2. Show what's new
3. Offer to add new features
4. Update existing files (preserve custom)
5. Update version number
6. Document what changed

### Major Updates (1.0.0 → 2.0.0)
**What:** Breaking changes, restructuring
**Impact:** May require code changes
**Process:** Manual with migration guide

**CLAUDE Process:**
1. Download migration guide
2. Backup current files
3. Explain breaking changes
4. Guide through migration step-by-step
5. Validate after each step
6. Update version number
7. Confirm everything works

## 📋 Update Workflow

### Step 1: Detection (Automatic or On-Request)

**Automatic (session start - from VERSION_DETECTION.md):**
```
User: [Opens project and starts working]

Claude: [AUTOMATIC CHECK]
"I notice this project is on framework v1.0.0, but v1.2.0 is available.

You're missing 2 updates:

**v1.1.0** (2025-10-13):
- Multi-Repository System Template
- Documentation Index Template
- Incremental Documentation Strategy

**v1.2.0** (2025-10-20):
- Lean Development Workflow methodology
- CI/CD Deployment Guide
- Enhanced behavioral rules

Would you like me to:
1. Apply all updates (v1.0.0 → v1.2.0) - Recommended
2. Apply only v1.1.0
3. Apply only v1.2.0
4. Skip for now

Your choice?"
```

**On-request:**
```
User: "Check for updates"

Claude: "Checking claude-brain-framework...

        Update Available: v1.5.0 (Minor)
        Current: v1.0.0

        New Features:
        - Enhanced agent patterns
        - MCP auto-detection
        - Chat summary improvements

        Safe to update automatically. Proceed?"
```

### Step 2: Handle User Choice

**If user chooses "Apply all" (recommended):**
```
Claude: "Applying v1.0.0 → v1.1.0 → v1.2.0...

        Reading CHANGELOG for migration steps...
        [Proceeds with full update]"
```

**If user chooses specific version (e.g., "Only v1.1.0"):**
```
Claude: "Applying only v1.1.0 updates...

        Note: You'll remain on v1.1.0. I'll notify you about v1.2.0
        in future sessions until applied.

        [Proceeds with v1.1.0 update only]"
```

**If user chooses "Skip for now":**
```
Claude: "Understood. Proceeding with your work.

        I'll remind you about available updates next session.
        [Proceeds with user's original request]"
```

**Critical Rule:** Track which updates were offered and skipped to avoid repetitive notifications.

---

### Step 3: Review
```
Claude: "Here's what will change in your project:
        
        Updated Files:
        - core/AGENT_PATTERNS.md (new agents added)
        - templates/CLAUDE_MD_UNIVERSAL.md (MCP section)
        
        New Files:
        - templates/MCP_INTEGRATION.md
        
        Your Customizations:
        ✓ Preserved in CLAUDE.md
        ✓ Preserved in Documentation/
        ✓ PRPs unchanged
        
        Proceed with update?"
```

### Step 4: Application
```
Claude: "Updating your project...
        
        ✓ Backed up current files
        ✓ Downloaded v1.5.0 templates
        ✓ Applied updates
        ✓ Preserved customizations
        ✓ Updated version to 1.5.0
        
        Update complete! Review changes:
        - New agent patterns available
        - MCP detection in init process
        - Chat summaries enhanced
        
        Want me to show you how to use new features?"
```

## 🔒 Customization Preservation

### What Gets Preserved
**Always kept:**
- Your CLAUDE.md customizations
- Your Documentation/ content
- Your PRPs (active and completed)
- Your .claude/agents/ configurations
- Project-specific patterns

**Updated (carefully):**
- Core methodology (if not customized)
- Templates (merge improvements)
- Agent catalog (add new, keep custom)

### How Preservation Works
```
1. Identify customized sections
   - Compare with framework defaults
   - Mark custom content

2. Apply updates smartly
   - Framework sections: Update
   - Custom sections: Preserve
   - Merged sections: Integrate carefully

3. Validate integration
   - Ensure no conflicts
   - Test critical paths
   - Verify patterns still work
```

## 🚨 Breaking Change Migration

### When Major Version Released

**CLAUDE Process:**
1. **Detect Breaking Changes**
   ```
   "Major update available: v2.0.0
    
    ⚠️ Breaking Changes:
    - CLAUDE.md structure reorganized
    - PRP template format changed
    - New agent invocation syntax
    
    This requires manual migration.
    I'll guide you through it step-by-step."
   ```

2. **Backup Current State**
   ```bash
   # Create backup
   cp -r [PROJECT] [PROJECT]_backup_v1.0.0
   ```

3. **Migration Guide**
   ```
   "Migration Steps:
    
    Step 1: Update CLAUDE.md structure
    - Current: Flat organization
    - New: Sectioned with @imports
    - Action: I'll reorganize while preserving content
    
    Step 2: Update PRP templates
    - Current: Single file format
    - New: Modular with external context
    - Action: Convert existing PRPs
    
    Step 3: Update agent syntax
    - Current: Manual invocation
    - New: Automatic delegation
    - Action: Update agent configs
    
    Proceed with Step 1?"
   ```

4. **Step-by-Step Execution**
   ```
   [User approves each step]
   
   "Step 1 complete:
    ✓ CLAUDE.md reorganized
    ✓ Content preserved
    ✓ New structure applied
    
    Validation:
    ✓ All references work
    ✓ Imports resolve correctly
    
    Ready for Step 2?"
   ```

5. **Final Validation**
   ```
   "Migration complete!
    
    ✓ All steps applied
    ✓ Customizations preserved
    ✓ New features available
    ✓ Tests still pass
    
    Version updated: v1.0.0 → v2.0.0
    
    Backup available at: [PROJECT]_backup_v1.0.0
    
    Review summary of changes?"
   ```

## 📝 Project Registry (Optional)

Users can maintain a registry of projects using the framework:

### Registry File (gitignored)
`/users/PROJECT_REGISTRY.md`
```markdown
# My Projects Using Claude Brain Framework

## Active Projects
- /Users/me/project-a (v1.5.0) - Updated 2025-10-09
- /Users/me/project-b (v1.0.0) - Needs update
- /Users/me/project-c (v1.5.0) - Up to date

## Update History
- 2025-10-09: Updated project-a to v1.5.0
- 2025-09-15: Updated project-c to v1.5.0
```

### Bulk Update Check
```
User: "Check all my projects for updates"

Claude: "Scanning registry...
        
        Projects needing updates:
        - project-b: v1.0.0 → v1.5.0 (minor, safe)
        
        Up to date:
        - project-a: v1.5.0 ✓
        - project-c: v1.5.0 ✓
        
        Update project-b?"
```

## ✅ Update Checklist

**CLAUDE: After every update:**
- [ ] Version number updated in CLAUDE.md
- [ ] Customizations preserved
- [ ] New features documented
- [ ] Tests still pass
- [ ] Project registry updated (if exists)
- [ ] User notified of changes

---

**This update process ensures your projects evolve with the framework while maintaining your specific customizations and patterns.**

**Framework Version:** 1.0.0
