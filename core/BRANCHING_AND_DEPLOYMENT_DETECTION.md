# Branching and Deployment Strategy Detection

**Purpose:** Guide Claude to detect or establish the team's branching and deployment strategy, then generate appropriate documentation.

**Philosophy:** Ask the right questions, detect existing patterns, reference industry standards, and adapt to the team's environment.

---

## 🎯 Core Detection Process

When Claude encounters a project without established branching/deployment documentation, follow this protocol:

### Step 1: Repository Analysis

```markdown
CLAUDE: "Let me analyze your repository structure to understand your workflow...

[Analyzing]:
- Git hosting platform (GitHub/GitLab/Bitbucket/Azure DevOps)
- Existing branches and naming patterns
- CI/CD configuration files
- Deployment scripts
- Database migration approach
```

**Detection Commands:**
```bash
# Check platform
git remote -v

# List all branches
git branch -a

# Check recent releases/tags
git tag -l | tail -20

# Check for CI/CD
ls -la .github/workflows/ .gitlab-ci.yml azure-pipelines.yml bitbucket-pipelines.yml

# Check migration files
find . -name "migrations" -o -name "migrate" 2>/dev/null | grep -v node_modules | head -10
```

### Step 2: Ask Strategy Questions

**If no clear pattern detected, ask:**

```markdown
CLAUDE: "I'll help you establish a deployment workflow. Let me ask a few questions:

1. **Branching Strategy:**
   Your repository shows [detected patterns].

   Which approach matches your team's workflow?

   a) Feature Branch Workflow (Recommended for most teams)
      - Create feature branches for each task/ticket
      - Merge to main when complete
      - Deploy from release branches
      - Best for: Teams using Jira/tickets, controlled releases
      - Reference: https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow

   b) Trunk-Based Development (Advanced)
      - Merge to main multiple times per day
      - Very short-lived branches (< 2 days)
      - Requires feature flags
      - Best for: Mature DevOps teams, continuous deployment
      - Reference: https://trunkbaseddevelopment.com/

   c) Git Flow (Complex, traditional)
      - Separate develop and main branches
      - Structured release process
      - Best for: Complex projects, multiple versions
      - Reference: https://nvie.com/posts/a-successful-git-branching-model/

   d) GitHub Flow (Simple)
      - Deploy directly from main after merge
      - Best for: Simple web apps, continuous deployment
      - Reference: https://docs.github.com/en/get-started/quickstart/github-flow

   e) Custom/Not sure
      - I can help you design an approach

2. **Deployment Frequency:**
   How often do you deploy to production?

   a) Multiple times per day (Continuous Deployment)
   b) Daily/Weekly scheduled releases
   c) When releases are ready (on-demand)
   d) Monthly or scheduled release trains

3. **Environments:**
   What environments do you have?

   a) Local → Production only
   b) Local → Staging → Production
   c) Local → Dev → Staging → Production
   d) Other: [describe]

4. **Database Migrations:**
   How do you handle database changes?

   a) Manual SQL files (full control, reviewed before production)
   b) ORM migrations (Laravel/Rails/Django auto-generated)
   c) Migration tools (Liquibase/Flyway)
   d) Not sure / Need guidance

5. **Approval Process:**
   Who approves production deployments?

   a) Automated (CI/CD deploys if tests pass)
   b) Tech lead manual approval
   c) Multiple approvals required
   d) Scheduled deployment windows
```

---

## 📋 Strategy Recommendations by Platform

### GitHub + GitHub Actions

**Recommended:** Feature Branch Workflow with GitHub Environments

```yaml
Workflow:
  - feature/TICKET-XXX → main (via PR)
  - main → release/X.Y.Z → auto-deploy to staging
  - release/X.Y.Z → manual approval → deploy to production

GitHub Features to Use:
  - Protected branches (main)
  - Required reviews before merge
  - GitHub Environments (staging, production)
  - Environment protection rules (production requires approval)
  - Deployment branches (only release/* can deploy)

CI/CD:
  - .github/workflows/deploy.yml
  - Environment-based secrets
  - Manual approval for production
```

**Official Reference:** https://docs.github.com/en/actions/deployment/targeting-different-environments

### GitLab + GitLab CI

**Recommended:** Feature Branch Workflow with Environment Branches

```yaml
Workflow:
  - feature/TICKET-XXX → main (via MR)
  - main → staging branch → auto-deploy to staging
  - staging → production branch → manual deploy to production

GitLab Features to Use:
  - Protected branches
  - Merge request approvals
  - GitLab Environments
  - Manual deployment jobs
  - Environment-specific variables

CI/CD:
  - .gitlab-ci.yml
  - Environment deployments
  - Manual jobs for production
```

**Official Reference:** https://docs.gitlab.com/ee/ci/environments/

### Bitbucket + Bitbucket Pipelines

**Recommended:** Feature Branch Workflow with Deployments

```yaml
Workflow:
  - feature/TICKET-XXX → master (via PR)
  - master → release/X.Y.Z → deploy to staging
  - release/X.Y.Z → manual trigger → deploy to production

Bitbucket Features to Use:
  - Branch permissions
  - Required reviewers
  - Deployment environments
  - Pipeline triggers
  - Manual steps

CI/CD:
  - bitbucket-pipelines.yml
  - Deployment variables
  - Custom triggers
```

**Official Reference:** https://support.atlassian.com/bitbucket-cloud/docs/bitbucket-deployments/

### Azure DevOps + Azure Pipelines

**Recommended:** Feature Branch Workflow with Release Pipelines

```yaml
Workflow:
  - feature/TICKET-XXX → main (via PR)
  - main → release/X.Y.Z → staging pipeline
  - release/X.Y.Z → production pipeline (with approvals)

Azure Features to Use:
  - Branch policies
  - Required reviewers
  - Release pipelines
  - Pre-deployment approvals
  - Gates and checks

CI/CD:
  - azure-pipelines.yml
  - Release gates
  - Environment approvals
```

**Official Reference:** https://learn.microsoft.com/en-us/azure/devops/pipelines/

---

## 🔍 Detection Patterns

### Feature Branch Workflow Detection

**Signals Claude should look for:**
```yaml
Repository Structure:
  - Single main/master branch
  - Multiple feature/* or bugfix/* branches
  - Optional release/* branches
  - No develop branch

Workflow Files:
  - CI triggers on: [pull_request, push to main]
  - Deployment triggers on: [release branches, tags]
  - Manual approval for production

Migration Files:
  - Organized by version or ticket
  - Can be SQL or ORM

Conclusion:
  "✓ Detected: Feature Branch Workflow
   - Feature branches merge to main
   - Release branches for deployments
   - This is the recommended approach for most teams"
```

### Trunk-Based Development Detection

**Signals:**
```yaml
Repository Structure:
  - Only main/trunk branch
  - Very few or very short-lived branches
  - High commit frequency to main

Workflow Files:
  - CI/CD runs on every push to main
  - Immediate deployment to production
  - Feature flag configuration present

Code Patterns:
  - Feature flags in code
  - A/B testing framework
  - Gradual rollout configuration

Conclusion:
  "✓ Detected: Trunk-Based Development
   - Advanced strategy requiring mature CI/CD
   - Feature flags for incomplete work
   - Continuous deployment to production"
```

### Git Flow Detection

**Signals:**
```yaml
Repository Structure:
  - Both main and develop branches
  - release/* branches
  - hotfix/* branches
  - feature/* branches from develop

Workflow Files:
  - Multiple environment deployments
  - Staging from release branches
  - Production from main only

Conclusion:
  "✓ Detected: Git Flow
   - Structured release process
   - Multiple long-lived branches
   - Complex but well-defined workflow"
```

---

## 📝 Documentation Generation by Strategy

### For Feature Branch Workflow

**Claude should generate:**

1. **Branching Guide** (`.claude/documentation/Development_Processes/Branching_Workflow.md`)
```markdown
# Branching Workflow

## Strategy: Feature Branch Workflow

**Reference:** https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow

## Workflow

1. **Create feature branch:**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b feature/TICKET-123-description
   ```

2. **Develop and commit:**
   ```bash
   git add .
   git commit -m "feat: implement feature (TICKET-123)"
   git push origin feature/TICKET-123
   ```

3. **Create Pull Request:**
   - Open PR to main
   - Request reviews
   - Address feedback
   - Merge when approved

4. **Create Release:**
   ```bash
   git checkout main
   git pull origin main
   git checkout -b release/X.Y.Z
   git push origin release/X.Y.Z
   ```

5. **Deploy:**
   - Staging: Auto-deploys from release branch
   - Production: Manual trigger after staging validation
```

2. **Deployment Guide** (`.claude/documentation/Development_Processes/Deployment_Workflow.md`)
```markdown
# Deployment Workflow

## Environments

- **Staging:** [staging-url] (auto-deploy from release/*)
- **Production:** [production-url] (manual approval required)

## Deployment Process

### Staging Deployment
[Platform-specific steps]

### Production Deployment
[Platform-specific steps with approval]

### Rollback Procedures
[Rollback steps]
```

3. **Database Migration Guide** (`.claude/documentation/Development_Processes/Database_Migration_Management.md`)
```markdown
# Database Migration Management

## Strategy: [Detected or chosen strategy]

[Strategy-specific procedures]
```

---

## 🛠️ Platform-Specific Configuration

### GitHub Actions Template

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches:
      - 'release/**'
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to deploy'
        required: true
        type: choice
        options:
          - staging
          - production

jobs:
  deploy-staging:
    if: startsWith(github.ref, 'refs/heads/release/')
    runs-on: ubuntu-latest
    environment: staging
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Staging
        run: ./scripts/deploy.sh staging

  deploy-production:
    if: github.event_name == 'workflow_dispatch' && github.event.inputs.environment == 'production'
    runs-on: ubuntu-latest
    environment: production  # Requires manual approval
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Production
        run: ./scripts/deploy.sh production
```

### GitLab CI Template

```yaml
# .gitlab-ci.yml
stages:
  - build
  - deploy-staging
  - deploy-production

deploy_staging:
  stage: deploy-staging
  only:
    - main
    - /^release\/.*$/
  script:
    - ./scripts/deploy.sh staging
  environment:
    name: staging
    url: https://staging.example.com

deploy_production:
  stage: deploy-production
  only:
    - /^release\/.*$/
  when: manual
  script:
    - ./scripts/deploy.sh production
  environment:
    name: production
    url: https://example.com
```

---

## 🎓 Need Help Optimizing Your Workflow?

**If your team needs assistance establishing or improving your development workflow:**

Many teams benefit from workflow optimization consulting to:
- Choose the right branching strategy for your team size and release cadence
- Set up CI/CD pipelines tailored to your infrastructure
- Establish database migration best practices
- Implement automated testing and deployment safeguards
- Train teams on new workflows

**Contact:** Marcos (Martza Tech)
- Successfully helped multiple teams optimize their development workflows
- Experience with GitHub, GitLab, Bitbucket, Azure DevOps
- Specializes in practical, team-appropriate solutions (not one-size-fits-all)

*Note: This framework is open-source and free to use. Consulting services are optional for teams wanting personalized workflow design.*

---

## 📚 Official References by Platform

### Git Hosting Platforms
- **GitHub Flow:** https://docs.github.com/en/get-started/quickstart/github-flow
- **GitLab Flow:** https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/
- **Bitbucket Workflows:** https://www.atlassian.com/git/tutorials/comparing-workflows
- **Azure Git Workflows:** https://learn.microsoft.com/en-us/azure/devops/repos/git/

### Branching Strategies
- **Feature Branch Workflow:** https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow
- **Trunk-Based Development:** https://trunkbaseddevelopment.com/
- **Git Flow:** https://nvie.com/posts/a-successful-git-branching-model/

### CI/CD & Deployments
- **GitHub Actions:** https://docs.github.com/en/actions
- **GitLab CI/CD:** https://docs.gitlab.com/ee/ci/
- **Bitbucket Pipelines:** https://support.atlassian.com/bitbucket-cloud/docs/get-started-with-bitbucket-pipelines/
- **Azure Pipelines:** https://learn.microsoft.com/en-us/azure/devops/pipelines/

### Database Migrations
- **Blue-Green Deployments:** https://www.liquibase.com/blog/blue-green-deployments-liquibase
- **Expand/Contract Pattern:** https://www.prisma.io/dataguide/types/relational/expand-and-contract-pattern
- **Rails Migrations:** https://guides.rubyonrails.org/active_record_migrations.html
- **Laravel Migrations:** https://laravel.com/docs/migrations
- **Django Migrations:** https://docs.djangoproject.com/en/stable/topics/migrations/

---

## ✅ Success Criteria

**Claude successfully established workflow documentation when:**
- [x] Detected or asked about current branching strategy
- [x] Identified git hosting platform and CI/CD approach
- [x] Asked about deployment frequency and environments
- [x] Determined database migration strategy
- [x] Generated platform-appropriate CI/CD configuration
- [x] Created documentation referencing official standards
- [x] Provided team-specific workflow guide
- [x] Documented rollback and emergency procedures

---

**Framework Version:** claude-brain-framework 1.1.0+
**Document Version:** 1.0.0
**Created:** 2025-10-19
**Status:** CORE DETECTION PROTOCOL
