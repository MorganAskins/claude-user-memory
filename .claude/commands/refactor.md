---
name: refactor
description: Quick command to invoke refactoring-specialist for safe, incremental code improvements. Identifies code smells and performs behavior-preserving transformations.
---

# /refactor Command

Execute code refactoring using the refactoring-specialist agent.

## Usage

```
/refactor [file or function]
/refactor src/services/user.ts    # Refactor specific file
/refactor UserService             # Refactor specific class
/refactor --smells                # Just detect code smells
/refactor --dry-run               # Show plan without executing
```

## What This Does

1. Invokes `@refactoring-specialist` with your target
2. Analyzes code for quality issues
3. Detects code smells systematically
4. Plans safe, incremental refactoring steps
5. Executes transformations with test verification
6. Commits each change separately for easy rollback

## Code Smells Detected

**Bloaters** (Too Big):
- Long Methods (> 20 lines)
- Large Classes
- Long Parameter Lists
- Data Clumps

**Object-Orientation Issues**:
- Switch Statements
- Refused Bequest
- Alternative Classes

**Change Preventers**:
- Divergent Change
- Shotgun Surgery

**Dispensables**:
- Duplicate Code
- Dead Code
- Lazy Classes

**Couplers**:
- Feature Envy
- Message Chains
- Middle Man

## Refactoring Techniques Applied

- **Extract Method**: Break down long functions
- **Extract Class**: Separate responsibilities
- **Replace Conditional with Polymorphism**: Clean up switch statements
- **Introduce Parameter Object**: Reduce parameter lists
- **Replace Magic Numbers**: Use named constants
- **Decompose Conditional**: Simplify complex conditions

## Output

You'll receive:

- **Code Smells Detected**: List with locations
- **Refactorings Applied**: Before/after for each
- **Metrics Comparison**: LOC, complexity, duplication
- **Commits Made**: Separate commit per change
- **Rollback Instructions**: How to revert
- **Recommendations**: Future improvements

## Examples

```bash
# Refactor a file
/refactor src/services/payment.ts

# Just detect smells (no changes)
/refactor --smells src/

# Preview refactoring plan
/refactor --dry-run src/utils/

# Refactor with specific focus
/refactor --duplication src/
/refactor --complexity src/handlers/

# Refactor recent changes
/refactor --changed
```

## Safety Guarantees

**The Refactoring Loop**:
```
1. ✅ Run tests (must pass)
2. ✅ Make ONE small change
3. ✅ Run tests (must pass)
4. ✅ Commit with descriptive message
5. 🔄 Repeat
```

**If tests fail**: Revert immediately, analyze, try smaller step.

## Before vs After Example

**Before** (Long Method):
```typescript
function processOrder(order) {
  // 50 lines of validation, calculation, notification...
}
```

**After** (Extracted Methods):
```typescript
function processOrder(order) {
  validateOrder(order);
  const total = calculateTotal(order.items);
  await chargeCustomer(order.customer, total);
  await sendConfirmation(order);
}
```

## Time

Typical completion: **5-15 minutes** depending on scope

## Next Steps

After `/refactor` completes:
1. Review the changes made
2. Run full test suite
3. Check that behavior is preserved
4. Push commits (or squash if preferred)
5. Update documentation if needed

---

**Executing command...**

Please invoke: `@refactoring-specialist {args}`

The refactoring-specialist will:
1. Assess code and test coverage
2. Detect code smells systematically
3. Plan safe, incremental changes
4. Execute with test verification at each step
5. Commit changes separately
6. Provide rollback instructions
