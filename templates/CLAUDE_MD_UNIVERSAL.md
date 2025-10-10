# [Project Name] - Context Engineering

**Universal template adaptable to any software project type**

## 🚨 CRITICAL WORKFLOW ENFORCEMENT

**CLAUDE: Automatically apply context engineering for ANY development request.**

### Automatic Behaviors
1. ✅ Check documentation automatically
2. ✅ Assess complexity
3. ✅ Generate PRP for complex work (>3 files or significant logic)
4. ✅ Follow established patterns
5. ✅ Suggest relevant agents
6. ✅ Update documentation

**User works naturally - methodology applies automatically.**

---

## 📋 PROJECT TYPE & CONTEXT

### Project Classification
**Primary Type:** [Select: Web Application / Infrastructure / Data Pipeline / ML/AI / Security / Mobile / Embedded / DevOps / CLI Tool / Library / Other]

**Domain:** [e.g., E-commerce, Healthcare, Finance, Analytics, Automation, Networking]

**Scale:** [e.g., Startup MVP, Enterprise System, Open Source, Internal Tool]

---

## 🛠️ TECHNOLOGY STACK

### Core Technologies
**[Adapt to your project type]**

#### Web Application Example:
- **Backend:** [Framework + Language + Version]
- **Frontend:** [Framework + Language + Version]
- **Database:** [Type + Version]
- **APIs:** [REST/GraphQL/gRPC]

#### Infrastructure/DevOps Example:
- **IaC:** [Terraform, Pulumi, CloudFormation]
- **Orchestration:** [Kubernetes, Docker Swarm, Nomad]
- **CI/CD:** [GitHub Actions, GitLab CI, Jenkins]
- **Cloud:** [AWS, GCP, Azure, On-prem]

#### Data/ML Example:
- **Language:** [Python, R, Scala]
- **Framework:** [TensorFlow, PyTorch, Spark]
- **Data Storage:** [S3, HDFS, PostgreSQL]
- **Processing:** [Airflow, Prefect, Luigi]

#### Security Example:
- **Language:** [Python, Go, Rust]
- **Frameworks:** [Security scanning tools]
- **Targets:** [Cloud, Network, Application]
- **Compliance:** [SOC2, HIPAA, PCI-DSS]

### Dependencies & Integrations
- **Package Manager:** [npm, pip, cargo, maven, etc.]
- **Key Libraries:** [List critical dependencies]
- **External Services:** [APIs, cloud services, SaaS tools]
- **Monitoring:** [Logging, metrics, alerting tools]

---

## ⚙️ DEVELOPMENT COMMANDS

### Environment Setup
```bash
# Project initialization
[install dependencies command]
[environment setup]
[configuration initialization]
```

### Development Workflow
```bash
# Core development
[start/run command]
[watch/hot-reload command]
[debug command]

# Testing
[unit test command]
[integration test command]
[e2e test command]

# Quality
[linting command]
[formatting command]
[type checking command]
[security scan command]
```

### Build & Deploy
```bash
# Build
[compile/build command]
[optimization command]
[artifact generation]

# Deploy
[deploy to dev]
[deploy to staging]
[deploy to production]
[rollback command]
```

### Validation (run after changes)
```bash
[your validation pipeline]
# Example: npm test && npm run lint && npm run build
```

---

## 🏗️ PROJECT ARCHITECTURE

### Directory Structure
```
[YOUR STRUCTURE]
/
├── [source directory]/
│   └── [organization pattern]
├── /.claude/                # Claude context engineering
│   ├── /documentation/      # System docs (ALWAYS check first)
│   ├── /prps/              # Implementation blueprints
│   ├── /agents/            # Specialized agents
│   └── /chat-summaries/    # Conversation tracking (optional)
├── /tests/ or /spec/        # Testing
└── [config files]           # Configuration
```

### Architectural Patterns
- **Design Pattern:** [MVC, Microservices, Event-Driven, Layered, etc.]
- **Data Flow:** [How data moves through system]
- **Communication:** [API, Message Queue, Event Bus, Direct Calls]
- **State Management:** [How state is handled]

### Key Components
**Component 1:** [Name and purpose]
- Location: [file/directory path]
- Responsibilities: [what it does]
- Dependencies: [what it relies on]

**Component 2:** [Name and purpose]
- Location: [file/directory path]
- Responsibilities: [what it does]
- Dependencies: [what it relies on]

---

## 🎯 DOMAIN KNOWLEDGE

### Business/Technical Domain
**[Adapt to your project]**

#### For Applications:
- **User Roles:** [Who uses this]
- **Core Workflows:** [Key user journeys]
- **Business Rules:** [Critical constraints]

#### For Infrastructure:
- **Resources Managed:** [What infrastructure]
- **Automation Workflows:** [Key processes]
- **Compliance Requirements:** [Standards to meet]

#### For Data/ML:
- **Data Sources:** [Where data comes from]
- **Processing Pipeline:** [How data flows]
- **Model/Analysis:** [What insights/predictions]

#### For Security:
- **Threat Model:** [What you protect against]
- **Security Controls:** [Protections in place]
- **Compliance:** [Regulations/standards]

### Critical Workflows
1. **[Workflow Name]:**
   - Trigger: [What starts it]
   - Steps: [Key steps]
   - Success Criteria: [When complete]
   - Files: [Relevant code]

2. **[Workflow Name]:**
   - Trigger: [What starts it]
   - Steps: [Key steps]
   - Success Criteria: [When complete]
   - Files: [Relevant code]

---

## 📚 DOCUMENTATION

### System Documentation
**Location:** `/.claude/documentation/`

**Structure:**
- `@.claude/documentation/Core_Systems/[System_1].md`
- `@.claude/documentation/Core_Systems/[System_2].md`
- `@.claude/documentation/Workflows/[Workflow].md` (if applicable)
- `@.claude/documentation/Architecture/[Component].md`

**CLAUDE: Always check relevant docs before implementation using @import syntax.**

### External References
- **[Framework/Tool]:** [Documentation URL]
- **[Service/API]:** [API docs, best practices]
- **[Standards]:** [RFC, specifications, compliance docs]

---

## 🤖 AGENT RECOMMENDATIONS

### Suggested Agents (based on project type)

**For Web Projects:**
- `code-reviewer` - Quality assurance
- `[framework]-specialist` - Framework-specific patterns
- `security-auditor` - Security validation
- `test-runner` - Automated testing

**For Infrastructure:**
- `terraform-validator` - IaC validation
- `security-auditor` - Cloud security
- `cost-optimizer` - Resource optimization
- `compliance-checker` - Standards validation

**For Data/ML:**
- `data-validator` - Data quality checks
- `model-evaluator` - Model performance
- `pipeline-optimizer` - Processing efficiency
- `experiment-tracker` - ML experiment tracking

**For Security:**
- `vulnerability-scanner` - Security assessment
- `compliance-auditor` - Regulatory compliance
- `threat-modeler` - Threat analysis
- `penetration-tester` - Security testing

### Agent Location
`.claude/agents/[agent-name].md`

**Invocation:** Automatic based on task, or manual: "Use [agent] for [task]"

---

## ✅ VALIDATION & QUALITY

### Quality Standards
- **Code Quality:** [Standards and tools]
- **Testing:** [Coverage requirements, test types]
- **Security:** [Security requirements, scan tools]
- **Performance:** [Benchmarks, SLAs]
- **Documentation:** [Documentation requirements]

### Validation Checklist
```bash
# After implementation
- [ ] Tests pass
- [ ] Quality checks pass
- [ ] Security scan clean
- [ ] Performance acceptable
- [ ] Documentation updated
- [ ] [Project-specific validations]
```

---

## 🔒 SECURITY & COMPLIANCE

### Security Practices
- **Authentication:** [How handled]
- **Authorization:** [Permission model]
- **Data Protection:** [Encryption, sanitization]
- **Secrets Management:** [How secrets stored/accessed]
- **Audit Logging:** [What's logged]

### Compliance Requirements
- **Standards:** [SOC2, HIPAA, PCI, GDPR, etc.]
- **Policies:** [Data retention, privacy, security]
- **Auditing:** [Audit requirements, reporting]

### Sensitive Data
**NEVER commit:**
- `.env`, `*.pem`, `*.key`
- Credentials, tokens, API keys
- Customer data, PII
- [Project-specific sensitive files]

---

## 🚀 DEPLOYMENT & OPERATIONS

### Environments
- **Development:** [Details]
- **Staging:** [Details]
- **Production:** [Details]
- **[Other envs]:** [Details]

### Deployment Process
- **CI/CD:** [Pipeline details]
- **Manual Steps:** [If any]
- **Rollback:** [How to rollback]
- **Health Checks:** [Post-deploy validation]

### Monitoring & Observability
- **Metrics:** [What's tracked]
- **Logging:** [Log aggregation, search]
- **Alerting:** [Alert conditions, channels]
- **Dashboards:** [Monitoring dashboards]

---

## 💡 PROJECT-SPECIFIC NOTES

### Known Issues & Gotchas
- [Issue 1 and workaround]
- [Issue 2 and workaround]
- [Common pitfall and solution]

### Performance Considerations
- [Performance pattern/consideration 1]
- [Performance pattern/consideration 2]
- [Optimization opportunities]

### Future Improvements
- [Planned enhancement 1]
- [Planned enhancement 2]
- [Technical debt to address]

---

## 📊 METRICS & TARGETS (if applicable)

### Performance Targets
- [Metric 1]: [Target value]
- [Metric 2]: [Target value]
- [Metric 3]: [Target value]

### Quality Targets
- Test Coverage: [Target %]
- Code Quality: [Standards]
- Security Score: [Target]

---

## 🔄 FEATURE DEVELOPMENT WORKFLOW

### Simple Changes
1. Check documentation
2. Implement following patterns
3. Run validation
4. Update docs if needed

### Complex Features
1. **CLAUDE AUTO-GENERATES PRP**
2. Clarify business/technical decisions
3. Implement systematically
4. Full validation
5. Agent review if appropriate
6. Update documentation
7. Move PRP to completed

---

**Context Engineering Version:** 1.0.0  
**Last Updated:** [Date]  
**Project Type:** [Your type]

**This template adapts to any software project - customize the relevant sections for your specific needs.**
