# Phase 1: Context

## Purpose

Establish the foundation of knowledge that informs all subsequent work. Context ensures the AI agent understands the business, the project, and the current state before making any decisions.

## Two Types of Context

### 1.1 Planning Context (Pre-Plan)

What the agent needs before designing a solution. This context helps make good architectural decisions and ensures alignment with business goals.

| Category | Description | Source |
|----------|-------------|--------|
| **Business Context** | What BrainDrive is, vision, mission, target users | `braindrive/overview.md`, `vision.md`, `mission.md` |
| **Technical Context** | Tech stack, conventions, architecture patterns | `braindrive/conventions.md`, `system-architecture.md` |
| **Project Landscape** | Active projects, their status, how they relate | `AGENT.md`, `projects/active/*/spec.md` |
| **Related Work** | Similar features built before, patterns to reuse | Previous project specs, `decisions.md` files |
| **Historical Decisions** | Why things are the way they are | `*/decisions.md`, transcripts |

**Where it lives:** BrainDrive-Library (`braindrive/` and `projects/` directories)

### 1.2 Building Context (Per-Session)

What the agent needs to pick up work in progress with a fresh context window.

| Category | Description | Source |
|----------|-------------|--------|
| **Feature Spec** | What we're building and why | `projects/active/[project]/spec.md` |
| **Build Plan** | How we're building it, current phase, what's done | `projects/active/[project]/build-plan.md` |
| **Current State** | Where we left off, blockers, recent changes | Build plan status, git log, test results |
| **Session History** | Previous session transcripts for this feature | Transcript files, session exports |

**Where it lives:** BrainDrive-Library (`projects/active/[project-name]/`)

## How to Load Context

### For New Features (Planning Context)

1. **Read the boot file:**
   ```
   Read AGENT.md from BrainDrive-Library
   ```
   This provides a quick overview of all active projects and recent activity.

2. **Load business context:**
   ```
   Read braindrive/overview.md, vision.md, conventions.md
   ```

3. **Check related projects:**
   ```
   Review similar projects in projects/active/
   Look for patterns and decisions that apply
   ```

### For Resuming Work (Building Context)

1. **Read the project folder:**
   ```
   Read projects/active/[project-name]/spec.md
   Read projects/active/[project-name]/build-plan.md
   ```

2. **Check current state:**
   ```
   Review build-plan.md for current phase status
   Check git log for recent changes
   Review any failing tests
   ```

3. **Load session history (if available):**
   ```
   Read relevant transcripts or session exports
   ```

## Context Materialization

The Librarian tool can materialize context from the Library to project working directories:

```
BrainDrive-Library/
├── braindrive/         # Company context
└── projects/active/    # Project context
        ↓
    librarian refresh
        ↓
project-repo/.ai-context/
├── company.md          # Materialized company context
└── project.md          # Materialized project context
```

This allows agents to read context from the working repo without navigating to the Library.

## Best Practices

### Always Start with Context

Never jump straight to planning or building. Even for "simple" tasks, spend 30 seconds loading context. It prevents:
- Duplicating existing solutions
- Violating established patterns
- Making decisions that conflict with business goals

### Check for Related Decisions

Before making any architectural decision, check `decisions.md` files for related choices:
- Has this been decided before?
- What was the rationale?
- Should we follow the same pattern or deviate?

### Update Context as You Work

Context isn't read-only. As you build, update:
- `decisions.md` with new architectural choices
- `spec.md` if requirements clarify
- `build-plan.md` with status and learnings

## Checklist

Before proceeding to Plan phase:

- [ ] Read AGENT.md for project landscape
- [ ] Loaded relevant business context (vision, conventions)
- [ ] Checked for related projects and decisions
- [ ] Understand the tech stack and patterns
- [ ] Know where this feature fits in the system

## Next Phase

Once you have sufficient context, proceed to [Phase 2: Plan](./2-plan.md) to define what you're building and how.
