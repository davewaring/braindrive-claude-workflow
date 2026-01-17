# Phase 5: Test

## Purpose

Verify the build meets requirements through continuous and final acceptance testing. This phase ensures quality before declaring the feature complete.

## Two Testing Approaches

### 5.1 Continuous Verification (During Build)

Integrated into each phase via `/milestone-check`.

- Run after each phase completes
- Execute success criteria commands
- Compare actual vs expected results
- Loop back to fix failures before proceeding

This happens during Phase 4 (Build) and ensures each phase is solid before moving on.

### 5.2 Final Acceptance (After Build)

Comprehensive validation after all phases complete.

| Test Type | Description | How |
|-----------|-------------|-----|
| **Integration Tests** | Components work together | Automated test suite |
| **User Acceptance** | Meets user stories from spec | Manual or Playwright |
| **Regression** | Existing functionality still works | Full test suite |
| **Edge Cases** | Handles boundary conditions | Targeted tests |

## The Test Loop

```
Run all tests →
    All pass? → Proceed to Learn
    Failures? →
        Diagnose root cause →
        Fix in Build phase →
        Re-run tests →
        Repeat until pass
```

## Testing Against the Spec

Pull test cases directly from `spec.md`:

### User Story Testing

For each user story in the spec:
```markdown
## User Story: Create New Entry
"As a user, I want to create a new journal entry so that I can record my thoughts"

### Test Cases:
- [ ] User can click "New Entry" button
- [ ] Modal opens with date pre-filled
- [ ] User can type in text area
- [ ] Submit saves and returns to list
- [ ] New entry appears in list
```

### Acceptance Criteria Testing

For each acceptance criterion:
```markdown
## Acceptance Criteria: Entry Persistence
"Entries should persist across sessions"

### Test Cases:
- [ ] Create entry, refresh page, entry still exists
- [ ] Create entry, close browser, reopen, entry still exists
- [ ] Create entry, log out, log in, entry still exists
```

## Test Execution

### Automated Tests

Run the full test suite:
```bash
# Frontend
npm test

# Backend
pytest tests/

# E2E
npx playwright test
```

### Manual Testing

For user-facing features, manual verification:
1. Follow the user flow from spec
2. Check that UI matches expectations
3. Test edge cases (empty states, errors, etc.)
4. Verify on different screen sizes (if applicable)

### API Testing

For backend features:
```bash
# Success case
curl -X POST /api/v1/feature \
  -H "Content-Type: application/json" \
  -d '{"field": "value"}' \
  | jq .

# Error case
curl -X POST /api/v1/feature \
  -H "Content-Type: application/json" \
  -d '{"invalid": "data"}' \
  | jq .
```

## Handling Test Failures

### Diagnosis Steps

1. **Read the error message** - What exactly failed?
2. **Reproduce the failure** - Can you trigger it manually?
3. **Isolate the cause** - Which component is at fault?
4. **Check recent changes** - What changed since it last worked?

### Fix Process

1. Make a minimal fix (don't refactor while fixing)
2. Re-run the failing test
3. Run full test suite to check for regressions
4. Update build-plan.md if the fix changed approach

### When to Escalate

If a test keeps failing after 3 attempts:
- Document what you've tried
- Identify possible root causes
- Flag for human review
- Consider if the spec needs clarification

## Test Documentation

### In build-plan.md

Document test status:
```markdown
## Test Results

### Phase 1 Tests
- [x] Build succeeds - PASS
- [x] No TS errors - PASS
- [x] Component renders - PASS

### Integration Tests
- [x] API endpoint works - PASS
- [ ] E2E flow complete - IN PROGRESS

### Edge Cases
- [ ] Empty state handled - TODO
- [ ] Error state handled - TODO
```

### In decisions.md

Document testing decisions:
```markdown
## Testing Approach

**Decision:** Use Playwright for E2E tests instead of Cypress

**Rationale:**
- Playwright has better cross-browser support
- Faster execution
- Claude can run it via MCP server

**Trade-offs:**
- Team needs to learn new tool
- Some existing Cypress tests need migration
```

## Quality Gates

Define what "done" means for testing:

### Minimum Quality

- [ ] All unit tests pass
- [ ] All integration tests pass
- [ ] No TypeScript errors
- [ ] Build succeeds

### Production Ready

- [ ] All of the above
- [ ] E2E tests pass
- [ ] Performance acceptable
- [ ] Security review complete
- [ ] Documentation updated

## Best Practices

### Test Early, Test Often

Don't save all testing for the end. Verify each phase as you go.

### Test the Unhappy Path

Common things to test:
- Empty data
- Invalid input
- Network errors
- Permission denied
- Timeout/slow responses

### Use Realistic Data

Don't just test with "test" and "foo". Use realistic:
- Names with spaces and special characters
- Large text inputs
- Edge case dates (leap years, time zones)

### Maintain Test Independence

Each test should:
- Set up its own data
- Not depend on other tests
- Clean up after itself

## Checklist

Before proceeding to Learn phase:

- [ ] All success criteria from build-plan.md verified
- [ ] Integration tests passing
- [ ] User acceptance criteria met
- [ ] Edge cases tested
- [ ] No regressions in existing functionality
- [ ] Test results documented

## Next Phase

Once all tests pass, proceed to [Phase 6: Learn](./6-learn.md) to capture learnings and improve the system.
