# Agent Patterns & Integration Guide

**Specialized Claude instances for focused tasks**

## 🤖 What Are Agents?

Agents are specialized Claude instances with:
- **Focused expertise** in specific domains
- **Separate context windows** (no pollution of main conversation)
- **Custom tool permissions** (security through least privilege)
- **Automatic invocation** (Claude delegates appropriately)

**★ Insight ─────────────────────────────────────**
Think of agents like microservices for AI - each does one thing well,
operates independently, and can be composed for complex workflows.
─────────────────────────────────────────────────

## 📚 Agent Catalog

### Development Agents

#### **code-reviewer**
**Purpose:** Quality assurance and pattern enforcement
**When to use:** After implementing features, before commits
**Tools:** Read, Grep, Glob, Bash (git diff)
**Focuses on:**
- Code simplicity and readability
- No code duplication
- Proper error handling
- No exposed secrets
- Test coverage
- Performance patterns

**Community source:** [wshobson/agents](https://github.com/wshobson/agents)

#### **test-runner**
**Purpose:** Automated testing and failure diagnosis
**When to use:** During development, before commits
**Tools:** Bash, Read, Grep
**Focuses on:**
- Running test suites
- Analyzing test failures
- Suggesting fixes
- Coverage analysis

**Community source:** [VoltAgent/awesome-claude-code-subagents](https://github.com/VoltAgent/awesome-claude-code-subagents)

#### **debugger**
**Purpose:** Error diagnosis and root cause analysis  
**When to use:** When encountering errors or unexpected behavior
**Tools:** Bash, Read, Grep, Glob
**Focuses on:**
- Stack trace analysis
- Log investigation
- Root cause identification
- Fix suggestions

---

### Language-Specific Agents

#### **laravel-api-tester**
**Purpose:** Laravel API endpoint validation
**When to use:** Laravel projects with REST APIs
**Tools:** Bash (artisan, phpunit), Read, Grep
**Focuses on:**
- API route validation
- Request/response testing
- Sanctum auth flows
- Middleware verification

#### **react-component-reviewer**
**Purpose:** React/TypeScript best practices
**When to use:** React projects
**Tools:** Read, Grep, Glob, Bash (npm scripts)
**Focuses on:**
- Component patterns
- Hook usage validation
- TypeScript strict mode
- Performance optimization

#### **python-pro**
**Purpose:** Python code quality and standards
**When to use:** Python projects
**Tools:** Bash (pytest, black, mypy), Read, Grep
**Focuses on:**
- PEP 8 compliance
- Type hint validation
- Test coverage
- Package structure

---

### Quality Assurance Agents

#### **security-auditor**
**Purpose:** Security vulnerability detection
**When to use:** Before deployments, after auth changes
**Tools:** Read, Grep, Glob, Bash
**Focuses on:**
- Exposed secrets/API keys
- Input validation
- Authentication flows
- Authorization checks
- SQL injection risks
- XSS vulnerabilities
- CORS configuration

**Community source:** [hesreallyhim/awesome-claude-code-agents](https://github.com/hesreallyhim/awesome-claude-code-agents)

#### **performance-analyzer**
**Purpose:** Performance bottleneck detection
**When to use:** When experiencing slowness, before production
**Tools:** Bash (profilers), Read, Grep
**Focuses on:**
- N+1 query detection
- Slow endpoints
- Memory leaks
- Bundle size analysis
- Database indexing

---

### Documentation Agents

#### **docs-architect**
**Purpose:** Technical documentation generation
**When to use:** After implementing new systems
**Tools:** Read, Grep, Glob, Write
**Focuses on:**
- System architecture docs
- API documentation
- Component documentation
- Integration guides

#### **api-documenter**
**Purpose:** OpenAPI/Swagger spec generation
**When to use:** API projects
**Tools:** Read, Grep, Write
**Focuses on:**
- OpenAPI 3.0 specs
- Request/response schemas
- Authentication documentation
- Example requests

---

### Infrastructure Agents

#### **devops-engineer**
**Purpose:** CI/CD and deployment automation
**When to use:** Setting up pipelines, deployment issues
**Tools:** Bash, Read, Write
**Focuses on:**
- Docker configuration
- CI/CD pipelines
- Environment setup
- Deployment scripts

#### **database-architect**
**Purpose:** Database design and optimization
**When to use:** Schema changes, performance issues
**Tools:** Bash (database CLIs), Read, Grep
**Focuses on:**
- Migration review
- Index optimization
- Query performance
- Relationship design

---

## 🎯 Tech Stack Agent Recommendations

### Laravel + React
**Essential:**
- `laravel-api-tester` - Validates API endpoints
- `react-component-reviewer` - Ensures React best practices
- `security-auditor` - Reviews auth and payment flows

**Recommended:**
- `test-runner` - Runs PHPUnit + Jest tests
- `performance-analyzer` - Detects N+1 queries, bundle bloat

### Django + Vue
**Essential:**
- `python-pro` - Python code quality
- `security-auditor` - Django security best practices
- `test-runner` - Pytest + Vue test execution

**Recommended:**
- `api-documenter` - DRF schema generation
- `performance-analyzer` - Query optimization

### Node.js + Next.js
**Essential:**
- `test-runner` - Jest/Vitest execution
- `react-component-reviewer` - Next.js patterns
- `security-auditor` - API route security

**Recommended:**
- `performance-analyzer` - SSR/ISR optimization
- `api-documenter` - API route documentation

### Python Data Science
**Essential:**
- `python-pro` - Code quality
- `test-runner` - Pytest execution

**Recommended:**
- `docs-architect` - Notebook documentation
- `performance-analyzer` - Data pipeline optimization

---

## 🔧 Agent Configuration

### Agent File Structure

Agents are markdown files with YAML frontmatter:

```markdown
---
name: code-reviewer
description: Senior code reviewer ensuring high standards
tools: Read, Grep, Glob, Bash
model: sonnet  # or opus, haiku
---

You are a senior code reviewer with expertise in [language/framework].

Your responsibilities:
- Review code for quality and maintainability
- Check for security vulnerabilities
- Ensure best practices are followed
- Suggest improvements with clear reasoning

When reviewing:
1. Run `git diff` to see recent changes
2. Focus on modified files first
3. Check against project CLAUDE.md standards
4. Provide actionable feedback

Checklist:
- [ ] Code is simple and readable
- [ ] No code duplication
- [ ] Error handling present
- [ ] No exposed secrets
- [ ] Tests cover changes
- [ ] Performance considered
```

### Creating Custom Agents

1. **Use `/agents` command** in Claude Code
2. **Specify purpose and expertise**
3. **Define tool permissions** (least privilege)
4. **Write detailed system prompt**
5. **Test with sample tasks**

Example creation:
```
Claude, I need a custom agent for:
- Reviewing Stripe payment integrations
- Checking webhook signature validation
- Ensuring idempotency
- Verifying error handling

Create a "stripe-integration-specialist" agent.
```

---

## 🚀 Using Agents Effectively

### Automatic Invocation

Claude delegates automatically:
```
User: "Review the authentication code"
Claude: [Automatically uses security-auditor agent]

User: "Run the test suite"
Claude: [Automatically uses test-runner agent]
```

### Manual Invocation

Explicit agent usage:
```
"Use the code-reviewer agent to analyze the payment service"
"Have the security-auditor check the new API endpoints"
"Ask the performance-analyzer to review database queries"
```

### Multi-Agent Workflows

Coordinate multiple agents:
```
User: "I just implemented user profile editing"

Claude: "I'll coordinate a full review:
        
        1. Using code-reviewer for code quality
        2. Using test-runner to verify tests pass
        3. Using security-auditor for auth/validation
        4. Using docs-architect to update documentation
        
        Running agents in sequence..."
```

---

## 📊 Agent Best Practices

### 1. One Purpose Per Agent
**DO:** Create focused agents (e.g., "stripe-specialist")
**DON'T:** Create generic "do-everything" agents

### 2. Limit Tool Access
**DO:** Give minimum tools needed (security)
**DON'T:** Grant all tools by default

### 3. Clear System Prompts
**DO:** Write detailed, specific instructions
**DON'T:** Use vague or generic prompts

### 4. Project-Specific Configuration
**DO:** Customize agents for your tech stack
**DON'T:** Use generic agents without adaptation

### 5. Version Control
**DO:** Commit agent files to your repo (`.claude/agents/`)
**DON'T:** Keep agents only in global config

---

## 🌐 Community Agent Resources

### Major Collections

**VoltAgent/awesome-claude-code-subagents**
- 100+ production-ready agents
- Organized by category
- YAML frontmatter format
- https://github.com/VoltAgent/awesome-claude-code-subagents

**wshobson/agents**
- Curated quality-focused collection
- Multi-agent workflow examples
- Real-world production usage
- https://github.com/wshobson/agents

**hesreallyhim/awesome-claude-code-agents**
- Community-contributed agents
- Diverse use cases
- Active development
- https://github.com/hesreallyhim/awesome-claude-code-agents

### How to Use Community Agents

1. **Browse catalogs** for relevant agents
2. **Copy agent file** to your project (`.claude/agents/`)
3. **Customize system prompt** for your stack
4. **Test with sample tasks**
5. **Refine based on results**

---

## 🔍 When to Create Custom Agents

### Good Candidates
- Domain-specific expertise (e.g., healthcare compliance)
- Repetitive specialized tasks (e.g., changelog generation)
- Company-specific patterns (e.g., internal API style)
- Integration specialists (e.g., specific SaaS platform)

### Not Worth Creating
- One-time tasks
- Simple operations
- Generic programming help
- Anything main Claude handles well

---

## 💡 Agent Invocation During Init

During project initialization, Claude will:

1. **Detect tech stack** from dependencies
2. **Match to agent catalog** 
3. **Recommend essential agents** for your stack
4. **Suggest optional agents** based on detected patterns
5. **Configure agents** if approved
6. **Document usage** in project CLAUDE.md

Example:
```
"Based on your Laravel + React + Stripe stack:

Essential Agents (Recommended):
✅ laravel-api-tester - For your 34 API endpoints
✅ react-component-reviewer - TypeScript strict mode enforcement  
✅ security-auditor - Stripe webhook validation

Optional Agents:
- test-runner (you have PHPUnit + Jest)
- performance-analyzer (detected some N+1 queries)
- stripe-integration-specialist (custom for payment flows)

Install recommended agents? (You can add more anytime)"
```

---

## 🎯 Success Metrics

Agents are working well when:
- **Automatic delegation** happens without user thinking about it
- **Consistent quality** in specialized areas
- **Faster workflows** for repetitive tasks
- **Better coverage** of quality checks

---

**Agents transform Claude from a single assistant into a coordinated team of specialists, each expert in their domain.**

For more examples and community contributions:
- [Anthropic Subagent Docs](https://docs.claude.com/en/docs/claude-code/sub-agents)
- [Community Agent Collections](https://github.com/topics/claude-code-agents)
