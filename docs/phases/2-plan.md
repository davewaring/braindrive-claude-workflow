# Phase 2: Plan

## Purpose

Define *what* we're building (spec) and *how* we're building it (build plan). This phase ensures alignment before writing code and creates verifiable success criteria.

## Outputs

| Document | Purpose | Location |
|----------|---------|----------|
| `spec.md` | What we're building and why | Library/projects/active/[project]/ |
| `build-plan.md` | How we're building it | Library/projects/active/[project]/ |

## Process

### Step 1: Interview (Requirement Discovery)

Use the `/interview` skill to surface hidden requirements through deep questioning.

**Why Interview First?**
- Narrows the solution space - every answer eliminates assumptions
- Surfaces hidden requirements - questions reveal things you haven't thought through
- Cheap to change - decisions now cost nothing; decisions during coding cost rework
- Better specs - 40+ questions lead to specs you feel ownership over

**What the Interview Covers:**
1. **Core Understanding** - What exactly is this feature?
2. **Scope Definition** - What's in v1, what's out?
3. **User Experience** - How will users interact with it?
4. **Technical Integration** - How does it fit with existing systems?
5. **Edge Cases** - What could go wrong?

**Skill:** `/interview`

### Step 2: Generate Feature Specification

Translate interview insights into `spec.md` - the stakeholder-readable document.

**Contents:**
- Feature overview and problem statement
- Target user and their context
- User stories and acceptance criteria
- MVP scope (explicit in/out)
- Future versions (v2, v3 outline)
- Integration points
- Open questions
- Success definition

**Skill:** `/feature-spec`

### Step 3: Generate Build Plan

Design the technical approach and break into verifiable phases.

**Contents:**
- Key technical decisions with rationale
- Architecture overview (components, data flow)
- Implementation roadmap (3-5 phases)
- Success criteria for each phase
- Human checkpoints
- Risks and mitigations

**Skill:** `/plan`

## Success Criteria Format

Each phase in the build plan must have verifiable success criteria:

```markdown
### Phase 1: Foundation

**Goal:** Plugin structure with working component

**Tasks:**
- [ ] Create plugin from template
- [ ] Set up main component
- [ ] Configure routing

**Success Criteria:**

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| Build succeeds | `npm run build` | Exit code 0 |
| No TS errors | `npx tsc --noEmit` | Exit code 0 |
| Component renders | Playwright test | Element visible |

**Exit Criteria:** User can navigate to plugin and see basic UI
```

## Types of Verifiable Criteria

1. **Build/Compile Checks**
   - `npm run build` - Exit code 0
   - `npx tsc --noEmit` - No TypeScript errors

2. **Automated Tests**
   - `npm test` - All tests pass
   - `pytest tests/` - Backend tests pass

3. **API Verification**
   - POST /api/v1/feature/create returns 200
   - Invalid input returns 422 with error details

4. **Visual Verification (Playwright)**
   - Component renders at expected route
   - User interactions work as expected

## Human Checkpoints

Define when human review is needed:

| Output Type | When to Review |
|-------------|----------------|
| User-facing UI/UX | After each phase that changes UI |
| API contracts | When defined, before implementation |
| Internal/infrastructure | After phase completion |
| Background processes | At major milestones |

**Principle:** Get human eyes on user-facing work early. Background work can batch reviews at phase completion.

## Best Practices

### Be Specific About UX

**Don't say:** "Users can create journal entries"

**Say:** "User clicks 'New Entry' button in the top right. A modal opens with a blank text area and today's date pre-filled. They can optionally add tags from a dropdown. Submit saves and returns to the list view."

### Define What's OUT

The out-of-scope list is as important as in-scope:

```markdown
## Out of Scope for v1

- [ ] Dark mode support (v2)
- [ ] Keyboard shortcuts (v2)
- [ ] Export functionality (v3)
```

### Order Phases by Dependency

Ensure each phase can be completed in order:

```markdown
1. **Foundation** - No dependencies
2. **Core Integration** - Depends on: Foundation
3. **Polish** - Depends on: Core Integration
```

### Include Negative Cases

Don't just test the happy path:
- What happens with invalid input?
- What happens when the backend is down?
- What happens with empty data?

## Common Mistakes

### Skipping the Interview
Jumping straight to spec-writing leads to specs full of assumptions.

### Vague Success Criteria
"The feature works" is not verifiable. Be specific about commands and expected results.

### No Out-of-Scope List
If you can't clearly state what's OUT, you don't have an MVP, you have a wishlist.

### Too Many Phases
3-5 phases is ideal. More than 5 means phases are too granular.

## Checklist

Before proceeding to Setup phase:

- [ ] Interview completed (20-40+ questions answered)
- [ ] spec.md written and saved to Library
- [ ] build-plan.md written and saved to Library
- [ ] Each phase has verifiable success criteria
- [ ] Human checkpoints identified
- [ ] Out-of-scope items explicitly listed

## Next Phase

Once spec and build plan are approved, proceed to [Phase 3: Setup](./3-setup.md) to prepare the execution environment.
