---
name: rebase
description: Interactive git rebase that resolves conflicts with clear upstream/yours labeling. Rebases against main/master or an explicit target branch with user guidance at every conflict.
---

# /rebase Command

Interactively rebase your current branch onto a target branch with guided conflict resolution.

## Usage

```
/rebase                    # Rebase onto main/master (auto-detected)
/rebase develop            # Rebase onto specific branch
/rebase origin/release-2.0 # Rebase onto specific remote branch
```

## Prerequisites

- Clean working tree (no uncommitted changes)
- On the feature branch you want to rebase
- Remote is fetched (agent will fetch automatically)

## What This Does

1. **Pre-Flight Checks**
   - Verifies clean working tree
   - Smart target branch detection (3-tier):
     1. PR base branch via `gh pr view` (most accurate — knows the PR target)
     2. Repo default branch via `gh repo view` (fallback if no PR exists)
     3. Local heuristic: `origin/HEAD` → `origin/main` → `origin/master`
   - Fetches all remotes with prune (`git fetch --all --prune`)
   - Shows divergence (how many commits to replay, how far behind)
   - Warns if branch is published (rebase rewrites history)

2. **Safety Backup**
   - Creates `backup/<branch>-pre-rebase-<timestamp>` branch
   - Always restorable if something goes wrong

3. **Rebase Execution**
   - Runs `git rebase origin/<target>`
   - If clean: reports success immediately

4. **Interactive Conflict Resolution** (if conflicts arise)
   - Shows which commit is being replayed (N of M)
   - For each conflicted file, clearly labels:
     - **UPSTREAM** version (what's on the target branch)
     - **YOUR** version (what your commit is changing)
   - Asks you to choose: keep upstream, keep yours, combine, skip commit, or abort
   - Verifies no conflict markers remain before continuing
   - Repeats for each commit with conflicts

5. **Post-Rebase Verification**
   - Shows rebased commit log
   - Compares against backup to verify nothing was lost
   - Recommends next steps (test, push with --force-with-lease)

## Examples

```bash
# Standard rebase onto default branch
/rebase

# Rebase onto a release branch
/rebase release/v3.0

# Rebase onto develop
/rebase develop
```

## Conflict Resolution Options

At each conflict, you'll be offered:

| Option | What It Does |
|--------|-------------|
| **Keep UPSTREAM** | Discards your changes for this file, keeps target branch version |
| **Keep YOURS** | Keeps your commit's changes, discards target branch version |
| **Combine** | Agent helps you manually merge both versions |
| **More context** | Shows full diffs and file history |
| **Skip commit** | Drops this commit entirely from the rebase |
| **Abort** | Cancels rebase, restores pre-rebase state |

## Why ours/theirs is confusing

During rebase, git SWAPS the meaning of ours/theirs compared to merge:
- `--ours` = the upstream/target branch (NOT your code)
- `--theirs` = YOUR commits being replayed

This agent always labels them clearly as **"upstream"** and **"your changes"** so you never have to remember the swap.

## Output

### On Clean Rebase ✅
```
✅ Rebase completed successfully!

   7 commits replayed onto origin/main
   No conflicts encountered.

   Backup: backup/feat/my-feature-pre-rebase-20260312-143022

   Next: git push --force-with-lease origin feat/my-feature
```

### On Conflicts (Interactive) ⚠️
```
⚠️ CONFLICT while replaying commit 3 of 7

   Commit: abc1234 - Add user validation

   Files with conflicts:
     ✗ src/services/auth.py
     ✗ src/utils/validation.py

   [Shows each conflict with clear upstream/yours labels]
   [Asks for your decision on each file]
```

### On Abort 🛑
```
🛑 Rebase aborted. Branch restored to pre-rebase state.
   Backup still available: backup/feat/my-feature-pre-rebase-...
```

## Safety Guarantees

- **Backup always created** before rebase starts
- **Never auto-resolves** conflicts without your approval
- **Never force pushes** — only recommends `--force-with-lease`
- **Never deletes** your backup branch
- **Abort always available** at any point during conflict resolution
- **Never runs** destructive git commands (checkout --, reset --hard, clean -f)

## Recovering from a Stuck Rebase

If you're already in the middle of a rebase:
```
/rebase
```
The agent will detect the in-progress rebase and help you finish it.

## Bulk Resolution

If many conflicts recur in the same files, the agent will offer:
- **Auto-prefer YOUR changes** for remaining conflicts
- **Auto-prefer UPSTREAM** for remaining conflicts
- **Continue one-by-one** (default)

## Time

| Scenario | Time |
|----------|------|
| Clean rebase (no conflicts) | 15-30 seconds |
| Few conflicts (1-3 files) | 2-5 minutes |
| Many conflicts | 5-15 minutes |
| Large rebase (50+ commits) | Depends on conflicts |

## Next Steps

After `/rebase` completes:

1. **Run tests** to verify nothing broke
2. **Push** with `git push --force-with-lease origin <branch>`
3. **Clean up backup** when confident: `git branch -d backup/<branch>-pre-rebase-...`
4. **Update PR** if one exists (the push will update it automatically)

## Troubleshooting

**"Working tree has uncommitted changes"**:
- Commit or stash your changes first
- `git stash` → `/rebase` → `git stash pop`

**"Branch appears to be published"**:
- Rebasing rewrites history — only safe if you own the branch
- After rebase, push with `--force-with-lease` (NOT `--force`)

**Repeated conflicts on same files**:
- Consider enabling `git rerere` for automatic resolution replay
- `git config --global rerere.enabled true`

**Want to undo the rebase**:
```bash
git reset --hard backup/<branch>-pre-rebase-<timestamp>
```

---

**Executing command...**

Please invoke: `@rebase-assistant`

The rebase-assistant will:
1. Run pre-flight checks (clean tree, detect target branch)
2. Create a safety backup branch
3. Start the rebase
4. Guide you through each conflict interactively
5. Verify the result and recommend next steps

Target branch: `{args}` (or auto-detected main/master if not specified)
