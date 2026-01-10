# Phase 3: Technical Design

## Purpose

Define HOW we're building the feature. This phase produces an architecture and implementation approach that Claude can follow autonomously.

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

### Step 2: Identify Integration Points

**For Plugins:**
Which Service Bridges will you use?
- **API Bridge** - Backend HTTP calls
- **Events Bridge** - Cross-plugin communication
- **Theme Bridge** - Light/dark mode awareness
- **Settings Bridge** - User preferences
- **Page Context Bridge** - Page metadata access
- **Plugin State Bridge** - Persistent plugin state

**For Core:**
- Which existing modules are affected?
- What new endpoints are needed?
- Database schema changes?

### Step 3: Architecture Overview

Create a high-level diagram or description:

```markdown
## Architecture

### Components
1. **FeatureUI** - Main React component
   - Renders the primary interface
   - Uses Theme Bridge for styling

2. **FeatureService** - Business logic
   - Calls backend via API Bridge
   - Manages local state

3. **Backend Endpoint** (if needed)
   - POST /api/v1/feature/action
   - Returns processed result

### Data Flow
1. User interacts with FeatureUI
2. FeatureUI calls FeatureService
3. FeatureService uses API Bridge to call backend
4. Backend processes and returns result
5. FeatureUI updates to show result
```

### Step 4: Database Schema (if applicable)

Define any new tables or modifications:

```python
class FeatureItem(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    user_id: int = Field(foreign_key="user.id")
    name: str
    data: dict
    created_at: datetime = Field(default_factory=datetime.utcnow)
```

### Step 5: API Design (if applicable)

Define new endpoints:

```markdown
## API Endpoints

### POST /api/v1/feature/create
Create a new feature item.

**Request:**
```json
{
  "name": "string",
  "data": {}
}
```

**Response:**
```json
{
  "id": 1,
  "name": "string",
  "data": {},
  "created_at": "2024-01-01T00:00:00Z"
}
```
```

### Step 6: Identify Constraints and Dependencies

List anything that limits or affects implementation:

```markdown
## Constraints
- Must work offline (no external API calls)
- Must support existing user data (migration needed)
- Performance: Response under 200ms

## Dependencies
- Requires Settings Bridge v1.0+
- Uses existing User model
- Needs new npm package: xyz
```

### Step 7: Provision Infrastructure

If you need external services, set them up NOW:
- Create database tables
- Set up API keys
- Configure environment variables
- Initialize any cloud services

Don't leave this for the build phase.

## Output

Create `technical-design.md` with:

1. **Decision: Plugin vs Core** - With justification
2. **Tech Stack** - Any deviations from defaults
3. **Architecture Overview** - Components and data flow
4. **Integration Points** - Service Bridges or core modules
5. **Database Schema** - New tables/fields
6. **API Design** - New endpoints
7. **Constraints & Dependencies** - Limitations and requirements

## Tips for BrainDrive

### Starting a New Plugin

1. Clone the [Plugin Template](https://github.com/BrainDriveAI/BrainDrive-PluginTemplate)
2. Follow [Plugin Dev Quickstart](https://docs.braindrive.ai/core/plugin-development/quickstart)
3. Reference the Service Bridge example that matches your needs
4. Use the 1-minute build cycle for rapid iteration

### Plugin Naming Convention

- Plugin name: `kebab-case` (e.g., `my-awesome-plugin`)
- Component IDs: `PascalCase` (e.g., `MyAwesomeModule`)
- Important: Plugin name ≠ module name (use different names)

### Core Modifications

- Minimize changes to existing files
- Add new endpoints in new files when possible
- Always include database migration
- Update API documentation

## Next Phase

Once you have a technical design, move to [Phase 4: Milestones](./phase-4-milestones.md) to break the work into testable chunks.
