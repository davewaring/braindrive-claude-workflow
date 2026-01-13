# Phase 1: Feature Specification

## Purpose

Surface hidden assumptions, define what we're building, and scope the MVP before writing any code. This is the most critical phase - time spent here saves exponentially more time during implementation.

## Output

This phase produces `feature-spec.md` - the "what/why" document that defines requirements, target user, and MVP scope.

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

### Step 3: Define the MVP

During or after the interview, explicitly define the MVP:

**Ask: "What is the one thing this feature MUST do to be useful?"**

Everything else is secondary. The MVP should prove the core works.

**Examples:**
- Chat plugin MVP: Send a message, get a response, see the conversation
- Settings plugin MVP: View settings, change a setting, see it persist
- Document processor MVP: Upload a document, extract text, display it

**Be explicit about what's OUT of scope:**

```markdown
## Out of Scope for v1

- [ ] Dark mode support (v2)
- [ ] Keyboard shortcuts (v2)
- [ ] Export functionality (v3)
- [ ] Multi-language support (future)
```

This list is as important as what's in scope. It prevents scope creep.

### Step 4: Generate the Feature Spec

Once the interview is complete, use `/feature-spec` to generate the document. The spec should include:

1. **Feature Overview** - Clear description of what we're building
2. **Target User** - Who this is for and their context
3. **Problem Statement** - What pain this solves
4. **User Stories** - Specific interactions and flows
5. **MVP Scope** - What's in v1, what's explicitly out
6. **Future Versions** - Brief outline of v2, v3
7. **Technical Context** - Plugin vs core, integration points
8. **Open Questions** - Anything still to be resolved
9. **Success Criteria** - How we know it's done

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

### Validate the MVP is Actually Minimal

Ask yourself:
- Can I remove anything else and still prove the concept?
- Am I including anything "because it's easy" rather than "because it's essential"?
- Would I be embarrassed to ship just this? (If no, you might be over-building)

## Common Mistakes

### Including "Easy" Things
Just because something is easy doesn't mean it belongs in the MVP. Stay focused on the core.

### Perfectionism
The MVP doesn't need to be polished. It needs to work and prove the concept.

### Hidden Scope
Watch for phrases like "and also" or "while we're at it" - these are scope creep in disguise.

### No Clear Boundary
If you can't clearly state what's OUT, you don't have an MVP, you have a wishlist.

## Next Phase

Once you have a complete feature spec with clear MVP scope, move to [Phase 2: Planning](./phase-2-planning.md) to design how to build it and define milestones.
