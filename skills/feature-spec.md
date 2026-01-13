# Feature Spec Skill

Use this skill to generate a feature specification document from interview notes or conversation context.

## Trigger
`/feature-spec [optional: feature name]`

## Instructions

When this skill is triggered, generate a comprehensive feature specification document based on:
1. The interview conducted (if `/interview` was run)
2. Any existing conversation context about the feature
3. User clarification if needed

### Process

1. **Review Context**
   - Read through the conversation to gather all feature information
   - Identify any gaps or unclear areas

2. **Clarify Gaps** (if needed)
   - If critical information is missing, ask the user using AskUserQuestion
   - Focus only on blockers - don't re-interview

3. **Generate Spec**
   - Read the feature-spec-template.md from the templates folder
   - Fill in all sections based on gathered information
   - Mark incomplete sections with `[TODO: ...]`

4. **Write to File**
   - Create the spec in the current project's docs folder
   - Name: `feature-spec-[feature-name].md`
   - Or ask user for preferred location

5. **Review with User**
   - Summarize what was captured
   - Highlight any TODO items or open questions
   - Ask if anything needs adjustment

### Spec Quality Checklist

Before presenting the spec, ensure:

- [ ] **Overview** is clear and concise (someone could understand the feature in 30 seconds)
- [ ] **Target user** is specific (which persona, what context)
- [ ] **Problem statement** explains the pain, not just the solution
- [ ] **User stories** describe specific flows, not vague capabilities
- [ ] **MVP scope** is clearly bounded (what's in AND what's out)
- [ ] **Technical context** identifies all integration points
- [ ] **Open questions** capture any unresolved items

### Template Reference

Use the structure from `templates/feature-spec-template.md`:

```markdown
# Feature Spec: [Name]

## Overview
## Target User
## Problem Statement
## User Stories
## Detailed Requirements
## Scope (MVP vs Future)
## Technical Context
## Open Questions
## Success Definition
```

### Handling Incomplete Information

For any section without clear information:
- Mark as `[TODO: needs clarification]`
- Or mark as `[TBD: to be decided during technical design]`
- Don't invent details - better to have explicit gaps

### Output

The skill outputs:
1. A complete feature-spec.md file
2. A summary of what's captured
3. A list of open questions or TODOs
4. Recommendation for next step (usually `/plan` to create the execution plan)

## Example Output Summary

```
## Feature Spec Generated

I've created `docs/feature-spec-user-settings.md` with:

**Captured:**
- Clear overview of settings management feature
- Target user: Builders who want to customize their BrainDrive
- Primary flow: Access settings → Modify → Save → See confirmation
- MVP scope: 5 core settings, excludes import/export

**Open Questions:**
- [ ] Should settings sync across devices?
- [ ] What's the reset to defaults behavior?

**Next Step:**
Run `/plan` to design the architecture and create the execution plan, or clarify open questions first.
```
