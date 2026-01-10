# Milestone Check Skill

Use this skill to verify that a milestone's success criteria are met.

## Trigger
`/milestone-check [milestone number or name]`

## Instructions

When this skill is triggered, run all verification checks for the specified milestone and report results.

### Process

1. **Load Milestone Definition**
   - Find the milestones.md file in the project
   - Locate the specified milestone
   - Extract all success criteria

2. **Run Each Verification**
   - Execute each verification command
   - Capture output and exit codes
   - Compare against expected results

3. **Report Results**
   - Show pass/fail for each criterion
   - Include relevant output for failures
   - Summarize overall status

4. **Recommend Next Action**
   - If all pass: Mark complete, suggest moving to next milestone
   - If any fail: Identify the issue, suggest fix approach
   - If blocked: Flag for human help

### Verification Execution

For each criterion in the milestone:

```markdown
| Criterion | Verification Command | Expected Result |
```

Run the verification command and check:
- **Exit code** matches expected (usually 0 for success)
- **Output** contains expected strings/patterns
- **No unexpected errors** in stderr

### Output Format

```markdown
## Milestone Check: [Name]

### Results

| Criterion | Status | Details |
|-----------|--------|---------|
| Build succeeds | ✅ PASS | Exit code 0 |
| No TS errors | ✅ PASS | Exit code 0 |
| API responds | ❌ FAIL | 404 Not Found |
| Tests pass | ⏭️ SKIP | Depends on API |

### Summary
- **Passed:** 2/4
- **Failed:** 1/4
- **Skipped:** 1/4

### Failed Criterion Details

#### API responds
**Command:** `curl -X GET http://localhost:8005/api/v1/feature/1`
**Expected:** 200 response with data
**Actual:** 404 Not Found

**Likely Issue:** Endpoint not implemented yet or routing misconfigured.

### Recommendation
Fix the API endpoint issue before proceeding. The endpoint should be defined in `backend/app/api/v1/endpoints/feature.py`.
```

### Handling Different Verification Types

**Shell Commands:**
```bash
npm run build  # Check exit code
npx tsc --noEmit  # Check exit code and stderr
npm test  # Check exit code and parse test output
```

**API Checks:**
```bash
curl -s -o /dev/null -w "%{http_code}" http://localhost:8005/api/v1/endpoint
# Compare response code
```

**Playwright Tests:**
```bash
npx playwright test tests/specific-test.spec.ts
# Check exit code and parse results
```

**File Existence:**
```bash
test -f path/to/expected/file.tsx && echo "EXISTS" || echo "MISSING"
```

### Retry Logic

If a check fails:
1. Report the failure with details
2. If it's a transient issue (server not running, etc.), suggest a fix
3. Offer to re-run after user confirms fix
4. Track attempt count - after 3 failures on same criterion, flag for human

### Skip Conditions

Skip a criterion if:
- It depends on a previous criterion that failed
- Required service is not running (and user confirms skip)
- It's marked as "human checkpoint" (just remind user to check)

### Human Checkpoints

For criteria marked as human checkpoints:
```markdown
### Human Checkpoint Required

The following require manual verification:
- [ ] Review: Does the UX feel right?
- [ ] Review: Is the design consistent with BrainDrive?

Please confirm these manually, then run `/milestone-check [number]` again or proceed to next milestone.
```

## Integration with Build Phase

During build, use this skill:
1. After implementing milestone code
2. Before committing
3. Before moving to next milestone

This creates the verification loop:
```
Implement → /milestone-check → Fix if needed → Commit → Next milestone
```
