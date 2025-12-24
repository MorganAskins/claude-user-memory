---
name: debug
description: Quick command to invoke brahma-investigator for systematic debugging. Performs root cause analysis with 3-retry protocol and think tool.
---

# /debug Command

Execute systematic debugging using the brahma-investigator agent.

## Usage

```
/debug [error or symptom description]
/debug "TypeError: Cannot read property 'x' of undefined"
/debug "API returns 500 on POST /users"
/debug "Tests failing in CI but passing locally"
/debug --production                 # Production incident mode
```

## What This Does

1. Invokes `@brahma-investigator` with your issue
2. Applies systematic debugging methodology:
   - Problem definition
   - Evidence collection
   - Hypothesis generation
   - Systematic testing (3-retry protocol)
   - Root cause confirmation
3. Uses Anthropic think protocol for complex issues
4. Documents findings and creates regression test

## Think Protocol Modes

| Mode | Duration | Use For |
|------|----------|---------|
| think | 30-60s | Clear error messages |
| think hard | 1-2min | Multi-component failures |
| think harder | 2-4min | Production incidents |

## 3-Retry Strategy

**Attempt 1** (think mode):
- Test most likely hypothesis
- Add logging for visibility
- 15 minute timeout

**Attempt 2** (think hard mode):
- Analyze why Attempt 1 failed
- Try alternative hypothesis
- 20 minute timeout

**Attempt 3** (think harder mode):
- Question fundamental assumptions
- Try completely different approach
- 30 minute timeout

**If all fail**: Escalate with complete investigation report

## Output

You'll receive:

- **Investigation Report**: Complete analysis
- **Root Cause**: Proven cause with evidence
- **Fix Applied**: Code change with reasoning
- **Regression Test**: Prevents recurrence
- **Knowledge Update**: Pattern documented

## Examples

```bash
# Debug an error
/debug "Connection refused on localhost:5432"

# Debug test failure
/debug "test_user_creation fails with timeout"

# Debug production issue
/debug --production "Spike in 500 errors since 2pm"

# Debug performance issue
/debug "API response time increased 3x"

# Debug flaky test
/debug "test_async_handler passes 80% of time"
```

## Common Investigation Patterns

**Test Failure**:
1. Check code under test first (not test)
2. Verify test dependencies
3. Add debug logging to code
4. Reproduce locally

**Production Error**:
1. Check recent deployments
2. Review error logs and metrics
3. Identify affected scope
4. Implement fix with safety checks

**Performance Issue**:
1. Profile to find bottleneck
2. Check database queries
3. Analyze external calls
4. Test optimization locally

## Investigation Report Format

```markdown
## Problem Statement
- Error: [exact error]
- Impact: [users affected]
- Frequency: [how often]

## Investigation Timeline
### Attempt 1-3
[Hypothesis, test, result for each]

## Root Cause
- Proven cause: [specific issue]
- Location: file.ts:42

## Fix Applied
[Before/after code]

## Prevention
- Regression test added
- Pattern documented
```

## Time

Typical completion: **10-30 minutes** depending on complexity

## Next Steps

After `/debug` completes:
1. Verify fix resolves the issue
2. Review regression test
3. Check for similar issues elsewhere
4. Deploy fix (if production issue)
5. Update runbooks if applicable

---

**Executing command...**

Please invoke: `@brahma-investigator {args}`

The brahma-investigator will:
1. Define problem clearly
2. Collect evidence systematically
3. Generate ranked hypotheses
4. Test with 3-retry protocol
5. Confirm root cause with proof
6. Apply fix and create regression test
7. Document in knowledge-core.md
