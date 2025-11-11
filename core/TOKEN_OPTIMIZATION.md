# Token Optimization Guide

**Proven approach to reduce token usage by 28% average (15-36% depending on query complexity)**

## The Problem

Traditional CLAUDE.md files load everything upfront:
- All methodology sections
- All documentation references
- All workflow guidelines
- All PRP templates

**Result:** 40-50k tokens loaded before any work starts, even for simple 1-line changes.

## The Solution

**Load minimal essentials upfront, fetch detailed docs on-demand.**

### Optimized CLAUDE.md Structure

```markdown
# CLAUDE.md - [Project Name]

[Brief project description]

## Project Structure
[Component locations, tech stack overview]

## Quick Start
[Development commands only]

## Critical Rules
[Database safety, SSH restrictions, git commit rules]
[Chat history saving protocol]

## Documentation Index
**CLAUDE: Fetch documentation only when needed. Don't load everything upfront.**

Documentation in `.claude/documentation/`:
- System_A_Documentation.md - [Brief description]
- System_B_Documentation.md - [Brief description]
- Feature_X_Documentation.md - [Brief description]

Component guides: [Backend/CLAUDE.md], [Frontend/CLAUDE.md]

## Methodology References
For complex features (>3 files), read [CLAUDE_FULL_METHODOLOGY.md]
For PRPs, read [lines X-Y of full methodology]
For database work, read [Database_Guidelines.md]

## Architecture Quick Reference
[Tech stack, auth system, key integrations - just names, not full docs]
```

### What Gets Loaded When

**Always Loaded (~5-8k tokens):**
- Project identity and structure
- Critical safety rules
- Quick start commands
- Documentation index (file names + 1-line descriptions)
- Architecture quick reference (technologies used)

**Loaded On-Demand (only when needed):**
- Full system documentation files
- Complete PRP workflow methodology
- Database migration procedures
- Deployment guides
- Component-specific patterns

## Real-World Results

**Test Project:** TagMyLink (790 lines → 203 lines CLAUDE.md)

| Test Scenario | Before | After | Savings |
|--------------|--------|-------|---------|
| Simple styling change | 47,465 tokens | 31,168 tokens | **34%** ↓ |
| System architecture question | 49,187 tokens | 31,250 tokens | **36%** ↓ |
| Complex feature + PRP | 53,000 tokens | 45,071 tokens | **15%** ↓ |
| **Average** | **49,884 tokens** | **35,830 tokens** | **28%** ↓ |

## Implementation Steps

### 1. Create Backup
```bash
cp CLAUDE.md CLAUDE_FULL_METHODOLOGY.md
```

### 2. Slim Down CLAUDE.md

**Keep:**
- Project identity (3-5 lines)
- Quick start commands (code block)
- Critical rules (database, SSH, git)
- Documentation index (file names only)

**Move to separate files:**
- Full PRP workflow → Keep in CLAUDE_FULL_METHODOLOGY.md
- Database procedures → Keep in existing Database docs
- Deployment guides → Keep in README-DEPLOYMENT.md

### 3. Add Retrieval Protocol

```markdown
## Documentation Access

**CLAUDE: Don't load all documentation upfront.**

When user asks about [System X]:
1. Identify relevant doc from index
2. Use Read tool to fetch that specific file
3. Extract relevant sections only
4. Proceed with task
```

### 4. Test and Measure

Run 3 test queries:
1. Simple change (styling, text update)
2. System question (architecture, how does X work)
3. Complex feature (full-stack implementation)

Ask Claude: "How many tokens used in this conversation?"

**Target:** 25-35% reduction in average token usage

## When to Use This Pattern

✅ **Good fit:**
- Projects with extensive documentation (>5 system docs)
- Multi-component projects (backend, frontend, mobile)
- Complex methodology (PRP workflows, phased development)
- Long CLAUDE.md files (>500 lines)

⚠️ **Less beneficial:**
- Simple projects with minimal documentation
- Single-component projects
- CLAUDE.md already lean (<200 lines)

## Migration Guide for Existing Projects

1. **Backup current CLAUDE.md**
2. **Create documentation index** (list all `.claude/documentation/` files)
3. **Extract core essentials** (rules, commands, structure)
4. **Move methodology to backup file** (keep for reference)
5. **Add on-demand retrieval instructions**
6. **Test with real queries**
7. **Refine based on results**

## Key Principles

1. **Always loaded ≠ Always needed** - Most conversations use 10-20% of total context
2. **Index over content** - List what exists, fetch when needed
3. **Critical rules stay loaded** - Safety rules must always be active
4. **Methodology on-demand** - Complex workflows loaded only for complex tasks

## Example: Before vs After

**BEFORE (580 lines, 45k tokens):**
```markdown
# CLAUDE.md

[Project overview: 50 lines]
[Critical rules: 100 lines]
[Full PRP workflow: 200 lines]
[Database migration guide: 80 lines]
[Development methodology: 150 lines]
```

**AFTER (180 lines, 8k tokens):**
```markdown
# CLAUDE.md

[Project overview: 20 lines]
[Critical rules: 50 lines]
[Documentation index: 30 lines - FILE NAMES ONLY]
[Methodology references: 20 lines - "Read X when needed"]
[Architecture quick ref: 60 lines]

Note: Full methodology in CLAUDE_FULL_METHODOLOGY.md
```

## Troubleshooting

**Q: Claude doesn't fetch documentation automatically?**
A: Add explicit retrieval protocol with "When user asks about X → Read Y.md"

**Q: Some queries still use high tokens?**
A: Expected for complex features requiring multiple docs. Focus on reducing simple query overhead.

**Q: How granular should documentation index be?**
A: One line per file. Example: `Billing_System.md - Stripe integration and webhooks`

**Q: Should I split large documentation files?**
A: Only if single file >10k tokens. Otherwise keep logical systems together.

## Validation

After implementing, verify with:

```bash
# Test 1: Simple query
"Fix button color in component X"

# Test 2: Architecture question
"How does authentication work in this system?"

# Test 3: Complex feature
"Implement feature X with backend API and frontend UI"

# Ask after each:
"How many tokens used in this conversation?"
```

**Success criteria:**
- Test 1: <15k tokens (was 40-50k)
- Test 2: <25k tokens (was 45-55k)
- Test 3: <35k tokens (was 50-60k)

## Framework Integration

This optimization is now **recommended** for all new projects using claude-brain-framework v1.3.0+

Existing projects can migrate gradually:
1. High-documentation projects first (biggest wins)
2. Test and validate with real usage
3. Share learnings to refine the pattern

---

**Version:** 1.0.0
**Tested on:** TagMyLink (Laravel + React)
**Framework:** claude-brain-framework v1.3.0
**Date:** 2025-11-10
