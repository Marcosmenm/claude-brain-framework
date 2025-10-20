# Common CI/CD Deployment Errors & Solutions

**Real-world troubleshooting guide for production deployments**

> **Based on production experience across Laravel, Node.js, Python, and Docker deployments**

This document catalogs common errors encountered during CI/CD implementation and their solutions, applicable across frameworks and platforms.

**See Also:** [core/CICD_DEPLOYMENT_GUIDE.md](../../core/CICD_DEPLOYMENT_GUIDE.md) for lean deployment methodology

---

## Table of Contents

1. [SSH Connection Errors](#ssh-connection-errors)
2. [Database Issues](#database-issues)
3. [Output Capture Problems](#output-capture-problems)
4. [Directory Structure Mismatches](#directory-structure-mismatches)
5. [Deprecated GitHub Actions](#deprecated-github-actions)
6. [Runtime Version Mismatches](#runtime-version-mismatches)
7. [Workflow Configuration Errors](#workflow-configuration-errors)
8. [Environment File Issues](#environment-file-issues)
9. [Frontend Build Issues](#frontend-build-issues)
10. [Migration Management](#migration-management)

---

## 1. SSH Connection Errors

### Error: `dial tcp ***:22: i/o timeout`

**Symptom:** GitHub Actions cannot connect to server via SSH

**Root Cause:** Server uses custom SSH port but workflow uses default port 22

**Solution:**
```yaml
# Add port parameter to all ssh-action steps
- uses: appleboy/ssh-action@v1.0.3
  with:
    host: ${{ secrets.HOST }}
    port: 2222  # ← Specify custom port
    username: ${{ secrets.USER }}
    key: ${{ secrets.SSH_KEY }}
```

**Lesson Learned:** Always verify custom SSH ports and explicitly configure them

---

## 2. Database Issues

### Error: `mysqldump: insufficient privileges to SHOW CREATE PROCEDURE`

**Symptom:** Database backup fails during deployment

**Root Cause:** Database user lacks SELECT privilege on `mysql.proc` table

**Solution Option A** (Grant privileges):
```sql
GRANT SELECT ON mysql.proc TO 'dbuser'@'%';
FLUSH PRIVILEGES;
```

**Solution Option B** (Adjust backup command):
```bash
# Remove --routines and --triggers from mysqldump
mysqldump -u user -p database > backup.sql

# Instead of:
# mysqldump -u user -p --routines --triggers database > backup.sql
```

**Framework-Specific:**
- **PostgreSQL:** `pg_dump dbname > backup.sql` (no special privileges needed)
- **MongoDB:** `mongodump --db dbname --out backup/`
- **SQLite:** `cp database.sqlite database_backup.sqlite`

**Lesson Learned:** Backup users need more than table-level permissions

---

### Error: `Base table or view already exists: Table 'users' already exists`

**Symptom:** Migrations try to create existing tables during deployment

**Root Cause:** Deployment script falls back to running all migrations when it can't find specific migration

**Solution:** Create intelligent migration runner

```bash
#!/bin/bash
# scripts/run-sql-migrations.sh

LATEST_MIGRATION=$(find database/migrations -name "*.sql" -type f | sort -V | tail -n 1)

# Check for "No Schema Changes" marker
if grep -qi "No Schema Changes" "$LATEST_MIGRATION"; then
    echo "No database changes needed"
    exit 0
fi

# Apply migration
mysql -u $DB_USERNAME -p$DB_PASSWORD $DB_DATABASE < "$LATEST_MIGRATION"
```

**Framework-Specific:**
- **Laravel:** `php artisan migrate --force`
- **Node.js (Knex):** `npx knex migrate:latest`
- **Python (Django):** `python manage.py migrate`
- **Python (Alembic):** `alembic upgrade head`

**Lesson Learned:** Differentiate between code-only releases and schema changes

---

## 3. Output Capture Problems

### Error: `cd: File name too long`

**Symptom:** Directory path variable contains entire command output including ANSI color codes

**Root Cause:** Bash command substitution `$(function)` captures ALL stdout, including log messages

**Bad Code:**
```bash
log() {
    echo -e "${GREEN}[INFO] $1${NC}"  # Goes to stdout
}

prepare_release() {
    log "Preparing release..."
    # ... commands ...
    echo "$release_dir"  # Intended return value
}

release_dir=$(prepare_release)  # Captures EVERYTHING from stdout ❌
```

**Solution:**
```bash
log() {
    echo -e "${GREEN}[INFO] $1${NC}" >&2  # Redirect to stderr
}

prepare_release() {
    log "Preparing release..."
    composer install >&2  # Redirect command output too
    echo "$release_dir"  # Only this goes to stdout
}

release_dir=$(prepare_release)  # Now captures only the path ✅
```

**Lesson Learned:** When using command substitution, redirect all non-return-value output to stderr (`>&2`)

---

## 4. Directory Structure Mismatches

### Error: `find: 'build/static': No such file or directory`

**Symptom:** Build optimization step fails looking for files in wrong directory

**Root Cause:** Build tool outputs to different structure than workflow expects

**Solution:**
```yaml
# Verify actual build output structure first
- name: Optimize Build
  run: |
    # Check what actually exists
    ls -R build/

    # Use correct path or make it flexible
    find build -name "*.js" -exec gzip -k {} \; || true
```

**Framework-Specific Build Outputs:**
- **React (CRA):** `build/`
- **Next.js:** `.next/` and `out/`
- **Vue.js:** `dist/`
- **Angular:** `dist/project-name/`
- **Laravel Mix:** `public/js/`, `public/css/`

**Lesson Learned:** Verify actual build tool output structure before writing deployment scripts

---

## 5. Deprecated GitHub Actions

### Error: `This request uses deprecated version of actions/upload-artifact: v3`

**Symptom:** Workflow fails immediately at artifact upload/download steps

**Root Cause:** GitHub deprecated v3 of artifact actions (April 2024)

**Solution:**
```yaml
# Update all artifact actions from v3 to v4
- uses: actions/upload-artifact@v4    # was @v3
  with:
    name: build-artifacts
    path: build/

- uses: actions/download-artifact@v4  # was @v3
  with:
    name: build-artifacts
    path: build/
```

**Lesson Learned:** Regularly audit and update GitHub Actions versions

---

## 6. Runtime Version Mismatches

### Error: `Your dependencies require PHP >= 8.2. You are running 8.1.23`

**Symptom:** Application loads but returns 500 errors, CLI commands fail

**Root Cause:** Web server configured for older runtime version than code requires

**Solution (Framework-Specific):**

#### **PHP / Laravel (Plesk)**
```bash
# Update subdomain PHP handler
/usr/sbin/plesk bin subdomain --update subdomain-name \
  -domain main-domain.com \
  -php_handler_id plesk-php82-fpm

# Restart PHP-FPM
systemctl restart plesk-php82-fpm
```

#### **Node.js (nvm)**
```bash
# Set Node version
nvm install 20.10.0
nvm use 20.10.0
nvm alias default 20.10.0

# Verify
node --version  # Should match package.json engines
```

#### **Python (pyenv)**
```bash
# Install and set Python version
pyenv install 3.11.5
pyenv global 3.11.5

# Verify
python --version
```

**Lesson Learned:** Deployment script runtime must match web server runtime

---

## 7. Workflow Configuration Errors

### Error: Duplicate job names

**Symptom:** Workflow fails with YAML parsing error

**Root Cause:** Job names must be unique within workflow file

**Bad Code:**
```yaml
jobs:
  build_staging:  # Line 57
    if: startsWith(github.ref, 'refs/heads/release/')
    ...

  build_staging:  # Line 145 - DUPLICATE! ❌
    if: github.ref == 'refs/heads/staging'
    ...
```

**Solution:** Remove duplicate or rename
```yaml
jobs:
  build_staging_release:
    if: startsWith(github.ref, 'refs/heads/release/')
    ...

  build_staging_branch:
    if: github.ref == 'refs/heads/staging'
    ...
```

**Lesson Learned:** Audit workflows for duplicate job names before committing

---

### Error: Deployments triggering on wrong branches

**Symptom:** Unintended auto-deployments from wrong branches

**Root Cause:** Job conditionals too permissive

**Solution:** Strictly enforce branch-based deployment rules
```yaml
# Feature Branch Workflow: ONLY release branches auto-deploy
on:
  push:
    branches:
      - 'release/**'  # ✅ Auto-deploy these
      - 'hotfix/**'   # ✅ Auto-deploy these
      # NO main, NO staging, NO feature branches

deploy_production:
  if: github.event_name == 'workflow_dispatch'  # ✅ Manual only
  environment: production
  steps:
    - uses: actions/checkout@v4
    - run: ./scripts/deploy.sh production
```

**Lesson Learned:** Match workflow triggers to your branching strategy

**See Also:** [BRANCHING_AND_DEPLOYMENT_DETECTION.md](../../core/BRANCHING_AND_DEPLOYMENT_DETECTION.md)

---

## 8. Environment File Issues

### Error: Bash cannot source .env file

**Symptom:** `source .env` command fails with syntax errors

**Root Cause:** Special characters in environment variables not properly quoted

**Bad Code:**
```bash
# .env file
MAIL_PASSWORD=VY2pa&$XMCGT^8dk%e4z6bYY  # Unquoted special chars ❌
```

**Solution:**
```bash
# .env file
MAIL_PASSWORD="VY2pa&$XMCGT^8dk%e4z6bYY"  # Quoted ✅

# Or use single quotes to prevent expansion
MAIL_PASSWORD='VY2pa&$XMCGT^8dk%e4z6bYY'
```

**Lesson Learned:** Always quote environment variable values containing special characters

---

## 9. Frontend Build Issues

### Error: ESLint can't find TypeScript config during CI

**Symptom:** `ESLint couldn't find config "@typescript-eslint/recommended"`

**Root Cause:** Dependencies installed but ESLint plugin not resolving in CI environment

**Quick Solution** (non-blocking):
```yaml
- name: Lint Code
  run: npm run lint || echo "Linting completed with warnings"
  continue-on-error: true  # Don't block deployment
```

**Proper Solution** (fix dependencies):
```json
// Verify package.json has correct devDependencies
{
  "devDependencies": {
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "eslint": "^8.57.0"
  }
}
```

**Lesson Learned:** Make linting/testing non-blocking initially, fix properly later

---

## 10. Migration Management

### Error: Migration executed but marked as "No Schema Changes"

**Symptom:** Confusion about whether migration needs to run

**Solution:** Track all releases with migration files, even code-only

**Example Migration File:**
```sql
-- Migration 1.15.0: Feature Release - No Schema Changes
-- Release Date: 2025-10-20
-- This release includes code-only features with NO database modifications.

/* INCLUDED FEATURES */
-- PROJ-775: CI/CD Pipeline Implementation
-- PROJ-772: Feature Update
-- PROJ-767: Bug Fix

-- NO SQL COMMANDS TO EXECUTE FOR THIS RELEASE
```

**Lesson Learned:** Document all releases, even without schema changes

---

## 🐛 Debugging Checklist

**When deployment fails, check in this order:**

1. ✅ **SSH connectivity** - Can GitHub Actions reach server?
2. ✅ **Permissions** - Does deployment user have file/DB permissions?
3. ✅ **Paths** - Are all paths absolute and correct?
4. ✅ **Runtime version** - Does deployment match web server version?
5. ✅ **Environment files** - Are .env values quoted correctly?
6. ✅ **Directory structure** - Do paths match actual build output?
7. ✅ **Dependencies** - Are all required packages installed?
8. ✅ **Database** - Does user have required privileges?
9. ✅ **Workflow syntax** - No duplicate jobs, correct conditionals?
10. ✅ **Logs** - Check application logs, CI logs, server logs

---

## 📋 General Best Practices

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
SSH_KEY=~/.ssh/id_rsa bash scripts/deploy.sh

# Then commit to trigger CI/CD
```

### 3. Use Descriptive Error Messages
```bash
# Good
error "Database backup failed: insufficient privileges on mysql.proc table"

# Bad
error "Backup failed"
```

### 4. Document Server Configuration Changes
```markdown
## Server Configuration Change Log
- 2025-10-20: Updated API server to PHP 8.2 FPM
- Reason: Code requires PHP >= 8.2 (dependency requirements)
- Command: plesk bin subdomain --update api -php_handler_id plesk-php82-fpm
```

### 5. Version Lock Critical Dependencies
```yaml
# Pin major versions to avoid breaking changes
- uses: actions/checkout@v4          # Not @latest
- uses: actions/upload-artifact@v4   # Specific version
- uses: appleboy/ssh-action@v1.0.3   # Exact version
```

---

## 📚 Framework-Specific Examples

**Complete workflow examples available:**

- [laravel-example.yml](laravel-example.yml) - PHP/Laravel deployment
- [nodejs-example.yml](nodejs-example.yml) - Node.js/Express deployment
- [python-example.yml](python-example.yml) - Python/Django deployment
- [docker-example.yml](docker-example.yml) - Container-based deployment

---

## 🔗 References

- [CICD_DEPLOYMENT_GUIDE.md](../../core/CICD_DEPLOYMENT_GUIDE.md) - Lean deployment methodology
- [LEAN_DEVELOPMENT_WORKFLOW.md](../../core/LEAN_DEVELOPMENT_WORKFLOW.md) - Incremental development
- [BRANCHING_AND_DEPLOYMENT_DETECTION.md](../../core/BRANCHING_AND_DEPLOYMENT_DETECTION.md) - Workflow strategies

---

**Last Updated:** 2025-10-20 | **Framework Version:** 1.2.0
