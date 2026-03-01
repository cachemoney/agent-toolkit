## Context

The `openspec-to-td` skill was designed to convert OpenSpec documents into trackable tasks. However, it relies heavily on rote templates embedded directly in its `SKILL.md` file and uses a rigid, single-issue paradigm suitable for human developers but sub-optimal for AI agents. The `td-task-management/references` indicate a much more robust "Multi-Issue Workflow" for agents, utilizing `td ws start`, `td ws tag`, and structured handoffs (`td ws handoff` with `--done`, `--decision`, etc.). To modernize the skill, it needs to adopt both these advanced agent workflows and the core philosophy-first principles of the `skill-creator-plus` framework.

## Goals / Non-Goals

**Goals:**
- Completely redesign the skill's philosophy around the distinction between defining requirements (OpenSpec) and tracking multi-issue state (td).
- Migrate the implementation instructions to use `td ws` (work sessions) and `td ws handoff` for agent continuity.
- Follow the `skill-creator-plus` principle of progressive disclosure: extracting priority logic, templates, and AI workflow references out of `SKILL.md` and into a `references/` structure.
- Hardcode explicit anti-patterns preventing 1:1 raw mapping of tasks and neglecting to document blockers using `td log`.

**Non-Goals:**
- Creating a new CLI or executable script. We are purely refining the mental framework (the prompt) that guides the agent's interaction with the existing `td` and `openspec` CLIs.
- Changing the structure of the underlying `.beads` / `.td` datastore.

## Decisions

1. **Adopting the Multi-Issue AI Workflow**
   - *Decision:* The skill will require agents to wrap any batch task execution stemming from an OpenSpec in a Work Session (`td ws start "Feature Name"`), tagging all related execution issues (`td ws tag`).
   - *Rationale:* Agents often lose track of state when juggling multiple tasks. Work sessions encapsulate logs and handoffs logically, directly addressing one of the most prominent constraints in AI software development.

2. **Progressive Disclosure of Workflows**
   - *Decision:* Rather than detailing the exact syntax of `td ws`, `td log --decision`, and `td handoff`, the main `SKILL.md` will link to `references/ai_agent_workflows.md` and `references/quick_reference.md`.
   - *Rationale:* `SKILL.md` must remain under 500 lines to function effectively as a core mental model. Dumping CLI syntax into the core prompt violates this.

3. **Explicit Handoff Anti-Patterns**
   - *Decision:* The anti-patterns section will explicitly instruct the agent *not* to log generic strings like "worked on issue," but instead to use structured logs (`td log --decision "Use JWTs"` or `td log --blocker "Missing API"`), ensuring proper state transfer.
   - *Rationale:* Following `skill-creator-plus`, identifying common traps ("bad pattern" vs. "why bad" vs. "better") is essential to curbing generic behavior.

## Risks / Trade-offs

- **Risk:** The agent may forget to load the necessary reference files inside `references/` if it's eager to start executing CLI commands.
  - *Mitigation:* The `SKILL.md` will carry prominent instructions that it MUST use `view_file` to read the referenced `td` AI workflow documentation before executing the batch creation of issues.
