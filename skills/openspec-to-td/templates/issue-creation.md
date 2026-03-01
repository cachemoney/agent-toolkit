# Issue Creation Templates

## Basic Issue Creation

## Basic Issue Creation

```bash
td create "[<change>] <category>: <task-description>" \
  --priority <smart-priority> \
  --type <smart-type> \
  --labels "spec:<change>,category:<category-slug>,complexity:<low|medium|high>" \
```

## Epic Issue Creation

```bash
td create "🎯 [EPIC] <change-name>" \
  --type epic \
  --priority 0 \
  --labels "spec:<change>,epic,openspec" \
```

## Discovery Issue Creation

```bash
td create "[<change>] DISCOVERED: <gap-description>" \
  --type task \
  --priority 1 \
  --labels "spec:<change>,discovered,proactive" \
```

## Dependency Creation

### Sequential dependencies within category
```bash
# Task 1.2 ALWAYS blocks on 1.1 by convention
td dep add <bd-1.2> <bd-1.1>
```

### Cross-category dependencies
```bash
# API endpoints block on database setup
td dep add <api-task-id> <db-task-id>

# Tests related to features (NOT blocking)
td dep add <test-task-id> <feature-task-id>
```
