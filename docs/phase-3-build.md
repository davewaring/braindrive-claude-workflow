# Phase 3: Build

## Purpose

Execute the plan with autonomous verification. Claude works through phases, verifying each one before moving to the next.

## Prerequisites

Before starting build phase, you should have:
- [ ] `feature-spec.md` - Complete feature definition with MVP scope
- [ ] `plan.md` - Architecture, phases, and success criteria

## The Verification Loop

For each phase in `plan.md`, Claude follows this loop:

```
1. Implement phase
2. Run all verification commands (success criteria)
3. If all pass:
   - Mark phase complete in plan.md
   - Move to next phase
4. If any fail:
   - Fix the issue
   - Re-run verification
   - Repeat until pass
5. If stuck (3+ attempts):
   - Document the issue
   - Flag for human help
   - Wait or move to unblocked work
```

## Build Workflows

### Workflow 1: General Workflow (Single Features)

Use for most feature development.

**Steps:**
1. **Research** (if needed)
   - Read relevant code
   - Check existing patterns
   - Look up API docs

2. **Plan Mode**
   - Let Claude create implementation plan
   - Review approach before coding

3. **Implement**
   - Work through one phase at a time
   - Use parallel sub-agents when possible
   - Commit after each phase

4. **Test & Verify**
   - Run success criteria from plan.md
   - Fix any failures

5. **Document**
   - Update plan.md status
   - Update changelog
   - Update architecture docs if structure changed

### Workflow 2: Issue-Based Development

Use when you want tight organization and history.

**Steps:**
1. Convert phases to GitHub issues
2. Create a branch for each issue
3. Work through issues in order
4. Create PR when phase complete
5. Merge after verification passes

**Benefits:**
- Clear history in GitHub
- Easy to pause and resume
- Multiple people can work in parallel
- Progress visible to stakeholders

### Workflow 3: Multi-Agent Development

Use when building multiple features in parallel.

**Steps:**
1. Create git worktrees for each feature
2. Run separate Claude instances in each worktree
3. Each instance works independently
4. Merge worktrees when features complete

**Example:**
```bash
# Create worktrees
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

## Best Practices

### Use Parallel Sub-Agents

When implementing, tell Claude to use parallel sub-agents:
> "Implement this phase using parallel sub-agents where there are no dependencies between tasks."

This speeds up development significantly.

### Commit After Each Phase

Don't wait until the end. Commit after each phase passes verification:
```
feat(plugin): phase 1 - foundation

- Set up plugin structure
- Created main component
- Verified: build passes, component renders
```

### Update plan.md As You Go

After each phase:
- Mark tasks as complete
- Update status
- Note any deviations or learnings

### Use Regression Prevention

When Claude makes a mistake, use `#` to add a lesson:
```
# Never import from '../../../core' - use Service Bridges instead
```

This updates CLAUDE.md and prevents the mistake from recurring.

### Don't Fear Throwing Away Work

If an approach isn't working after 3 attempts:
- Use Claude's checkpoints to rewind
- Try a different approach
- Ask a human for guidance

Code is cheap. Time spent fighting a bad approach is expensive.

## Human Handoff Points

Some things require human judgment. Know when to stop and ask:

**Design Decisions:**
- "The UX could go two ways. Option A does X, Option B does Y. Which feels right?"

**Ambiguous Requirements:**
- "The spec says 'handle errors gracefully' but doesn't define what that means. What should happen when...?"

**Quality Judgment:**
- "All tests pass, but I'm not confident about the performance. Want to review before I continue?"

**Blocked Progress:**
- "I've tried 3 approaches and can't get past this issue. Here's what I've tried..."

## After Build: Run Retro

When the feature is complete, run `/retro` to:
- Capture what worked well
- Identify what could improve
- Update CLAUDE.md with learnings
- Suggest improvements to this workflow

This makes the next feature easier to build.

## Quick Reference

| Situation | Action |
|-----------|--------|
| Starting a phase | Read success criteria first |
| All tests pass | Commit and move to next phase |
| Test fails | Debug, fix, re-run (max 3 attempts) |
| Stuck for 3+ attempts | Flag for human, document issue |
| Phase complete | Update plan.md status, commit |
| Feature complete | Run /retro |
