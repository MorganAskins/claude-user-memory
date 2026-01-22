---
name: commit
description: Quick command to invoke commit-validator for pre-commit validation and clean commits. Runs pre-commit hooks, auto-fixes issues, and prepares code for commit.
---

# /commit Command

Run pre-commit validation and prepare code for a clean commit.

## Usage

```
/commit
/commit --check     # Dry run, don't commit
/commit --fix-only  # Fix issues, don't commit
```

## Prerequisites

⚠️ **Best used after**:
- Implementation complete (from `/implement`)
- Tests passing
- Ready to commit changes

## What This Does

1. **Environment Check**
   - Verifies pre-commit is installed
   - Checks for `.pre-commit-config.yaml`
   - Installs hooks if needed

2. **Run Pre-Commit Hooks**
   - Executes `pre-commit run --all-files`
   - Captures all hook results
   - Identifies auto-fixed files

3. **Auto-Fix Issues**
   - Applies formatter fixes (black, prettier, etc.)
   - Removes trailing whitespace
   - Fixes end-of-file newlines
   - Re-runs to verify fixes

4. **Fix Remaining Issues** (up to 3 attempts)
   - Attempt 1: Targeted fixes for linting errors
   - Attempt 2: Alternative approaches
   - Attempt 3: Minimal compliance (with documentation)

5. **Stage and Commit**
   - Stages all modified files
   - Creates commit with descriptive message
   - Reports commit hash and summary

## Examples

```bash
# Full validation and commit
/commit

# Check without committing (dry run)
/commit --check

# Fix issues but don't commit
/commit --fix-only

# After implementation workflow
/implement
/commit
```

## Output

You'll receive:

### On Success ✅
```
✅ Pre-commit validation complete

Hooks passed: 7/7
Auto-fixes applied: 3 files
Manual fixes: 0

✅ Changes committed: abc1234

Files: 5 changed, +245 -12
Message: feat: Add Redis caching to ProductService

Commands:
  git show HEAD     # View commit
  git push          # Push to remote
```

### On Partial Success ⚠️
```
⚠️ Pre-commit validation partially complete

Hooks passed: 5/7
Auto-fixes applied: 3 files
Remaining issues: 2

Blocking Issues:
1. src/auth.py:45 - Type error (needs manual fix)
2. tests/test_api.py:120 - Security warning

Manual action required before commit.
```

### On Failure ❌
```
❌ Pre-commit validation failed

Hooks failed: 3/7
Issues: 15

Critical Issues:
- 8 type errors in src/
- 5 linting errors
- 2 security warnings

Recommendation:
1. Fix type errors first
2. Run /commit again
```

## Pre-Commit Hooks Supported

**Code Formatters**:
- black, autopep8, isort (Python)
- prettier (JavaScript/TypeScript/JSON/YAML/Markdown)
- gofmt (Go)
- rustfmt (Rust)

**Linters**:
- ruff, flake8, pylint (Python)
- eslint (JavaScript/TypeScript)
- golint (Go)
- clippy (Rust)

**Type Checkers**:
- mypy, pyright (Python)
- typescript (JavaScript)

**Security**:
- bandit (Python)
- safety (dependencies)
- detect-secrets
- semgrep

**General**:
- trailing-whitespace
- end-of-file-fixer
- check-yaml, check-json
- check-merge-conflict

## ⛔ Safety Guarantee

The commit-validator will **NEVER** run destructive git commands:
- `git checkout -- .` / `git checkout .` (destroys changes)
- `git reset --hard` (destroys commits and changes)
- `git clean -f` (destroys untracked files)
- `git restore .` (destroys changes)
- `git stash` (without explicit user request)

If validation repeatedly fails, the agent will **report the issue and ask you** rather than discarding your work.

## Self-Correction Protocol

If hooks fail, commit-validator will:

**Attempt 1** (targeted fix):
- Analyze specific error messages
- Apply targeted fixes for each issue type
- Re-run pre-commit

**Attempt 2** (alternative approach):
- Try different fix strategies
- Adjust configurations if needed
- Re-run pre-commit

**Attempt 3** (minimal compliance):
- Add documented ignore comments where necessary
- Focus on getting to a committable state
- Document remaining issues for follow-up

**After 3 failures**:
- Report all remaining issues
- Provide specific fix recommendations
- Block commit until manual intervention

## Time

Typical completion:

| Scenario | Time |
|----------|------|
| Clean code | 30 seconds |
| Minor fixes | 1-2 minutes |
| Multiple issues | 3-4 minutes |
| Complex fixes | 5+ minutes |

## Creating Pre-Commit Config

If no `.pre-commit-config.yaml` exists, the agent will offer to create one:

**Python Project**:
```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-json

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.9
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
```

**JavaScript/TypeScript Project**:
```yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-json

  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.1.0
    hooks:
      - id: prettier

  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v8.56.0
    hooks:
      - id: eslint
```

## Integration with /workflow

When used as part of `/workflow`, commit validation becomes the final phase:

```
/workflow Add feature X

Phases:
1. Research (@docs-researcher)
2. Planning (@implementation-planner)
3. Implementation (@code-implementer)
4. Commit Validation (@commit-validator)  ← NEW

Result: Complete, committed, quality-validated code
```

## Troubleshooting

**pre-commit not found**:
```bash
# Install pre-commit
pip install pre-commit

# Or with pipx
pipx install pre-commit
```

**Hooks failing to install**:
```bash
# Clean and reinstall
pre-commit clean
pre-commit install --install-hooks
```

**Timeout on large codebase**:
```bash
# Run on changed files only
pre-commit run --files $(git diff --name-only)
```

**Conflicting formatter settings**:
- Check for multiple formatter configs
- Ensure consistent settings across tools
- Remove duplicate formatters

## Next Steps

After `/commit` completes:

**On Success**:
1. ✅ Review commit: `git show HEAD`
2. ✅ Push to remote: `git push origin [branch]`
3. ✅ Create PR if on feature branch
4. ✅ Deploy if appropriate

**On Failure**:
1. ❌ Review reported issues
2. ❌ Fix blocking problems manually
3. ❌ Run `/commit` again
4. ❌ Consider `/debug` for complex issues

---

**Executing command...**

Please invoke: `@commit-validator`

The commit-validator will:
1. Check pre-commit environment
2. Run all configured hooks
3. Auto-fix what can be auto-fixed
4. Fix remaining issues (up to 3 attempts)
5. Stage and commit changes

**Protection**: Quality gates prevent committing broken code
