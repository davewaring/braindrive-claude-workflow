# Interview Skill

Use this skill to conduct a deep interview before building a feature. This surfaces hidden requirements and prevents assumptions.

## Trigger
`/interview [optional: initial idea or brainstorm]`

## Instructions

When this skill is triggered, conduct a thorough interview with the user about the feature they want to build. Use the AskUserQuestion tool to ask questions in batches of 2-4 related questions at a time.

### Interview Structure

**Round 1: Core Understanding**
Ask about:
- What exactly are we building? (Get a clear description)
- What problem does this solve? (The pain point)
- Who is this for? (BrainDrive persona: Owner/Builder/Entrepreneur)
- What's the context of use? (When/where will they use this?)

**Round 2: Scope & Intent**
Ask about:
- Is this a prototype (testing feasibility) or production feature?
- Is this a plugin or does it require core modifications?
- What does success look like? (How will we know it works?)
- What's explicitly NOT in scope?

**Round 3: User Experience**
Ask about:
- Walk me through the primary user flow step by step
- What should the user see first?
- What happens when they complete the main action?
- Are there any secondary flows or edge cases?

**Round 4: Technical Context**
Ask about:
- Any specific technologies required or forbidden?
- Integration points with existing BrainDrive features?
- Performance or security requirements?
- Dependencies on external services?

**Round 5: Details & Edge Cases**
Ask about:
- What happens with invalid input?
- What happens when something goes wrong?
- Any data that needs to persist?
- Anything else I should know?

### Question Guidelines

- **Be specific, not vague** - "What happens when the user clicks Submit?" not "How does the form work?"
- **Avoid obvious questions** - Don't ask things you could infer
- **Go deep** - Follow up on interesting answers
- **Challenge assumptions** - "Are you sure you need X?" or "What if we simplified to just Y?"
- **Use multiSelect** when asking about features or options that aren't mutually exclusive

### Completion Criteria

Continue interviewing until:
1. You can clearly describe what we're building
2. You know who it's for and what problem it solves
3. You understand the primary user flow in detail
4. Scope is clearly defined (what's in vs out)
5. Technical approach is clear (or marked as needing research)
6. The user confirms they have nothing more to add

### After Interview

Once the interview is complete:
1. Summarize what you learned
2. Offer to generate a feature spec using the feature-spec-template.md
3. Ask if there's anything to clarify before writing the spec

### Example Questions

**Good questions:**
- "When the user creates a new entry, do they start with a blank form or are there default values/prompts?"
- "You mentioned 'simple settings' - can you give me 2-3 examples of settings users would configure?"
- "What should happen if the API call fails? Show an error? Retry? Fall back to cached data?"

**Bad questions (too vague):**
- "What do you want the feature to do?"
- "How should errors work?"
- "What's the UI like?"

## Notes

- For big features, expect 20-40+ questions across multiple rounds
- It's better to over-interview than under-interview
- The user can always say "I haven't decided yet" - capture that as an open question
- Reference BrainDrive personas (Adam Carter, Katie Carter, Privacy-Focused Pat) when relevant
