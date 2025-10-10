# Quick Start Guide

**Get up and running with Claude Brain Framework in 10 minutes**

## Prerequisites

- Claude Code installed and running
- A project you want to enhance with context engineering

## Scenario A: "I Read the Instructions!"

### Step 1: Clone the Framework
```bash
git clone https://github.com/Marcosmenm/claude-brain-framework
cd claude-brain-framework
```

### Step 2: Open Claude Code
Open Claude Code in the `claude-brain-framework` directory.

### Step 3: Initiate Framework Application
Say to Claude:
```
Help me apply this context engineering framework to my project at /path/to/your/project
```

### Step 4: Multi-Cycle Interview

Claude analyzes your code first, then asks targeted questions:

**Cycle 1: Tech Stack Validation**
Claude detects your stack from package files and dependencies, then confirms findings.

**Cycle 2: Architecture Understanding**  
Claude analyzes your code structure, identifies patterns (API architecture, service layers, etc.), and asks clarifying questions only when needed.

**Cycle 3: Business Domain**
Claude examines models, controllers, and services to understand your business logic. Questions focus on business rules that can't be inferred from code.

**Cycle 4: Integration & Optimization**
Claude identifies MCP integration opportunities and areas for improvement.

**Cycle 5: Agent Recommendations**
Based on your tech stack, Claude suggests relevant specialized agents.

**Cycle 6: Documentation Planning**
Claude presents a list of documentation files to generate based on your codebase.

**Cycle 7: Documentation Generation**
Claude creates actual documentation files populated with analysis findings.

**Cycle 8: Completion**
Claude generates your complete context engineering structure.

### Step 5: Start Developing

Just work naturally! Say what you need:
```
I need to add email notifications when X happens
```

Claude automatically:
- Checks documentation
- Generates PRP for complex features
- Follows your patterns
- Updates documentation

---

## Scenario B: "What Am I Supposed to Do With This?"

### Ultra-Simple Path

1. **Download this framework:**
   ```bash
   git clone https://github.com/Marcosmenm/claude-brain-framework
   cd claude-brain-framework
   ```

2. **Open Claude Code in this folder**

3. **Say to Claude:**
   ```
   I want to use this framework for my project at: [YOUR PROJECT PATH]
   Please help me set it up.
   ```

4. **Answer Claude's questions naturally**

5. **Done!** Claude set everything up.

---

## What Just Happened?

Your project now has:

- **CLAUDE.md** - Project brain (auto-generated from your code)
- **.claude/documentation/** - System docs populated with actual analysis
- **.claude/prps/** - Feature tracking (active/completed)
- **.claude/agents/** - Specialized Claude instances (optional)
- **.claude/chat-summaries/** - Conversation tracking (optional)

---

## Next Steps

**Verify it's working:**
```
Show me what you know about my project architecture
```

**Try developing naturally:**
```
I need to implement user profile image uploads
```

Notice Claude follows your patterns automatically - no manual PRP creation needed!

---

## Common Questions

**"How do I know it's working?"**
Ask Claude about your project. If it references specific files and patterns without you explaining, it's working!

**"Can I customize?"**
Yes! Edit the markdown files to fit your needs.

**"How do I update when framework improves?"**
```
Check for claude-brain-framework updates
```

**"Multiple projects?"**
Apply to each project. Claude can track all of them.

---

## Troubleshooting

**"Claude isn't reading my CLAUDE.md"**
Make sure Claude Code is running from your project directory.

**"Interview too long"**
Say "Use defaults for the rest" and Claude will fill in sensible values.

**"Want to restart"**
Delete generated files and reinitialize.

---

**Ready! Start building with full context engineering.**

[README](README.md) | [Examples](examples/) | [Methodology](core/METHODOLOGY.md)
