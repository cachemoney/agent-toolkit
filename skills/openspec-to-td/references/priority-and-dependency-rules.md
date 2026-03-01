# Priority and Dependency Rules

## Dependency Patterns

### Pattern 1: Sequential within a Group
Tasks in the same numbered group depend on each other sequentially.

```
1.1 Setup DB schema
1.2 Create repository layer   ← requires 1.1
1.3 Add service layer         ← requires 1.2
```

### Pattern 2: Database → API
Any API endpoint or business logic that writes to / reads from a DB table
depends on the migration that creates it.

```
1.1 Create users table migration
2.1 Add user registration endpoint   ← requires 1.1
```

### Pattern 3: Config → Implementation
Setup and configuration must precede any code that relies on it.

```
1.1 Configure JWT secret in env
2.1 Implement JWT generation   ← requires 1.1
```

### Pattern 4: Implementation ← → Tests (Parallel, not blocking)
Tests are **related** to their feature but shouldn't block it.
Use a `related` relationship, not a hard dependency.

```
2.1 Implement user registration
3.1 Write registration tests   ← related-to 2.1, runs in parallel
```

### Pattern 5: Core → Polish
UI polish, metrics, alerts depend on core functionality existing first.

```
2.1 Basic transaction import
4.1 Add import progress indicator   ← requires 2.1
```

## Dependency-Type Semantics

| Type | Meaning |
|------|---------|
| Hard dependency | Task B cannot begin until Task A is complete |
| Related | Tasks share context but can proceed in parallel |

Use discretion — not every sequential task is a hard dependency. Ask: "Can this be
started in parallel?" If yes, it's related, not blocked.

## Proactive Gap Detection

When translating OpenSpec tasks into `td` issues, automatically check for:

### Missing Rollback for Migrations
```
If task involves "migration" but no rollback task → create:
  "[change] DISCOVERED: Add rollback migration for <task>"
```

### Missing Rate Limiting for API Endpoints
```
If task involves "API endpoint" but no rate limiting → create:
  "[change] DISCOVERED: Add rate limiting to <endpoint>"
```

### Missing Error Handling for External Services
```
If task calls an external service but no circuit breaker → create:
  "[change] DISCOVERED: Add retry/circuit breaker for <service>"
```

### Missing Monitoring/Metrics for Features
```
If feature task but no observability → create:
  "[change] DISCOVERED: Add metrics/logging for <feature>"
```

### Missing Tests
```
If implementation task but no test task → create:
  "[change] DISCOVERED: Write tests for <feature>"
```
