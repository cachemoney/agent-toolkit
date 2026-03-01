## ADDED Requirements

### Requirement: Defined Procedural Anti-Patterns
The skill SHALL list concrete anti-patterns in the "bad pattern/why bad/better alternative" structure, explicitly warning against generic logging (e.g., "fixed bug") and failures to use `td ws handoffs` for state preservation.

#### Scenario: Agent is logging work
- **WHEN** an agent is about to log its progress on a ticket
- **THEN** it avoids the anti-pattern of non-descriptive logging and instead utilizes `--decision` flags for context

### Requirement: Dynamic Output Variation
The skill SHALL require dynamic variation in the naming, grouping, and breakdown of issues based on the specific context of the OpenSpec, intentionally preventing the agent from converging on a repetitive list structure.

#### Scenario: Converting highly complex features
- **WHEN** the OpenSpec contains a complex, multi-faceted requirement
- **THEN** the agent breaks down the issue structure dynamically based on logical boundaries (e.g., DB migration vs. API design) rather than a rigid sequence
