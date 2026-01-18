# BrainDrive AI Development Workflow

A systematic framework for AI-native software development that creates a flywheel of continuous improvement. This repo focuses on **development automation** - executing builds and capturing learnings.

## Vision

Claude Code should be able to build features start-to-finish with well-defined plans and success criteria, with humans handling only what Claude cannot yet handle. Every feature built improves the system for the next one.

## The Six-Phase Framework

```
Context → Plan → Setup → Build → Test → Learn
                                          ↓
                              (feeds back into Context)
```

| Phase | Purpose | Key Output |
|-------|---------|------------|
| **1. Context** | Establish foundation knowledge | Planning + Building context loaded |
| **2. Plan** | Define what/how we're building | `spec.md` + `build-plan.md` |
| **3. Setup** | Prepare execution environment | Permissions, tools, checkpoints defined |
| **4. Build** | Execute with verification | Working code, phases completed |
| **5. Test** | Verify requirements met | All criteria pass |
| **6. Learn** | Capture and integrate learnings | System improves for next feature |

See [docs/framework.md](docs/framework.md) for the complete framework documentation.

## Repository Structure

```
braindrive-claude-workflow/
├── README.md                          # This file
├── docs/
│   ├── framework.md                   # Complete framework documentation
│   └── phases/                        # Phase-specific guidance
│       ├── 1-context.md
│       ├── 2-plan.md
│       ├── 3-setup.md
│       ├── 4-build.md
│       ├── 5-test.md
│       └── 6-learn.md
├── skills/                            # Development automation skills
│   ├── milestone-check.md             # Phase 4-5: Verify phase success
│   └── retro.md                       # Phase 6: Capture learnings
├── templates/
│   └── archived/                      # Archived templates (active ones in Library)
├── setup/
│   ├── configure/                     # One-time setup
│   │   ├── permissions.md             # Permission configuration
│   │   ├── mcp-config.json            # MCP server configuration
│   │   └── CLAUDE.md.template         # Project CLAUDE.md template
│   └── prepare/                       # Per-feature setup
│       └── checkpoints.md             # Checkpoint guidance
└── context/                           # Reference context (real context lives in Library)
    └── braindrive-context.md          # BrainDrive-specific patterns
```

## Ecosystem

This workflow is part of a **two-repo system**:

| Repository | Role |
|------------|------|
| **BrainDrive-Library** | Knowledge + Tools - specs, plans, decisions, transcripts, templates, skills, and the Librarian CLI |
| **braindrive-claude-workflow** | Process - development automation skills, phase guidance (this repo) |

**Content flow:**
```
Transcripts → Librarian (tools/librarian/) → Library (context)
                                                  ↓
                                        AI agents read context
                                                  ↓
                                        Plan using Library skills
                                                  ↓
                                        Build using workflow skills
                                                  ↓
                                        Learnings → back to Library
```

## Quick Start

### First-Time Setup

1. **Configure permissions** - Copy config from `setup/configure/permissions.md` to `~/.claude/settings.local.json`
2. **Install skills** - Copy skills from Library (`system/skills/`) and this repo (`skills/`) to your project's `.claude/` directory
3. **Set up CLAUDE.md** - Use `setup/configure/CLAUDE.md.template` as a starting point

### Per-Feature Workflow

1. **Context** - Read `AGENT.md` from BrainDrive-Library to load planning context
2. **Plan** (skills in Library)
   - Run `/interview` - Deep requirement discovery (20-40+ questions)
   - Run `/feature-spec` - Generate spec from interview
   - Run `/plan` - Generate build plan from spec
3. **Setup** - Review checkpoints, ensure environment ready
4. **Build** - Execute phases, use `/milestone-check` after each
5. **Test** - Verify all success criteria pass
6. **Learn** - Run `/retro` to capture and integrate learnings

## Skills

### This Repo (Development Automation)

| Skill | Phase | Purpose |
|-------|-------|---------|
| `/milestone-check` | Build/Test | Verify phase success criteria |
| `/retro` | Learn | Capture learnings and improve the system |

### BrainDrive-Library (Planning)

| Skill | Phase | Purpose |
|-------|-------|---------|
| `/interview` | Plan | Deep interview (20-40+ questions) to surface requirements |
| `/feature-spec` | Plan | Generate feature spec from interview output |
| `/plan` | Plan | Generate build plan with phases and success criteria |
| `/capture` | Learn | Capture session to Library |
| `/librarian` | Context | Manage Library content |

## Key Documents

Planning outputs live in BrainDrive-Library:

| Document | Location | Purpose |
|----------|----------|---------|
| `AGENT.md` | Library root | Boot file for AI agents |
| `spec.md` | Library/projects/active/[project]/ | What we're building and why |
| `build-plan.md` | Library/projects/active/[project]/ | How we're building it |
| `decisions.md` | Library/projects/active/[project]/ | Key decisions and rationale |

## Design Principles

1. **Context-First** - Never plan without understanding. Never build without a plan.
2. **Autonomous with Checkpoints** - Maximize agent autonomy within phases. Humans review at boundaries.
3. **Verifiable Success** - Every phase has executable commands and expected results.
4. **User-Facing First** - Get human eyes on user-facing work early.
5. **Continuous Learning** - Every feature makes the next one easier.
6. **Single Source of Truth** - Specs and plans live in the Library.

## BrainDrive Defaults

Pre-configured for BrainDrive development:

**Tech Stack:**
- Frontend: React 18 + TypeScript + Material-UI + Vite
- Backend: FastAPI + SQLModel + SQLite
- Plugins: Webpack Module Federation + Service Bridges

**Resources:**
- [Plugin Template](https://github.com/BrainDriveAI/BrainDrive-PluginTemplate)
- [Plugin Dev Quickstart](https://docs.braindrive.ai/core/plugin-development/quickstart)

## Changelog

### January 2025 (v3)
- Consolidated to two-repo architecture (Library + Workflow)
- Moved planning skills (interview, feature-spec, plan, capture) to BrainDrive-Library
- Moved Librarian CLI to BrainDrive-Library/tools/librarian/
- This repo now focuses on development automation (milestone-check, retro)

### January 2025 (v2)
- Expanded from 3 phases to 6 phases (Context, Plan, Setup, Build, Test, Learn)
- Added framework.md as comprehensive system documentation
- Clarified repository responsibilities (Workflow vs Library vs Librarian)
- Split Context into Planning Context and Building Context
- Split Setup into Configure (one-time) and Prepare (per-feature)
- Added checkpoint guidance for human review timing
- Moved planning outputs to BrainDrive-Library

### January 2025 (v1)
- Consolidated from 5 phases to 3 phases
- Reduced templates from 3 to 2 (feature-spec + plan)
- Added `/plan` skill
- Streamlined permissions configuration

## License

MIT
