# CI/CD Deployment Guide

**Lean, incremental approach to production deployments**

> **"Deploy the pipeline incrementally, just like you develop code."**

## 🎯 Core Philosophy

Apply the same **lean incremental methodology** to CI/CD setup that you use for development. Set up deployment pipelines in testable phases, not all at once.

**See Also:** [LEAN_DEVELOPMENT_WORKFLOW.md](LEAN_DEVELOPMENT_WORKFLOW.md) for development methodology

---

## 📊 The Problem: Big-Bang Pipeline Setup

### ❌ What Fails

**Typical Pattern:**
- Write complete CI/CD workflow with 15 steps
- Push to GitHub
- Get 23 configuration errors
- Spend 4 hours debugging which step broke what

### ✅ Lean Alternative

**Incremental Pattern:**
- Iteration 1: Test CI connectivity (1 step)
- Iteration 2: Add code checkout (2 steps)
- Iteration 3: Add dependency installation (3 steps)
- Iteration 4: Add build process (4 steps)
- Continue incrementally...

**Result:** Each push tests ONE new thing. Errors are immediately obvious.

---

## 🔄 The 5-Phase Deployment Setup

### Phase 1: Basic Connectivity (~30 min)

**Goal:** Verify CI can reach your infrastructure

**Steps:**
1. SSH connection working
2. File upload working
3. Basic health check endpoint responding

**Health Check Levels:**

#### Level 1: Basic HTTP Response
```javascript
// routes/health.js
app.get('/health', (req, res) => {
  res.json({ status: 'ok' });
});
```

#### Level 2: Database Connectivity
```javascript
app.get('/health', async (req, res) => {
  try {
    await db.query('SELECT 1');
    res.json({ status: 'ok', database: 'connected' });
  } catch (error) {
    res.status(503).json({ status: 'error', database: 'disconnected' });
  }
});
```

#### Level 3: Comprehensive Health Check
```javascript
app.get('/health', async (req, res) => {
  const checks = {
    status: 'ok',
    timestamp: new Date().toISOString(),
    uptime: process.uptime(),
    database: await checkDatabase(),
    cache: await checkCache(),
    externalAPI: await checkExternalServices(),
    diskSpace: await checkDiskSpace(),
    memory: process.memoryUsage(),
  };

  const allHealthy = Object.values(checks).every(
    check => check !== 'error' && check !== 'disconnected'
  );

  res.status(allHealthy ? 200 : 503).json(checks);
});
```

#### Level 4: Deep Health Check (Production-Grade)
```javascript
app.get('/health/deep', async (req, res) => {
  const results = await Promise.allSettled([
    checkDatabase(),
    checkCache(),
    checkFileSystem(),
    checkExternalAPIs(),
    checkQueueConnections(),
    checkScheduledJobs(),
  ]);

  const health = {
    status: results.every(r => r.status === 'fulfilled') ? 'healthy' : 'degraded',
    checks: results.map((r, i) => ({
      name: ['database', 'cache', 'filesystem', 'external', 'queue', 'jobs'][i],
      status: r.status === 'fulfilled' ? 'pass' : 'fail',
      details: r.value || r.reason,
      timestamp: new Date().toISOString(),
    })),
    version: process.env.APP_VERSION,
    environment: process.env.NODE_ENV,
  };

  res.status(health.status === 'healthy' ? 200 : 503).json(health);
});
```

**Recommendation:**
- **Development/Staging:** Level 2 (database check)
- **Production:** Level 3 or 4 (comprehensive checks)
- **Critical Systems:** Level 4 + alerting integration

**Test Phase 1:**
```bash
curl https://your-domain.com/health
# Expected: 200 OK with health status
```

✅ Confirm working before Phase 2

---

### Phase 2: Build Process (~1-2 hours)

**Goal:** Dependencies install, tests run, artifacts generated

**Steps:**
1. Install dependencies (npm install, composer install, etc.)
2. Run test suite
3. Generate build artifacts (if applicable)

**Test Phase 2:**
```bash
# Locally
npm install && npm test && npm run build

# In CI
# (workflow runs successfully)
```

✅ Confirm all passing before Phase 3

---

### Phase 3: Deployment Mechanics (~2-3 hours)

**Goal:** Safe, repeatable deployment process

**Zero-Downtime Deployment Strategies:**

#### Strategy A: Blue-Green Deployment
```bash
# Deploy to "green" environment
rsync -avz build/ user@server:/var/www/green/

# Switch symlink atomically
ln -sfn /var/www/green /var/www/current

# Restart services
systemctl reload nginx
```

#### Strategy B: Rolling Deployment
```bash
# Deploy to new release directory
RELEASE_DIR="/var/www/releases/$(date +%Y%m%d%H%M%S)"
mkdir -p $RELEASE_DIR
rsync -avz build/ user@server:$RELEASE_DIR/

# Update current symlink
ln -sfn $RELEASE_DIR /var/www/current

# Keep last 5 releases for rollback
ls -dt /var/www/releases/* | tail -n +6 | xargs rm -rf
```

#### Strategy C: Container-Based (Docker)
```bash
# Build new image
docker build -t myapp:$VERSION .

# Push to registry
docker push myapp:$VERSION

# Update service (zero downtime)
docker service update --image myapp:$VERSION myapp_web

# Health check validates before traffic switch
```

**Rollback Mechanism:**
```bash
# scripts/rollback.sh
#!/bin/bash

CURRENT_RELEASE=$(readlink /var/www/current)
PREVIOUS_RELEASE=$(ls -dt /var/www/releases/* | sed -n '2p')

ln -sfn $PREVIOUS_RELEASE /var/www/current
systemctl reload nginx

echo "Rolled back from $CURRENT_RELEASE to $PREVIOUS_RELEASE"
```

**Database Migration Strategy:**
```bash
# Smart migration runner
if [ -f "database/migrations/latest.sql" ]; then
  if grep -qi "No Schema Changes" "database/migrations/latest.sql"; then
    echo "No database changes needed"
  else
    # Backup before migration
    mysqldump database > backup_$(date +%Y%m%d_%H%M%S).sql

    # Apply migration
    mysql database < database/migrations/latest.sql

    # Verify migration
    php artisan migrate:status
  fi
fi
```

**Test Phase 3:**
```bash
# Deploy to staging
./scripts/deploy.sh staging

# Verify deployment
curl https://staging.your-domain.com/health
# Expected: 200 OK with new version number

# Test rollback
./scripts/rollback.sh
curl https://staging.your-domain.com/health
# Expected: 200 OK with previous version
```

✅ Confirm deployment + rollback working before Phase 4

---

### Phase 4: Production Hardening (~ongoing)

**Goal:** Production-ready with monitoring, secrets, performance

**Secrets Management:**

#### Option A: Environment Variables (Simple)
```yaml
# .github/workflows/deploy.yml
env:
  DATABASE_URL: ${{ secrets.DATABASE_URL }}
  API_KEY: ${{ secrets.API_KEY }}
```

#### Option B: Vault Integration (Enterprise)
```bash
# Fetch from HashiCorp Vault
vault kv get -field=database_url secret/myapp/production
```

#### Option C: Cloud Provider Secrets
```bash
# AWS Secrets Manager
aws secretsmanager get-secret-value --secret-id prod/database --query SecretString
```

**Monitoring & Alerting:**

```yaml
# Example: GitHub Actions with Slack notification
- name: Deploy to Production
  run: ./scripts/deploy.sh production

- name: Notify Slack on Success
  if: success()
  uses: slackapi/slack-github-action@v1
  with:
    payload: |
      {
        "text": "✅ Production deployment successful: ${{ github.sha }}"
      }

- name: Notify Slack on Failure
  if: failure()
  uses: slackapi/slack-github-action@v1
  with:
    payload: |
      {
        "text": "❌ Production deployment FAILED: ${{ github.sha }}"
      }
```

**Performance Optimization:**

```yaml
# Compress assets
- name: Optimize Build
  run: |
    find build -name "*.js" -exec gzip -k {} \;
    find build -name "*.css" -exec gzip -k {} \;

# Cache dependencies
- name: Cache Dependencies
  uses: actions/cache@v4
  with:
    path: node_modules
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

---

## 🚀 Workflow Branching Strategies

### Strategy A: Feature Branch Workflow

**Deployment Triggers:**
- `release/*` branches → Auto-deploy to staging
- `hotfix/*` branches → Auto-deploy to staging
- `master` branch → Manual deploy to production (workflow_dispatch)

```yaml
on:
  push:
    branches:
      - 'release/**'
      - 'hotfix/**'
  workflow_dispatch:  # Manual production deploys only

jobs:
  deploy_staging:
    if: startsWith(github.ref, 'refs/heads/release/') || startsWith(github.ref, 'refs/heads/hotfix/')
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh staging

  deploy_production:
    if: github.event_name == 'workflow_dispatch'
    runs-on: ubuntu-latest
    environment: production  # Requires manual approval
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh production
```

---

### Strategy B: Trunk-Based Development

**Deployment Triggers:**
- `main` branch → Auto-deploy to staging
- Tagged releases → Auto-deploy to production

```yaml
on:
  push:
    branches:
      - main
    tags:
      - 'v*'

jobs:
  deploy_staging:
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh staging

  deploy_production:
    if: startsWith(github.ref, 'refs/tags/v')
    runs-on: ubuntu-latest
    environment: production
    steps:
      - uses: actions/checkout@v4
      - run: ./scripts/deploy.sh production
```

---

## 🐛 Debugging Checklist

**When deployment fails, check in this order:**

1. ✅ **SSH connectivity** - Can CI reach server?
2. ✅ **Permissions** - Does user have file/DB permissions?
3. ✅ **Paths** - Are all paths absolute and correct?
4. ✅ **Environment variables** - Properly quoted, all set?
5. ✅ **Dependency versions** - Match between CI and server?
6. ✅ **Directory structure** - Paths match actual build output?
7. ✅ **Database** - User has required privileges?
8. ✅ **Workflow syntax** - No duplicate jobs, correct conditionals?
9. ✅ **Health checks** - Endpoint responding correctly?
10. ✅ **Logs** - Check application logs, CI logs, server logs

---

## 📋 Best Practices

### 1. Always Use Explicit Paths
```bash
# Good
cd /var/www/vhosts/project/httpdocs
./scripts/deploy.sh

# Bad
cd project
./deploy.sh  # Ambiguous
```

### 2. Test Locally Before CI/CD
```bash
# Run deployment script locally first
SSH_KEY=~/.ssh/id_rsa bash scripts/deploy.sh staging

# Then commit to trigger CI/CD
```

### 3. Version Lock Critical Dependencies
```yaml
# Pin major versions to avoid breaking changes
- uses: actions/checkout@v4          # Not @latest
- uses: actions/upload-artifact@v4   # Specific version
- uses: appleboy/ssh-action@v1.0.3   # Exact version
```

### 4. Document Server Configuration Changes
```markdown
## Server Configuration Change Log
- 2025-10-20: Updated API server to PHP 8.2 FPM
- Reason: Code requires PHP >= 8.2
- Command: plesk bin subdomain --update api -php_handler_id plesk-php82-fpm
```

### 5. Track All Releases (Even Code-Only)
```sql
-- Migration 1.15.0: Feature Release - No Schema Changes
-- Release Date: 2025-10-20
-- Features: PROJ-775, PROJ-772, PROJ-767
-- NO SQL COMMANDS FOR THIS RELEASE
```

---

## 📚 Framework-Specific Examples

**See:** [examples/cicd/](../examples/cicd/) for complete workflow examples:

- `laravel-example.yml` - PHP/Laravel deployment
- `nodejs-example.yml` - Node.js/Express deployment
- `python-example.yml` - Python/Django deployment
- `docker-example.yml` - Containerized deployment
- `COMMON_ERRORS.md` - Common deployment errors and fixes

---

## 🔗 References

- [LEAN_DEVELOPMENT_WORKFLOW.md](LEAN_DEVELOPMENT_WORKFLOW.md) - Incremental development methodology
- [COMMON_ERRORS.md](../examples/cicd/COMMON_ERRORS.md) - Troubleshooting deployment issues
- [BRANCHING_AND_DEPLOYMENT_DETECTION.md](BRANCHING_AND_DEPLOYMENT_DETECTION.md) - Workflow detection

---

**Last Updated:** 2025-10-20 | **Framework Version:** 1.2.0
