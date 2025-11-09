# CI/CD Deployment Guide

**Lean, incremental approach to production deployments**

> **"Deploy the pipeline incrementally, just like you develop code."**

## 🎯 Core Philosophy

Apply the same **lean incremental methodology** to CI/CD setup that you use for development. Set up deployment pipelines in testable phases, not all at once.

**See Also:** [LEAN_DEVELOPMENT_WORKFLOW.md](LEAN_DEVELOPMENT_WORKFLOW.md) for development methodology

---

## ⚠️ CRITICAL: Deployment Safety Questions (Ask BEFORE Implementing)

Before writing ANY deployment code (rsync, Docker, cloud deployment, etc.), Claude MUST ask these questions:

### Safety Verification Protocol

When starting deployment implementation, always ask the user:

```markdown
CLAUDE: "Before I implement your deployment strategy, I need to understand
what data must be preserved. This prevents catastrophic loss during deployments:

1. **Data That Survives Deployments:**
   - What user-generated files exist? (uploads, documents, images, etc.)
   - Are there environment-specific files? (.env, local configs, API keys)
   - Do any files persist between deployments that shouldn't be replaced?
   - Are there third-party integrations with stored data?

2. **Deployment Approach:**
   - Should I DELETE old code, or just REPLACE it?
   - What about cache/temp directories - are they safe to delete?
   - Should logs be preserved across deployments?
   - How many previous releases should be kept for rollback?

3. **Environment Differences:**
   - Does production have different preservation needs than staging?
   - Are development and production configured differently?
   - Are any files specific to particular environments?

4. **Backup & Recovery:**
   - Where can deployment backups be stored?
   - How quickly do you need to rollback if something fails?
   - Are database changes separate from code deployment?

5. **Deployment Method:**
   - Are you using rsync, Docker, cloud deployment, or something else?
   - Is there a centralized storage system (S3, CDN, database)?
   - Are file permissions and ownership important?
```

**Why this matters:** Deployment operations like `rsync --delete` can destroy data if
preservation needs aren't understood. It's better to ask than to guess.

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

**⚠️ SAFETY NOTE:** Before implementing any deployment strategy below, ensure you have answered the [Safety Verification Protocol](#safety-verification-protocol) questions above. Different strategies have different data preservation implications.

**Zero-Downtime Deployment Strategies:**

#### Strategy A: Blue-Green Deployment
```bash
# ✅ SAFE: Deploy to isolated directory
rsync -avz build/ user@server:/var/www/green/

# ⚠️ IF USING --delete: Must exclude preserved data
rsync -avz --delete \
  --exclude='uploads/' \
  --exclude='.env*' \
  --exclude='storage/app/' \
  build/ user@server:/var/www/green/

# ✅ Copy preserved data if migrating from blue
ssh user@server "
  [ -d /var/www/blue/uploads ] && \
    cp -r /var/www/blue/uploads /var/www/green/
"

# Switch symlink atomically
ln -sfn /var/www/green /var/www/current

# Restart services
systemctl reload nginx
```

**Preservation Note:** This strategy keeps both blue and green directories, so you can manually copy preserved files before switching. Ask: *What files need to survive the switch?*

#### Strategy B: Rolling Deployment (Recommended for Data Safety)
```bash
# ✅ SAFEST: Deploy to new release directory (nothing deleted on sync)
RELEASE_DIR="/var/www/releases/$(date +%Y%m%d%H%M%S)"
mkdir -p $RELEASE_DIR

# Deploy WITHOUT --delete (safest approach)
rsync -avz build/ user@server:$RELEASE_DIR/

# ✅ Restore preserved files from previous release
PREV_RELEASE=$(ls -dt /var/www/releases/* 2>/dev/null | head -1)
if [ -n "$PREV_RELEASE" ]; then
  ssh user@server "
    # Copy any preserved directories
    [ -d $PREV_RELEASE/uploads ] && cp -r $PREV_RELEASE/uploads $RELEASE_DIR/ || true
    [ -d $PREV_RELEASE/storage/app ] && cp -r $PREV_RELEASE/storage/app $RELEASE_DIR/storage/ || true
    [ -f $PREV_RELEASE/.env ] && cp $PREV_RELEASE/.env $RELEASE_DIR/ || true
  "
fi

# Update current symlink atomically
ln -sfn $RELEASE_DIR /var/www/current

# Keep last 5 releases for rollback
ssh user@server "ls -dt /var/www/releases/* | tail -n +6 | xargs rm -rf"
```

**Why this is safer:**
- No `--delete` flag means nothing accidental gets removed
- New directory means clean code deployment
- Preserved files copied from previous release
- Atomic symlink switch = zero downtime
- Multiple releases kept for quick rollback

#### Strategy C: Container-Based (Docker)
```bash
# Build new image
docker build -t myapp:$VERSION .

# Push to registry
docker push myapp:$VERSION

# ✅ SAFETY: Update service (zero downtime with named volumes)
docker service update --image myapp:$VERSION myapp_web

# Health check validates before traffic switch
```

**Docker Volume Safety:**
```yaml
# docker-compose.yml - Demonstrates preservation
services:
  web:
    image: myapp:${VERSION}
    volumes:
      # Code: Updated on redeploy
      - ./app:/app/app:ro
      # ✅ Data: Preserved across container restarts
      - uploads_volume:/app/public/uploads
      - storage_volume:/app/storage

volumes:
  uploads_volume:
    driver: local  # Persists on host
  storage_volume:
    driver: local  # Persists on host
```

**Safety Note:** Containers are stateless; use volumes or external storage for data that must survive deployments. Ask: *Are there files/data that need to survive container restarts?*

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

### 1. Answer Safety Questions First ⚠️
Before ANY deployment implementation, answer the [Safety Verification Protocol](#safety-verification-protocol) questions.
Document what data must be preserved and how.

### 2. Always Use Explicit Paths
```bash
# Good
cd /var/www/vhosts/project/httpdocs
./scripts/deploy.sh

# Bad
cd project
./deploy.sh  # Ambiguous
```

### 3. Test Locally Before CI/CD
```bash
# Run deployment script locally first
SSH_KEY=~/.ssh/id_rsa bash scripts/deploy.sh staging

# Then commit to trigger CI/CD
```

### 4. Deployment Strategy Safety
```bash
# ✅ SAFE: rsync without --delete (adds/updates only)
rsync -avz build/ user@server:/var/www/deploy/

# ⚠️ RISKY: rsync with --delete (removes files)
# ONLY use --delete with explicit exclusions
rsync -avz --delete \
  --exclude='uploads/' \
  --exclude='.env*' \
  build/ user@server:/var/www/deploy/

# ✅ SAFEST: Use release directories
RELEASE_DIR="/var/www/releases/$(date +%s)"
rsync -avz build/ user@server:$RELEASE_DIR/
ln -sfn $RELEASE_DIR /var/www/current
```

### 5. Version Lock Critical Dependencies
```yaml
# Pin major versions to avoid breaking changes
- uses: actions/checkout@v4          # Not @latest
- uses: actions/upload-artifact@v4   # Specific version
- uses: appleboy/ssh-action@v1.0.3   # Exact version
```

### 6. Document Server Configuration Changes
```markdown
## Server Configuration Change Log
- 2025-10-20: Updated API server to PHP 8.2 FPM
- Reason: Code requires PHP >= 8.2
- Command: plesk bin subdomain --update api -php_handler_id plesk-php82-fpm
```

### 7. Track All Releases (Even Code-Only)
```sql
-- Migration 1.15.0: Feature Release - No Schema Changes
-- Release Date: 2025-10-20
-- Features: PROJ-775, PROJ-772, PROJ-767
-- NO SQL COMMANDS FOR THIS RELEASE
```

---

## ⚠️ Common Deployment Mistakes & Prevention

| Mistake | Why It Happens | Prevention |
|---------|----------------|-----------|
| **Data loss from rsync --delete** | Forgot to exclude preserved directories | Always list what to preserve first (see Safety Protocol above) |
| **Deleted .env files** | Deployment replaces everything | Use `--exclude='.env*'` or keep .env outside deployment |
| **Lost user uploads** | Sync deletes files not in source | Ask preservation questions BEFORE writing deployment code |
| **No rollback capability** | Deployed directly to active directory | Use release directories with versioning |
| **Cache/logs corruption** | Deleted cache without clearing app | Keep logs/cache separate or handle in code |
| **Database migration failures** | No backup before schema changes | Always backup before database migration deployments |
| **Untested health checks** | Assumed health endpoint works | Test health check endpoint before final deployment |
| **Insufficient permissions** | Files deployed with wrong ownership | Use `chown` or Docker user configuration appropriately |
| **Hard-coded paths** | Script works locally but fails on server | Always use absolute paths in deployment scripts |

**How to avoid:** Answer the [Safety Verification Protocol](#safety-verification-protocol) questions EVERY time.

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
