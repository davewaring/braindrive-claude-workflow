# Plan Skill

Use this skill to generate a plan document from a feature spec. The plan is the single execution document that combines architecture, roadmap, and milestones.

## Trigger

`/plan [optional: feature name]`

## Instructions

When this skill is triggered, generate a comprehensive plan document based on:
1. The feature spec (if `feature-spec.md` exists)
2. Any existing conversation context about technical decisions
3. User clarification if needed

### Process

1. **Review Feature Spec**
   - Read the `feature-spec.md` to understand what we're building
   - Identify the MVP scope and success criteria
   - Note any technical constraints mentioned

2. **Gather Technical Decisions** (if not already discussed)
   Use AskUserQuestion to clarify:
   - Plugin or core modification?
   - Any deviations from BrainDrive defaults (React/FastAPI/SQLite)?
   - Key architectural decisions?
   - External services or infrastructure needed?

3. **Design Architecture**
   Based on the feature spec and decisions:
   - Identify main components
   - Map the data flow
   - Define integration points (Service Bridges for plugins)
   - Outline database schema if needed
   - Define API endpoints if needed

4. **Break Into Phases**
   Divide work into 3-5 testable phases:
   - Each phase should be independently verifiable
   - Order by dependency (what must be done first)
   - Include clear success criteria for each

5. **Generate Plan**
   - Read the `plan-template.md` from the templates folder
   - Fill in all sections based on gathered information
   - Mark incomplete sections with `[TODO: ...]`

6. **Write to File**
   - Create the plan in the project's docs or plans folder
   - Name: `plan.md` (or `plan-[feature-name].md` if multiple features)
   - Or ask user for preferred location

7. **Review with User**
   - Summarize the architecture and phases
   - Highlight any TODO items or open questions
   - Ask if anything needs adjustment before build phase

### Plan Quality Checklist

Before presenting the plan, ensure:

- [ ] **Key decisions** are documented with rationale
- [ ] **Architecture** is clear (someone could understand the structure in 2 minutes)
- [ ] **Phases** are ordered by dependency
- [ ] **Success criteria** are specific and verifiable (commands to run, expected results)
- [ ] **Exit criteria** for each phase are clear
- [ ] **Open items** capture any unresolved questions

### Template Reference

Use the structure from `templates/plan-template.md`:

```markdown
# Plan: [Name]

**Status:** [Not Started / In Progress / Complete]
**Created:** [Date]
**Updated:** [Date]

## Overview
## Key Decisions
## Architecture
## Implementation Roadmap
  ### Phase 1: [Name]
  ### Phase 2: [Name]
  ### Phase 3: [Name]
## Technical Details
## Security Considerations
## Risks & Mitigations
## Open Items
## Completion Checklist
```

### Handling Missing Information

For any section without clear information:
- Ask the user using AskUserQuestion if it's blocking
- Mark as `[TODO: needs decision]` if it can wait
- Don't invent technical details - better to have explicit gaps

### Success Criteria Format

For each phase, use this format for success criteria:

```markdown
| Criterion | Verification | Expected Result |
|-----------|--------------|-----------------|
| Build succeeds | `npm run build` | Exit code 0 |
| Tests pass | `npm test` | All tests green |
| API responds | `curl -X POST /api/v1/...` | 200 with expected body |
```

### Output

The skill outputs:
1. A complete `plan.md` file
2. A summary of the architecture
3. A list of phases with their goals
4. Any open questions or TODOs
5. Confirmation ready to proceed to build phase

## Example Output Summary

```
## Plan Generated

I've created `plans/active/user-settings/plan.md` with:

**Architecture:**
- Plugin using Settings Bridge + API Bridge
- 2 new backend endpoints
- SQLite table for user preferences

**Phases:**
1. Foundation - Plugin structure, basic UI (2 tasks)
2. Backend Integration - API endpoints, database (4 tasks)
3. Polish - Error handling, tests, docs (3 tasks)

**Open Items:**
- [ ] Decide: Should settings sync across devices?

**Next Step:**
Ready for Phase 3 (Build). Run `/milestone-check` after each phase to verify success criteria.
```

## Notes

- The plan should be detailed enough that Claude can execute it autonomously
- Focus on verifiable success criteria - if Claude can't verify it, flag for human checkpoint
- Keep the plan as a living document - update status as phases complete
