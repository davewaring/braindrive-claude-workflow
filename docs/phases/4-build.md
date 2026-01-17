# Phase 4: Build

## Purpose

Execute the plan with autonomous verification. Claude works through phases, verifying each one before moving to the next.

## Prerequisites

Before starting build:
- [ ] `spec.md` complete and approved
- [ ] `build-plan.md` complete with success criteria
- [ ] Setup phase complete (environment ready)

## The Execution Loop

For each phase in `build-plan.md`:

```
1. Mark phase as "in progress" in build-plan.md
2. Implement the tasks
3. Run success criteria (verify)
4. If all pass → mark complete, proceed
5. If fail → fix and re-verify
6. At phase end → human checkpoint (if required)
```

## Phase Execution

### Starting a Phase

1. Read the phase from `build-plan.md`
2. Review success criteria first (know what "done" looks like)
3. Mark phase as in progress
4. Begin implementation

### During Implementation

- Work through tasks in order
- Use parallel sub-agents when tasks are independent
- Follow existing patterns from context
- Don't over-engineer - do exactly what the phase requires

### Verifying a Phase

Use `/milestone-check [phase-number]` to verify:

```
/milestone-check 1
```

This runs all success criteria commands and reports:
- Which criteria passed
- Which criteria failed
- Suggested fixes for failures

### Completing a Phase

When all criteria pass:
1. Update `build-plan.md` status
2. Commit changes with descriptive message
3. Check if human review is required
4. If yes → stop and request review
5. If no → proceed to next phase

## Build Workflows

### Standard Flow (Single Features)

```
Read build-plan.md →
For each phase:
    Implement → Verify → Commit → Checkpoint? → Next
```

### Issue-Based Flow

For tight organization and history:
1. Convert phases to GitHub issues
2. Create branch for each issue
3. Work through issues in order
4. Create PR when phase complete
5. Merge after verification passes

### Multi-Agent Flow

For parallel feature development:
```bash
# Create worktrees for each feature
git worktree add ../feature-a feature/auth
git worktree add ../feature-b feature/settings

# Work in parallel (separate terminals)
cd ../feature-a && claude
cd ../feature-b && claude

# Merge when done
git checkout main
git merge feature/auth
git merge feature/settings
```

## When to Stop

| Situation | Action |
|-----------|--------|
| Phase complete, all criteria pass | Checkpoint (if required), then next phase |
| Test fails | Debug, fix, re-verify (max 3 attempts) |
| Stuck for 3+ attempts | Document issue, flag for human help |
| Unclear requirement | Stop, ask for clarification |
| User-facing decision needed | Stop, present options |
| External dependency blocked | Stop, report blocker |

## Handling Failures

### Test Failures

1. Read the error message carefully
2. Identify root cause
3. Make minimal fix
4. Re-run verification
5. If 3+ failures on same issue → stop and document

### Build Failures

1. Check for TypeScript errors
2. Check for missing dependencies
3. Check for syntax errors
4. Verify imports are correct
5. Don't change multiple things at once

### Stuck Situations

When you've tried 3+ times:
```markdown
## Blocked: [Issue Description]

**What I've tried:**
1. Approach A - failed because...
2. Approach B - failed because...
3. Approach C - failed because...

**My hypothesis:**
[What you think the root cause is]

**Suggested next steps:**
[What you'd try next or what help you need]
```

## Commit Strategy

Commit after each phase passes verification:

```
feat(plugin): phase 1 - foundation

- Set up plugin structure
- Created main component
- Verified: build passes, component renders
```

Format:
- `feat` for new features
- `fix` for bug fixes
- `refactor` for restructuring
- Include phase number
- List key changes
- Note verification status

## Best Practices

### Use Parallel Sub-Agents

When implementing, use parallel agents for independent tasks:
> "Implement this phase using parallel sub-agents where there are no dependencies between tasks."

### Update build-plan.md As You Go

After each phase:
- Mark tasks complete
- Update status
- Note any deviations
- Record learnings

### Don't Fear Throwing Away Work

If an approach isn't working:
1. Use checkpoints to rewind
2. Try a different approach
3. Ask for guidance

Code is cheap. Time spent fighting a bad approach is expensive.

### Regression Prevention

When Claude makes a mistake, add a lesson to CLAUDE.md:
```
# Never import from '../../../core' - use Service Bridges instead
```

## Checklist

For each phase:

- [ ] Phase marked as in progress
- [ ] Tasks implemented
- [ ] `/milestone-check` passed
- [ ] build-plan.md updated
- [ ] Changes committed
- [ ] Human checkpoint completed (if required)

## Next Phase

After all build phases complete, proceed to [Phase 5: Test](./5-test.md) for final acceptance testing.
