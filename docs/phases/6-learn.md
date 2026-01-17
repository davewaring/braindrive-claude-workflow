# Phase 6: Learn

## Purpose

Capture learnings and feed them back into the system. This is the flywheel mechanism that makes every feature improve the next one.

## Why Learning Matters

Without explicit learning:
- Same mistakes get repeated
- Good patterns get forgotten
- The system doesn't improve

With explicit learning:
- Mistakes become guardrails
- Patterns become conventions
- Each feature makes the next easier

## The Learning Process

### Step 1: Run Retrospective

Use the `/retro` skill after feature completion:

```
/retro
```

This guides you through capturing:
- What went well?
- What was harder than expected?
- What patterns emerged?
- What would we do differently?
- What context was missing?

### Step 2: Categorize Learnings

Sort learnings into categories:

| Category | Example | Where to Update |
|----------|---------|-----------------|
| **Business Context** | "Users actually prefer X over Y" | `braindrive/vision.md` |
| **Technical Pattern** | "Always use Service Bridge for X" | `braindrive/conventions.md` |
| **Project Decision** | "Chose A because of B" | `projects/[project]/decisions.md` |
| **Process Improvement** | "Interview should ask about X" | Workflow skills/templates |
| **Guardrail** | "Never do X, it causes Y" | Project CLAUDE.md |

### Step 3: Integrate Learnings

Update the appropriate sources:

#### Into BrainDrive-Library

**For business learnings:**
```markdown
# In braindrive/vision.md

## User Preferences (Learned)
- Users prefer inline editing over modal dialogs
- Mobile users expect swipe gestures
```

**For technical patterns:**
```markdown
# In braindrive/conventions.md

## Service Bridge Patterns (Learned)
- Always use API Bridge for backend calls
- Never import directly from core modules
```

**For project decisions:**
```markdown
# In projects/[project]/decisions.md

## Decision: Use SQLite Instead of PostgreSQL

**Context:** We evaluated both options for the caching layer.

**Decision:** SQLite

**Rationale:**
- Simpler deployment
- Good enough for our scale
- Aligns with existing patterns

**Learned:** Works well for single-user scenarios.
May need to revisit for multi-user features.
```

#### Into Workflow System

**For process improvements:**
- Update interview questions in `/interview` skill
- Add sections to templates
- Update phase guidance docs

**For guardrails:**
```markdown
# In project CLAUDE.md

## Constraints (Learned from [feature])
- Never import from '../../../core' - use Service Bridges
- Always validate user input server-side
- Don't use localStorage for sensitive data
```

### Step 4: Propagate Changes

Ensure learnings are available for future work:

1. **Commit to Library** - Push changes to BrainDrive-Library
2. **Refresh materialized context** - Run `librarian refresh`
3. **Update CLAUDE.md** - Add relevant guardrails to project config
4. **Share with team** - Document in PR or team channel

## What to Capture

### Technical Learnings

| Learning Type | Example | Action |
|---------------|---------|--------|
| **Pattern** | "Pagination works best with cursor-based approach" | Add to conventions |
| **Gotcha** | "MUI DatePicker needs locale config" | Add to CLAUDE.md |
| **Integration** | "Service Bridge X needs header Y" | Document in bridge docs |

### Process Learnings

| Learning Type | Example | Action |
|---------------|---------|--------|
| **Missing Question** | "Should have asked about mobile requirements" | Update interview skill |
| **Template Gap** | "Spec should include API contract section" | Update template |
| **Phase Issue** | "Foundation phase was too big" | Note for future planning |

### Business Learnings

| Learning Type | Example | Action |
|---------------|---------|--------|
| **User Insight** | "Users expect auto-save" | Add to vision/personas |
| **Scope Creep** | "Feature X always leads to request Y" | Note in feature patterns |
| **Priority** | "Performance matters more than features" | Update decision criteria |

## Retrospective Questions

Guided questions for `/retro`:

### What Went Well?
- Which patterns saved time?
- What tools were most helpful?
- What decisions were clearly right?

### What Was Harder Than Expected?
- Where did we struggle?
- What took longer than planned?
- What required human intervention?

### What Would We Do Differently?
- Different architecture?
- Different sequence?
- Different tools?

### What Context Was Missing?
- What did we wish we knew earlier?
- What assumptions were wrong?
- What related work did we miss?

### What Should We Automate?
- Repetitive tasks?
- Verification that's manual now?
- Documentation that could be generated?

## The Flywheel Effect

```
Feature 1: Learn patterns A, B, C
    ↓
Feature 2: Use A, B, C; Learn D, E
    ↓
Feature 3: Use A-E; Learn F, G
    ↓
...
Feature N: Rich context, fast execution
```

Each feature adds to the system:
- More patterns in conventions
- More guardrails in CLAUDE.md
- Better questions in interview
- More complete templates
- Richer business context

## Best Practices

### Capture While Fresh

Run `/retro` immediately after feature completion. Don't wait - details fade quickly.

### Be Specific

**Bad:** "API was hard"
**Good:** "The auth header format wasn't documented. Added to Service Bridge docs."

### Include the Why

**Bad:** "Use approach X"
**Good:** "Use approach X because Y doesn't work when Z"

### Don't Over-Learn

Not every experience needs documentation. Focus on:
- Things that will recur
- Non-obvious gotchas
- Decisions others will face

## Checklist

Before closing the feature:

- [ ] `/retro` completed
- [ ] Learnings categorized
- [ ] Library updated (decisions, conventions)
- [ ] CLAUDE.md updated (guardrails)
- [ ] Templates/skills improved (if applicable)
- [ ] Changes committed and pushed
- [ ] Context refreshed for next feature

## Completing the Cycle

After Learn phase:
1. The feature is complete
2. The system is improved
3. Next feature starts with better context

The cycle continues with the next feature, starting again at Phase 1: Context - now enriched with everything learned from this feature.

---

**The system improves itself. Every feature makes the next one easier.**
