# Build Plan: [Feature Name]

> **Save to:** `BrainDrive-Library/projects/active/[project-name]/build-plan.md`

**Status:** [Not Started / In Progress / Complete]
**Created:** [Date]
**Updated:** [Date]
**Repository:** [Link if applicable]

---

## Overview

[2-3 sentence summary of what we're building and why.]

See `spec.md` for detailed requirements and user stories.

---

## Key Decisions

| Decision | Choice | Rationale |
|----------|--------|-----------|
| [Decision 1] | **[Choice]** | [Why this choice] |
| [Decision 2] | **[Choice]** | [Why this choice] |
| [Decision 3] | **[Choice]** | [Why this choice] |

---

## Architecture

### Component Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                     [System Name]                            │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│   ┌──────────────┐     ┌──────────────────────────┐         │
│   │              │     │                          │         │
│   │  Component A │────▶│      Component B         │         │
│   │              │     │                          │         │
│   └──────────────┘     └────────────┬─────────────┘         │
│                                      │                       │
└──────────────────────────────────────┼───────────────────────┘
                                       │
                                       ▼
                          ┌────────────────────────┐
                          │      External API      │
                          └────────────────────────┘
```

### Components

#### 1. [Component Name]
- **Purpose:** [What it does]
- **Location:** `path/to/component/`
- **Key files:** [List main files]

#### 2. [Component Name]
- **Purpose:** [What it does]
- **Location:** `path/to/component/`
- **Key files:** [List main files]

### Data Flow

1. User [action]
2. [Component A] [processes/routes]
3. [Component B] [handles/stores]
4. Response flows back to user

---

## Implementation Roadmap

### Schedule Overview

| Phase | Goal | Owner | Status |
|-------|------|-------|--------|
| 1 | [Goal] | [Name] | Not Started |
| 2 | [Goal] | [Name] | Not Started |
| 3 | [Goal] | [Name] | Not Started |

### Phase 1: [Name]

**Goal:** [One sentence describing what this phase accomplishes]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Success Criteria:**

| Criterion | Verification | Expected Result |
|-----------|--------------|-----------------|
| [Criterion 1] | `[command]` | [Expected output] |
| [Criterion 2] | `[command]` | [Expected output] |
| Build succeeds | `npm run build` | Exit code 0 |

**Exit Criteria:** [One sentence: what must be true to move to Phase 2]

### Phase 2: [Name]

**Goal:** [One sentence]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Success Criteria:**

| Criterion | Verification | Expected Result |
|-----------|--------------|-----------------|
| [Criterion 1] | `[command]` | [Expected output] |

**Exit Criteria:** [What must be true to move to Phase 3]

### Phase 3: [Name]

**Goal:** [One sentence]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]

**Success Criteria:**

| Criterion | Verification | Expected Result |
|-----------|--------------|-----------------|
| [Criterion 1] | `[command]` | [Expected output] |
| All tests pass | `npm test` | All green |

**Exit Criteria:** [What must be true to consider feature complete]

---

## Technical Details

### Tech Stack

| Layer | Technology | Notes |
|-------|------------|-------|
| Frontend | [React/Vue/etc.] | [Any notes] |
| Backend | [FastAPI/Node/etc.] | [Any notes] |
| Database | [SQLite/Postgres/etc.] | [Any notes] |

### Database Schema (if applicable)

```python
# Example SQLModel schema
class FeatureItem(SQLModel, table=True):
    __tablename__ = "feature_items"

    id: Optional[int] = Field(default=None, primary_key=True)
    name: str = Field(max_length=255)
    created_at: datetime = Field(default_factory=datetime.utcnow)
```

### API Endpoints (if applicable)

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/feature/create` | Create new item |
| GET | `/api/v1/feature/{id}` | Get item by ID |
| PUT | `/api/v1/feature/{id}` | Update item |
| DELETE | `/api/v1/feature/{id}` | Delete item |

### Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| [package] | [version] | [why needed] |

---

## Security Considerations

| Threat | Mitigation |
|--------|------------|
| [Threat 1] | [How we handle it] |
| [Threat 2] | [How we handle it] |

---

## Risks & Mitigations

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| [Risk 1] | Low/Med/High | [How to handle] |
| [Risk 2] | Low/Med/High | [How to handle] |

---

## Open Items

- [ ] [Question or decision needed]
- [ ] [Research needed]

---

## Completion Checklist

### Code
- [ ] All phases complete
- [ ] All tests passing
- [ ] No linting errors
- [ ] Code reviewed

### Documentation
- [ ] CLAUDE.md updated (if structure changed)
- [ ] README updated (if applicable)

### Deployment
- [ ] Database migrations run (if applicable)
- [ ] Environment variables documented
- [ ] Feature tested in staging

---

## Human Checkpoints

### After Phase 1
- [ ] [Review item]

### After Phase 2
- [ ] [Review item]

### After Phase 3
- [ ] Final review before merge

---

## Notes

[Any additional context, learnings, or reference links]

---

*Use `/milestone-check [phase]` to verify each phase. Run `/retro` after completion.*
