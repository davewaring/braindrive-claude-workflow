# Milestones: [Feature Name]

> **ARCHIVED:** This template is kept for reference only. For new features, use `plan-template.md` which consolidates architecture, roadmap, and milestones into a single execution document. This reduces document drift and provides a single source of truth.
>
> See the AI Installer project (January 2025) for the rationale behind this consolidation.

---

> Based on technical design dated [Date]

## Overview

| Milestone | Description | Est. Complexity |
|-----------|-------------|-----------------|
| 1 | [Name] | Low / Medium / High |
| 2 | [Name] | Low / Medium / High |
| 3 | [Name] | Low / Medium / High |
| 4 | [Name] | Low / Medium / High |
| 5 | [Name] | Low / Medium / High |

## Dependency Graph

```
Milestone 1 ──▶ Milestone 2 ──▶ Milestone 3
                    │
                    └──▶ Milestone 4 ──▶ Milestone 5
```

---

## Milestone 1: [Name]

### Description
[What this milestone accomplishes - 2-3 sentences]

### Tasks
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

### Files to Create/Modify
- `path/to/file1.tsx` - [what changes]
- `path/to/file2.py` - [what changes]

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| Build succeeds | `npm run build` | Exit code 0, no errors |
| No TypeScript errors | `npx tsc --noEmit` | Exit code 0 |
| [Criterion 3] | `[command]` | [expected] |
| [Criterion 4] | `[command]` | [expected] |

### Human Checkpoint
- [ ] [Any manual verification needed?]

### Commit Message Template
```
feat(feature): milestone 1 - [name]

- [Change 1]
- [Change 2]
- Verified: [what was verified]
```

---

## Milestone 2: [Name]

### Description
[What this milestone accomplishes]

### Dependencies
- Requires: Milestone 1 complete

### Tasks
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

### Files to Create/Modify
- `path/to/file1.tsx`
- `path/to/file2.py`

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| API endpoint responds | `curl -X POST http://localhost:8005/api/v1/feature/create -H "Content-Type: application/json" -d '{"name":"test"}'` | 201 response with id |
| [Criterion 2] | `[command]` | [expected] |
| [Criterion 3] | `[command]` | [expected] |

### Human Checkpoint
- [ ] [Any manual verification?]

---

## Milestone 3: [Name]

### Description
[What this milestone accomplishes]

### Dependencies
- Requires: Milestone 2 complete

### Tasks
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

### Files to Create/Modify
- `path/to/file.tsx`

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| [Criterion 1] | `[command]` | [expected] |
| [Criterion 2] | `[command]` | [expected] |
| Unit tests pass | `npm test -- --coverage` | All tests pass, coverage > 80% |

### Human Checkpoint
- [ ] Review: Does the core functionality work as expected?

---

## Milestone 4: [Name]

### Description
[What this milestone accomplishes]

### Dependencies
- Requires: Milestone 3 complete

### Tasks
- [ ] [Task 1]
- [ ] [Task 2]

### Files to Create/Modify
- `path/to/file.tsx`

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| Settings persist | `[command or Playwright test]` | [expected] |
| [Criterion 2] | `[command]` | [expected] |

### Human Checkpoint
- [ ] [Any manual verification?]

---

## Milestone 5: [Name - Usually Polish/Edge Cases]

### Description
[Final polish, error handling, edge cases]

### Dependencies
- Requires: All previous milestones complete

### Tasks
- [ ] Add error handling for [case]
- [ ] Add loading states
- [ ] Handle edge case: [describe]
- [ ] Final cleanup and documentation

### Files to Create/Modify
- [Various files for polish]

### Success Criteria

| Criterion | Verification Command | Expected Result |
|-----------|---------------------|-----------------|
| All tests pass | `npm test && pytest` | All green |
| No linting errors | `npm run lint` | Exit code 0 |
| Playwright E2E passes | `npx playwright test` | All tests pass |
| Error states display | `[Playwright test]` | Error UI shown |

### Human Checkpoint
- [ ] Final review before merge
- [ ] Test with real/production-like data

---

## Completion Checklist

### Code
- [ ] All milestones complete
- [ ] All tests passing
- [ ] No linting errors
- [ ] Code reviewed

### Documentation
- [ ] Changelog updated
- [ ] Architecture docs updated (if structure changed)
- [ ] README updated (if applicable)

### Deployment
- [ ] Database migrations run (if applicable)
- [ ] Environment variables documented
- [ ] Feature tested in staging

---

## Notes

[Any additional notes, learnings, or context for future reference]
