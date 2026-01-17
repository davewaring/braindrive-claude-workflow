# Capture Session Skill

Capture this coding session directly into the BrainDrive Library.

## Trigger

`/capture [optional: project name]`

## Instructions

When triggered, capture the current session by updating the BrainDrive Library directly.

### Process

1. **Identify What to Capture**
   - Review the conversation for key decisions, actions, and outcomes
   - Identify which project(s) this session relates to
   - Note any status changes

2. **Create Transcript Summary**
   - Location: `~/BrainDrive-Library/transcripts/YYYY-MM/YYYY-MM-DD-topic-participants.md`
   - Use today's date
   - Include: summary, key decisions, action items, files changed

3. **Update Decisions (if any)**
   - Location: `~/BrainDrive-Library/projects/active/[project]/decisions.md`
   - For each significant decision: what, context, rationale
   - Create the file if it doesn't exist

4. **Update AGENT.md (if relevant)**
   - Update project status in Active Projects table (if changed)
   - Add entry to Recent Activity section
   - Update Action Items (if new ones assigned)

5. **Commit and Push**
   - Stage all Library changes
   - Commit with descriptive message
   - Push to remote

### Transcript Format

```markdown
# [Topic] - [Date]

**Participants:** [Names]
**Project:** [project-name]

---

## Summary

[2-3 sentence summary of what was accomplished]

## Key Decisions

### [Decision 1]
- **Decision:** [What was decided]
- **Rationale:** [Why]

## Action Items

- [ ] [Item 1]
- [ ] [Item 2]

## Files Changed

- [List of files created/modified, if applicable]
```

### Decision Format

```markdown
## Decision: [Title]

**Date:** YYYY-MM-DD
**Context:** [Why this came up]

**Decision:** [What was decided]

**Rationale:** [Why this choice]

**Trade-offs:** [What we considered]
```

### Output

After capturing, report:
- What transcript was created
- What files were updated
- Commit hash

### Example

```
## Session Captured

**Transcript:** transcripts/2026-01/2026-01-17-auth-refactor-dave-w-claude.md

**Updated:**
- projects/active/security-audit/decisions.md (2 new decisions)
- AGENT.md (status update, recent activity)

**Commit:** a1b2c3d - "Capture auth refactor session"

Pushed to origin/main.
```
