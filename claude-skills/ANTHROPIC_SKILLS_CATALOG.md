# 📚 Anthropic Skills Catalog

**Complete reference guide for all official Anthropic skills**

---

## Overview

This document catalogs all skills available in the official Anthropic Skills repository, providing detailed information about each skill's purpose, structure, and usage patterns.

**Skills Repository:** https://github.com/anthropics/skills
**Local Location:** `claude-skills/anthropic/`
**Last Updated:** 2025-11-11

---

## Table of Contents

1. [Development & Technical Skills](#development--technical-skills)
2. [Document Processing Skills](#document-processing-skills)
3. [Creative & Design Skills](#creative--design-skills)
4. [Enterprise & Communication Skills](#enterprise--communication-skills)
5. [Meta Skills](#meta-skills)
6. [Skill Selection Guide](#skill-selection-guide)

---

## Development & Technical Skills

### 🔧 mcp-builder
**Purpose:** Guide for creating high-quality MCP (Model Context Protocol) servers

**Use When:**
- Building MCP servers to integrate external APIs
- Creating tools for LLMs to interact with services
- Developing Python (FastMCP) or TypeScript (MCP SDK) integrations

**Structure:**
```
mcp-builder/
├── SKILL.md              # Main guide (4-phase workflow)
└── reference/
    ├── mcp_best_practices.md
    ├── python_mcp_server.md
    ├── node_mcp_server.md
    └── evaluation.md
```

**Key Features:**
- 4-phase development workflow (Research → Implement → Review → Evaluate)
- Agent-centric design principles
- Language-specific implementation guides
- Quality checklists
- Evaluation framework

**Real-World Example:**
```
User: "I need to build an MCP server for GitHub API"
Claude: [Loads mcp-builder skill]
  → Phase 1: Research GitHub API and MCP protocol
  → Phase 2: Implement tools with proper schemas
  → Phase 3: Code quality review
  → Phase 4: Create evaluation questions
```

---

### 🛠️ artifacts-builder
**Purpose:** Tools for creating HTML artifacts and interactive components

**Use When:**
- Building interactive HTML previews
- Creating demo applications
- Generating shareable web components

**Best For:**
- Quick prototyping
- User interface demonstrations
- Educational examples

---

### 🧪 webapp-testing
**Purpose:** Web application testing workflows and best practices

**Use When:**
- Setting up automated testing
- Creating test suites
- Implementing QA workflows

**Structure:**
```
webapp-testing/
├── SKILL.md
├── scripts/
└── references/
```

**Best For:**
- React applications
- Full-stack web apps
- CI/CD testing pipelines

---

## Document Processing Skills

### 📄 document-skills/pdf
**Purpose:** Comprehensive PDF manipulation toolkit

**Use When:**
- Extracting text and tables from PDFs
- Creating new PDFs programmatically
- Merging, splitting, or rotating PDFs
- Filling PDF forms
- Generating invoices or reports

**Structure:**
```
pdf/
├── SKILL.md          # Main guide with quick start
├── reference.md      # Advanced features and examples
└── forms.md          # Form filling instructions
```

**Key Capabilities:**
```python
# Extract text
from pypdf import PdfReader
reader = PdfReader("document.pdf")

# Merge PDFs
from pypdf import PdfWriter
writer = PdfWriter()
# ... merge logic

# Extract tables
import pdfplumber
with pdfplumber.open("doc.pdf") as pdf:
    tables = pdf.pages[0].extract_tables()
```

**Real-World Example:**
```
User: "Generate PDF invoices for all orders"
Claude: [Loads pdf skill]
  → Uses pypdf for PDF creation
  → Applies professional formatting
  → Generates batch invoices
```

**Python Libraries Used:**
- `pypdf` - Basic operations (merge, split, rotate)
- `pdfplumber` - Text and table extraction
- `reportlab` - PDF generation from scratch

---

### 📝 document-skills/docx
**Purpose:** Word document creation and manipulation

**Use When:**
- Creating formatted Word documents
- Extracting content from .docx files
- Generating reports with styles
- Handling tracked changes

**Best For:**
- Business documents
- Report generation
- Template-based content

---

### 📊 document-skills/pptx
**Purpose:** PowerPoint presentation creation and editing

**Use When:**
- Creating presentations programmatically
- Generating slide decks from data
- Automating presentation workflows

**Best For:**
- Data visualization presentations
- Template-based slides
- Automated reporting

---

### 📈 document-skills/xlsx
**Purpose:** Excel spreadsheet processing and generation

**Use When:**
- Creating Excel reports
- Processing spreadsheet data
- Generating data exports
- Working with formulas

**Best For:**
- Financial reports
- Data analysis exports
- Automated data processing

---

## Creative & Design Skills

### 🎨 algorithmic-art
**Purpose:** Generative art creation and creative coding

**Use When:**
- Creating visual artwork programmatically
- Generating creative assets
- Building generative art systems

**Structure:**
```
algorithmic-art/
├── SKILL.md
├── scripts/
└── assets/
```

**Best For:**
- Creative projects
- Visual experiments
- Unique asset generation

---

### 🖼️ canvas-design
**Purpose:** Visual design workflows and canvas-based creation

**Use When:**
- Designing user interfaces
- Creating visual layouts
- Working with design systems

**Structure:**
```
canvas-design/
├── SKILL.md
├── references/
└── assets/
```

**Best For:**
- UI/UX design
- Layout creation
- Design prototyping

---

### 🎭 theme-factory
**Purpose:** Theme generation and customization workflows

**Use When:**
- Creating design themes
- Building color palettes
- Generating branded assets

**Structure:**
```
theme-factory/
├── SKILL.md
├── scripts/
└── assets/
```

**Best For:**
- Brand identity work
- Design system development
- Multi-theme applications

---

## Enterprise & Communication Skills

### 📋 brand-guidelines
**Purpose:** Brand consistency enforcement and guidelines

**Use When:**
- Maintaining brand standards
- Enforcing design guidelines
- Creating branded content

**Best For:**
- Corporate projects
- Marketing materials
- Brand-critical applications

---

### 💬 internal-comms
**Purpose:** Internal communication templates and workflows

**Use When:**
- Creating team communications
- Drafting announcements
- Standardizing internal messaging

**Best For:**
- Company-wide communications
- Team announcements
- Policy communications

---

### 🎪 slack-gif-creator
**Purpose:** GIF creation for Slack integration

**Use When:**
- Creating animated responses
- Building Slack bots with visual feedback
- Generating custom Slack reactions

**Structure:**
```
slack-gif-creator/
├── SKILL.md
├── scripts/
└── assets/
```

**Best For:**
- Slack integrations
- Team communication tools
- Animated content generation

---

## Meta Skills

### 🏗️ skill-creator
**Purpose:** Guide for creating effective new skills

**Use When:**
- Creating custom skills
- Learning skill structure
- Building domain-specific skills

**6-Step Creation Process:**
1. **Understanding:** Gather concrete examples
2. **Planning:** Identify reusable contents
3. **Initializing:** Run `init_skill.py` script
4. **Editing:** Develop resources and SKILL.md
5. **Packaging:** Use `package_skill.py` to validate
6. **Iterating:** Refine based on feedback

**Skill Structure Guidance:**
```
skill-name/
├── SKILL.md (required)
│   ├── YAML frontmatter (name + description)
│   └── Markdown instructions
└── Bundled Resources (optional)
    ├── scripts/      - Executable code
    ├── references/   - Documentation
    └── assets/       - Output files
```

**Progressive Disclosure Principle:**
- **Level 1:** Metadata (~100 words) - Always in context
- **Level 2:** SKILL.md body (<5k words) - When skill triggers
- **Level 3:** Bundled resources (unlimited) - As needed

**Real-World Example:**
```
User: "I want to create a Laravel API patterns skill"
Claude: [Loads skill-creator]
  → Step 1: Gather examples of Laravel APIs
  → Step 2: Plan scripts/references/assets
  → Step 3: Run init_skill.py
  → Step 4: Develop SKILL.md and resources
  → Step 5: Package and validate
  → Step 6: Test with real projects
```

---

### 📋 template-skill
**Purpose:** Minimal starting template for new skills

**Use When:**
- Quick skill prototyping
- Learning skill format
- Starting from scratch without init script

**Structure:**
```yaml
---
name: skill-name
description: When Claude should use this skill
---

# Instructions go here
```

---

## Skill Selection Guide

### By Project Type

#### Laravel/PHP Projects
**Recommended Skills:**
- `mcp-builder` - For API development
- `document-skills/pdf` - For invoices/reports
- `webapp-testing` - For testing workflows

#### React/Frontend Projects
**Recommended Skills:**
- `artifacts-builder` - For component previews
- `canvas-design` - For UI design
- `theme-factory` - For theming
- `webapp-testing` - For testing

#### Python Projects
**Recommended Skills:**
- `mcp-builder` - For MCP servers
- `document-skills/xlsx` - For data processing
- `document-skills/pdf` - For report generation

#### E-commerce Platforms
**Recommended Skills:**
- `brand-guidelines` - Brand consistency
- `document-skills/pdf` - Invoices
- `document-skills/xlsx` - Sales reports
- `internal-comms` - Customer communication

#### Creative Agencies
**Recommended Skills:**
- `algorithmic-art` - Creative assets
- `canvas-design` - Design workflows
- `theme-factory` - Client theming
- `brand-guidelines` - Brand work

#### SaaS Platforms
**Recommended Skills:**
- `webapp-testing` - Quality assurance
- `mcp-builder` - API development
- `artifacts-builder` - Demo creation
- `document-skills/pdf` - User reports

---

### By Task Type

#### Document Generation
1. **PDF:** `document-skills/pdf`
2. **Word:** `document-skills/docx`
3. **Excel:** `document-skills/xlsx`
4. **PowerPoint:** `document-skills/pptx`

#### Development Work
1. **API Integration:** `mcp-builder`
2. **Testing:** `webapp-testing`
3. **Prototyping:** `artifacts-builder`

#### Creative Work
1. **Visual Design:** `canvas-design`
2. **Generative Art:** `algorithmic-art`
3. **Theming:** `theme-factory`

#### Enterprise Work
1. **Brand Consistency:** `brand-guidelines`
2. **Communications:** `internal-comms`
3. **Slack Integration:** `slack-gif-creator`

#### Meta Tasks
1. **Create New Skill:** `skill-creator`
2. **Quick Template:** `template-skill`

---

## Skill Anatomy Deep Dive

### YAML Frontmatter (Required)

```yaml
---
name: skill-name
description: Specific description of when Claude should use this skill
license: Optional license information
---
```

**Best Practices:**
- Use kebab-case for skill names
- Write descriptions in third-person
- Be specific about when to use the skill
- Include context triggers

### Markdown Instructions (Required)

**Structure Patterns:**

1. **Process-Oriented Skills** (like mcp-builder):
```markdown
# Skill Name

## Overview

## Process
### Phase 1: ...
### Phase 2: ...

## Reference Files
```

2. **Tool-Oriented Skills** (like pdf):
```markdown
# Skill Name

## Overview

## Quick Start

## Library/Tool Details

## Common Operations

## Advanced Features
```

3. **Template-Oriented Skills** (like brand-guidelines):
```markdown
# Skill Name

## Overview

## Guidelines

## Templates

## Usage Examples
```

### Optional Bundled Resources

#### scripts/
**When to Include:**
- Code being rewritten repeatedly
- Deterministic reliability needed
- Token efficiency important

**Examples:**
```
scripts/
├── rotate_pdf.py
├── generate_chart.py
└── utils/
    └── helpers.py
```

#### references/
**When to Include:**
- Documentation Claude should reference
- Large schemas or specifications
- Detailed workflow guides

**Examples:**
```
references/
├── api_docs.md
├── database_schema.md
├── policies.md
└── examples.md
```

**Best Practice:**
- Keep SKILL.md lean (<5k words)
- Move detailed info to references
- Include grep patterns for large files

#### assets/
**When to Include:**
- Files used in output (not loaded into context)
- Templates for copying
- Images, fonts, icons

**Examples:**
```
assets/
├── logo.png
├── template.pptx
├── frontend-boilerplate/
└── fonts/
```

---

## Usage Statistics & Recommendations

### Most Versatile Skills (Use Across Many Projects)

1. **document-skills/pdf** - Almost every project generates PDFs
2. **mcp-builder** - Any API integration work
3. **skill-creator** - Building custom skills
4. **webapp-testing** - Quality assurance for web apps

### Specialized but High-Impact

1. **brand-guidelines** - Critical for brand-focused work
2. **algorithmic-art** - Unique for creative projects
3. **slack-gif-creator** - Specific but powerful for Slack

### Learning & Development

1. **template-skill** - Start here for skill structure
2. **skill-creator** - Comprehensive skill creation guide
3. **mcp-builder** - Example of well-structured process skill

---

---

## Framework Integration & Usage

**This catalog documents official Anthropic skills only.**

For framework-specific integration details:
- **Usage in projects:** See [README.md](README.md#usage-in-projects)
- **Maintenance & updates:** See [README.md](README.md#maintenance)
- **Custom skill creation:** Load `anthropic/skill-creator/SKILL.md`
- **Integration strategy:** See `../core/SKILLS_INTEGRATION.md`

---

**Version:** 2.0.0 (Token-Optimized)
**Purpose:** Skills reference only
**Last Updated:** 2025-11-11
