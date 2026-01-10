# Recommended Permissions for BrainDrive Development

Configure these permissions in Claude Code to reduce friction during development while maintaining safety.

## How to Configure

Permissions are set in `~/.claude/settings.json` or per-project in `.claude/settings.json`.

```json
{
  "permissions": {
    "allow": [...],
    "deny": [...]
  }
}
```

## Recommended Allow List

These commands are safe to auto-approve for BrainDrive development:

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run build)",
      "Bash(npm run dev)",
      "Bash(npm test*)",
      "Bash(npm run lint*)",
      "Bash(npx tsc*)",
      "Bash(npx playwright*)",
      "Bash(pytest*)",
      "Bash(uvicorn*)",
      "Bash(alembic*)",
      "Bash(git status*)",
      "Bash(git diff*)",
      "Bash(git log*)",
      "Bash(git branch*)",
      "Bash(git checkout*)",
      "Bash(git add*)",
      "Bash(git commit*)",
      "Bash(curl*localhost*)",
      "Bash(ls*)",
      "Bash(cat*)",
      "Bash(mkdir*)",
      "Bash(cp*)",
      "Bash(mv*)",
      "Read(*)",
      "Write(*.md)",
      "Write(*.ts)",
      "Write(*.tsx)",
      "Write(*.py)",
      "Write(*.json)",
      "Write(*.css)",
      "Edit(*)"
    ]
  }
}
```

## Recommended Deny List

Block these to prevent accidents:

```json
{
  "permissions": {
    "deny": [
      "Bash(git push*--force*)",
      "Bash(git reset*--hard*)",
      "Bash(rm -rf*)",
      "Bash(*DROP TABLE*)",
      "Bash(*DELETE FROM*)",
      "Bash(git push*origin main*)",
      "Write(*.env*)",
      "Write(*credentials*)",
      "Write(*secret*)"
    ]
  }
}
```

## Permission Categories

### Safe to Auto-Approve

**Build & Test Commands:**
- `npm run build` - Building the frontend
- `npm test` - Running tests
- `npm run lint` - Linting code
- `npx tsc` - TypeScript checking
- `pytest` - Python tests
- `npx playwright test` - E2E tests

**Git Read Operations:**
- `git status` - Check status
- `git diff` - View changes
- `git log` - View history
- `git branch` - List branches

**File Operations:**
- Reading any file
- Writing code files (`.ts`, `.tsx`, `.py`, etc.)
- Writing documentation (`.md`)

### Require Confirmation

**Git Write Operations:**
- `git commit` - Review the commit message
- `git push` - Confirm before pushing
- `git merge` - Review what's being merged

**Database Operations:**
- Any direct database modifications
- Migration runs (`alembic upgrade`)

**External API Calls:**
- Calls to non-localhost URLs

### Always Deny

**Destructive Operations:**
- `git push --force` - Can lose history
- `git reset --hard` - Can lose work
- `rm -rf` - Can delete important files
- Direct `DELETE` or `DROP` SQL

**Sensitive Files:**
- `.env` files (contain secrets)
- Credential files
- API key files

## Per-Project Overrides

For a specific project, create `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(alembic upgrade head)"
    ]
  }
}
```

This adds project-specific permissions without modifying global settings.

## Tips

### Avoid Permission Fatigue
- Pre-approve common safe operations
- Group related permissions together
- Use wildcards for variations (`npm test*` covers `npm test`, `npm test -- --coverage`)

### Stay Safe
- Never auto-approve commands that touch production
- Review commits before pushing
- Keep destructive commands on the deny list

### Check Your Settings
```bash
claude config list  # Show current settings
```

## Notification Hook

Instead of auto-approving everything, set up a notification hook:

```json
{
  "hooks": {
    "on_permission_request": {
      "command": "osascript -e 'display notification \"Claude needs permission\" with title \"Claude Code\"'"
    }
  }
}
```

This notifies you when Claude needs permission, so you don't have to watch the terminal constantly.
