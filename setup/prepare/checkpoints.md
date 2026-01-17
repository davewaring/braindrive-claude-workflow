# Checkpoint Guidance

This document defines when Claude should stop for human review during feature development.

## Core Principle

**User-facing work gets reviewed early. Background work can batch reviews at phase completion.**

The goal is to get human eyes on what users will actually see and interact with before too much work is done, while allowing internal/infrastructure work to proceed autonomously.

## Checkpoint Matrix

### By Output Type

| Output Type | When to Checkpoint |
|-------------|-------------------|
| **User-facing UI** | After each phase that changes what users see |
| **User-facing UX flows** | After implementing each flow |
| **API contracts** | When defined, before implementation begins |
| **Data models** | When schema is designed, before migration |
| **Internal services** | After phase completion |
| **Infrastructure** | At major milestones |
| **Tests/tooling** | At PR time |

### By Risk Level

| Risk Level | Characteristics | Checkpoint Frequency |
|------------|-----------------|---------------------|
| **High** | Auth, payments, data migration, external APIs | Review before AND after |
| **Medium** | New features, significant refactors | Review after each phase |
| **Low** | Bug fixes, minor tweaks, internal tooling | Review at PR |

### By Reversibility

| Reversibility | Examples | Checkpoint |
|---------------|----------|------------|
| **Hard to reverse** | Database migrations, external API contracts | Review before executing |
| **Moderate** | Architecture changes, public API changes | Review after implementation |
| **Easy to reverse** | UI changes, internal code | Review at phase end or PR |

## When to Stop Immediately

Claude should always stop and request human input when:

1. **Ambiguous Requirements**
   - The spec doesn't clearly define expected behavior
   - Multiple valid interpretations exist
   - Edge case behavior isn't specified

2. **Architectural Decisions**
   - Choice between fundamentally different approaches
   - Trade-offs that affect future development
   - Deviation from established patterns

3. **User Experience Decisions**
   - How to handle error states
   - Empty state presentation
   - Interaction patterns not specified in spec

4. **Security Considerations**
   - Handling sensitive data
   - Authentication/authorization logic
   - Input validation approach

5. **Blocked Progress**
   - Same issue after 3+ attempts
   - Missing dependencies or access
   - External service not responding

## When to Continue Autonomously

Claude should continue without stopping when:

1. **Within Defined Scope**
   - Task is clearly specified in build plan
   - Success criteria are unambiguous
   - Following established patterns

2. **Verification Passing**
   - All tests passing
   - Build succeeding
   - No TypeScript errors

3. **Internal Work**
   - Refactoring that doesn't change behavior
   - Adding tests
   - Documentation updates
   - Code cleanup

## Configuring Checkpoints in Build Plans

Document checkpoints explicitly in each build plan:

```markdown
## Human Checkpoints

### Required After Phase 1
- [ ] Review plugin structure - is this the right approach?

### Required After Phase 2
- [ ] UX review - does the interaction feel right?
- [ ] Design review - consistent with BrainDrive patterns?

### Required After Phase 3
- [ ] Final review before merge
- [ ] Test with realistic data

### Optional (Request if Uncertain)
- Performance review if processing large datasets
- Security review if handling user input
```

## Checkpoint Communication

When stopping for a checkpoint, Claude should provide:

```markdown
## Checkpoint: [Phase Name] Complete

### What Was Done
- [List of completed tasks]

### Verification Status
- Build: ✅ Passing
- Tests: ✅ All pass
- TypeScript: ✅ No errors

### Ready for Review
- [Specific items that need human review]

### Questions (if any)
- [Any decisions that need human input]

### Next Steps (after approval)
- [What will happen in next phase]
```

## Examples

### High-Touch Feature (User-Facing Dashboard)

```markdown
## Checkpoints

After Phase 1 (Foundation):
- [ ] Review component structure

After Phase 2 (Core UI):
- [ ] UX review - does the layout work?
- [ ] Design review - matches mockups?

After Phase 3 (Data Integration):
- [ ] Review data display format
- [ ] Verify loading/error states

After Phase 4 (Polish):
- [ ] Final visual review
- [ ] Test on different screen sizes
```

### Low-Touch Feature (Internal Service)

```markdown
## Checkpoints

After Phase 3 (Complete):
- [ ] Code review
- [ ] Verify all tests pass
- [ ] Check performance metrics
```

## Best Practices

### Define Upfront

Determine checkpoint requirements during Phase 2 (Plan), not during build. This sets clear expectations.

### Be Specific

Not "review the UI" but "verify the modal opens from the correct button and displays user data correctly."

### Trust the Process

If success criteria are well-defined and passing, the checkpoint can be lightweight. Don't require detailed review for every phase.

### Batch When Appropriate

For internal work, it's fine to complete multiple phases before checkpoint. User-facing work should checkpoint more frequently.
