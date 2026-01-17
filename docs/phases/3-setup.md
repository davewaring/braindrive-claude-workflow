# Phase 3: Setup

## Purpose

Prepare the execution environment before building begins. Setup ensures Claude has the right tools, permissions, and guardrails to execute autonomously while maintaining quality.

## Two Types of Setup

### 3.1 Configure (One-Time / Project-Level)

Environment and tooling that persists across features. Set up once, use for every feature.

| Category | Description | Where Defined |
|----------|-------------|---------------|
| **Execution Environment** | Dev server, database, test fixtures | Project setup scripts |
| **Tool Definitions** | MCP servers (Playwright, SQLite, GitHub) | `mcp-config.json` |
| **Permissions** | What Claude can do autonomously vs needs approval | `settings.json` |
| **Sub-Agents** | Specialized agents for specific tasks | CLAUDE.md |

**Configuration Files:**
- `~/.claude/settings.json` - User-level (global)
- `.claude/settings.json` - Project-level (shared with team)
- `.claude/settings.local.json` - Local overrides (personal)

### 3.2 Prepare (Per-Feature)

Feature-specific setup before each build begins.

| Category | Description | Where Defined |
|----------|-------------|---------------|
| **Success Criteria** | Verifiable commands from build plan | `build-plan.md` |
| **Test Definitions** | What tests will be written/run | `build-plan.md` |
| **Boundaries** | When to stop and ask vs continue autonomously | `build-plan.md` |
| **Checkpoints** | Which phases need human review | `build-plan.md` |

## Permission Configuration

### Recommended Permissions

```json
{
  "permissions": {
    "allow": [
      "Read(**)", "Edit(**)", "Write(**)",
      "Glob", "Grep", "Task(*)",
      "Bash(ls:*)", "Bash(git add:*)", "Bash(git status:*)",
      "Bash(git diff:*)", "Bash(git log:*)",
      "Bash(npm install:*)", "Bash(npm run dev:*)",
      "Bash(npm run build:*)", "Bash(npm test:*)"
    ],
    "ask": [
      "Bash(git commit:*)",
      "Bash(git push:*)"
    ],
    "deny": [
      "Bash(git push --force:*)",
      "Bash(git reset --hard:*)",
      "Bash(rm -rf:*)"
    ]
  }
}
```

### Permission Philosophy

| Category | Examples | Permission |
|----------|----------|------------|
| **Safe Operations** | File read/write, build, test | Allow |
| **Review Points** | Git commits, pushes | Ask |
| **Dangerous** | Force push, hard reset, rm -rf | Deny |

## MCP Servers

Recommended Model Context Protocol servers for BrainDrive development:

```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["@anthropic-ai/mcp-server-playwright"]
    },
    "sqlite": {
      "command": "npx",
      "args": ["@anthropic-ai/mcp-server-sqlite", "--db-path", "./data/app.db"]
    },
    "github": {
      "command": "npx",
      "args": ["@anthropic-ai/mcp-server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

## Checkpoint Configuration

Define when Claude should stop for human review:

### By Output Type

| Output Type | Checkpoint Timing |
|-------------|-------------------|
| User-facing UI/UX | Review after each phase |
| API contracts | Review when defined |
| Internal/infrastructure | Review after phase completion |
| Background processes | Review at major milestones |

### By Risk Level

| Risk Level | Examples | Checkpoint |
|------------|----------|------------|
| **High** | Auth changes, data migrations, external API integration | Review before and after |
| **Medium** | New features, significant refactors | Review after phase |
| **Low** | Bug fixes, minor UI tweaks | Review at PR |

### In Build Plan

Document checkpoints explicitly:

```markdown
## Human Checkpoints

### After Phase 2
- [ ] Review: Does the UX feel right?
- [ ] Review: Is the design consistent with BrainDrive?

### After Phase 3
- [ ] Final review before merge
- [ ] Test with real data
```

## Environment Setup Checklist

### One-Time Setup

- [ ] Install Claude Code CLI
- [ ] Configure permissions (`~/.claude/settings.local.json`)
- [ ] Install MCP servers
- [ ] Set up project CLAUDE.md
- [ ] Copy skills to `.claude/` directory

### Per-Feature Setup

- [ ] Verify build plan has success criteria for each phase
- [ ] Confirm checkpoint requirements
- [ ] Ensure development environment is running
- [ ] Verify database is in expected state
- [ ] Run existing tests to establish baseline

## Boundary Definition

Define when Claude should stop vs continue:

### Stop and Ask When

- Unclear requirements encountered
- Multiple valid approaches exist
- User-facing decisions needed
- External dependencies blocked
- 3+ failed attempts at same task

### Continue Autonomously When

- Success criteria are clear
- Tests are passing
- Within defined phase scope
- Following established patterns

## Best Practices

### Test the Setup

Before starting build:
1. Run `npm run build` - verify clean build
2. Run `npm test` - verify tests pass
3. Start dev server - verify it runs
4. Check database connectivity

### Document Environment Requirements

In CLAUDE.md or build plan:
```markdown
## Prerequisites
- Node.js 18+
- Python 3.11+
- SQLite installed
- Dev server running on :3000
- Backend running on :8000
```

### Pre-provision Infrastructure

Don't leave this for build phase:
- Create database tables
- Set up API keys
- Configure environment variables
- Initialize test data

## Checklist

Before proceeding to Build phase:

- [ ] Permissions configured appropriately
- [ ] MCP servers installed and working
- [ ] Development environment running
- [ ] Tests passing (baseline established)
- [ ] Checkpoints documented in build plan
- [ ] Success criteria are executable commands

## Next Phase

Once setup is complete, proceed to [Phase 4: Build](./4-build.md) to execute the plan.
