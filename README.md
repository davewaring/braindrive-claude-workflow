# BrainDrive Claude Code Workflow

A systematic approach to developing BrainDrive features using Claude Code, designed to maximize Claude's autonomous capability while maintaining quality and alignment with user intent.

## Vision

Claude Code should be able to build features start-to-finish with well-defined plans and success criteria, with humans handling only what Claude cannot yet handle.

## The System: 5 Phases Before Code

### Phase 1: Feature Definition (Interview Process)
Use the `/interview` skill to surface hidden assumptions and fully define what you're building through 20-40+ in-depth questions.

**Output:** `feature-spec.md`

### Phase 2: MVP & Scope Definition
Define what's in v1 vs. future versions. Identify the absolute minimum needed to validate the concept.

**Output:** Scoped requirements with clear MVP boundaries

### Phase 3: Technical Design
Define how you're building it - tech stack, architecture, database schema, API design.

**Output:** `technical-design.md`

### Phase 4: Milestones & Success Criteria
Break work into testable chunks with AI-verifiable success definitions.

**Output:** `milestones.md`

### Phase 5: Build
Execute the plan with autonomous verification using the verification loop.

## Quick Start

1. **Install the skills** - Copy the `skills/` folder to your project's `.claude/` directory
2. **Load the context** - Reference the BrainDrive context bundle in your CLAUDE.md
3. **Run `/interview`** - Start the feature definition process
4. **Follow the phases** - Work through each phase using the templates

## Repository Structure

```
braindrive-claude-workflow/
├── README.md                    # This file
├── skills/                      # Claude Code skills
│   ├── interview.md             # Deep interview using AskUserQuestion
│   ├── feature-spec.md          # Generate spec from interview
│   ├── milestone-check.md       # Run success criteria verification
│   └── retro.md                 # Post-feature retrospective
├── templates/                   # Document templates
│   ├── feature-spec-template.md
│   ├── technical-design-template.md
│   └── milestones-template.md
├── setup/                       # Standard Claude Code setup
│   ├── CLAUDE.md.template       # Template for BrainDrive projects
│   ├── mcp-config.json          # Recommended MCP servers
│   └── permissions.md           # Recommended permission settings
├── context/                     # BrainDrive context bundle
│   └── braindrive-context.md    # Key context for Claude
└── docs/                        # Process documentation
    ├── phase-1-feature-definition.md
    ├── phase-2-mvp-scoping.md
    ├── phase-3-technical-design.md
    ├── phase-4-milestones.md
    └── phase-5-build.md
```

## Skills

| Skill | Purpose |
|-------|---------|
| `/interview` | Triggers deep interview (20-40+ questions) to surface requirements |
| `/feature-spec` | Generates feature spec from interview output |
| `/milestone-check` | Runs success criteria verification |
| `/retro` | Post-feature retrospective that improves the system |

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

## License

MIT
