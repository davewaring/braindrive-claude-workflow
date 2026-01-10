# Phase 1: Feature Definition (Interview Process)

## Purpose

Surface hidden assumptions and fully define what we're building before writing any code. This is the most critical phase - time spent here saves exponentially more time during implementation.

## The Interview Approach

Instead of trying to write a perfect prompt, have Claude interview you. This surfaces requirements you didn't know you had and prevents Claude from making assumptions.

### Why Interview First?

- **Narrows the solution space** - Every answer eliminates assumptions Claude might make
- **Surfaces hidden requirements** - Questions reveal things you haven't thought through
- **Cheap to change** - Decisions made now cost nothing; decisions during coding cost rework
- **Better specs** - 40+ questions lead to specs you feel ownership over

## Process

### Step 1: Start with a Brainstorm

Before running `/interview`, jot down your initial thoughts:
- What's the core idea?
- What problem are you trying to solve?
- Any initial constraints or preferences?

This doesn't need to be detailed - the interview will flesh it out.

### Step 2: Run the Interview

Use the `/interview` skill. Claude will ask you questions about:

**What we're building:**
- What exactly is this feature?
- What are the core user interactions?
- What should it look like? (Be specific about UX)

**Who it's for:**
- Which BrainDrive persona? (Owner/Builder/Entrepreneur)
- What's their technical level?
- What context will they be in when using this?

**The problem:**
- What pain point does this solve?
- How do users currently handle this? (Workarounds)
- What would make this feel "solved"?

**Scope and intent:**
- Is this a prototype (feasibility check) or production feature?
- Is this a plugin or core modification?
- What's explicitly NOT in scope?

**Technical considerations:**
- Any specific technologies required or forbidden?
- Integration points with existing systems?
- Performance or security requirements?

### Step 3: Continue Until Complete

The interview should be exhaustive. For significant features, expect 20-40+ questions. Don't rush - this is where you define success.

Signs you're done:
- You can visualize exactly how the feature works
- You know what "done" looks like
- You've explicitly stated what's out of scope
- Technical approach is clear (or identified as needing research)

## Output

The interview produces a `feature-spec.md` document containing:

1. **Feature Overview** - Clear description of what we're building
2. **Target User** - Who this is for and their context
3. **Problem Statement** - What pain this solves
4. **User Stories** - Specific interactions and flows
5. **Scope** - What's in, what's out, prototype vs production
6. **Technical Context** - Plugin vs core, integration points
7. **Open Questions** - Anything still to be resolved

## Tips

### Be Specific About UX

Don't say: "Users can create journal entries"

Say: "User clicks 'New Entry' button in the top right. A modal opens with a blank text area and today's date pre-filled. They can optionally add tags from a dropdown. Submit saves and returns to the list view."

### Decide Prototype vs Production Upfront

**Prototype:**
- Skip error handling edge cases
- Skip polish and accessibility
- Focus on core functionality only
- Goal: Prove feasibility

**Production:**
- Full error handling
- Security considerations
- Edge cases covered
- Performance optimized
- Accessibility compliant

### Don't Hide Uncertainty

If you're not sure about something, say so. Better to identify unknowns now than discover them during implementation.

## Next Phase

Once you have a complete feature spec, move to [Phase 2: MVP & Scope Definition](./phase-2-mvp-scoping.md) to prioritize what to build first.
