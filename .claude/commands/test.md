---
name: test
description: Quick command to invoke test-generator for creating comprehensive test suites. Generates unit tests, integration tests, and edge case coverage.
---

# /test Command

Generate tests using the test-generator agent.

## Usage

```
/test [file or function]
/test src/services/user.ts        # Generate tests for file
/test UserService                  # Generate tests for class
/test --coverage                   # Focus on coverage gaps
/test --edge-cases                 # Focus on edge cases
```

## What This Does

1. Invokes `@test-generator` with your target
2. Analyzes code structure and behavior
3. Identifies testing framework in use
4. Generates comprehensive test suite:
   - Unit tests (isolated, fast)
   - Integration tests (component interaction)
   - Edge case tests (boundaries, errors)
5. Runs generated tests to verify they work

## Test Categories Generated

**Unit Tests**:
- Individual functions
- Class methods
- Pure logic

**Integration Tests**:
- API endpoints
- Database operations
- Service interactions

**Edge Cases**:
- Empty inputs
- Null/undefined
- Boundary values
- Error conditions

## Output

You'll receive:

- **Test Strategy**: Coverage goals and approach
- **Generated Test Files**: Complete, runnable tests
- **Test Cases Summary**: What each test covers
- **Coverage Analysis**: Functions and edge cases covered
- **Run Commands**: How to execute the tests

## Examples

```bash
# Generate tests for a file
/test src/utils/validation.ts

# Generate tests for a class
/test PaymentService

# Focus on missing coverage
/test --coverage src/services/

# Generate edge case tests
/test --edge-cases src/api/handlers.ts

# Generate integration tests
/test --integration src/routes/
```

## Testing Patterns

**AAA Pattern** (Arrange-Act-Assert):
```typescript
it('should return user by id', async () => {
  // Arrange
  const userId = '123';
  const expectedUser = { id: userId, name: 'John' };

  // Act
  const result = await userService.getById(userId);

  // Assert
  expect(result).toEqual(expectedUser);
});
```

## Edge Cases Covered

- Empty string `""`
- Empty array `[]`
- `null` / `undefined`
- Zero `0`
- Negative numbers
- Boundary values
- Invalid types
- Network failures
- Timeouts

## Time

Typical completion: **2-5 minutes** depending on code complexity

## Next Steps

After `/test` completes:
1. Review generated tests for accuracy
2. Run tests: `npm test` / `pytest` / etc.
3. Check coverage report
4. Add additional edge cases if needed
5. Commit test files

---

**Executing command...**

Please invoke: `@test-generator {args}`

The test-generator will:
1. Analyze code structure and dependencies
2. Identify testing framework
3. Check existing test coverage
4. Generate comprehensive test suite
5. Run tests to verify they pass
6. Report coverage and any gaps
