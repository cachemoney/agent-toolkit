# Issue Creation Templates (td CLI)

## Basic Issue Creation

```bash
td create "<change>: <category> - <task-description>" \
  --type <task|feature|chore> \
  --priority <P0|P1|P2>
```

> Title format: `[<change>] <Category>: <specific action>`
> Example: `[add-auth] Setup: Create PostgreSQL users table`

## Epic Issue Creation

Create an epic issue as a container for all spec tasks:

```bash
td create "🎯 [EPIC] <change-name>" \
  --type feature \
  --priority P0
```

After creating individual tasks, group them in a work session instead of manual linking:

```bash
td ws start "<change-name>"
td ws tag <epic-id> <task-id1> <task-id2> ...
```

## Discovery Issue Creation

For proactively-detected gaps (missing tests, rate limiting, rollbacks, etc.):

```bash
td create "[<change>] DISCOVERED: <gap-description>" \
  --type task \
  --priority P1
```

## Priority Logic

| Priority | When to use |
|----------|-------------|
| **P0** | Infrastructure, migrations, environment setup — blocks everything else |
| **P1** | Core implementation, tests, documentation — the main work |
| **P2** | UI polish, nice-to-haves, optional enhancements |

**Keyword signals:**
- P0: "migration", "schema", "config", "setup", "init"
- P1: "implement", "add", "write tests", "document"
- P2: "improve", "polish", "optional", "enhancement"

**Bump priority up if:** task mentions "urgent", "critical", "blocking", "security"
**Bump priority down if:** task mentions "nice-to-have", "future", "optional"

## Issue Type Detection

| Type | Signals |
|------|---------|
| `feature` | "implement", "add", "create" — new functionality |
| `task` | "setup", "configure", "refactor", "improve", "test", "validate" |
| `chore` | "document", "cleanup", "remove deprecated", "maintenance" |
| `bug` | "bug", "issue", "error", "fix", "broken" |
| `epic` | "epic", "large-scale", "multi-phase" |

## Complexity Labels (optional)

Add complexity context in the task description or notes:
- `low`: "setup", "config", clear steps, well-defined
- `medium`: "implement", "integrate", requires design decisions
- `high`: "refactor", "migrate", "redesign", cross-cutting changes

## Full Example

```bash
# 1. Create the epic
td create "🎯 [EPIC] add-auth" --type feature --priority P0
# → td-001

# 2. Create infrastructure tasks (P0)
td create "[add-auth] Setup: Create PostgreSQL users table" --type task --priority P0
# → td-002
td create "[add-auth] Setup: Configure JWT secret in environment" --type task --priority P0
# → td-003

# 3. Create implementation tasks (P1)
td create "[add-auth] Implement: JWT generation and validation" --type feature --priority P1
# → td-004
td create "[add-auth] Implement: User registration endpoint" --type feature --priority P1
# → td-005

# 4. Create proactive discoveries
td create "[add-auth] DISCOVERED: Add refresh token rotation" --type task --priority P1
# → td-006

# 5. Group in a work session
td ws start "add-auth implementation"
td ws tag td-001 td-002 td-003 td-004 td-005 td-006
```
