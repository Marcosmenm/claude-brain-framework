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
