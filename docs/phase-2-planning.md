# Phase 2: Planning

## Purpose

Define HOW we're building the feature and break the work into testable milestones. This phase produces `plan.md` - a single execution document that combines architecture, technical decisions, roadmap, and success criteria.

## Output

This phase produces `plan.md` - the "how" document for engineering that includes:
- Key decisions and rationale
- Architecture overview
- Implementation roadmap with phases
- Success criteria for each phase
- Technical details (database, API, dependencies)

## Why a Single Plan Document?

Previous workflows used separate documents for technical design and milestones. Experience showed:
- **Multiple docs drift out of sync** - Architecture changes but milestones don't get updated
- **Hard to find the "current truth"** - Which doc has the latest status?
- **Maintenance overhead** - 3 docs to update vs 1

The consolidated `plan.md` provides:
- **Single source of truth** for execution
- **Clear status** at a glance
- **Less drift** between architecture and tasks

## Process

### Step 1: Plugin or Core?

Decide where this feature belongs:

**Build as a Plugin if:**
- It's a new capability users can install/uninstall
- It doesn't require changes to core auth/security
- It can work through Service Bridges
- Other users might want to customize or replace it

**Build as Core if:**
- It's fundamental infrastructure (auth, routing, etc.)
- It needs to be available to all plugins
- It's a Service Bridge extension
- Security requires it to be in core

Most features should be plugins. Core modifications require justification.

### Step 2: Make Key Decisions

Document the major decisions that shape the implementation:

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Implementation | Plugin / Core | [Why] |
| Frontend | React + MUI (default) | [Or deviation] |
| Backend | FastAPI (default) | [Or deviation] |
| Database | SQLite (default) | [If changes needed] |

### Step 3: Design the Architecture

Create a high-level view of components and data flow:

```markdown
## Architecture

### Components
1. **FeatureUI** - Main React component
2. **FeatureService** - Business logic, API calls
3. **Backend Endpoint** - /api/v1/feature/...

### Data Flow
1. User interacts with FeatureUI
2. FeatureUI calls FeatureService
3. FeatureService uses API Bridge to call backend
4. Backend processes and returns result
5. FeatureUI updates to show result
```

### Step 4: Break Into Phases/Milestones

Divide the work into 3-5 phases. Each phase should be:
- **Independently testable** - Can verify it works without later phases
- **Valuable on its own** - Delivers some functionality
- **Small enough to complete** - Can finish in one focused session
- **Clear when done** - Obvious success/failure

**Example:**
```markdown
### Phase 1: Foundation
Set up plugin structure, basic UI shell

### Phase 2: Core Integration
Connect to backend, implement main functionality

### Phase 3: Polish
Error handling, edge cases, documentation
```

### Step 5: Define Success Criteria for Each Phase

For each phase, define criteria Claude can verify:

**Types of Verifiable Criteria:**

1. **Build/Compile Checks**
   - `npm run build` - Exit code 0
   - `npx tsc --noEmit` - No TypeScript errors

2. **Automated Tests**
   - `npm test` - All tests pass
   - `pytest tests/` - Backend tests pass

3. **API Verification**
   - POST /api/v1/feature/create returns 200
   - Invalid input returns 422 with error details

4. **Visual Verification (Playwright)**
   - Component renders at expected route
   - User interactions work as expected

**Format each phase with clear exit criteria:**

```markdown
### Phase 1: Foundation

**Goal:** Plugin structure with working component that displays in BrainDrive

**Tasks:**
- [ ] Create plugin from template
- [ ] Set up main component
- [ ] Configure routing

**Success Criteria:**

| Criterion | Verification | Expected |
|-----------|--------------|----------|
| Build succeeds | `npm run build` | Exit code 0 |
| No TS errors | `npx tsc --noEmit` | Exit code 0 |
| Component renders | Manual or Playwright | Plugin visible |

**Exit Criteria:** User can navigate to plugin and see the basic UI
```

### Step 6: Identify Human Checkpoints

Some things Claude can't verify. Be explicit:

```markdown
## Human Checkpoints

### After Phase 2
- [ ] Review: Does the UX feel right?
- [ ] Review: Is the design consistent with BrainDrive?

### After Phase 3
- [ ] Final review before merge
- [ ] Test with real data
```

### Step 7: Generate the Plan

Use `/plan` to generate `plan.md` from your feature spec and planning decisions. The plan should follow the template structure.

## BrainDrive Defaults

Unless you have a specific reason to deviate, use these:

**Frontend:**
- React 18 + TypeScript
- Material-UI (MUI) v5
- Vite for building
- Zod for validation

**Backend:**
- FastAPI
- SQLModel (SQLAlchemy + Pydantic)
- SQLite (default database)
- Alembic for migrations

**Plugins:**
- Webpack Module Federation
- Service Bridges for core integration
- Plugin Template as starting point

## Tips for Effective Planning

### Order Phases by Dependency

Ensure Claude can complete phases in order:
```markdown
1. **Foundation** - No dependencies
2. **Core Integration** - Depends on: Foundation
3. **Polish** - Depends on: Core Integration
```

### Be Specific in Success Criteria

Bad: "The feature works"
Good: "POST /api/v1/feature returns 200 with id field in response"

### Include Negative Cases

Don't just test the happy path:
- What happens with invalid input?
- What happens when the backend is down?
- What happens with empty data?

### Provision Infrastructure Now

If you need external services, set them up during planning:
- Create database tables
- Set up API keys
- Configure environment variables

Don't leave this for the build phase.

## Next Phase

Once you have a complete plan with phases and success criteria, move to [Phase 3: Build](./phase-3-build.md) to start implementation.
