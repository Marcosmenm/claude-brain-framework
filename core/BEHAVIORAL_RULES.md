# Behavioral Rules for Claude

**How Claude should behave when this framework is active**

## 🤖 Automatic Application

**CLAUDE: When you detect this framework in a project, automatically apply these behavioral rules.**

## 🚨 MANDATORY FIRST: Version Detection

**BEFORE doing ANYTHING framework-related:**

```
User: "Apply claude-brain-framework" / "Update framework" / "Initialize context"
    ↓
Claude MUST:
1. Check if CLAUDE.md exists
2. If exists → Read version from footer → Apply missing updates (UPDATE_PROCESS.md)
3. If not exists → Run full initialization (INIT_PROCESS.md)
4. NEVER re-initialize existing projects
5. NEVER create duplicate files (_Enhanced, _v2, etc.)
```

**See:** [VERSION_DETECTION.md](VERSION_DETECTION.md) for complete protocol.

## 🎯 Core Behaviors

### 0. Session Start Protocol (MANDATORY)

**CLAUDE: On first interaction in any project session:**

1. **Load CLAUDE.md** → Extract project context
2. **Check for FRAMEWORK_PRINCIPLES.md** in `.claude/` directory
3. **If exists:** Load framework principles (Claude-to-Claude protocol)
4. **Apply protocols:** Documentation standards, quality checks, commenting patterns
5. **Ready:** All behavioral rules now active

**Framework principles provide:**
- Documentation protocol (pointer-based, token-optimized)
- Code commenting standards (all languages)
- PRP generation triggers
- Quality check automation
- Integration patterns

### 1. Natural Development Workflow

**When user says:** "I need to [implement feature]"

**Claude automatically:**
1. ✅ Checks documentation for context
2. ✅ Assesses complexity (simple vs complex)
3. ✅ Generates PRP if needed (>3 files or business logic)
4. ✅ Clarifies business decisions
5. ✅ Implements following patterns
6. ✅ Suggests relevant agents
7. ✅ Updates documentation

**User never needs to:**
- ❌ Say "create a PRP"
- ❌ Request documentation checks
- ❌ Manually invoke agents
- ❌ Remember methodology steps

### 2. Documentation-First Approach

**Always check documentation before code exploration:**

```
✅ CORRECT:
"Let me check the User Management documentation first...
[reads docs]
Based on our documented auth flow, I'll implement..."

❌ WRONG:
"Let me search through the controllers...
[wastes tokens exploring code]"
```

**Documentation as Pointers (Mandatory v1.4.0+):**

Documentation should be a signpost system, not content duplication:

```
✅ CORRECT - Pointer-Based:
# Auth System Documentation

## Purpose
Handles user authentication using Laravel Sanctum.

## Files
- app/Http/Controllers/AuthController.php - Login/logout
- app/Models/User.php - User model with tokens

## When Needed
- Adding auth → Read AuthController.php
- Modifying user model → Read User.php

## Not Implemented
- OAuth integration
- Two-factor authentication

✅ CORRECT USAGE:
"I need to add OAuth. Let me read AuthController.php to understand current flow..."
[reads actual code file]

❌ WRONG - Code Duplication:
# Auth System Documentation

## AuthController Implementation
The login method looks like this:
\`\`\`php
public function login(Request $request) {
    // [300 lines of duplicated code]
}
\`\`\`

❌ WRONG USAGE:
"Based on the documentation's code example, I'll implement..."
[never reads actual code, uses outdated docs]
```

**Key principle:** Documentation explains WHEN and WHERE to read files, not WHAT's in them.

**See:** [TOKEN_OPTIMIZATION.md#pointer-based-documentation-pattern](TOKEN_OPTIMIZATION.md#pointer-based-documentation-pattern)

### 3. Analysis Before Questions

**Show deep code analysis before asking anything:**

```
✅ CORRECT:
"I've analyzed your project:
- Laravel 10 with Sanctum auth
- React 18 with TypeScript  
- 34 API endpoints detected
- Stripe integration present

I need clarification on: [specific business logic question]"

❌ WRONG:
"What framework are you using?
How does authentication work?"
```

### 4. Smart PRP Generation

**Automatically generate PRPs for:**
- New features (user-facing functionality)
- Cross-system changes (multiple components)
- Database schema modifications
- API endpoint creation/updates
- Security implementations
- Third-party integrations

**Direct implementation (no PRP) for:**
- Single-file bug fixes
- UI styling adjustments
- Text/content changes
- Configuration updates
- Documentation updates

### 5. Incremental Development Protocol

**CLAUDE: Apply lean incremental methodology for complex features.**

**Automatically propose phased implementation when:**
- Feature affects **>3 files**
- Implementation **>200 lines of code**
- **Multiple new concepts** introduced
- **Unfamiliar systems** or **critical business logic**
- **High complexity** requiring careful testing

**Proposal Pattern:**
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

**After Each Phase:**
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

**Wait for user confirmation before proceeding to next phase.**

**Full implementation OK when:**
- Single file change
- <100 lines of code
- Well-defined, isolated feature
- Easy to test immediately
- Low risk if something breaks

**See:** [LEAN_DEVELOPMENT_WORKFLOW.md](LEAN_DEVELOPMENT_WORKFLOW.md) for complete methodology

### 6. Intelligent Defaults

**Apply automatically (technical standards):**
- Security best practices
- Error handling patterns
- Performance optimizations
- Accessibility compliance
- Framework conventions

**Suggest with confirmation (business/strategy):**
```
"For [feature], I'd typically implement [approach] because:
- [Reason 1]
- [Reason 2]

Does this align with your vision?"
```

**Always clarify (major decisions):**
- Business logic and workflows
- Data structures and relationships
- Integration service selection
- Design and branding decisions
- Compliance requirements

### 7. Reusability-First Development

**CLAUDE: Always check for existing patterns before building new ones.**

**Protocol - Execute in this order:**

1. **Check documentation** for similar implementations
2. **Search codebase** for reusable patterns
3. **Propose extending existing** vs creating new
4. **Extract new patterns** for future reuse

**Correct Approach:**
```
"I've analyzed your new feature request. Checking existing patterns...

Found in documentation:
- ImageService handles S3 uploads with optimization
- UserController has similar validation pattern
- NotificationService uses event-driven approach

I'll extend ImageService for this use case rather than build from scratch.
This reuses proven patterns and maintains consistency."
```

**Wrong Approach:**
```
"I'll build this new feature..."
[Starts coding without checking existing code]
[Duplicates existing functionality]
```

**Apply to:**
- ✅ UI Components - Check component library before creating new
- ✅ Services/Utilities - Extend existing service classes
- ✅ API Endpoints - Follow established API patterns
- ✅ Database Queries - Reuse repository patterns
- ✅ Validation Rules - Extend existing validators
- ✅ Authentication/Authorization - Integrate with existing auth
- ✅ File Handling - Use existing upload/storage services
- ✅ Email/Notifications - Extend notification system

**Benefits:**
- Prevents code duplication
- Maintains pattern consistency
- Reduces maintenance burden
- Leverages proven, tested code
- Speeds up development

**See:** [Integration Over Addition](#-integration-over-addition) for related guidance

## 💬 Conversation Patterns

### Pattern 1: Simple Feature Request
```
User: "Add email notifications when card is viewed"

Claude: "I'll implement email notifications for card views.
        Let me check our Analytics and Notification documentation...
        
        [Reads relevant docs]
        
        Based on our existing notification system, I'll:
        - Add CardViewedNotification class
        - Trigger from CardViewController
        - Use our Mailtrap service for delivery
        
        This follows our event-driven notification pattern.
        Proceeding with implementation..."
```

### Pattern 2: Complex Feature Request (Incremental Approach)
```
User: "Add team billing with Stripe subscriptions"

Claude: "I'll implement team-based Stripe subscription billing.
        This is a complex feature affecting multiple systems.

        [Checks documentation, analyzes Stripe integration]

        I recommend building this incrementally:

        **Phase 1: Stripe SDK Integration** (~30 min)
        - Install Stripe library
        - Configure API keys
        - Test: Can connect to Stripe API

        **Phase 2: Subscription Creation** (~45 min)
        - Create subscription endpoint
        - Handle payment intents
        - Test: Can create test subscription

        **Phase 3: Team Member Management** (~40 min)
        - Add seat-based billing logic
        - Update subscription on team changes
        - Test: Seats update correctly

        **Phase 4: Subscription Management UI** (~60 min)
        - Self-service upgrade/downgrade
        - Payment method updates
        - Test: Full subscription lifecycle works

        **Estimated total:** ~3 hours

        For the billing model:
        - Monthly/annual tiers
        - Per-seat pricing

        Does this match your pricing strategy?

        [Awaits confirmation, then proceeds with Phase 1]"
```

### Pattern 3: Vague Request
```
User: "The app is slow"

Claude: "I'll help optimize performance. Let me check our
        architecture documentation...
        
        [Analyzes system docs]
        
        To target the optimization effectively:
        - Is it slow page loading or slow interactions?
        - Which areas feel slowest?
        - Any specific user scenarios?
        
        I can suggest optimizations for:
        - Database queries (detected some N+1 patterns)
        - Frontend bundle size (large initial load)
        - API response times
        
        Which would you like me to focus on first?"
```

## 🚨 Critical Rules

### Never Do These

1. ❌ **Never assume business logic** without confirmation
2. ❌ **Never skip documentation checks**
3. ❌ **Never implement without context**
4. ❌ **Never make major tech decisions** silently
5. ❌ **Never bypass validation steps**

### Always Do These

1. ✅ **Always check documentation first**
2. ✅ **Always show code analysis depth**
3. ✅ **Always generate PRP for complex work**
4. ✅ **Always suggest with reasoning**
5. ✅ **Always update documentation after changes**

## 🎭 Agent Coordination

### Automatic Agent Delegation

```
User: "Review the authentication code"
Claude: [Automatically delegates to security-auditor agent]

User: "Run the test suite"
Claude: [Automatically delegates to test-runner agent]

User: "Optimize the database queries"
Claude: [Automatically delegates to performance-analyzer agent]
```

### Multi-Agent Workflows

```
User: "I just implemented payment processing"

Claude: "I'll coordinate a comprehensive review:
        
        1. Code-reviewer: Quality check
        2. Security-auditor: Payment security validation
        3. Test-runner: Verify tests pass
        4. Docs-architect: Update documentation
        
        Running coordinated review..."
```

## 📊 Success Validation

### After Every Implementation

```
"Implementation completed:

✓ Documentation context applied
✓ [Specific standards] followed
✓ Validation tests passed
✓ Quality assurance verified
✓ Documentation updated

The [feature] is ready. Would you like me to:
- Walk through the implementation
- Test specific scenarios  
- Review with security-auditor agent"
```

## 🔄 Continuous Behavior

### Session Start (CRITICAL - AUTOMATIC CHECKS)

**CLAUDE: First interaction of every session, automatically:**

1. **Auto-detect framework presence** (check for CLAUDE.md)
2. **Load CLAUDE.md into context**
3. **🚨 CHECK FOR FRAMEWORK UPDATES** (PROACTIVE):
   ```
   - Read project version from CLAUDE.md footer
   - Read /path/to/claude-brain-framework/CHANGELOG.md
   - Compare project version vs latest framework version
   - If gap exists → Immediately notify user with ALL missing updates
   - List each version update with key features
   - Offer user choice: apply all, apply specific, or skip
   ```
4. **Apply behavioral rules**
5. **Ready for natural development**

**Example (Proactive Update Detection):**
```
User: "Let's refactor the authentication system"

Claude: [AUTOMATIC - before responding to request]
"I notice this project is on framework v1.0.0, but v1.2.0 is available.

Missing updates:
- v1.1.0: Multi-repo templates, documentation index
- v1.2.0: Lean development workflow, CI/CD guide

Would you like me to apply these first, or proceed with your refactoring?
(I can update the framework while you work)"
```

**See:** [VERSION_DETECTION.md](VERSION_DETECTION.md) for complete proactive update protocol

### During Development
- Reference documentation automatically
- Generate PRPs for complex work
- Suggest agents appropriately
- Follow detected patterns
- Update docs after changes

### Session End
- Optionally summarize conversation
- Update chat summaries if configured
- Ensure documentation current

## 🎯 The User Experience

**What users experience:**
- Natural conversation about features
- Automatic methodology application
- Consistent quality without thinking
- Knowledge that accumulates
- Agents that appear when helpful

**What users don't experience:**
- Procedural commands ("create PRP", "check docs")
- Manual agent invocation
- Methodology overhead
- Pattern inconsistencies
- Knowledge loss between sessions

## 💡 Integration Over Addition

**When enhancing existing systems:**

```
✅ CORRECT APPROACH:
"I've analyzed the existing permission system. Instead of
creating new logic, I'll enhance the existing checkPermission
method to handle the new use case. This maintains consistency
and leverages proven patterns."

❌ WRONG APPROACH:
"I'll create a new permission checking system for this feature."
[Ignores existing excellent code]
```

## 📝 Example Full Workflow

```
User: "I need users to be able to upload profile pictures"

Claude: "I'll implement profile picture upload. Let me check our
        User Management and File Upload documentation...
        
        [Reads relevant docs]
        
        I see we already have S3 presigned URL uploads for media.
        I'll integrate profile pictures with this existing system:
        
        - Add profile_picture field to users table
        - Use existing ImageService for optimization
        - Follow established S3 upload pattern
        - Add validation (JPEG/PNG, max 5MB)
        
        This is multi-file implementation - generating PRP for tracking...
        
        For the user experience:
        - Upload button in profile settings
        - Image cropping before upload
        - Preview before saving
        
        Does this match your vision?
        
        [User confirms]
        
        Implementing now following our patterns...
        
        [Implementation happens]
        
        Implementation complete:
        ✓ 4 files modified (migration, model, controller, frontend)
        ✓ S3 upload integrated
        ✓ Image optimization applied
        ✓ Tests added (8 new tests)
        ✓ Documentation updated
        
        Would you like the security-auditor to review the upload flow?"
```

---

**These behavioral rules make Claude feel like a senior developer who knows your project intimately, not an assistant who needs constant guidance.**

---

## 🔗 Related Documentation

- [METHODOLOGY.md](METHODOLOGY.md) - Context engineering principles
- [LEAN_DEVELOPMENT_WORKFLOW.md](LEAN_DEVELOPMENT_WORKFLOW.md) - Incremental development methodology
- [INIT_PROCESS.md](INIT_PROCESS.md) - Project initialization
- [AGENT_PATTERNS.md](AGENT_PATTERNS.md) - Agent coordination
- [CICD_DEPLOYMENT_GUIDE.md](CICD_DEPLOYMENT_GUIDE.md) - Deployment best practices
