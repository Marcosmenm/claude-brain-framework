# Anonymous SaaS Platform Example

**This is a structural example showing how Claude Brain Framework is applied to a project.**

**Note:** This is NOT a complete application. It demonstrates the methodology structure.

## What This Example Shows

### 1. CLAUDE.md Configuration
See [CLAUDE.md](CLAUDE.md) - Shows how a real project configures context engineering

**Demonstrates:**
- Tech stack documentation
- Development commands
- Architecture overview
- Business domain knowledge
- Agent recommendations
- File organization with `@imports`

### 2. System Documentation
See [Documentation/](Documentation/) - Shows how systems are documented

**Demonstrates:**
- Core system documentation structure
- User workflows and business logic
- Technical architecture details
- Integration points

### 3. Feature Blueprints
See [PRPs/](PRPs/) - Shows PRP structure and usage

**Demonstrates:**
- Active PRP for in-development feature
- Completed PRP with implementation notes
- Change tracking and decision documentation

### 4. Agent Configuration
See [.claude/agents/](. claude/agents/) - Shows agent setup

**Demonstrates:**
- Agent definitions with YAML frontmatter
- Tool permissions
- Specialized agent purposes

## Project Context (Fictional)

**Type:** Multi-tenant SaaS platform
**Domain:** Team productivity and workflow automation
**Stack:** Node.js + React + PostgreSQL
**Scale:** Startup MVP → growing user base

This fictional platform helps teams:
- Manage projects and tasks
- Automate repetitive workflows
- Track team performance
- Integrate with external tools

## How to Use This Example

### 1. Study the Structure
```bash
# Examine how files are organized
tree .

# Read CLAUDE.md to see configuration
cat CLAUDE.md

# Review documentation structure
ls Documentation/
```

### 2. Understand the Patterns
- How `@imports` reduce file size
- How agents are configured for specific tasks
- How PRPs track complex features
- How documentation evolves with code

### 3. Apply to Your Project
```
1. Copy relevant structure to your project
2. Customize CLAUDE.md for your tech stack
3. Create your system documentation
4. Configure appropriate agents
5. Start using PRPs for features
```

## Key Takeaways

**Context Engineering isn't about:**
- ❌ Building a complex documentation site
- ❌ Writing encyclopedic guides
- ❌ Creating rigid processes

**It IS about:**
- ✅ Systematic context management
- ✅ Living documentation that evolves
- ✅ Automatic methodology application
- ✅ Knowledge that accumulates

## Real-World Adaptation

To adapt this to your project:

1. **Replace tech stack** in CLAUDE.md
2. **Document YOUR systems** (not these fictional ones)
3. **Configure agents** for YOUR workflow
4. **Start small** - add PRPs as you work
5. **Let it evolve** - documentation grows with development

---

**This example is intentionally minimal to show structure, not overwhelm with content.**

**For full framework documentation, see the main repository.**
