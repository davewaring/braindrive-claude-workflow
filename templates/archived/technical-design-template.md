# Technical Design: [Feature Name]

> **ARCHIVED:** This template is kept for reference only. For new features, use `plan-template.md` which consolidates architecture, roadmap, and milestones into a single execution document. This reduces document drift and provides a single source of truth.
>
> See the AI Installer project (January 2025) for the rationale behind this consolidation.

---

> Based on feature spec dated [Date]

## Decision Summary

| Aspect | Decision |
|--------|----------|
| Implementation | Plugin / Core |
| Frontend Framework | React 18 + TypeScript + MUI (default) |
| Backend Framework | FastAPI + SQLModel (default) |
| Database Changes | Yes / No |
| New Endpoints | Yes / No |

## Architecture Overview

### Component Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    BrainDrive Core                       │
├─────────────────────────────────────────────────────────┤
│                                                          │
│   ┌──────────────┐     ┌──────────────────────────┐     │
│   │              │     │     Service Bridges       │     │
│   │   Feature    │────▶│  - API Bridge            │     │
│   │   Plugin     │     │  - Events Bridge         │     │
│   │              │     │  - [Others as needed]    │     │
│   └──────────────┘     └────────────┬─────────────┘     │
│                                      │                   │
└──────────────────────────────────────┼───────────────────┘
                                       │
                                       ▼
                          ┌────────────────────────┐
                          │      Backend API       │
                          │  /api/v1/feature/...   │
                          └────────────────────────┘
```

### Components

#### 1. [Component Name]
- **Purpose:** [What it does]
- **Location:** `src/components/[name]/`
- **Dependencies:** [What it imports/uses]

#### 2. [Component Name]
- **Purpose:** [What it does]
- **Location:** `src/services/[name]/`
- **Dependencies:** [What it imports/uses]

### Data Flow

1. User [action] in UI
2. Component calls [service/function]
3. Service uses [Bridge] to call backend
4. Backend [processes/stores/retrieves]
5. Response flows back to UI
6. UI updates to show [result]

## Service Bridge Usage

### API Bridge
```typescript
// Example usage
import { useAPIBridge } from '@braindrive/service-bridges';

const api = useAPIBridge();
const result = await api.post('/api/v1/feature/action', { data });
```

### [Other Bridges]
```typescript
// Usage examples for each bridge used
```

## Database Schema

### New Tables

```python
# [table_name].py
from sqlmodel import SQLModel, Field
from typing import Optional
from datetime import datetime

class FeatureItem(SQLModel, table=True):
    __tablename__ = "feature_items"

    id: Optional[int] = Field(default=None, primary_key=True)
    user_id: int = Field(foreign_key="user.id", index=True)
    name: str = Field(max_length=255)
    data: dict = Field(default_factory=dict, sa_column_kwargs={"type_": JSON})
    created_at: datetime = Field(default_factory=datetime.utcnow)
    updated_at: Optional[datetime] = Field(default=None)
```

### Schema Changes to Existing Tables

| Table | Change | Migration |
|-------|--------|-----------|
| [table] | [add column X] | [migration name] |

### Migration Plan
```bash
# Generate migration
alembic revision --autogenerate -m "add_feature_tables"

# Apply migration
alembic upgrade head
```

## API Design

### Endpoints

#### POST /api/v1/feature/create
Create a new feature item.

**Request:**
```json
{
  "name": "string",
  "data": {}
}
```

**Response (201):**
```json
{
  "id": 1,
  "name": "string",
  "data": {},
  "created_at": "2024-01-01T00:00:00Z"
}
```

**Errors:**
- `400` - Invalid request body
- `401` - Not authenticated
- `422` - Validation error

#### GET /api/v1/feature/{id}
Get a feature item by ID.

**Response (200):**
```json
{
  "id": 1,
  "name": "string",
  "data": {},
  "created_at": "2024-01-01T00:00:00Z"
}
```

**Errors:**
- `401` - Not authenticated
- `404` - Item not found

### [Additional Endpoints]

## Frontend Structure

```
src/
├── components/
│   └── Feature/
│       ├── FeatureContainer.tsx    # Main container with state
│       ├── FeatureView.tsx         # Presentation component
│       ├── FeatureForm.tsx         # Form for input
│       └── index.ts                # Exports
├── services/
│   └── featureService.ts           # API calls
├── hooks/
│   └── useFeature.ts               # Custom hook for feature logic
├── types/
│   └── feature.ts                  # TypeScript types
└── utils/
    └── featureHelpers.ts           # Utility functions
```

## Error Handling

### Frontend
- API errors caught and displayed via toast/alert
- Loading states shown during async operations
- Retry logic for transient failures

### Backend
- Input validation with Pydantic
- Consistent error response format
- Logging with structlog

## Security Considerations

- [ ] User authentication required for all endpoints
- [ ] User can only access their own data (user_id filter)
- [ ] Input sanitization for [specific fields]
- [ ] Rate limiting on [specific endpoints]

## Performance Considerations

- [ ] Pagination for list endpoints (limit: 50 default)
- [ ] Database indexes on [fields]
- [ ] Caching strategy: [describe if applicable]

## Dependencies

### New Packages
| Package | Version | Purpose |
|---------|---------|---------|
| [package] | [version] | [why needed] |

### Infrastructure
- [ ] [Any external services needed]
- [ ] [Environment variables to configure]

## Testing Strategy

### Unit Tests
- [ ] Service functions
- [ ] Utility functions
- [ ] Component logic

### Integration Tests
- [ ] API endpoints
- [ ] Database operations

### E2E Tests (Playwright)
- [ ] Core user flow
- [ ] Error states

## Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | Low/Med/High | Low/Med/High | [How to handle] |

## Open Technical Questions

- [ ] [Question needing research or decision]

---

## Approval

- [ ] Architecture reviewed by: _______________
- [ ] Date: _______________
- [ ] Ready for Milestones: [ ]
