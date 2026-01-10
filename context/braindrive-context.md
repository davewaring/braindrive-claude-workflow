# BrainDrive Context for Claude Code

This document provides Claude with essential context when working on BrainDrive projects.

## What is BrainDrive?

BrainDrive is a user-owned AI platform with the tagline **"Your AI. Your Rules."**

**Core Values:**
- **Ownership** - Users own their AI, data, and experience
- **Freedom** - Runs locally, no external dependencies required
- **Empowerment** - Enables users to build their own AI-powered tools
- **Sustainability** - Open source, community-driven development

## Target Audience

### Primary Persona: Adam Carter (The Builder)
- Tech-savvy professional, intermediate-advanced skill level
- Values ownership and customization
- Wants to build custom AI-powered workflows
- Comfortable with code but appreciates good UX

### Secondary Personas
- **Katie Carter** - Non-technical user (v1.0 focus)
- **Privacy-Focused Pat** - Values data sovereignty

**Terminology:** Use "Owner", "Builder", "Entrepreneur" instead of "user"

## Tech Stack

### Frontend
- **Framework:** React 18 + TypeScript
- **UI Library:** Material-UI (MUI) v5
- **Build Tool:** Vite
- **Routing:** React Router v7
- **Layout:** React Grid Layout (Page Builder)
- **Validation:** Zod

### Backend
- **Framework:** FastAPI (Python)
- **ORM:** SQLModel (SQLAlchemy + Pydantic)
- **Database:** SQLite (default)
- **Migrations:** Alembic
- **Auth:** JWT tokens
- **Logging:** structlog

### Plugin System
- **Loading:** Webpack Module Federation
- **Integration:** Service Bridges
- **Lifecycle:** Python-based manager

## Architecture

### Plugin-First Philosophy

**Build plugins, not core modifications.**

Core is only for:
- Authentication and security
- Service Bridges
- Fundamental infrastructure

Everything else should be a plugin.

### Service Bridges

Plugins integrate with BrainDrive through 6 Service Bridges:

| Bridge | Purpose | Example Use |
|--------|---------|-------------|
| **API Bridge** | Backend HTTP calls | Fetch/save data |
| **Events Bridge** | Pub/sub messaging | Cross-plugin communication |
| **Theme Bridge** | Theme state access | Light/dark mode styling |
| **Settings Bridge** | User preferences | Store user choices |
| **Page Context Bridge** | Page metadata | Know current page info |
| **Plugin State Bridge** | Persistent state | Save plugin data |

### Module Federation

Plugins are separate repositories loaded at runtime:
- Each plugin is independently deployable
- Plugins can be installed/uninstalled without affecting core
- Versioned independently

## Key Resources

### Documentation
- **Docs Site:** https://docs.braindrive.ai
- **API Reference:** [Complete endpoint documentation]
- **Plugin Quickstart:** https://docs.braindrive.ai/core/plugin-development/quickstart

### Repositories

**Core:**
- [BrainDrive-Core](https://github.com/BrainDriveAI/BrainDrive-Core) - Main application
- [BrainDrive-Docs-Site](https://github.com/BrainDriveAI/BrainDrive-Docs-Site) - Documentation

**Plugin Development:**
- [BrainDrive-PluginTemplate](https://github.com/BrainDriveAI/BrainDrive-PluginTemplate) - Starter template

**Service Bridge Examples:**
- [API Bridge Example](https://github.com/BrainDriveAI/BrainDrive-API-Service-Bridge-Example-Plugin)
- [Events Bridge Example](https://github.com/BrainDriveAI/BrainDrive-Events-Service-Bridge-Example-Plugin)
- [Theme Bridge Example](https://github.com/BrainDriveAI/BrainDrive-Theme-Service-Bridge-Example-Plugin)
- [Settings Bridge Example](https://github.com/BrainDriveAI/BrainDrive-Settings-Service-Bridge-Example-Plugin)
- [Page Context Bridge Example](https://github.com/BrainDriveAI/BrainDrive-Page-Context-Service-Bridge-Example-Plugin)
- [Plugin State Bridge Example](https://github.com/BrainDriveAI/BrainDrive-Plugin-State-Service-Bridge-Example-Plugin)

**Utilities:**
- [BrainDriveScripts](https://github.com/DJJones66/BrainDriveScripts) - Build/dev scripts

## Development Patterns

### File Organization (Frontend)
```
src/
├── components/
│   └── Feature/
│       ├── FeatureContainer.tsx  # State management
│       ├── FeatureView.tsx       # Presentation
│       └── index.ts              # Exports
├── services/
│   └── featureService.ts         # API calls
├── hooks/
│   └── useFeature.ts             # Custom hooks
└── types/
    └── feature.ts                # TypeScript types
```

### API Endpoint Pattern (Backend)
```
backend/app/api/v1/endpoints/
├── feature.py                    # One file per resource
```

### Naming Conventions
- Plugin names: `kebab-case` (e.g., `my-plugin`)
- Component IDs: `PascalCase` (e.g., `MyComponent`)
- **Critical:** Plugin name ≠ module name (use different names)

### Plugin 1-Minute Build Cycle
Configure webpack to output directly to BrainDrive's plugin folder:
1. Edit code
2. Build compiles to plugin folder
3. Hard refresh browser (disable cache)
4. See changes - no reinstall needed

## API Overview

### Authentication
- JWT tokens (access + refresh)
- HTTP-only cookies for browser
- Bearer token for API clients

### Base URL
```
http://localhost:8005/api/v1/
```

### Key Endpoints
```
POST /auth/login
POST /auth/register
GET  /conversations
POST /conversations/{id}/messages
GET  /plugins
POST /plugins/install
GET  /settings
POST /settings
```

### Response Format
```json
{
  "data": {},
  "status": "success" | "error",
  "message": "..."
}
```

## Common Gotchas

### Plugin Development
1. Plugin name and module name MUST be different
2. Always use Service Bridges, never import from core directly
3. Disable browser cache during development
4. Check `lifecycle_manager.py` for plugin configuration

### Backend
1. Use SQLModel for database models (combines SQLAlchemy + Pydantic)
2. Always create Alembic migrations for schema changes
3. Use dependency injection for database sessions

### Frontend
1. Use MUI components for consistency
2. Support both light and dark themes (Theme Bridge)
3. React class components are the established pattern in plugins

## Style Guide Summary

### Documentation Tone
- Direct and empowering
- Technical but accessible
- Active voice, present tense, second person ("you")
- Avoid: "simply", "just", "obviously", "please"

### Code Comments
- Only where logic isn't self-evident
- Explain "why" not "what"
- Keep them current with code changes

## Links for Deep Dives

When you need more detail, reference these files in BrainDrive-Docs-Site:

| Topic | File |
|-------|------|
| Vision & Mission | `docs-context/vision.md` |
| Target Personas | `docs-context/personas/adam-carter.md` |
| Tech Stack Details | `docs-context/project-overviews/BrainDrive-System.md` |
| API Reference | `docs-core/reference/API.md` |
| Service Bridges | `docs-core/reference/service-bridges-api.md` |
| Plugin Concepts | `docs-core/concepts/plugins.md` |
| Style Guide | `docs-context/technical-docs-style-guide.md` |
| Source Hierarchy | `docs-context/sources.md` |

---

*This context file is part of the [braindrive-claude-workflow](https://github.com/davewaring/braindrive-claude-workflow) system.*
