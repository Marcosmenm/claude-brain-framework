# 🧠 Claude Brain Framework

**The self-installing, self-updating AI development methodology for Claude Code**

> Stop repeating context. Start shipping faster.

## What Is This?

Claude Brain Framework is a **context engineering system** that transforms Claude Code from a helpful assistant into a project-aware development partner. Unlike static documentation or simple prompts, this framework:

- **Self-installs** through intelligent conversation (no scripts to run)
- **Self-configures** via multi-cycle project interviews
- **Self-updates** when the framework evolves
- **Self-adapts** to your existing project structure

Think of it as **programming Claude's behavior** rather than just writing documentation.

## Why Does This Matter?

### The Problem

Without structured context:
- ❌ Repeat the same explanations every conversation
- ❌ Waste 500+ tokens searching for basic information
- ❌ Inconsistent code patterns across features
- ❌ Knowledge lost between sessions
- ❌ New features start from zero context

### The Solution

With Claude Brain Framework:
- ✅ **90% token reduction** for context gathering
- ✅ **10x faster** feature development start
- ✅ **100% pattern consistency** through methodology enforcement
- ✅ **Permanent knowledge** capture across sessions
- ✅ **Complete audit trail** of decisions and changes

## Quick Start

### 1. Clone This Repository
```bash
git clone https://github.com/Marcosmenm/claude-brain-framework
cd claude-brain-framework
```

### 2. Open Claude Code
Open Claude Code in this directory so Claude can read the framework files.

### 3. Apply to Your Project
Say to Claude:
```
"Help me apply this context engineering framework to my project at /path/to/your/project"
```

### 4. Answer the Interview
Claude will ask questions about:
- Your tech stack and architecture
- Business domain and workflows
- Missing components it detected
- Agent recommendations for your project

### 5. Start Developing
Claude now has deep context about your project and will:
- Follow your patterns automatically
- Suggest appropriate agents for tasks
- Generate PRPs for complex features
- Maintain documentation consistency

**That's it! No config files to write, no tools to install.**

## What Gets Created

After initialization, your project will have:

```
your-project/
├── CLAUDE.md (Project brain - what Claude knows)
├── /Documentation/
│   └── [System documentation generated from your code]
├── /PRPs/
│   ├── /active/ (Features in development)
│   └── /completed/ (Implementation history)
└── /.claude/
    ├── /agents/ (Recommended agents for your stack)
    └── /chat-summaries/ (Optional: conversation summaries)
```

## Core Concepts

### 1. Context Engineering
Not just "prompt engineering" - systematic management of what Claude knows, when it knows it, and how it uses that knowledge.

**Learn more:** [core/METHODOLOGY.md](core/METHODOLOGY.md)

### 2. Multi-Cycle Initialization
Instead of filling out forms, Claude interviews you intelligently, analyzing your code and asking targeted questions to build complete context.

**Learn more:** [core/INIT_PROCESS.md](core/INIT_PROCESS.md)

### 3. Agent Integration
Specialized Claude instances for code review, testing, documentation, and more - automatically suggested based on your tech stack.

**Learn more:** [core/AGENT_PATTERNS.md](core/AGENT_PATTERNS.md)

### 4. PRP Methodology
Product Requirements Prompts create structured blueprints for features, tracking changes and decisions throughout development.

**Learn more:** [templates/PRP_TEMPLATE.md](templates/PRP_TEMPLATE.md)

### 5. Update Propagation
When the framework improves, Claude can update your projects while preserving customizations.

**Learn more:** [core/UPDATE_PROCESS.md](core/UPDATE_PROCESS.md)

## Real-World Results

### Multi-Tenant SaaS Platform (Laravel + React)
**Problem:** 150+ files, 3 components, constant context loss
**Solution:** Applied Claude Brain Framework
**Results:**
- 90% reduction in context-gathering tokens
- 10x faster onboarding for new features
- Zero context drift across 6-month development
- Complete knowledge retention across sessions

*More examples: [examples/](examples/)*

## Framework Components

### Core Methodology
- [METHODOLOGY.md](core/METHODOLOGY.md) - Context engineering principles
- [BEHAVIORAL_RULES.md](core/BEHAVIORAL_RULES.md) - How Claude should behave
- [INIT_PROCESS.md](core/INIT_PROCESS.md) - Multi-cycle project initialization
- [UPDATE_PROCESS.md](core/UPDATE_PROCESS.md) - Framework evolution management
- [AGENT_PATTERNS.md](core/AGENT_PATTERNS.md) - Agent recommendations and usage

### Templates
- [CLAUDE_MD_UNIVERSAL.md](templates/CLAUDE_MD_UNIVERSAL.md) - Universal single-project template
- [CLAUDE_MD_MULTI_REPO_SYSTEM.md](templates/CLAUDE_MD_MULTI_REPO_SYSTEM.md) - Multi-repository systems (Backend + Web + Mobile)
- [DOCUMENTATION_INDEX_TEMPLATE.md](templates/DOCUMENTATION_INDEX_TEMPLATE.md) - Documentation catalog and navigation
- [PRP_TEMPLATE.md](templates/PRP_TEMPLATE.md) - Feature implementation blueprints
- [DOCUMENTATION_TEMPLATE.md](templates/DOCUMENTATION_TEMPLATE.md) - System documentation
- [CHAT_SUMMARY_TEMPLATE.md](templates/CHAT_SUMMARY_TEMPLATE.md) - Conversation summaries

### Examples
- [anonymous-saas-platform/](examples/anonymous-saas-platform/) - Single-project SaaS example
- [multi-repo-ecommerce/](examples/multi-repo-ecommerce/) - Multi-repository system example (NEW in v1.1.0)

## Philosophy

> **"Context is a finite resource. Every token counts."**
> — Anthropic Engineering

This framework treats context engineering as a first-class engineering discipline:
- **Just-in-time loading** - Only read what's needed, when needed
- **Modular organization** - Import files instead of monolithic dumps
- **Living documentation** - Evolves with your project
- **Behavioral programming** - Program how Claude thinks, not just what it knows

## Community & Updates

### Stay Updated
- **Watch this repo** for release notifications
- **Star** to bookmark and show support
- **Read [CHANGELOG.md](CHANGELOG.md)** for detailed changes

### Contributing
Contributions welcome! See [CREDITS.md](CREDITS.md) for acknowledgments and inspiration sources.

## License

MIT License - see [LICENSE](LICENSE) for details.

---

**Ready to transform how you work with Claude Code?**

[Get Started →](QUICK_START.md) | [See Examples →](examples/) | [Read Methodology →](core/METHODOLOGY.md)
