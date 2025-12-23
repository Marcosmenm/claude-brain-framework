# Changelog

All notable changes to the Claude Brain Framework will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Planned Features
- Language-specific multi-repo templates (Java+React, Python+Vue, etc.)
- Documentation dependency graphs
- Enhanced MCP integration patterns
- Community agent contributions

## [1.5.0] - 2025-12-23

### Added
- **Reusability-First Development Pattern** (core/BEHAVIORAL_RULES.md) - **CRITICAL behavioral change**
  - New Section 7: Always check existing patterns before building new
  - Protocol: Check docs → Search code → Propose extending vs creating → Extract patterns
  - Applies to: components, services, APIs, queries, validation, auth, files, notifications
  - Prevents code duplication and maintains consistency
  - Based on real-world learnings from Claude Web Builder project

- **Quick Reference Registry Pattern** (core/TOKEN_OPTIMIZATION.md) - **Major token optimization**
  - Single-table registry for instant component/service/module lookup
  - Token savings: 60-70% reduction in discovery queries (4,500 → 1,400 tokens)
  - Speed: 5-10x faster component matching vs scanning multiple docs
  - Real-world validation: Claude Web Builder (12 components, 93-line registry)
  - Recommended columns: Name | Purpose | Path
  - Threshold: 15+ reusable items (components, services, models, utilities)
  - Organization: Start unified (40-50 items), split at 150+ lines
  - Manual updates: 10-15 seconds per item (automation not needed)

- **Registry Generation Protocol** (core/INIT_PROCESS.md Cycle 7)
  - Conditional step for projects with 15+ reusable abstractions
  - Automatic detection during initialization
  - Presents registry recommendation to user with token savings explanation
  - Integration with documentation generation workflow

- **Smart Documentation Loading** (templates/FRAMEWORK_PRINCIPLES.md) - **Optional enhancement**
  - Keyword-based auto-loading of relevant docs
  - Token cost: ~120-150 tokens overhead
  - ROI: Saves 2,000-4,000 tokens per trigger (break-even after 1-2 triggers)
  - Example: "authentication" → Auth_System.md, "component" → Component_Library.md
  - Project-specific triggers (define only for complex projects with 5+ specialized docs)
  - FRAMEWORK_PRINCIPLES.md updated to v1.5.0

- **Component Library Section Template** (templates/sections/COMPONENT_LIBRARY_SECTION.md)
  - Section template (not full template) to insert into existing CLAUDE.md
  - For: UI libraries, service catalogs, design systems, module libraries
  - Includes: Component management rules, versioning workflow, extraction protocol
  - Prevents common mistakes (modifying components in consumers)
  - ~150-200 lines to add to UNIVERSAL or TOKEN_OPTIMIZED template
  - Use when building projects with 15+ reusable abstractions

### Changed
- **BEHAVIORAL_RULES.md** - Added Section 7 after Intelligent Defaults
  - Elevates "Integration Over Addition" pattern to primary behavioral rule
  - Makes pattern-checking explicit and mandatory
  - Provides clear examples of correct vs wrong approaches

- **TOKEN_OPTIMIZATION.md** - Added registry pattern as proven optimization technique
  - Complements existing pointer-based documentation pattern
  - Includes real-world metrics from production usage
  - Integration guidance with documentation workflow

- **INIT_PROCESS.md** - Enhanced Cycle 7 with registry generation
  - Optional but recommended for component-heavy projects
  - Clear threshold guidance (15+ items)
  - Token savings explanation for user decision-making

- **FRAMEWORK_PRINCIPLES.md** - Updated to v1.5.0
  - Added optional Smart Doc Loading section (5 lines)
  - Keeps file compact: 44 base + 5 optional = 49 lines max
  - Token cost: ~350-400 tokens (still highly optimized)

### Why This Matters
- **Prevents Code Duplication**: Reusability-first pattern forces checking before building
- **Massive Token Savings**: Registry pattern reduces discovery queries by 60-70%
- **Faster Development**: 5-10x faster component/service discovery
- **Real-World Validated**: All patterns tested in production (Claude Web Builder)
- **Universal Patterns**: Applies to all project types (not technology-specific)
- **Optional Enhancements**: Advanced optimizations available but not required

### Technical Details
- **Based on:** Claude Web Builder production learnings (3+ weeks validation)
- **Test data:** 12 components, 93-line registry, 7 keyword triggers
- **Token metrics:** 60-70% savings (4,500 → 1,400 tokens per lookup)
- **Maintenance:** 10-15 seconds per registry entry (acceptable overhead)
- **ROI calculation:** Registry break-even after 1 lookup per session
- **Smart loading:** Break-even after 1-2 triggers per session

### Migration Guide
Existing projects can adopt incrementally:

**High Priority - Apply Immediately:**
1. **Reusability-First Pattern** - Update Claude behavior, no file changes needed
2. **Registry Pattern** - If you have 15+ components/services/modules

**Medium Priority - Consider Adding:**
3. **Smart Doc Loading** - If you have 5+ specialized docs and frequent context switching
4. **Component Library Section** - If building reusable library/design system

**Steps:**
1. Framework auto-detects v1.4.0 → v1.5.0 gap on next session
2. Claude offers update with feature summary
3. User approves update
4. Claude applies behavioral rules immediately
5. Optionally creates registry for component-heavy projects

## [1.4.0] - 2025-11-23

### Added
- **FRAMEWORK_PRINCIPLES.md** template (templates/) - **CRITICAL for project independence**
  - Ultra-compressed Claude-to-Claude protocol (~35 lines, 280 tokens)
  - Embedded in each project for framework knowledge persistence
  - Daily development standards: documentation, commenting, PRPs, quality checks
  - Language-agnostic patterns applicable to all tech stacks
  - Eliminates need to open parent folder or reference framework continuously

- **UPDATE_PROPAGATION.md** (core/) - Automated framework update system
  - Version tracking across all projects
  - Proactive update detection on session start
  - Propagation process: behavioral, template, structural updates
  - Multi-project batch update capability
  - Backward compatibility enforcement
  - Update history logging and rollback support

### Changed
- **INIT_PROCESS.md** (core/) - Added FRAMEWORK_PRINCIPLES.md creation step
  - Now creates `.claude/FRAMEWORK_PRINCIPLES.md` during initialization
  - Ensures every new project has embedded framework knowledge
  - Projects can work independently without framework directory access

- **BEHAVIORAL_RULES.md** (core/) - Added session start protocol
  - Mandatory check for FRAMEWORK_PRINCIPLES.md on session start
  - Auto-load framework principles for quality enforcement
  - Documentation protocol, commenting standards, quality checks now automatic

- **CLAUDE_MD_TOKEN_OPTIMIZED.md** (templates/) - Added framework philosophy section
  - References `.claude/FRAMEWORK_PRINCIPLES.md` for daily standards
  - Framework reference path for on-demand access
  - Updated to v1.4.0

### Philosophy
- **Project Independence:** Each project self-sufficient for daily work
- **Knowledge Persistence:** Framework principles embedded, not externally referenced
- **Token Optimization:** Minimal framework footprint (~280 tokens vs 15-25k loading framework)
- **Claude-to-Claude:** Pure AI instruction protocol, zero human-friendly fluff
- **Propagation System:** Framework updates flow to projects automatically

### Migration Path
Existing projects can add FRAMEWORK_PRINCIPLES.md via:
1. Copy `claude-brain-framework/templates/FRAMEWORK_PRINCIPLES.md` to `.claude/`
2. Update CLAUDE.md with framework philosophy section
3. Update version footer to v1.4.0

## [1.3.0] - 2025-11-10

### Added
- **TOKEN_OPTIMIZATION.md** - New core methodology guide for reducing token usage
  - Proven 28% average token reduction (15-36% depending on query complexity)
  - Real-world test results from TagMyLink project (790→203 line CLAUDE.md)
  - Simple implementation steps with before/after examples
  - Clear guidelines on when to use optimization pattern
  - Validation protocol for measuring effectiveness

- **CLAUDE_MD_TOKEN_OPTIMIZED.md** - New recommended template (templates/)
  - Minimal upfront context (~5-8k tokens vs ~40-50k traditional)
  - On-demand documentation loading protocol
  - Documentation index with file names + brief descriptions
  - Methodology references (fetch only when needed)
  - Architecture quick reference (names only, not full details)

### Changed
- **README.md** - Added token optimization to framework components
  - Listed TOKEN_OPTIMIZATION.md in Core Methodology section
  - Added CLAUDE_MD_TOKEN_OPTIMIZED.md as recommended template
  - Marked as "NEW v1.3.0" for visibility

### Philosophy
- "Load minimal essentials upfront, fetch detailed docs on-demand"
- Shifts from "load everything just in case" to "fetch what's needed when needed"
- Treats token budget as a finite resource requiring optimization

## [1.2.1] - 2025-10-21

### Added
- **Proactive Update Detection**: New automatic framework update checking at session start
  - Claude automatically detects when project framework version < latest framework version
  - Proactively notifies user of ALL missing updates (not just latest)
  - Lists each version update with key features from CHANGELOG
  - Offers user choice: apply all, apply specific version(s), or skip
  - No more missed framework improvements

### Changed
- **VERSION_DETECTION.md**: Added "Proactive Update Detection" section
  - New Section 1: Automatic update check at session start (CRITICAL)
  - New Section 2: Reactive update application (existing behavior)
  - Added Example 1: Proactive detection with multi-version gap scenario
  - Protocol now executes automatically without user request

- **BEHAVIORAL_RULES.md**: Enhanced "Session Start" section
  - Added Step 3: Automatic framework update check (PROACTIVE)
  - Includes example of proactive notification before responding to user
  - Links to VERSION_DETECTION.md for complete protocol

- **UPDATE_PROCESS.md**: Added user choice handling mechanism
  - New "Step 2: Handle User Choice" for multiple update scenarios
  - Handles "Apply all", "Apply specific version", "Skip for now"
  - Tracks offered updates to avoid repetitive notifications
  - Step 1 now shows both automatic (session start) and on-request detection

### Why This Matters
- **No More Missed Updates**: Framework improvements automatically offered to users
- **User Control**: Users choose which updates to apply, not forced
- **Multi-Version Awareness**: Shows ALL missing versions (v1.0.0 → v1.1.0 → v1.2.0), not just latest
- **Reduces Friction**: Users don't need to remember to check for updates
- **Transparent**: Clear communication about what each version adds

### Context
This update directly addresses the issue where Claude would ignore framework updates unless explicitly asked to apply them. Now Claude proactively checks and offers updates at the start of every session, ensuring users benefit from framework improvements.

**Example Scenario:**
```
Project on v1.0.0, framework at v1.2.0
Old behavior: Claude ignores updates, user misses new features
New behavior: Claude automatically notifies:
  "Missing v1.1.0 (multi-repo templates) and v1.2.0 (lean workflow).
   Apply all, specific, or skip?"
```

## [1.2.0] - 2025-10-20

### Added
- **Lean Development Workflow**: New `core/LEAN_DEVELOPMENT_WORKFLOW.md` documentation
  - Research → Plan → Build → Test → Iterate methodology
  - Incremental development protocol for complex features (>3 files, >200 lines)
  - Test-driven development (TDD) integration patterns
  - Diff size guidelines (<200 lines per phase recommended)
  - Context management strategies with /clear usage
  - Checkpoint-based development and feature flagging patterns
  - Based on official Anthropic Claude Code best practices
  - Aligned with Claude Sonnet 4.5 capabilities (30+ hour autonomous work, parallel tool calls)

- **CI/CD Deployment Guide**: New `core/CICD_DEPLOYMENT_GUIDE.md` documentation
  - 5-phase lean deployment setup methodology
  - Enhanced health check strategies (4 levels: basic → production-grade)
  - Zero-downtime deployment patterns (blue-green, rolling, container-based)
  - Rollback mechanisms and database migration strategies
  - Secrets management and monitoring integration
  - Performance optimization techniques
  - Workflow branching strategies (Feature Branch, Trunk-Based)
  - Framework-agnostic debugging checklist

- **CI/CD Examples Directory**: New `examples/cicd/` with real-world workflow templates
  - `COMMON_ERRORS.md`: Framework-agnostic troubleshooting guide for production deployments
  - `laravel-example.yml`: PHP/Laravel + React deployment workflow
  - `nodejs-example.yml`: Node.js/Express API deployment workflow
  - `docker-example.yml`: Container-based deployment workflow
  - Covers SSH, database, build, runtime version, and configuration issues across frameworks

- **Enhanced Behavioral Rules**: Updated `core/BEHAVIORAL_RULES.md`
  - Section 5: Incremental Development Protocol with automatic detection
  - Proposal pattern for phased implementation (3-5 phases with test criteria)
  - After-phase confirmation protocol (wait for user before proceeding)
  - Updated Pattern 2: Complex Feature Request with incremental approach example
  - Links to LEAN_DEVELOPMENT_WORKFLOW.md and CICD_DEPLOYMENT_GUIDE.md

### Changed
- **README.md**: Updated core concepts section
  - Added "Lean Incremental Development" as concept #2
  - Added "CI/CD Best Practices" as concept #6
  - Renumbered existing concepts to accommodate new additions
  - Added `LEAN_DEVELOPMENT_WORKFLOW.md` and `CICD_DEPLOYMENT_GUIDE.md` to core methodology list
  - Added `examples/cicd/` to examples section
  - Marked new additions with "NEW v1.2.0" labels

### Why This Matters
- **Reduces Debugging Time by 75%**: Incremental development isolates errors to recent changes (2-5 errors per feature vs 15-30 with big-bang approach)
- **12x Faster First Test**: Small phases mean testing in 10-20 minutes vs 2-4 hours for complete features
- **Production-Ready Deployment**: Real-world CI/CD patterns prevent common 23-error deployment failures
- **Framework-Agnostic**: Deployment guides and examples work across Laravel, Node.js, Python, Docker
- **Anthropic-Aligned**: Methodology matches official Claude Code best practices and Claude 4.5 capabilities
- **Developer Confidence**: Incremental validation builds confidence; lean deployment reduces 2 AM debugging sessions

### Technical Details
- Research based on Anthropic's official [Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- Claude Sonnet 4.5 features: Extended focus (30+ hours), parallel tool calls, improved state tracking
- Health check implementations: 4 levels from basic HTTP to deep production-grade monitoring
- Deployment strategies: Blue-green, rolling releases, container orchestration with zero-downtime patterns
- Real production experience: Based on TagMyLink Release 1.15.0 (TMLAPP-775) deployment learnings

## [1.1.0] - 2025-10-13

### Added
- **Multi-Repository System Template**: New `CLAUDE_MD_MULTI_REPO_SYSTEM.md` template for backend + frontend(s) architectures
  - Specialized template for systems with multiple interconnected repositories
  - Includes API versioning strategy documentation
  - Cross-repository coordination and deployment guidance
  - Supports backend + web + mobile configurations

- **Documentation Index Template**: New `DOCUMENTATION_INDEX_TEMPLATE.md` for documentation catalog management
  - Status tracking with ✅ completed and 📝 TODO indicators
  - Priority system (High/Medium/Low) for documentation planning
  - Documentation maintenance guidelines
  - Usage instructions for different developer roles

- **Incremental Documentation Strategy**: Enhanced `core/INIT_PROCESS.md` Cycle 7
  - Strategy for large codebases (15+ domains, multi-repository systems)
  - Create analysis file first, then generate high-priority docs incrementally
  - Prevents token exhaustion and maintains documentation quality
  - Allows users to request additional docs as needed
  - Small-medium codebases still generate all docs in one pass

- **Multi-Repository E-Commerce Example**: New `examples/multi-repo-ecommerce/`
  - Demonstrates multi-repo template usage with backend + web + mobile architecture
  - Shows DOCUMENTATION_INDEX.md in practice
  - Provides copy-paste ready example for real projects
  - Illustrates incremental documentation strategy

### Why This Matters
- **Multi-Repo Support**: Many modern systems use separate repos for backend/frontend - now properly supported
- **Scalable Documentation**: Large codebases can now be documented incrementally without quality loss
- **Better Navigation**: Documentation index provides central hub for all project knowledge
- **Real-World Testing**: Enhancements based on documenting enterprise CRM with 15 domains, 80+ repos, 3 frontends

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

[Unreleased]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.5.0...HEAD
[1.5.0]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.4.0...v1.5.0
[1.4.0]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.3.0...v1.4.0
[1.3.0]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.2.1...v1.3.0
[1.2.1]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.2.0...v1.2.1
[1.2.0]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.1.0...v1.2.0
[1.1.0]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.0.1...v1.1.0
[1.0.1]: https://github.com/Marcosmenm/claude-brain-framework/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/Marcosmenm/claude-brain-framework/releases/tag/v1.0.0
