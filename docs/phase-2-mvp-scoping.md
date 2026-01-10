# Phase 2: MVP & Scope Definition

## Purpose

Define what's in v1 vs. future versions. The goal is to identify the absolute minimum needed to validate the concept works, then explicitly defer everything else.

## Why MVP Matters

Building everything at once leads to:
- Longer time to first working version
- More code to debug when things go wrong
- Features that might not even be needed
- Scope creep during development

An MVP lets you:
- Validate the core concept quickly
- Get real feedback before investing more
- Iterate based on actual usage
- Ship something valuable sooner

## Process

### Step 1: Review the Feature Spec

Read through the `feature-spec.md` from Phase 1. Identify:
- The core value proposition (what's the main thing?)
- All the features and behaviors mentioned
- Any dependencies between features

### Step 2: Identify the Core

Ask: "What is the one thing this feature MUST do to be useful?"

Everything else is secondary. The MVP should prove the core works.

**Examples:**
- Chat plugin MVP: Send a message, get a response, see the conversation
- Settings plugin MVP: View settings, change a setting, see it persist
- Document processor MVP: Upload a document, extract text, display it

### Step 3: List What's OUT of Scope for v1

Be explicit. Write down everything that's NOT in the MVP:

```markdown
## Out of Scope for v1

- [ ] Dark mode support (v2)
- [ ] Keyboard shortcuts (v2)
- [ ] Export functionality (v3)
- [ ] Multi-language support (future)
- [ ] Advanced error recovery (v2)
```

This list is as important as what's in scope. It prevents scope creep.

### Step 4: Define v2 and v3

Briefly outline what future versions might include. This helps validate that the MVP architecture can support them.

```markdown
## Future Versions

### v2 (Polish)
- Dark mode support
- Keyboard shortcuts
- Better error messages

### v3 (Extended Features)
- Export functionality
- Batch operations

### Future Consideration
- Multi-language support
- API access
```

### Step 5: Validate the MVP is Actually Minimal

Ask yourself:
- Can I remove anything else and still prove the concept?
- Am I including anything "because it's easy" rather than "because it's essential"?
- Would I be embarrassed to ship just this? (If no, you might be over-building)

## Output

Update the feature spec with a clear MVP section:

```markdown
## MVP Scope (v1)

### Included
- Core feature A
- Essential behavior B
- Minimum UI needed

### Explicitly Excluded
- Nice-to-have X (v2)
- Enhancement Y (v3)
- Future idea Z

## Future Versions

### v2
- ...

### v3
- ...
```

## Common Mistakes

### Including "Easy" Things
Just because something is easy doesn't mean it belongs in the MVP. Stay focused on the core.

### Perfectionism
The MVP doesn't need to be polished. It needs to work and prove the concept.

### Hidden Scope
Watch for phrases like "and also" or "while we're at it" - these are scope creep in disguise.

### No Clear Boundary
If you can't clearly state what's OUT, you don't have an MVP, you have a wishlist.

## Tips for BrainDrive

### Plugin MVPs
For new plugins, the MVP should:
- Use at least one Service Bridge (prove integration works)
- Have a single, focused UI component
- Demonstrate the core value in under 5 minutes of use

### Core Modification MVPs
For core changes, the MVP should:
- Touch the minimum files possible
- Have a feature flag if the change is risky
- Include migration path if changing data structures

## Next Phase

Once you have a clearly scoped MVP, move to [Phase 3: Technical Design](./phase-3-technical-design.md) to plan how to build it.
