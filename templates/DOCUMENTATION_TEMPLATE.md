# [System Name] Documentation

**[One-line description of purpose]**

---

## Purpose

[2-3 sentences explaining what this system does and why it exists]

---

## Core Implementation Files

- **`[path/to/main/file]`** - [Purpose only, not implementation]
- **`[path/to/key/file]`** - [Purpose only]
- **`[path/to/config]`** - [Configuration location]

**Claude: Read these files when working on this system. Don't duplicate their contents here.**

---

## When to Reference This System

**Load this documentation when:**
- User requests [specific feature type]
- Working on [related functionality]
- Debugging [specific issue type]
- Modifying [specific component]

**Then read the relevant files above.**

---

## Current Limitations (CRITICAL)

**What's NOT implemented:**
- ❌ [Feature 1] - Not built yet
- ❌ [Feature 2] - Planned but not implemented
- ⚠️ [Feature 3] - Partially implemented, [specific limitation]

**Why document limitations:** Prevents Claude from assuming features exist.

---

## Platform/Environment-Specific Behavior

**If applicable:**
- **[Platform A]:** [Specific behavior or gotchas]
- **[Platform B]:** [Different behavior]
- **[Environment]:** [Special considerations]

---

## Related Systems

**This system interacts with:**
- **[System A]:** [Nature of interaction] - See [System_A_Documentation.md]
- **[System B]:** [Nature of interaction] - See [System_B_Documentation.md]

---

## Common Tasks

**Adding [new feature type]:**
→ Modify `[specific file]` (read file for implementation patterns)

**Modifying [existing feature]:**
→ Check `[specific file]`, update `[related file]`

**Debugging [common issue]:**
→ Check logs in `[location]`, verify `[specific file]` configuration

**Claude: These are pointers. Read the actual files to understand HOW to implement.**

---

## Configuration

**Location:** `[config file path]`
**Environment variables:** `[.env variables if any]`

**Claude: Read the config file when configuration changes are needed.**

---

## Quick Troubleshooting

**Issue:** [Common problem]
→ **Check:** [Specific file or log]
→ **Solution:** [Pointer to where fix should be made]

**Issue:** [Another common problem]
→ **Check:** [Specific location]
→ **Solution:** [Where to make changes]

---

## ⚠️ What This Documentation Does NOT Include

This documentation intentionally does NOT include:
- ❌ Code examples (read actual files instead)
- ❌ Step-by-step implementation tutorials
- ❌ Complete API references (in the code)
- ❌ Configuration option lists (in config files)
- ❌ Database schema details (read migrations)

**Why:** Claude can read source code. Documentation should explain WHEN and WHERE to read, not duplicate WHAT's there.

**See:** [../core/TOKEN_OPTIMIZATION.md#pointer-based-documentation-pattern](../core/TOKEN_OPTIMIZATION.md#pointer-based-documentation-pattern)

---

**Version:** 2.0.0 (Token-Optimized)
**Last Updated:** [Date]
**Purpose:** Signpost system, not content duplication
