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
5. **Documentation as pointers** - Explain WHEN and WHERE to read files, not WHAT's in them
6. **Avoid code duplication** - Claude can read source code; documentation explains purpose and location

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

## Pointer-Based Documentation Pattern

**Documentation should be a signpost system, not a content duplication system.**

### What Documentation SHOULD Do

✅ **Explain what exists** - "The PWA system handles offline functionality"
✅ **Point to locations** - "Implementation: `src/service-worker.js`, config: `pwa-config.json`"
✅ **Describe scenarios** - "When user requests offline access → reference PWA docs"
✅ **Document limitations** - "NOT IMPLEMENTED: Push notifications, background sync"
✅ **Platform-specific gotchas** - "iOS requires user gesture for PWA install"
✅ **List related systems** - "PWA interacts with: Cache API, Auth system, API layer"

### What Documentation SHOULD NOT Do

❌ **Duplicate code** - Don't copy implementation from source files
❌ **Line-by-line explanations** - Claude reads the actual code
❌ **Configuration references** - Don't list every config option (it's in the code)
❌ **Step-by-step tutorials** - Claude figures out implementation from code
❌ **Complete API references** - Redundant when source is readable
❌ **Repeated structures** - Don't explain the same pattern in multiple docs

### Example: Token-Optimized Documentation Structure

```markdown
# PWA System Documentation

## Purpose
Enables offline functionality and app-like experience for TagMyLink users.

## Core Implementation Files
- `src/service-worker.js` - Cache strategies and offline handling
- `src/pwa-config.json` - PWA manifest and configuration
- `src/hooks/usePWA.ts` - React hook for PWA status

## When to Reference This System
- User reports offline functionality issues
- Implementing new cacheable features
- Updating PWA manifest or icons
- Modifying service worker behavior

## Current Limitations (CRITICAL)
- ❌ Push notifications NOT implemented
- ❌ Background sync NOT implemented
- ❌ Offline form submission queued but not tested
- ⚠️ iOS PWA install requires manual user gesture

## Platform-Specific Behavior
- **iOS:** Must be added to home screen manually, limited cache
- **Android:** Automatic install prompt, full cache support
- **Desktop:** Chrome/Edge support, Safari limited

## Related Systems
- Cache API (managed by service worker)
- Authentication (offline token refresh not supported)
- API Layer (offline requests queued)

## Common Tasks
**Adding new cached route:**
→ Modify `src/service-worker.js` cache patterns

**Updating PWA manifest:**
→ Edit `pwa-config.json`, update icons in `public/icons/`

**Testing offline:**
→ Chrome DevTools > Application > Service Workers > Offline
```

**Token Savings:** 60-85% vs traditional comprehensive docs

### Traditional vs Pointer-Based

**TRADITIONAL (450 lines, 3.2k tokens):**
```markdown
# PWA Documentation

## Service Worker Implementation

The service worker is implemented in src/service-worker.js.

### Cache Strategy
We use a cache-first strategy for static assets:

\`\`\`javascript
// Don't duplicate this - it's already in the file!
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});
\`\`\`

### Configuration Options
- cacheName: 'tagmylink-v1'
- cacheUrls: ['/index.html', '/app.js', ...]
- offlineUrl: '/offline.html'
[... 400 more lines duplicating what's in code ...]
```

**POINTER-BASED (80 lines, 500 tokens):**
```markdown
# PWA Documentation

## Purpose
Offline functionality for TagMyLink users.

## Files
- `src/service-worker.js` - Cache strategies
- `pwa-config.json` - Configuration

## When Needed
- Offline issues → Read service-worker.js
- PWA config → Read pwa-config.json

## Not Implemented
- Push notifications
- Background sync

## Common Tasks
Add cached route → Modify service-worker.js patterns
Update manifest → Edit pwa-config.json
```

**Result:** 84% token reduction, same utility for Claude.

---

## Quick Reference Registry Pattern

**For projects with 20+ reusable components/modules/services**

### The Problem

Finding specific components/services wastes tokens even with pointer-based docs:
- Must read DOCUMENTATION_INDEX → system docs → scan directories → read multiple files
- Token cost: 4,000-5,000 tokens per component search
- Slow discovery process

### The Solution

**Single-table registry for instant lookup:**

```markdown
# COMPONENT_REGISTRY.md (or SERVICE_REGISTRY.md, MODEL_REGISTRY.md)

| Name | Purpose | Path |
|------|---------|------|
| hero-split | Hero section with image and CTA | components/heroes/hero-split/ |
| AuthService | User authentication and tokens | app/Services/AuthService.php |
| UserModel | User account and relationships | app/Models/User.php |
```

**Claude scans table → finds match → reads specific file if needed**

### Real-World Results

**Test Project:** Claude Web Builder (12 components, 93-line registry)

| Without Registry | With Registry | Savings |
|------------------|---------------|---------|
| ~4,500 tokens | ~1,400 tokens | **69%** ↓ |
| Multiple file reads | Single table scan | **5-10x faster** |

**ROI:** Registry costs ~1,400 tokens, saves 2,500-3,500 per lookup. Break-even after 1 query per session.

### When to Use

✅ **Use when:**
- 15+ reusable components/modules/services
- Frequent "which component does X?" questions
- Component library, service catalog, or design system

⚠️ **Skip when:**
- <10 items (documentation index sufficient)
- Unique one-off implementations

### Registry Structure

**Recommended columns:**
- **Name** - Identifier (matches file/class name)
- **Purpose** - What it does (1 line max)
- **Path** - Location to read full details

**Optional columns:** Type/Category, Status, Tags (add only if useful)

**Organization:**
- **Start unified** - One registry up to 40-50 items
- **Split when large** - Separate registries at 150+ lines or fundamentally different types
- **Use category headers** - Group items logically within unified registry

**Example split:**
```
.claude/documentation/
├── COMPONENT_REGISTRY.md    # UI components
├── SERVICE_REGISTRY.md      # Backend services
├── MODEL_REGISTRY.md        # Data models
```

### Maintenance

**Manual updates work best:**
- Add one line when creating new item (10-15 seconds)
- Batch updates every 3-5 items
- Automation not worth complexity

**Template:**
```markdown
| new-item | Brief purpose description | path/to/item/ |
```

### Integration with Documentation

**Registry = Quick lookup** (find which item exists, get path)
**Full documentation = Deep context** (how it works, configuration, patterns)

**Workflow:**
1. User asks about component → Claude reads registry → finds match
2. If details needed → Claude reads full documentation at path
3. Implement using discovered pattern

### Token Savings Summary

- **Discovery:** 60-70% token reduction
- **Speed:** 5-10x faster component matching
- **Typical savings:** 2,500-3,500 tokens per lookup
- **Best for:** Projects with 15+ reusable abstractions

**See:** [INIT_PROCESS.md Cycle 7](INIT_PROCESS.md) for registry generation during initialization

---

## Framework Integration

This optimization is now **mandatory** for all new projects using claude-brain-framework v1.4.0+

**Documentation Philosophy:**
> "Documentation should serve as a pointer and context guide, not a complete reference manual. Claude can read source code - documentation should explain WHEN and WHY to read specific files, not duplicate their contents."

Existing projects can migrate gradually:
1. High-documentation projects first (biggest wins)
2. Test and validate with real usage
3. Share learnings to refine the pattern

---

**Version:** 1.1.0 (Added Pointer-Based Pattern)
**Tested on:** TagMyLink (Laravel + React), Claude Skills Integration
**Framework:** claude-brain-framework v1.4.0
**Date:** 2025-11-11
