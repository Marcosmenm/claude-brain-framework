# [Project Name] Documentation Index

**Complete documentation structure for [Project Name]**

## 📚 Documentation Status

### ✅ Core_Systems/ ([X] files planned)

**Purpose:** Business domain and system functionality documentation

#### Completed:
- [x] **[System_Name.md](Core_Systems/System_Name.md)** - Brief description
- [x] **[Another_System.md](Core_Systems/Another_System.md)** - Brief description

#### To Be Created:
- [ ] **System_Name.md** - Brief description of what this will cover
- [ ] **Another_System.md** - Brief description of what this will cover

### 📐 Architecture/ ([X] files planned)

**Purpose:** Technical architecture, design patterns, and system structure

- [x] **[Architecture_Component.md](Architecture/Architecture_Component.md)** - Brief description
- [ ] **Component_Name.md** - Brief description (TODO)

### 🔄 Workflows/ ([X] files planned)

**Purpose:** End-to-end process flows and user journeys

- [ ] **Workflow_Name.md** - Brief description (TODO)

---

## 📖 How to Use This Documentation

### For New Developers

**Onboarding Path:**
1. **Start Here:** Read [Overall_Architecture.md](Architecture/Overall_Architecture.md)
2. **Understand Tech Stack:** Review tech stack section in CLAUDE.md
3. **Core Systems:** Explore Core_Systems/ based on your team/role
4. **Development Setup:** Follow setup instructions in CLAUDE.md

### For Feature Development

**Development Path:**
1. **Check relevant Core_Systems docs** for the feature area
2. **Review related Workflows** to understand end-to-end flow
3. **Reference Architecture docs** for design patterns
4. **Check Database_Schema.md** for entity relationships (if applicable)

### For Troubleshooting

**Troubleshooting Path:**
1. **Check "Troubleshooting" section** in relevant Core_Systems doc
2. **Review error logs** with context from documentation
3. **Check Related Systems** section for integration issues

### For API Integration

**Integration Path:**
1. **Read API_Design.md** (if exists) for conventions
2. **Check specific system docs** for endpoint details
3. **Review Authentication docs** for auth requirements

---

## 🔄 Documentation Maintenance

### Update Process

**When to update documentation:**
- ✅ After implementing new features
- ✅ After architecture changes
- ✅ After API changes
- ✅ When bugs reveal documentation gaps
- ✅ When onboarding reveals unclear sections

**How to update:**
1. Edit the relevant markdown file
2. Update "Change History" section at bottom of file
3. Update "Last Updated" date
4. Update this index if adding/removing files
5. Commit with message: `docs: [description of change]`

### Adding New Documentation

**To add a new documentation file:**
1. Copy appropriate template from framework (`DOCUMENTATION_TEMPLATE.md`)
2. Create file in correct folder (Core_Systems/, Architecture/, Workflows/)
3. Add entry to this index with ✅ or [ ] checkbox
4. Update CLAUDE.md to reference new doc (if critical)
5. Cross-reference from related docs

### Keeping Docs Current

**Documentation Quality Checklist:**
- [ ] Code examples still accurate
- [ ] API endpoints still correct
- [ ] File paths still valid
- [ ] Troubleshooting section reflects common issues
- [ ] Related Systems links are accurate
- [ ] No broken internal links

---

## 📊 Documentation Generation Source

**Analysis Method:** [Describe how documentation was generated]
- Manual codebase review
- Claude Code analysis with claude-brain-framework
- Team knowledge capture sessions
- Existing documentation consolidation

**Analysis Date:** [YYYY-MM-DD]

**Framework Version:** claude-brain-framework v[X.X.X]

**Analysis Artifacts:**
- [Link to analysis file if exists, e.g., `documentation_generation_analysis.md`]

---

## 🎯 Documentation Priorities

### High Priority (Create/Update Next)
**These docs have highest impact on development velocity:**
1. [System_Name.md] - Why important
2. [Another_System.md] - Why important

### Medium Priority
**Useful but not blocking:**
3. [System_Name.md] - Why useful
4. [System_Name.md] - Why useful

### Lower Priority (Can Defer)
**Nice to have, can be inferred from code or higher-priority docs:**
5. [System_Name.md] - Why lower priority

---

## 🔗 External Resources

**Official Documentation:**
- [Technology/Framework]: [Link to official docs]
- [Technology/Framework]: [Link to official docs]

**Internal Resources:**
- Team Wiki: [Link if exists]
- Architecture Decision Records (ADRs): [Link if exists]
- API Documentation (Swagger/OpenAPI): [Link if exists]

**Training Resources:**
- Onboarding Guide: [Link if exists]
- Video Tutorials: [Link if exists]

---

## 📈 Documentation Metrics

**Coverage:**
- Total Systems Identified: [X]
- Core Systems Documented: [X]/[Y] ([Z]%)
- Architecture Docs Completed: [X]/[Y] ([Z]%)
- Workflows Documented: [X]/[Y] ([Z]%)

**Usage:**
- Most Referenced Docs: [List top 3-5 based on team feedback]
- Most Updated Docs: [List top 3-5 that change frequently]

**Feedback:**
- [Note common feedback themes from team]
- [Note frequently asked questions not covered]

---

## 💡 Documentation Tips

### For Documentation Writers

**Best Practices:**
- ✅ Start with "Quick Context" section (purpose, key files, common issues)
- ✅ Include code examples with actual file paths
- ✅ Add troubleshooting section based on real issues
- ✅ Cross-reference related systems
- ✅ Keep language clear and concise
- ✅ Use diagrams for complex flows (ASCII art or markdown-based)

**Common Pitfalls:**
- ❌ Documenting implementation details that change frequently
- ❌ Assuming reader knowledge (explain acronyms, link to concepts)
- ❌ Writing docs that become outdated immediately
- ❌ Not including "why" explanations (only "what" and "how")

### For Documentation Consumers

**Reading Strategies:**
- 📖 Read "Quick Context" first (3-minute overview)
- 🎯 Jump to relevant sections (use Cmd+F / Ctrl+F)
- 🔗 Follow "Related Systems" links for broader context
- 🚨 Check "Troubleshooting" when stuck
- 💻 Try code examples in "Development Context"

---

## 🔔 Notification & Updates

**How to stay updated:**
- Watch this repository for documentation changes
- Subscribe to documentation update notifications (if available)
- Check "Change History" section in docs for recent updates
- Review this index periodically for new documentation

**Documentation Review Cadence:**
- 🔄 **Quarterly:** Full documentation review and update cycle
- 📅 **Monthly:** High-priority docs reviewed for accuracy
- 🐛 **As-needed:** Updates when bugs or changes occur

---

**Generated by:** Claude Code (claude-brain-framework v[X.X.X])
**Project:** [Project Name]
**Last Updated:** [YYYY-MM-DD]
**Maintained by:** [Team/Person]
**Questions?** [Contact information or discussion link]
