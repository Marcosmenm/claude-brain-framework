# Changelog

All notable changes to the Claude Brain Framework will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned Features
- Migration guides for version updates
- Additional language-specific templates
- Enhanced MCP integration patterns
- Community agent contributions

## [1.0.1] - 2025-10-10

### Fixed
- **File Organization**: Moved `Documentation/` and `PRPs/` into `.claude/` folder for better organization
  - Changed from `/Documentation/` to `/.claude/documentation/`
  - Changed from `/PRPs/` to `/.claude/prps/`
  - All Claude-related files now centralized in `.claude/` directory

- **Documentation Generation**: Added Cycle 7 to initialization process that actually generates documentation files
  - Previous version created empty folders; now generates populated documentation
  - Documentation includes actual analysis findings from code review
  - Each documentation file contains code references and TODO sections for clarification

- **Documentation Planning**: Added Cycle 6 for documentation planning
  - Claude now presents documentation plan to user before generating files
  - User can approve/modify the list of documentation to be created
  - Ensures documentation matches actual project structure

### Changed
- Updated `core/INIT_PROCESS.md` with new folder structure and documentation generation cycles
- Updated `templates/CLAUDE_MD_UNIVERSAL.md` with corrected file paths
- Updated `QUICK_START.md` to reflect 8-cycle initialization process
- Reorganized directory structure examples across all documentation

### Why This Matters
- **Better Organization**: All context engineering files in one `.claude/` folder prevents clutter
- **Actual Documentation**: Users now get populated documentation, not just empty folders
- **User Control**: Documentation planning cycle gives users visibility and control over what's generated

---

## 🔄 Migration Guide: v1.0.0 → v1.0.1

### For NEW Installations
Simply follow the [Quick Start Guide](QUICK_START.md). The new 8-cycle process will:
- Create `.claude/` folder structure automatically
- Generate populated documentation files during Cycle 7
- Set up everything correctly from the start

### For EXISTING v1.0.0 Installations

**You need to take action if you installed v1.0.0 and have:**
- Empty `Documentation/` folders at project root
- Empty `PRPs/` folders at project root
- No actual documentation files generated

#### Step 1: Reorganize File Structure

**Move folders into `.claude/` directory:**

```bash
# In your project root
mkdir -p .claude
mv Documentation .claude/documentation
mv PRPs .claude/prps

# If you have agents folder
mv .claude/agents .claude/agents  # Already in right place

# Update .gitignore if needed
echo ".claude/chat-summaries/" >> .gitignore
```

#### Step 2: Generate Missing Documentation

**Ask Claude to run the missing Cycle 7:**

```
I upgraded claude-brain-framework from v1.0.0 to v1.0.1.
I need you to generate the documentation that was missing in v1.0.0.

Please:
1. Analyze my codebase to identify core systems
2. Present a documentation plan for my approval
3. Generate populated documentation files in .claude/documentation/

This is the missing Cycle 7 from the new initialization process.
```

Claude will:
- Analyze your models, controllers, services, and architecture
- Propose documentation files (Core_Systems, Architecture, etc.)
- Generate actual populated documentation with code analysis
- Create files in `.claude/documentation/` with real content

#### Step 3: Update CLAUDE.md References

**Update path references in your CLAUDE.md:**

```markdown
# Old paths:
@Documentation/Core_Systems/[System].md
/PRPs/active/

# New paths:
@.claude/documentation/Core_Systems/[System].md
/.claude/prps/active/
```

#### Step 4: Verify Everything Works

```bash
# Check new structure
ls -la .claude/
ls -la .claude/documentation/
ls -la .claude/prps/

# Verify documentation has content (not empty)
wc -l .claude/documentation/Core_Systems/*.md
```

---

### What Changed & Why

**v1.0.0 Problem:**
- Created `Documentation/` and `PRPs/` at project root → Cluttered project structure
- Only created empty folders → No actual documentation generated

**v1.0.1 Solution:**
- All Claude files in `.claude/` namespace → Clean project organization
- Cycle 6 & 7 actually generate content → Real documentation from code analysis

---

## [1.0.0] - 2025-10-10

### Added
- Initial release of Claude Brain Framework
- Multi-cycle initialization interview system
- Core methodology documentation
- Behavioral programming rules for Claude
- Agent pattern catalog with community examples
- CLAUDE.md templates for various project types
- PRP (Product Requirements Prompt) template
- Documentation generation templates
- Chat summary system for optional conversation tracking
- Example anonymous SaaS platform project
- .gitignore for privacy protection
- Credits and acknowledgments for community contributions

### Core Components
- `core/METHODOLOGY.md` - Context engineering principles
- `core/BEHAVIORAL_RULES.md` - Claude behavior programming
- `core/INIT_PROCESS.md` - Multi-cycle interview process
- `core/UPDATE_PROCESS.md` - Framework update management
- `core/AGENT_PATTERNS.md` - Agent integration guide

### Templates
- `CLAUDE_MD_SINGLE_PROJECT.md` - Single component projects
- `CLAUDE_MD_MULTI_COMPONENT.md` - Frontend + Backend projects
- `PRP_TEMPLATE.md` - Feature implementation blueprints
- `DOCUMENTATION_TEMPLATE.md` - System documentation
- `CHAT_SUMMARY_TEMPLATE.md` - Conversation summaries

### Philosophy
- Just-in-time context loading with `@import` syntax
- Context as finite resource optimization
- Living documentation that evolves with projects
- Behavioral programming over static prompts

---

## Version Guidelines

### Major Version (X.0.0) - Breaking Changes
- Requires migration guide
- May change core file structures
- Could break existing implementations
- User must review and approve updates

### Minor Version (0.X.0) - New Features
- Backward compatible additions
- Safe for automatic updates
- New templates or patterns
- Enhanced existing features

### Patch Version (0.0.X) - Bug Fixes
- Always safe to update
- Documentation improvements
- Template corrections
- Performance optimizations

---

## How to Update Your Projects

When a new version is released:

1. **Check CHANGELOG** - Review what changed
2. **Ask Claude** - "Check for claude-brain-framework updates"
3. **Review Impact** - Claude will explain changes
4. **Approve Update** - Claude applies updates preserving customizations

For breaking changes (major versions), Claude will:
- Backup your current files
- Provide migration guide
- Guide you through step-by-step
- Validate nothing broke

---

[Unreleased]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.0.1...HEAD
[1.0.1]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/Marcosmenm/claude-brain-framework/releases/tag/v1.0.0
