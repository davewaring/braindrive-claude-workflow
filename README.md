# BrainDrive Claude Code Workflow

A systematic approach to developing BrainDrive features using Claude Code, designed to maximize Claude's autonomous capability while maintaining quality and alignment with user intent.

## Vision

Claude Code should be able to build features start-to-finish with well-defined plans and success criteria, with humans handling only what Claude cannot yet handle.

## The System: 2 Documents, 3 Phases

### Documents

| Document | Purpose | Audience |
|----------|---------|----------|
| `feature-spec.md` | What we're building and why | Stakeholders, new collaborators |
| `plan.md` | How we're building it (architecture + roadmap + milestones) | Engineering |

This consolidated approach (refined January 2025) reduces document drift and provides a single source of truth for execution.

### Phase 1: Feature Specification
Use the `/interview` skill to surface hidden assumptions and fully define what you're building through 20-40+ in-depth questions. Define MVP scope.

**Output:** `feature-spec.md`

### Phase 2: Planning
Design the architecture, make key technical decisions, and break work into testable phases with success criteria.

**Output:** `plan.md`

### Phase 3: Build
Execute the plan with autonomous verification using the verification loop.

**Output:** Working feature

## Quick Start

1. **Install the skills** - Copy the `skills/` folder to your project's `.claude/` directory
2. **Load the context** - Reference the BrainDrive context bundle in your CLAUDE.md
3. **Run `/interview`** - Start the feature definition process
4. **Run `/feature-spec`** - Generate the feature specification
5. **Run `/plan`** - Generate the execution plan
6. **Build** - Work through phases, using `/milestone-check` to verify each one

## Repository Structure

```
braindrive-claude-workflow/
├── README.md                    # This file
├── skills/                      # Claude Code skills
│   ├── interview.md             # Deep interview using AskUserQuestion
│   ├── feature-spec.md          # Generate spec from interview
│   ├── plan.md                  # Generate plan from spec
│   ├── milestone-check.md       # Verify phase success criteria
│   └── retro.md                 # Post-feature retrospective
├── templates/                   # Document templates
│   ├── feature-spec-template.md # What/why template
│   ├── plan-template.md         # How template (architecture + milestones)
│   └── archived/                # Historical reference templates
│       ├── technical-design-template.md
│       └── milestones-template.md
├── setup/                       # Standard Claude Code setup
│   ├── CLAUDE.md.template       # Template for BrainDrive projects
│   ├── mcp-config.json          # Recommended MCP servers
│   └── permissions.md           # Permission configuration guide
├── context/                     # BrainDrive context bundle
│   └── braindrive-context.md    # Key context for Claude
└── docs/                        # Process documentation
    ├── phase-1-feature-spec.md  # Interview + MVP scoping
    ├── phase-2-planning.md      # Architecture + milestones
    ├── phase-3-build.md         # Execution with verification
    └── archived/                # Historical 5-phase docs
```

## Skills

| Skill | Purpose |
|-------|---------|
| `/interview` | Triggers deep interview (20-40+ questions) to surface requirements |
| `/feature-spec` | Generates feature spec from interview output |
| `/plan` | Generates execution plan from feature spec |
| `/milestone-check` | Runs success criteria verification for a phase |
| `/retro` | Post-feature retrospective that improves the system |

## Why 2 Documents?

Previous workflows used 3-5 separate documents (feature spec, technical design, milestones, build plan, etc.). Experience showed:

- **Multiple docs drift out of sync** - Architecture changes but milestones don't get updated
- **Hard to find current truth** - Which doc has the latest status?
- **Maintenance overhead** - More docs to keep aligned

The 2-document approach provides:
- **Clear separation** - `feature-spec.md` = what/why (for stakeholders), `plan.md` = how (for engineering)
- **Single source of truth** - One place to check status and next steps
- **Less drift** - Fewer documents to keep synchronized

See the AI Installer project (January 2025) for the rationale behind this consolidation.

## BrainDrive Defaults

This workflow is pre-configured for BrainDrive development:

**Tech Stack:**
- Frontend: React 18 + TypeScript + Material-UI + Vite
- Backend: FastAPI + SQLModel + SQLite
- Plugins: Webpack Module Federation + Service Bridges

**Key Resources:**
- [Plugin Template](https://github.com/BrainDriveAI/BrainDrive-PluginTemplate)
- [Plugin Dev Quickstart](https://docs.braindrive.ai/core/plugin-development/quickstart)
- [Service Bridge Examples](https://github.com/BrainDriveAI?q=service-bridge)

## Contributing

This workflow system is designed to improve over time through the `/retro` skill. After completing a feature, run `/retro` to capture learnings and suggest improvements to the system.

## Changelog

### January 2025
- Consolidated from 5 phases to 3 phases
- Reduced from 3 templates to 2 templates (feature-spec + plan)
- Added `/plan` skill for generating consolidated execution plans
- Updated `/milestone-check` to work with plan.md format
- Archived historical templates and phase docs for reference

## License

MIT
