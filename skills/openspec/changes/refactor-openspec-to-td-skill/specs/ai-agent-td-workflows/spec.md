## ADDED Requirements

### Requirement: AI Agent Work Sessions (ws) Integration
The skill SHALL require the agent to group related OpenSpec tasks into `td` work sessions (via `td ws start` and `td ws tag`) rather than individually tracking them piecemeal without context.

#### Scenario: Translating an OpenSpec into tasks
- **WHEN** the agent identifies multiple interconnected tasks that must be executed
- **THEN** it groups those tasks into a unified `td` work session to persist context

### Requirement: Structured Logging and Handoffs
The skill SHALL instruct the agent to use explicit, structured logs (using `--decision`, `--blocker`, `--uncertain`) and mandate the use of `td ws handoff` or `td handoff` before a session terminates.

#### Scenario: An agent encounters ambiguity or context limits
- **WHEN** the agent reaches the end of its context window or is waiting on a blocker
- **THEN** it executes a `td handoff` detailing what was completed and what remains, utilizing appropriate `td` logging flags
