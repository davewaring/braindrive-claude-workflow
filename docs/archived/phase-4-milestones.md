# Phase 4: Milestones & Success Criteria

## Purpose

Break the work into testable chunks with AI-verifiable success definitions. This is what enables Claude to work autonomously - clear criteria it can check itself.

## Key Principle

**If Claude can't verify it, a human must.**

Maximize what Claude can verify to maximize autonomous development.

## Process

### Step 1: Break Into 3-5 Milestones

Each milestone should be:
- **Independently testable** - Can verify it works without later milestones
- **Valuable on its own** - Delivers some functionality
- **Small enough to complete** - Can finish in one focused session
- **Clear when done** - Obvious success/failure

**Example Breakdown:**
```markdown
## Milestones

### Milestone 1: Basic UI Shell
Set up the plugin structure with a working component that displays in BrainDrive.

### Milestone 2: Backend Integration
Connect to backend via API Bridge, send/receive data.

### Milestone 3: Core Functionality
Implement the main feature logic.

### Milestone 4: Settings & Persistence
Add user settings and persist state across sessions.

### Milestone 5: Polish & Edge Cases
Handle errors, loading states, and edge cases.
```

### Step 2: Define Success Criteria for Each Milestone

For each milestone, define criteria Claude can verify:

#### Types of Verifiable Criteria

**1. Automated Tests (Best)**
```markdown
### Success Criteria
- [ ] `npm test` passes with all tests green
- [ ] `pytest tests/test_feature.py` passes
- [ ] Coverage > 80% for new code
```

**2. API Verification**
```markdown
### Success Criteria
- [ ] POST /api/v1/feature/create returns 200 with valid payload
- [ ] GET /api/v1/feature/{id} returns created item
- [ ] Invalid input returns 422 with error details
```

**3. Visual Verification (Playwright)**
```markdown
### Success Criteria
- [ ] Component renders at /page/feature
- [ ] Clicking "Create" button opens modal
- [ ] Form submission shows success message
- [ ] Error state displays when API fails
```

**4. Functional Checks**
```markdown
### Success Criteria
- [ ] Build completes without errors: `npm run build`
- [ ] No TypeScript errors: `npx tsc --noEmit`
- [ ] No linting errors: `npm run lint`
- [ ] Plugin appears in Plugin Manager list
```

### Step 3: Write Verification Commands

For each criterion, write the exact command Claude should run:

```markdown
## Milestone 1: Basic UI Shell

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| Build succeeds | `npm run build` | Exit code 0 |
| No TS errors | `npx tsc --noEmit` | Exit code 0 |
| Component renders | `npx playwright test tests/render.spec.ts` | All tests pass |
| Appears in Plugin Manager | Manual check or Playwright | Plugin visible |
```

### Step 4: Identify Human Checkpoints

Some things Claude can't verify. Be explicit:

```markdown
## Human Checkpoints

### After Milestone 3
- [ ] Review: Does the UX feel right?
- [ ] Review: Is the design consistent with BrainDrive?

### After Milestone 5
- [ ] Final review before merge
- [ ] Test on real data
```

### Step 5: Order Milestones by Dependency

Ensure Claude can complete milestones in order:

```markdown
## Milestone Order

1. **UI Shell** - No dependencies
2. **Backend Integration** - Depends on: UI Shell
3. **Core Functionality** - Depends on: Backend Integration
4. **Settings** - Depends on: Core Functionality
5. **Polish** - Depends on: All above
```

## Output

Create `milestones.md` with:

```markdown
# Feature: [Name] - Milestones

## Overview
Brief description of the feature and total milestone count.

## Milestone 1: [Name]

### Description
What this milestone accomplishes.

### Success Criteria
| Criterion | Verification | Expected |
|-----------|--------------|----------|
| ... | ... | ... |

### Human Checkpoint
- [ ] ...

---

## Milestone 2: [Name]
...
```

## Verification Loop

During build phase, Claude follows this loop for each milestone:

```
1. Implement milestone
2. Run all verification commands
3. If all pass:
   - Mark milestone complete
   - Move to next milestone
4. If any fail:
   - Fix the issue
   - Re-run verification
   - Repeat until pass
5. If stuck (3+ attempts):
   - Document the issue
   - Flag for human help
   - Wait or move to unblocked work
```

## Tips for Effective Criteria

### Be Specific
Bad: "The feature works"
Good: "POST /api/v1/feature returns 200 with id field in response"

### Be Verifiable
Bad: "The UI looks good"
Good: "Playwright screenshot matches baseline within 5% difference"

### Include Negative Cases
Don't just test the happy path:
- What happens with invalid input?
- What happens when the backend is down?
- What happens with empty data?

### Use Existing Test Patterns
Check BrainDrive-Core for existing test patterns:
- Frontend: Jest + React Testing Library
- Backend: pytest
- E2E: Playwright

## Next Phase

Once you have milestones defined, move to [Phase 5: Build](./phase-5-build.md) to start implementation.
