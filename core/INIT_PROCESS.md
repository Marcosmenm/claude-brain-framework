# Project Initialization Process

**CLAUDE: This file contains instructions for initializing context engineering in new projects.**

## 🎯 When to Use This Process

When a user says:
- "Help me apply this framework to my project at [path]"
- "Initialize context engineering for my project"
- "Set up Claude Brain Framework for [project]"

## 🚀 Multi-Cycle Initialization Interview

### Overview

This is an **intelligent interview process**, not a questionnaire. You analyze code FIRST, then ask targeted questions only about what you cannot infer.

**Key Principle:** Show your analysis depth. Users should see you've done homework before asking questions.

---

## Cycle 1: Tech Stack Detection & Validation

### What to Do
1. **Scan package files** (package.json, composer.json, requirements.txt, go.mod, etc.)
2. **Analyze dependencies** and versions
3. **Detect frameworks** and major libraries
4. **Identify testing tools** present
5. **Find configuration files** (webpack, vite, docker, etc.)

### Present Findings
```
"I've analyzed your project structure and dependencies:

Detected Configuration:
✅ [Backend framework + version]
  - [Key packages with versions]
  - [Authentication/authorization tools]
  - [Testing framework]

✅ [Frontend framework + version]
  - [Build tools]
  - [UI libraries]
  - [State management]

✅ [Database type]
  - [ORM/query builder]
  - [Migration count detected]

✅ [Third-Party Integrations]
  - [Payment, email, storage, etc.]

Is this accurate? Anything I'm missing?"
```

### Only Ask If
- Multiple valid options detected (e.g., both MySQL and PostgreSQL configs)
- Unusual patterns found that need clarification
- Critical tools not detected but might exist

---

## Cycle 2: Architecture Analysis

### What to Do
1. **Analyze route files** (api.php, routes.js, urls.py, etc.)
2. **Examine directory structure** for patterns (MVC, service layer, repository pattern)
3. **Identify middleware** and request pipeline
4. **Detect API style** (REST, GraphQL, gRPC)
5. **Find deployment configs** (Docker, CI/CD)

### Present Analysis
```
"Based on code analysis, I've identified your architecture:

API Communication:
✅ [API style] with [X] endpoints detected
✅ [Authentication method] via [middleware/guards]
✅ [CORS/security configuration]

Application Structure:
✅ [Architectural pattern] (monolith/microservices/serverless)
✅ [Code organization pattern] (service layer, repository, etc.)
✅ [Number] service classes in [path]

Detected Workflows:
1. [Major workflow 1 with files involved]
2. [Major workflow 2 with files involved]

[Specific question about something ambiguous if needed]"
```

### Only Ask If
- Business logic that can't be inferred from code structure
- Multiple patterns detected (inconsistent architecture)
- Security considerations that need confirmation

---

## Cycle 3: Business Domain Deep Dive

### What to Do
1. **Analyze models/entities** for core business concepts
2. **Examine controllers/handlers** for workflows
3. **Study services** for business logic
4. **Review database migrations** for relationships
5. **Check validation rules** for business constraints

### Present Domain Understanding
```
"I've analyzed your models, controllers, and services:

Core Business Entities:
✅ [Entity 1] - [purpose inferred from code]
✅ [Entity 2] - [relationships detected]
✅ [Entity 3] - [key fields and constraints]

Business Workflows Detected:
- [Workflow 1]: [Steps inferred from controllers]
- [Workflow 2]: [Process flow from services]

Business Logic Insights:
- [Key pattern 1 detected]
- [Important constraint found]

Questions I need clarification on:
1. [Specific business rule that's ambiguous]
2. [Workflow trigger/completion that's unclear]
3. [Data ownership/lifecycle question]"
```

### Always Ask About
- Business rules not inferable from code (approval workflows, pricing logic)
- User roles and permissions (beyond what's in database)
- Data lifecycle (what happens when X is deleted/archived)
- Integration business logic (payment flows, email triggers)

---

## Cycle 4: Component & Integration Analysis

### What to Do
1. **Detect MCP integration opportunities** (Stripe, GitHub, AWS, databases)
2. **Identify missing components** (tests, docs, CI/CD)
3. **Find optimization opportunities** (N+1 queries, missing indexes)
4. **Check security patterns** (input validation, auth flows)

### Present Findings
```
"Component Analysis:

Detected Integrations:
🔌 [Service 1] - [Package detected] → MCP server available
🔌 [Service 2] - [Config found] → MCP connection possible

Missing/Incomplete:
⚠️ No frontend tests detected
⚠️ [X] API endpoints lack input validation
⚠️ Database missing indexes on [tables]

Should I:
1. Document MCP integration points?
2. Add testing structure to CLAUDE.md?
3. Note optimization opportunities?"
```

---

## Cycle 5: Agent Recommendations

### What to Do
1. **Match tech stack to agent catalog**
2. **Identify workflow-specific agents** (based on detected patterns)
3. **Suggest essential vs optional agents**
4. **Provide agent descriptions** relevant to THIS project

### Present Recommendations
```
"Based on your [stack description], I recommend:

Essential Agents:
✅ [Agent 1] - [Why essential for this project]
✅ [Agent 2] - [Specific use case in your codebase]

Recommended Agents:
- [Agent 3] - [Nice to have because...]
- [Agent 4] - [Useful for...]

Install recommended agents?"
```

### Agent Selection Criteria
- **Essential**: Directly addresses detected patterns/issues
- **Recommended**: Supports common workflows in this stack
- **Optional**: General purpose, user can add later

---

## Cycle 6: Documentation Planning

### What to Do
1. **List core systems detected** from entity/model analysis
2. **Identify architectural components** that need documentation
3. **Present documentation plan** to user for confirmation
4. **Get user approval** before generating files

### Present Documentation Plan
```
"Based on my analysis, I'll create documentation for:

Core Systems (Business Domain):
📄 [System_1].md - [Brief description of what it covers]
📄 [System_2].md - [Brief description]
📄 [System_3].md - [Brief description]

Architecture:
📄 [Backend_Architecture].md - [Tech stack and patterns]
📄 [Infrastructure].md - [Deployment and services] (if applicable)

This documentation will capture:
- What I've learned from code analysis
- Business rules and workflows discovered
- API endpoints and data models
- Integration points

Should I proceed with generating these documentation files?"
```

### Only Proceed When
- User explicitly approves the documentation list
- User confirms the systems/components are correctly identified
- User adds/removes any documentation files from the list

---

## Cycle 7: Documentation Generation

### What to Create
1. **Actually generate documentation files** (not just empty folders)
2. **Populate with analysis findings** from previous cycles
3. **Include code references** to specific files analyzed
4. **Add placeholders** for information that needs user input

### For Each Core System Documentation
**Content Structure:**
```markdown
# [System Name] - Documentation

## Overview
[1-2 paragraphs based on model/controller/service analysis]

## User Roles
[Inferred from permissions/guards detected]

## Business Rules
[From validation rules and service logic analysis]

## Data Model
### Entities
- **[Entity]:** [Fields detected from model/migration]

### Relationships
[Detected from model relationships]

## API Endpoints
[From route analysis - actual endpoints detected]

## Frontend Integration (if applicable)
[Component paths and usage detected]

## Related Systems
[Dependencies found in code]

## TODO: Requires Clarification
- [Specific business logic that needs user explanation]
- [Workflow triggers that weren't clear from code]
```

### For Architecture Documentation
**Content Structure:**
```markdown
# [Component] Architecture

## Overview
[Based on directory structure and configuration analysis]

## Technology Stack
[Actual versions from package files]

## Design Patterns
[Patterns detected: service layer, repository, etc.]

## Integration Points
[External services detected from configs/environment]

## Configuration
[Environment variables found in .env.example]

## Deployment
[From Docker/CI files if present]

## TODO: Requires Clarification
- [Deployment-specific details not in code]
- [Infrastructure details not visible in repository]
```

### Validation After Generation
```
"Documentation generation complete:

✅ Core Systems (Business Domain):
   - [System_1].md ([X] lines) - [Key sections]
   - [System_2].md ([Y] lines) - [Key sections]

✅ Architecture:
   - [Component].md ([Z] lines) - [Key sections]

Each file contains:
- Analysis findings from your code
- Actual endpoints/models/services detected
- Code references for traceability
- TODO sections for information I couldn't infer

Please review the documentation and let me know if anything needs correction or additional detail."
```

---

## Cycle 8: Final Structure Generation & Validation

### What to Create

#### 1. CLAUDE.md
```markdown
# [Project Name] - Context Engineering

## Tech Stack
[Exact versions detected]

## Architecture
[Patterns analyzed]

## Business Domain
[Entities and workflows discovered]

## Development Commands
[Actual commands that work for this stack]

## File Structure
[Important paths with explanations]

## Validation Procedures
[Stack-specific validation commands]

## Agent Recommendations
[Configured agents with usage guidance]

## MCP Integrations
[Detected integration points with setup instructions]
```

#### 2. Agent Structure (if approved)
```
/.claude/agents/
├── [agent-1].md
├── [agent-2].md
└── README.md (usage guide)
```

#### 3. Documentation Structure
```
/.claude/documentation/
├── Core_Systems/
│   ├── [Major_System_1].md (based on detected entities)
│   ├── [Major_System_2].md
│   └── [Major_System_3].md
├── Architecture/
│   ├── [Backend_Architecture].md (if applicable)
│   └── [Infrastructure].md (if applicable)
└── README.md (overview with file map)
```

#### 4. PRP Structure
```
/.claude/prps/
├── /active/ (empty, ready for use)
├── /completed/ (empty, will fill during development)
└── _TEMPLATE.md (customized for this stack)
```

#### 5. Chat Summaries (if requested)
```
/.claude/chat-summaries/
└── _TEMPLATE.md (summary template)
```

### Present Completion
```
"Context engineering structure created:

✅ CLAUDE.md ([X] lines)
  - [Key sections with brief descriptions]

✅ .claude/documentation/
  - [Number] core system docs generated with actual content
  - [Number] architecture docs with analysis findings

✅ .claude/prps/
  - Template customized for [stack]

✅ .claude/agents/ (if applicable)
  - [Number] agents configured

Ready for development! You can now work naturally:

Just say what you need (e.g., 'Add email notifications when X happens')

I'll automatically:
1. Check documentation for context
2. Generate PRP if complex
3. Follow your patterns
4. Update docs
5. Suggest relevant agents"
```

---

## 🎯 Key Principles for Initialization

### 1. Analysis Before Questions
**DO:** Show comprehensive code analysis before asking anything
**DON'T:** Ask basic questions answerable from package files

### 2. Targeted Questions Only
**DO:** Ask specific questions about ambiguous business logic
**DON'T:** Ask vague questions like "How does authentication work?"

### 3. Intelligent Defaults
**DO:** Suggest sensible defaults based on detected patterns
**DON'T:** Force users to specify every detail

### 4. Respect Existing Patterns
**DO:** Adapt templates to match detected code style
**DON'T:** Force generic templates that don't match project

### 5. Progressive Disclosure
**DO:** Can skip/abbreviate cycles if user says "use defaults"
**DON'T:** Force full interview if user wants quick setup

---

## 🔍 After Initialization

### Automatic Behaviors

Once initialized, Claude should:

1. **Check CLAUDE.md automatically** when starting any task
2. **Reference documentation** before exploring code
3. **Generate PRPs automatically** for complex work (>3 files)
4. **Suggest agents** when appropriate for task type
5. **Update documentation** after implementing changes
6. **Follow detected patterns** consistently

### User Experience

Users should be able to:
- Work naturally without thinking about methodology
- Say "I need X" and have Claude handle the process
- Trust that patterns will be followed
- See documentation stay current automatically

---

## 📝 Example Initialization Flow

```
User: "Apply this framework to /Users/me/ecommerce-api"

Claude: "I'll initialize context engineering for your project.
        Let me analyze the codebase first..."

[Scans files - 30 seconds]

Claude: "I've analyzed your project. I can see:
        
        ✅ Backend: Laravel 10.48 with PHP 8.2
          - Sanctum authentication
          - Spatie permissions
          - 34 API endpoints
          
        ✅ Frontend: React 18 with TypeScript
          - Vite build system
          - TanStack Query for API calls
          
        ✅ Database: PostgreSQL
          - 47 migrations
          - Eloquent ORM
        
        ✅ Integrations: Stripe, AWS S3, SendGrid
        
        Is this accurate?"

User: "Yes, that's correct"

Claude: "Great! Based on code analysis:
        
        Architecture: Monolithic API with service layer pattern
        - 15 service classes in app/Services/
        - Repository pattern for data access
        - Event-driven notifications
        
        I noticed you're using event-driven notifications -
        should I document the event/listener patterns?"

User: "Yes please"

Claude: "Perfect. I've identified 3 core business domains:
        - Product catalog management
        - Order processing workflow
        - Customer account system
        
        For order processing, I see multiple status transitions.
        What triggers order approval vs automatic fulfillment?"

User: "Orders over $500 require manual approval"

Claude: "Got it. Based on your Laravel + React + Stripe stack,
        I recommend these agents:
        
        ✅ Laravel API tester
        ✅ React component reviewer  
        ✅ Security auditor (for payment flows)
        
        Install these?"

User: "Yes"

Claude: "Initialization complete!

        Created:
        ✅ CLAUDE.md (312 lines)
        ✅ .claude/documentation/
           - Product_Catalog.md (187 lines)
           - Order_Processing.md (234 lines)
           - Customer_Accounts.md (156 lines)
           - Backend_Architecture.md (198 lines)
        ✅ .claude/prps/ template (Laravel/React optimized)
        ✅ .claude/agents/ - 3 configured agents

        You're ready to develop naturally. Just describe what
        you need and I'll handle the methodology automatically."
```

---

**This initialization process ensures every project gets context engineering tailored to its actual architecture, patterns, and business domain - not generic templates.**
