---
name: review
description: Quick command to invoke code-reviewer for thorough code review. Analyzes code for quality, security, maintainability, and best practices.
---

# /review Command

Execute code review using the code-reviewer agent.

## Usage

```
/review [file or directory]
/review                     # Review recent changes
/review src/auth            # Review specific directory
/review --security          # Focus on security
/review --pr 123            # Review PR #123
```

## What This Does

1. Invokes `@code-reviewer` with your target
2. Performs systematic review:
   - Security analysis (OWASP Top 10)
   - Correctness checks
   - Performance review
   - Maintainability assessment
   - Style & conventions
3. Generates detailed review report
4. Provides actionable recommendations

## Review Focus Areas

**Security** (Critical):
- Injection vulnerabilities
- Authentication issues
- Data exposure risks
- Dependency vulnerabilities

**Correctness** (High):
- Logic errors
- Edge cases
- Error handling
- Type safety

**Performance** (Medium):
- N+1 queries
- Unnecessary computations
- Caching opportunities

**Maintainability** (Medium):
- Code duplication
- Complexity
- Naming clarity

## Output

You'll receive a comprehensive review including:

- **Overall Assessment**: APPROVE / REQUEST CHANGES / BLOCK
- **Critical Issues**: Must fix before merge
- **Recommendations**: Should fix
- **Minor Suggestions**: Nice to have
- **What's Good**: Positive observations
- **Metrics**: Issue counts by severity
- **Checklist**: Action items for author

## Examples

```bash
# Review all changed files
/review

# Review specific file
/review src/services/payment.ts

# Review with security focus
/review --security src/auth/

# Review a pull request
/review --pr 42
```

## Severity Levels

| Level | Meaning | Action |
|-------|---------|--------|
| 🔴 Critical | Security vuln, data loss risk | Must fix |
| 🟡 Major | Bug, performance issue | Should fix |
| 🟢 Minor | Style, convention | Nice to have |
| ✨ Positive | Good practice | Acknowledged |

## Time

Typical completion: **2-5 minutes** depending on scope

## Next Steps

After `/review` completes:
1. Address critical issues first
2. Consider major recommendations
3. Optionally address minor suggestions
4. Re-run `/review` to verify fixes

---

**Executing command...**

Please invoke: `@code-reviewer {args}`

The code-reviewer will:
1. Analyze code systematically by priority
2. Check OWASP Top 10 for security-sensitive code
3. Verify patterns against DeepWiki
4. Generate actionable review report
5. Provide clear approve/reject decision
