# Plan Skill

Use this skill to generate a build plan from a feature spec. The build plan is the single execution document that combines architecture, roadmap, and milestones.

**Framework Phase:** 2 - Plan
**Output Location:** `BrainDrive-Library/projects/active/[project-name]/build-plan.md`

## Trigger

`/plan [optional: feature name]`

## Instructions

When this skill is triggered, generate a comprehensive build plan based on:
1. The spec (if `spec.md` exists in Library)
2. Any existing conversation context about technical decisions
3. User clarification if needed

### Process

1. **Review Spec**
   - Read the `spec.md` from BrainDrive-Library to understand what we're building
   - Identify the MVP scope and success criteria
   - Note any technical constraints mentioned
   - Check related projects for patterns and decisions

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

5. **Generate Build Plan**
   - Read `templates/build-plan-template.md` from the workflow repo
   - Fill in all sections based on gathered information
   - Mark incomplete sections with `[TODO: ...]`
   - Include human checkpoints based on output types

6. **Write to File**
   - Create the build plan in BrainDrive-Library: `projects/active/[project-name]/build-plan.md`
   - Or ask user for preferred location if not using Library

7. **Review with User**
   - Summarize the architecture and phases
   - Highlight any TODO items or open questions
   - Ask if anything needs adjustment before Setup phase

### Plan Quality Checklist

Before presenting the plan, ensure:

- [ ] **Key decisions** are documented with rationale
- [ ] **Architecture** is clear (someone could understand the structure in 2 minutes)
- [ ] **Phases** are ordered by dependency
- [ ] **Success criteria** are specific and verifiable (commands to run, expected results)
- [ ] **Exit criteria** for each phase are clear
- [ ] **Open items** capture any unresolved questions

### Template Reference

Use the structure from `templates/build-plan-template.md`:

```markdown
# Build Plan: [Name]

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
## Human Checkpoints
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
1. A complete `build-plan.md` file saved to Library
2. A summary of the architecture
3. A list of phases with their goals
4. Human checkpoints identified
5. Any open questions or TODOs
6. Confirmation ready to proceed to Setup phase

## Example Output Summary

```
## Build Plan Generated

I've created `BrainDrive-Library/projects/active/user-settings/build-plan.md` with:

**Architecture:**
- Plugin using Settings Bridge + API Bridge
- 2 new backend endpoints
- SQLite table for user preferences

**Phases:**
1. Foundation - Plugin structure, basic UI (2 tasks)
2. Backend Integration - API endpoints, database (4 tasks)
3. Polish - Error handling, tests, docs (3 tasks)

**Human Checkpoints:**
- After Phase 2: UX review (user-facing UI)
- After Phase 3: Final review before merge

**Open Items:**
- [ ] Decide: Should settings sync across devices?

**Next Step:**
Proceed to Setup phase (verify environment, permissions), then Build.
Run `/milestone-check` after each phase to verify success criteria.
```

## Notes

- The build plan should be detailed enough that Claude can execute it autonomously
- Focus on verifiable success criteria - if Claude can't verify it, flag for human checkpoint
- Keep the build plan as a living document - update status as phases complete
- Include human checkpoints for user-facing outputs
