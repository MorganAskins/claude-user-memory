---
name: migrate
description: Quick command to invoke migration-specialist for safe database, API, and dependency migrations. Handles schema changes, data migrations, and version upgrades.
---

# /migrate Command

Execute migrations using the migration-specialist agent.

## Usage

```
/migrate [migration type and target]
/migrate database add user_email_column
/migrate api v1 to v2
/migrate dependency react 17 to 18
/migrate --plan-only                    # Just create plan
```

## What This Does

1. Invokes `@migration-specialist` with your target
2. Assesses migration scope and risk
3. Researches upgrade paths via DeepWiki
4. Creates detailed migration plan with rollback
5. Generates migration files for your framework
6. Executes with verification at each step

## Migration Types

**Database Schema**:
- Add/modify/remove columns
- Create/drop indexes
- Change data types
- Add constraints

**Data Migrations**:
- Transform existing data
- Backfill new columns
- Data cleanup

**API Migrations**:
- Version upgrades
- Breaking change handling
- Deprecation management

**Dependency Migrations**:
- Major version upgrades
- Framework migrations
- Platform changes

## Migration Strategies

| Strategy | Downtime | Risk | Use For |
|----------|----------|------|---------|
| Big Bang | Yes | High | Dev/staging |
| Phased | Minimal | Medium | Most cases |
| Zero-Downtime | None | Low | Production |
| Blue-Green | None | Low | Major upgrades |

## Output

You'll receive:

- **Migration Assessment**: Scope, risk, estimated time
- **Detailed Plan**: Step-by-step with rollback
- **Migration Files**: Framework-specific
- **Execution Log**: Each step with verification
- **Data Integrity Report**: Before/after validation
- **Rollback Instructions**: How to revert

## Examples

```bash
# Database: Add column
/migrate database add email_verified boolean to users

# Database: Add index
/migrate database add index on users(email)

# API: Version upgrade
/migrate api v1 to v2 for /users endpoint

# Dependency: Major upgrade
/migrate dependency prisma 4 to 5

# Framework: Major upgrade
/migrate framework next 13 to 14

# Planning only
/migrate --plan-only database rename column
```

## Database Migration Patterns

**Adding Column (Safe)**:
```sql
-- Add nullable first
ALTER TABLE users ADD COLUMN middle_name VARCHAR(100);
-- Backfill
UPDATE users SET middle_name = '' WHERE middle_name IS NULL;
-- Add constraint
ALTER TABLE users ALTER COLUMN middle_name SET NOT NULL;
```

**Renaming Column (Zero-Downtime)**:
```sql
-- 1. Add new column
-- 2. Backfill data
-- 3. Update app to write both
-- 4. Switch reads to new
-- 5. Drop old column
```

## Rollback Plan Included

Every migration includes:
```bash
# Step 1: Stop application
# Step 2: Rollback database/changes
# Step 3: Restore previous code
# Step 4: Restart application
```

**Rollback tested**: Always on staging first

## Time

Typical completion varies by migration type:

| Type | Time |
|------|------|
| Add column | 5-10 min |
| Add index | 5-15 min |
| Rename column | 15-30 min |
| API version | 30-60 min |
| Major dependency | 1-4 hours |

## Safety Rules

**Never**:
- ❌ Migrate without backup
- ❌ Skip staging test
- ❌ Migrate without rollback plan
- ❌ Change schema and data simultaneously

**Always**:
- ✅ Take backup first
- ✅ Test rollback procedure
- ✅ Use transactions
- ✅ Batch large operations
- ✅ Monitor during and after

## Next Steps

After `/migrate` completes:
1. Verify data integrity
2. Test application functionality
3. Monitor for 24 hours
4. Keep backup for X days
5. Update documentation

---

**Executing command...**

Please invoke: `@migration-specialist {args}`

The migration-specialist will:
1. Assess migration scope and risk
2. Research upgrade paths
3. Create detailed plan with rollback
4. Generate framework-specific files
5. Execute with verification
6. Validate data integrity
7. Provide comprehensive report
