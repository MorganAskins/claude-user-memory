---
name: pr-feedback
description: Quick command to analyze GitHub PR feedback from Copilot, reviewers, and bots. Triages comments and creates actionable implementation plans.
---

# /pr-feedback Command

Analyze PR feedback and create an implementation plan for valid suggestions.

## Usage

```
/pr-feedback              # Analyze current branch's PR
/pr-feedback 123          # Analyze PR #123
/pr-feedback --copilot    # Focus on Copilot suggestions only
/pr-feedback --plan       # Output as implementation plan
```

## What This Does

1. Fetches ALL comments on the PR:
   - GitHub Copilot suggestions
   - Human reviewer comments
   - CI/linter bot feedback
   - Security scanner results

2. Validates each suggestion:
   - Reads the actual code
   - Checks against project conventions
   - Verifies with DeepWiki when needed
   - Cross-references multiple reviewers

3. Categorizes feedback:
   - ✅ **Valid**: Should be implemented
   - ❌ **Invalid**: False positive with explanation
   - 🤔 **Discuss**: Needs human decision

4. Creates prioritized implementation plan

## Common Use Case

You opened a PR and Copilot left 15 comments. Instead of manually reviewing each one:

```
/pr-feedback

→ Analyzes all 15 Copilot comments
→ Finds 8 are valid, 5 are false positives, 2 need discussion
→ Creates prioritized fix plan for the 8 valid ones
→ Explains why the 5 are wrong (so you can dismiss them)
```

## Output

### Feedback Summary
- Total comments analyzed
- Valid suggestions (with fixes)
- Invalid suggestions (with explanations)
- Items needing discussion

### Implementation Plan
- Prioritized list of changes
- Estimated time per fix
- Commands to start implementing

### Dismissal Explanations
- Why each invalid suggestion is wrong
- Useful for responding to reviewers

## Examples

```bash
# Analyze current PR's feedback
/pr-feedback

# Analyze specific PR
/pr-feedback 42

# Focus only on Copilot (ignore human comments)
/pr-feedback --copilot

# Generate implementation plan format
/pr-feedback --plan

# Combination
/pr-feedback 42 --copilot --plan
```

## Copilot-Specific Handling

The agent knows Copilot's patterns:

**Usually Valid**:
- Null/undefined checks
- Error handling gaps
- Security improvements
- Resource cleanup

**Often False Positives**:
- Style changes conflicting with project
- Over-engineering suggestions
- Generic "could be simplified" comments
- Outdated pattern recommendations

## Priority Levels

| Level | Examples | Action |
|-------|----------|--------|
| 🔴 Critical | Security issues, data loss bugs | Fix immediately |
| 🟡 High | Logic bugs, performance issues | Fix before merge |
| 🟢 Medium | Maintainability, test coverage | Should fix |
| ⚪ Low | Style, documentation | Nice to have |

## Time

Typical completion: **1-3 minutes** depending on comment volume

## Workflow Integration

### Standalone Usage
```
/pr-feedback
# Review output, then manually fix issues
```

### With Implementation
```
/pr-feedback --plan
# Creates detailed plan, then:
/implement
# Executes the plan
```

### Full Automation
```
/workflow Analyze PR feedback and address valid suggestions
# Runs: pr-feedback → plan → implement
```

## Next Steps

After `/pr-feedback` completes:

1. **Review invalid suggestions** - Dismiss them on GitHub with the explanations
2. **Discuss flagged items** - Get team input on subjective suggestions
3. **Implement valid fixes** - Use `/implement` or fix manually
4. **Request re-review** - Push changes and notify reviewers

## Comparison with /review

| Command | Purpose | Direction |
|---------|---------|-----------|
| `/review` | Generate feedback on code | Code → Comments |
| `/pr-feedback` | Analyze existing feedback | Comments → Action |

Use `/review` to create reviews. Use `/pr-feedback` to act on reviews.

---

**Executing command...**

Please invoke: `@pr-feedback-analyst {args}`

The pr-feedback-analyst will:
1. Detect current PR or use provided number
2. Fetch all comments via `gh` CLI
3. Categorize by source (Copilot, human, bot)
4. Validate each against actual codebase
5. Create prioritized implementation plan
6. Explain why invalid suggestions should be ignored
