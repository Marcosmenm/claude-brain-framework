# Framework Principles v1.5.0

**Claude-to-Claude protocol. Load on session start.**

## Documentation Protocol
Before creating docs: Check exists elsewhere → consolidate
Structure: Pointer-based (file paths only), not code duplication
Length: <150 lines per doc
Update: Modify docs after code changes
Format: System name, file locations, when to reference, not implemented features

## Smart Doc Loading (Optional - Advanced)
For projects with 5+ specialized docs, add keyword triggers:
Detect request keywords → auto-load relevant docs before responding
Example: "authentication" → Auth_System.md, "component" → Component_Library.md
Define project-specific triggers below (if needed)
Cost: ~120-150 tokens, saves 2,000-4,000 tokens when triggered

## Code Comments (All Languages)
Pattern: `/* Section Name */` `// Section Name` `# Section Name`
Comment "why" decisions, not "what" code does
No decoration, phases, verbose descriptions

## PRP Generation
Auto-generate: >3 files OR business logic OR new feature OR integration
Skip: single file bug fix OR styling OR config OR text changes

## Complex Features
>3 files OR unfamiliar systems → propose phased implementation
Each phase independently testable, wait validation between phases

## Quality Check (Execute before new docs)
1. Exists elsewhere? → Consolidate
2. Duplicates code? → File path pointer instead
3. >150 lines? → Split or remove redundancy

## Integration Pattern
Analyze existing → integrate with proven patterns → enhance existing
Never create parallel systems when existing works

## Cross-Project Reference
Projects: /Users/marcosm/Documents/dev/[project]/.claude/documentation/
Framework: /Users/marcosm/Documents/dev/claude-brain-framework/

## On-Demand Framework Docs
Methodology: core/METHODOLOGY.md
PRPs: templates/PRP_TEMPLATE.md
Token optimization: core/TOKEN_OPTIMIZATION.md
Behavior: core/BEHAVIORAL_RULES.md
Init: core/INIT_PROCESS.md
Updates: core/UPDATE_PROPAGATION.md
