# Retro Skill

Use this skill after completing a feature to capture learnings and improve the workflow system.

## Trigger
`/retro`

## Instructions

When this skill is triggered, conduct a retrospective on the just-completed feature and suggest improvements to the workflow system.

### Process

1. **Gather Context**
   - Review the feature spec, technical design, and milestones
   - Look at the git history for this feature
   - Identify any issues or struggles encountered

2. **Interview for Feedback**
   - Ask the user 3-5 focused questions about the experience
   - Focus on what worked, what didn't, and what was surprising

3. **Analyze Patterns**
   - Identify recurring issues
   - Note any workarounds that were needed
   - Find gaps in templates or documentation

4. **Suggest Improvements**
   - Propose specific changes to templates, skills, or docs
   - Prioritize by impact

5. **Update System** (with user approval)
   - Update CLAUDE.md with new learnings
   - Improve templates based on feedback
   - Add new patterns to documentation

### Retro Questions

Ask these using AskUserQuestion (adapt based on context):

**Round 1: Overall Experience**
- How smooth was the development process? (1-5 scale)
- What was the biggest friction point?

**Round 2: Specific Phases**
- Did the interview surface the right requirements?
- Was the technical design detailed enough?
- Were the milestone success criteria useful?

**Round 3: Improvements**
- What would you do differently next time?
- What should be added to the templates?
- Any new patterns we should document?

### Analysis Checklist

Review these areas:

**Planning Phase:**
- [ ] Were requirements clear enough?
- [ ] Did we miss any major requirements?
- [ ] Was scope well-defined?

**Technical Design:**
- [ ] Was the architecture appropriate?
- [ ] Any unexpected technical challenges?
- [ ] Did the tech stack choices work well?

**Milestones:**
- [ ] Were milestones sized appropriately?
- [ ] Were success criteria verifiable?
- [ ] How many attempts to pass each milestone?

**Build Phase:**
- [ ] How much rework was needed?
- [ ] Were there any blocking issues?
- [ ] How much human intervention was required?

### Output Format

```markdown
## Feature Retro: [Feature Name]

### Summary
- **Overall Smoothness:** 4/5
- **Time Spent:** [estimate]
- **Rework Required:** Low / Medium / High

### What Worked Well
1. [Thing that worked]
2. [Another thing]

### What Could Improve
1. [Issue] → **Suggested Fix:** [improvement]
2. [Issue] → **Suggested Fix:** [improvement]

### Learnings to Capture

#### For CLAUDE.md
```markdown
# Add to CLAUDE.md:
- When building [type of feature], always [pattern]
- Avoid [antipattern] because [reason]
```

#### For Templates
- Add [field] to feature-spec-template.md
- Add [check] to milestones-template.md

#### For Skills
- Update /interview to ask about [topic]
- Add [criterion] to /milestone-check

### Action Items
- [ ] Update CLAUDE.md with learnings
- [ ] Improve [template]
- [ ] Add [pattern] to documentation

Shall I make these updates now?
```

### System Updates

With user approval, update:

**CLAUDE.md** - Add new patterns and lessons:
```markdown
## Learnings from [Feature Name]

### Patterns
- [Pattern description]

### Antipatterns to Avoid
- [What to avoid and why]
```

**Templates** - Add missing fields or sections

**Skills** - Improve based on friction points

**Docs** - Add new guidance or examples

### Continuous Improvement Loop

This skill creates a continuous improvement cycle:

```
Build Feature → /retro → Update System → Next Feature (improved)
```

Over time, the workflow system becomes more refined and features become easier to build.

### When to Skip Retro

Skip if:
- Feature was trivial (< 1 hour of work)
- No significant learnings
- Immediate time pressure

But generally, run retro - even 5 minutes of reflection improves the next feature.

## Example Retro Summary

```markdown
## Feature Retro: User Settings Plugin

### Summary
- **Overall Smoothness:** 3/5
- **Rework Required:** Medium

### What Worked Well
1. Interview surfaced the "sync across devices" question early
2. Milestone success criteria caught a bug before commit

### What Could Improve
1. **Template missing error state section** → Add "Error Handling" section to feature-spec-template
2. **Settings Bridge example was outdated** → Update example repo

### Learnings to Capture

#### For CLAUDE.md
```markdown
- When using Settings Bridge, always check for undefined before accessing nested values
- Settings changes should emit an event for other plugins to react
```

### Action Items
- [x] Updated CLAUDE.md with Settings Bridge pattern
- [x] Added Error Handling section to feature-spec-template.md
- [ ] (Separate task) Update Settings Bridge example repo
```
