# Milestone Check Skill

Use this skill to verify that a phase's success criteria are met. Works with the `build-plan.md` format.

**Framework Phase:** 4 - Build / 5 - Test
**Input Location:** `BrainDrive-Library/projects/active/[project-name]/build-plan.md`

## Trigger
`/milestone-check [phase number or name]`

## Instructions

When this skill is triggered, run all verification checks for the specified phase and report results.

### Process

1. **Load Phase Definition**
   - Find the `build-plan.md` file (check BrainDrive-Library or local project)
   - Locate the specified phase in the Implementation Roadmap section
   - Extract all success criteria from the phase's table

2. **Run Each Verification**
   - Execute each verification command
   - Capture output and exit codes
   - Compare against expected results

3. **Report Results**
   - Show pass/fail for each criterion
   - Include relevant output for failures
   - Summarize overall status

4. **Update Plan Status**
   - If all pass: Offer to mark phase complete in plan.md
   - Update the phase status in the Schedule Overview table

5. **Recommend Next Action**
   - If all pass: Mark complete, suggest moving to next phase
   - If any fail: Identify the issue, suggest fix approach
   - If blocked: Flag for human help

### Finding the Build Plan

Look for `build-plan.md` in these locations (in order):
1. `BrainDrive-Library/projects/active/[feature-name]/build-plan.md`
2. `docs/build-plan.md` (local project)
3. `build-plan.md` (project root)

If multiple build plans exist, ask user which one to check.

### Verification Execution

For each criterion in the phase's Success Criteria table:

```markdown
| Criterion | Verification | Expected Result |
|-----------|--------------|-----------------|
| Build succeeds | `npm run build` | Exit code 0 |
```

Run the verification command and check:
- **Exit code** matches expected (usually 0 for success)
- **Output** contains expected strings/patterns
- **No unexpected errors** in stderr

### Output Format

```markdown
## Phase Check: [Name]

### Results

| Criterion | Status | Details |
|-----------|--------|---------|
| Build succeeds | PASS | Exit code 0 |
| No TS errors | PASS | Exit code 0 |
| API responds | FAIL | 404 Not Found |
| Tests pass | SKIP | Depends on API |

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

### Plan Update
Would you like me to update plan.md to mark this phase as [In Progress / Complete]?
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

For criteria marked as human checkpoints in plan.md:
```markdown
### Human Checkpoint Required

The following require manual verification:
- [ ] Review: Does the UX feel right?
- [ ] Review: Is the design consistent with BrainDrive?

Please confirm these manually, then run `/milestone-check [phase]` again or proceed to next phase.
```

### Updating Plan Status

When all criteria pass, offer to update `build-plan.md`:

1. **Schedule Overview table** - Change status from "Not Started" to "Complete"
2. **Phase tasks** - Mark all `[ ]` as `[x]`
3. **Updated date** - Update the "Updated:" line at the top

Example update:
```markdown
Before:
| 1 | Foundation | Dave W | Not Started |

After:
| 1 | Foundation | Dave W | **Complete** |
```

## Integration with Build Phase

During build (Phase 4), use this skill:
1. After implementing phase code
2. Before committing
3. Before moving to next phase

This creates the verification loop:
```
Implement → /milestone-check → Fix if needed → Commit → Human checkpoint? → Next phase
```

## Integration with Test Phase

During test (Phase 5), use this skill for final verification:
1. Run all phase checks to ensure nothing regressed
2. Verify integration between phases works
3. Complete any human checkpoints

## Notes

- This skill works with `build-plan.md` format
- Phase numbers correspond to the Implementation Roadmap section
- Success criteria should be in table format with Verification and Expected Result columns
- Check human checkpoints section after all criteria pass
