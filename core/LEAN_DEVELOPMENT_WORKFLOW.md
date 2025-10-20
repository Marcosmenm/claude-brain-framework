# Lean Development Workflow with Claude

**Incremental development methodology for AI-assisted software engineering**

> **"Small diffs, fast feedback, continuous delivery."**

## 🎯 Core Philosophy

Claude Sonnet 4.5 excels at **incremental, test-driven development** rather than big-bang implementations. Based on [official Anthropic guidelines](https://www.anthropic.com/engineering/claude-code-best-practices), this methodology maximizes success rates and minimizes debugging complexity.

---

## 📊 The Problem: Big-Bang Development

### ❌ What Fails

**Typical Pattern:**
- User requests complex feature
- Claude generates 15 files, 2,000 lines of code
- User runs it → 23 errors appear
- **Problem:** Which of 15 files caused which of 23 errors?

### 🔴 Why It Fails

1. **Exponential debugging complexity** - More code = exponentially more interaction bugs
2. **No isolation** - Can't determine which change broke what
3. **Context overload** - Too many concepts simultaneously
4. **Difficult rollback** - Everything is intertwined
5. **No intermediate validation** - First test after everything is written

---

## ✅ The Solution: Research → Plan → Build → Test → Iterate

### The Anthropic-Recommended Pattern

**Claude 4.5's Strengths:**
- Extended focus (30+ hours autonomous work)
- Parallel tool calls (read multiple files simultaneously)
- Small diffs (<200 lines per iteration)
- State tracking across sessions

**Workflow:**

```
1. RESEARCH (no code yet)
   └─> Understand existing patterns, dependencies, architecture

2. PLAN (break into phases)
   └─> 3-5 testable increments, each <200 lines

3. BUILD (smallest testable unit)
   └─> Implement Phase 1 only

4. TEST (validate before proceeding)
   └─> User confirms working

5. ITERATE (repeat 3-4 for remaining phases)
   └─> Build on validated foundation
```

---

## 🎯 When to Use Lean vs Full Implementation

### ✅ Use Lean Incremental Approach When:

- Feature touches **>3 files**
- Implementation **>200 lines total**
- **Multiple new concepts** (e.g., auth + email + permissions)
- **Unfamiliar systems** or **critical business logic**
- **High complexity** or **team collaboration**

### ⚡ Full Implementation OK When:

- **Single file change**
- **<100 lines of code**
- **Well-defined, isolated feature**
- **Easy to test/verify immediately**
- **Low risk** if something breaks

---

## 🤖 Claude's Behavioral Protocol

### Detection: When to Suggest Breakdown

**CLAUDE: Automatically propose incremental approach when:**

```markdown
User request contains:
❌ "Add contact form" → Direct implementation OK
✅ "Add contact form with email notifications and admin dashboard" → Propose phases
✅ "Implement payment processing with Stripe" → Propose phases
✅ "Refactor authentication to use OAuth2" → Propose phases
```

### Proposal Template

**CLAUDE: Use this pattern:**

```
"I can implement [feature]. This will involve [X systems/files/concepts].

I recommend we build this incrementally to make debugging easier:

**Phase 1: [Core functionality - MVP]** (~X min)
- [Specific tasks]
- **Test:** [How to verify]

**Phase 2: [Add Feature Y]** (~X min)
- [Specific tasks]
- **Test:** [How to verify]

**Phase 3: [Add Feature Z]** (~X min)
- [Specific tasks]
- **Test:** [How to verify]

**Estimated total:** ~X hours

Each phase is independently testable. Sound good, or prefer I implement everything at once?"
```

**Key Elements:**
1. Acknowledge the request
2. Explain incremental benefit
3. Break into 3-5 phases (not too granular)
4. Include test criteria for each
5. **Ask for user preference** (don't force it)

---

### Implementation: Pause Between Phases

**CLAUDE: After completing each phase:**

```
"✅ Phase 1 complete. Here's what I added:
- [File 1]: [What changed]
- [File 2]: [What changed]

**To test:**
```bash
[Exact command]
```

**Expected result:** [What should happen]

Please verify before I proceed to Phase 2."
```

**Wait for user confirmation before next phase.**

---

## 🧪 Test-Driven Development Integration

### The TDD Pattern

**Anthropic's recommended workflow:**

1. **Define behavior (write tests first)**
   ```javascript
   it('accepts valid credentials', async () => {
     const response = await login('user@example.com', 'password123');
     expect(response.status).toBe(200);
   });
   ```
   **Tests FAIL** ❌ (no implementation)

2. **Implement minimum code to pass**
   ```javascript
   router.post('/login', async (req, res) => {
     // Minimal implementation
   });
   ```
   **Tests PASS** ✅

3. **Add next test (Phase 2)**
   ```javascript
   it('returns JWT token on successful login', async () => {
     expect(response.body.token).toBeDefined();
   });
   ```
   **Test FAILS** ❌ (not implemented)

4. **Implement to pass new test**
   **Test PASSES** ✅

**Repeat...**

### Benefits

- Tests define success criteria (no ambiguity)
- Regression prevention (previous phases stay working)
- Confidence in changes (green tests = safe to proceed)
- Easier debugging (failed test = specific broken feature)

---

## 📐 Diff Size Guidelines

**Anthropic recommendation: <200 lines per phase when possible**

| Phase Complexity | Target Diff | Example |
|-----------------|-------------|---------|
| **Minimal** | 10-50 lines | Single endpoint, utility function |
| **Small** | 50-100 lines | Service with 2-3 methods |
| **Medium** | 100-200 lines | Feature with tests, multiple files |
| **Large** | 200-400 lines | Major refactor, complex integration |
| **Too Large** | >400 lines | ⚠️ **Break into smaller phases** |

---

## 🔍 Context Management

### Use /clear Between Phases

**Pattern:**

```
User: "Let's add authentication"
Claude: [Researches code, proposes 4 phases]
User: "Start Phase 1"
Claude: [Implements Phase 1]
User: [Tests] "Works! Phase 2"
User: /clear  ← Reset context, focus on Phase 2 only
Claude: [Implements Phase 2 without rehashing Phase 1]
```

**When to /clear:**
- ✅ Between phases (keep focus tight)
- ✅ After successful test
- ✅ When changing topics

**When NOT to /clear:**
- ❌ Active debugging (need error context)
- ❌ Mid-phase implementation
- ❌ Before final testing

---

## 🚀 Advanced Patterns

### Pattern 1: Checkpoint-Based Development

**For complex features, create stable checkpoints:**

```
Checkpoint A: Core Integration
→ Test: Basic connection works

Checkpoint B: Main Functionality
→ Test: Primary feature operational

Checkpoint C: Enhanced Features
→ Test: Additional features working

Checkpoint D: Production Hardening
→ Test: Error handling, edge cases covered
```

**Benefit:** Can return to any checkpoint if something breaks

---

### Pattern 2: Feature Flagging for Risky Changes

**Deploy incomplete features safely:**

```javascript
// config/features.js
module.exports = {
  NEW_AUTH_SYSTEM: process.env.ENABLE_NEW_AUTH === 'true'
};

// Use in code
if (features.NEW_AUTH_SYSTEM) {
  // New implementation (being built incrementally)
} else {
  // Old implementation (still works)
}
```

**Benefits:**
- Deploy safely to production
- Test with subset of users
- Easy rollback (toggle flag)
- Incremental migration

---

## 📊 Success Metrics

| Metric | Big-Bang | Lean Incremental | Improvement |
|--------|----------|------------------|-------------|
| **Time to First Test** | 2-4 hours | 10-20 min | **12x faster** |
| **Debugging Time** | 40-60% of dev | 5-15% of dev | **75% reduction** |
| **Errors per Feature** | 15-30 errors | 2-5 errors | **80% fewer** |
| **Code Review Time** | 2-3 hours | 20-30 min | **6x faster** |
| **Rollback Frequency** | 15-20% | <5% | **70% reduction** |

---

## 🎓 Integrate with Your CLAUDE.md

**Add to your project's CLAUDE.md:**

```markdown
## Development Methodology

**This project follows lean incremental development:**

### Required Approach for Complex Features
For features affecting >3 files or >200 lines:
1. Research existing patterns first
2. Propose 3-5 incremental phases
3. Implement smallest testable unit
4. Wait for test confirmation before next phase
5. Keep diffs <200 lines per phase

### Checkpoint Requirements
Each phase must include:
- **What's added:** Specific files/functions
- **How to test:** Exact commands
- **Expected result:** Success criteria
- **Estimated time:** Realistic completion time

See `/core/LEAN_DEVELOPMENT_WORKFLOW.md` for full methodology.
```

---

## 🔄 Connection to CI/CD

**Same lean principles apply to deployment setup:**

**Bad:** Write complete 15-step pipeline → 23 errors → 4 hours debugging

**Good:** Iteration 1 (test connection) → Iteration 2 (add checkout) → Iteration 3 (add build) → continue incrementally

**See:** [CICD_DEPLOYMENT_GUIDE.md](CICD_DEPLOYMENT_GUIDE.md) for lean CI/CD methodology

---

## 🎯 Quick Reference Card

### CLAUDE's Checklist for Complex Features:

```
□ Does this affect >3 files?
□ Is this >200 lines of code?
□ Multiple new concepts?
□ Unfamiliar territory?
□ Critical business logic?

If YES to any → Propose incremental phases
```

### After Each Phase:

```
□ Show what changed
□ Provide test command
□ Describe expected result
□ Wait for confirmation
□ Proceed only after "✅"
```

---

## 📚 References

- [Anthropic: Claude Code Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)
- [Claude 4.5 Release Notes](https://www.anthropic.com/news/claude-sonnet-4-5)
- [BEHAVIORAL_RULES.md](BEHAVIORAL_RULES.md) - Claude's operational guidelines
- [CICD_DEPLOYMENT_GUIDE.md](CICD_DEPLOYMENT_GUIDE.md) - Lean CI/CD methodology

---

**Last Updated:** 2025-10-20 | **Framework Version:** 1.2.0
