# BrainDrive AI Development Framework

> A systematic approach to AI-native software development that creates a flywheel of continuous improvement.

## Overview

This framework defines how we work with AI coding agents (Claude Code, Codex, etc.) to build BrainDrive features. It's designed to maximize autonomous execution while maintaining quality, alignment, and continuous learning.

**Core Principle:** The system improves itself. Every feature built feeds learnings back into context, making the next feature easier to build.

---

## The Six Phases

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐             │
│   │ CONTEXT  │───▶│   PLAN   │───▶│  SETUP   │───▶│  BUILD   │──┐          │
│   └──────────┘    └──────────┘    └──────────┘    └──────────┘  │          │
│        ▲                                               │        │          │
│        │                                               ▼        │          │
│        │          ┌──────────┐    ┌──────────┐    ┌──────────┐  │          │
│        └──────────│  LEARN   │◀───│   TEST   │◀───│  (loop)  │◀─┘          │
│                   └──────────┘    └──────────┘    └──────────┘             │
│                        │                                                    │
│                        └─────────▶ Feeds back into Context (flywheel)      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Phase 1: Context

**Purpose:** Establish the foundation of knowledge that informs all subsequent work.

Context splits into two distinct types:

### 1.1 Planning Context (Pre-Plan)

What the agent needs to understand *before* designing a solution.

| Category | Description | Source |
|----------|-------------|--------|
| **Business Context** | What BrainDrive is, vision, mission, target users | `braindrive/overview.md`, `vision.md`, `mission.md` |
| **Technical Context** | Tech stack, conventions, architecture patterns | `braindrive/conventions.md`, `system-architecture.md` |
| **Project Landscape** | Active projects, their status, how they relate | `AGENT.md`, `projects/active/*/spec.md` |
| **Related Work** | Similar features built before, patterns to reuse | Previous project specs, decisions.md files |
| **Historical Decisions** | Why things are the way they are | `*/decisions.md`, transcripts |

**Where it lives:** BrainDrive-Library (`braindrive/` and `projects/` directories)

**How agents access it:** Read `AGENT.md` as boot file, then drill into relevant project folders.

### 1.2 Building Context (Per-Session)

What the agent needs to pick up work in progress with a fresh context window.

| Category | Description | Source |
|----------|-------------|--------|
| **Feature Spec** | What we're building and why | `projects/active/[project]/spec.md` |
| **Build Plan** | How we're building it, current phase, what's done | `projects/active/[project]/build-plan.md` |
| **Current State** | Where we left off, blockers, recent changes | Build plan status, git log, test results |
| **Session History** | Previous session transcripts for this feature | Transcript files, session exports |

**Where it lives:** BrainDrive-Library (`projects/active/[project-name]/`)

**How agents access it:** Librarian materializes to `.ai-context/` in working repos, or agent reads directly from Library.

---

## Phase 2: Plan

**Purpose:** Define *what* we're building (spec) and *how* we're building it (build plan).

### 2.1 Interview (Requirement Discovery)

Deep questioning to surface hidden requirements before any design work.

- 20-40+ questions across multiple rounds
- Covers: core understanding, scope, UX, technical integration, edge cases
- Surfaces assumptions and resolves ambiguity early
- **Output:** Interview transcript/notes

**Skill:** `/interview`

### 2.2 Feature Specification

Translate interview insights into a clear, stakeholder-readable document.

- What problem we're solving and for whom
- User stories and acceptance criteria
- MVP scope vs future versions
- Integration points with existing systems
- Success definition

**Output:** `spec.md` in `projects/active/[project-name]/`

**Skill:** `/feature-spec`

### 2.3 Build Plan

Design the technical approach and break into verifiable phases.

- Key technical decisions with rationale
- Architecture and component design
- 3-5 implementation phases
- Success criteria for each phase (executable commands + expected results)
- Risks and mitigations

**Output:** `build-plan.md` in `projects/active/[project-name]/`

**Skill:** `/plan`

### Human Checkpoint

User reviews and approves spec + build plan before proceeding to Setup.

---

## Phase 3: Setup

**Purpose:** Prepare the execution environment before building begins.

Setup splits into two concerns:

### 3.1 Configure (One-Time / Project-Level)

Environment and tooling that persists across features.

| Category | Examples |
|----------|----------|
| **Execution Environment** | Dev server, database, test fixtures |
| **Tool Definitions** | MCP servers (Playwright, SQLite, GitHub) |
| **Permissions** | What Claude can do autonomously vs needs approval |
| **Sub-Agents** | Specialized agents for specific tasks |

**Where defined:**
- `setup/permissions.md` - Permission patterns
- `setup/mcp-config.json` - MCP server configuration
- Project-level `CLAUDE.md` - Project-specific settings

### 3.2 Prepare (Per-Feature)

Feature-specific setup before building begins.

| Category | Examples |
|----------|----------|
| **Success Criteria** | Verifiable commands from build plan |
| **Test Definitions** | What tests will be written/run |
| **Boundaries** | When to stop and ask vs continue autonomously |
| **Checkpoints** | Which phases need human review |

**Where defined:** `build-plan.md` (success criteria per phase)

### Checkpoint Guidance

| Output Type | Checkpoint Timing |
|-------------|-------------------|
| User-facing UI/UX | Review after each phase |
| API contracts | Review when defined |
| Internal/infrastructure | Review after phase completion |
| Background processes | Review at major milestones |

**Principle:** Get human eyes on user-facing work earlier. Background work can batch reviews.

---

## Phase 4: Build

**Purpose:** Execute the plan with autonomous verification.

### Execution Model

```
For each phase in build-plan:
    1. Mark phase as "in progress"
    2. Execute implementation tasks
    3. Run phase success criteria (self-verify)
    4. If all pass → mark complete, proceed
    5. If fail → fix and re-verify
    6. At phase end → human checkpoint (if required)
```

### Agent Autonomy

Within a phase, the agent operates autonomously:
- Reads relevant code and context
- Implements changes
- Runs verification commands
- Fixes issues discovered during verification
- Only stops at defined checkpoints or when blocked

### When to Stop

| Situation | Action |
|-----------|--------|
| Phase complete, all criteria pass | Human checkpoint, then next phase |
| Blocked by unclear requirement | Stop, ask for clarification |
| Blocked by external dependency | Stop, report blocker |
| Unexpected architectural decision needed | Stop, present options |
| User-facing output ready for review | Stop, get feedback |

**Skill:** `/milestone-check [phase]` - Verify phase success criteria

---

## Phase 5: Test

**Purpose:** Verify the build meets requirements through continuous and final testing.

### 5.1 Continuous Verification (During Build)

Integrated into the build loop via `/milestone-check`.

- Run after each phase
- Execute success criteria commands
- Compare actual vs expected results
- Loop back to fix failures before proceeding

### 5.2 Final Acceptance (After Build)

Comprehensive validation after all phases complete.

| Test Type | Description |
|-----------|-------------|
| **Integration Tests** | Components work together |
| **User Acceptance** | Meets user stories from spec |
| **Regression** | Existing functionality still works |
| **Edge Cases** | Handles boundary conditions |

### Test Loop

```
Run tests →
    All pass? → Proceed to Learn
    Failures? → Diagnose → Fix → Re-test
```

---

## Phase 6: Learn

**Purpose:** Capture learnings and feed them back into the system.

This is the flywheel mechanism that makes the system compound in value.

### 6.1 Capture

After feature completion, run retrospective:

- What went well?
- What was harder than expected?
- What patterns emerged?
- What would we do differently?
- What context was missing?

**Skill:** `/retro`

### 6.2 Integrate

Feed learnings back into:

| Target | What Gets Updated |
|--------|-------------------|
| **Planning Context** | New patterns, conventions, architectural decisions |
| **Building Context** | Project-specific learnings in decisions.md |
| **Templates** | Improved spec/plan templates based on gaps found |
| **Skills** | Enhanced prompts based on what worked |
| **CLAUDE.md** | New constraints, patterns, or warnings |

### 6.3 Propagate

Ensure learnings are available for future work:

- Commit updates to BrainDrive-Library
- Update relevant project decisions.md
- Add to conventions.md if broadly applicable
- Update workflow templates if process-related

**Result:** Next feature starts with better context than this one did.

---

## Repository Responsibilities

| Repository | Responsibility |
|------------|----------------|
| **BrainDrive-Library** | Knowledge + Tools - specs, plans, decisions, context, transcripts, Librarian CLI, planning skills |
| **braindrive-claude-workflow** | Process - development automation skills (milestone-check, retro), phase guidance, this framework |

### Content Flow

```
Transcripts/Sessions → Librarian (Library/tools/) → Library (specs, plans, decisions)
                                                          ↓
                                                AI agents read context
                                                          ↓
                                                Plan using Library skills
                                                          ↓
                                                Build using workflow skills
                                                          ↓
                                                Learnings → back to Library
```

---

## Quick Reference

### Phase Checklist

- [ ] **Context** - Agent has planning context (business, tech, related work)
- [ ] **Plan** - Interview complete, spec written, build plan approved
- [ ] **Setup** - Environment ready, permissions set, checkpoints defined
- [ ] **Build** - All phases executed, success criteria verified
- [ ] **Test** - Continuous checks passed, final acceptance complete
- [ ] **Learn** - Retro done, learnings integrated back

### Skills

| Skill | Phase | Purpose | Source |
|-------|-------|---------|--------|
| `/interview` | Plan | Deep requirement discovery | Library |
| `/feature-spec` | Plan | Generate spec from interview | Library |
| `/plan` | Plan | Generate build plan from spec | Library |
| `/capture` | Learn | Capture session to Library | Library |
| `/milestone-check` | Build/Test | Verify phase success criteria | Workflow |
| `/retro` | Learn | Capture and integrate learnings | Workflow |

### Key Documents

| Document | Location | Purpose |
|----------|----------|---------|
| `AGENT.md` | Library root | Boot file for AI agents |
| `spec.md` | Library/projects/active/[project]/ | What we're building |
| `build-plan.md` | Library/projects/active/[project]/ | How we're building it |
| `decisions.md` | Library/projects/active/[project]/ | Why we made key choices |
| `CLAUDE.md` | Project root | Project-specific agent config |

---

## Design Principles

1. **Context-First** - Never plan without understanding. Never build without a plan.

2. **Autonomous with Checkpoints** - Maximize agent autonomy within phases. Humans review at phase boundaries.

3. **Verifiable Success** - Every phase has executable commands and expected results. No ambiguous "it works."

4. **User-Facing First** - Get human eyes on user-facing work early. Batch reviews for background work.

5. **Continuous Learning** - Every feature makes the next one easier. The system improves itself.

6. **Single Source of Truth** - Specs and plans live in the Library. No drift between documents.

7. **Human Intent, AI Execution** - Humans define what and why. AI handles how and does.
