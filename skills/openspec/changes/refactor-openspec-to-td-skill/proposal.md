## Why

The current `openspec-to-td` skill is based on outdated checklist patterns and doesn't leverage the full capabilities of either the `skill-creator-plus` framework or the advanced AI agent workflows available in the `td` CLI. We need to refactor it to establish a strong philosophical mental model for agents and to natively integrate multi-issue work sessions (`td ws`) and structured handoffs, enabling seamless and context-aware implementation of complex OpenSpecs.

## What Changes

- **Adopt Philosophy-First Design**: The skill will establish a mental framework focused on bridging immutable intent (OpenSpec) with mutable execution reality (td), moving away from rigid checklists.
- **Integrate AI Target `td` Workflows**: Replace standard, single-issue ticket creation with instructions on creating and managing `td ws` (work sessions), tagging grouped issues, and utilizing structured `--decision` and `--blocker` logs.
- **Progressive Disclosure**: Abstract verbose templates, dependency detection patterns, and CLI command references into a `references/` subdirectory to keep `SKILL.md` under 500 lines.
- **Implement Explicit Anti-Patterns**: Provide specific "bad/why/better" anti-patterns, such as failing to perform a `td ws handoff` or doing a rote 1:1 translation without critical analysis.
- **Add Variation Guidance**: Ensure the agent varies issue chunking and logging behavior based on the specific context of the OpenSpec.

## Capabilities

### New Capabilities

- `mental-model`: Establishes the core philosophy of the skill, defining the boundaries between defining "what" (OpenSpec) and tracking "execution" (td with handoffs).
- `ai-agent-td-workflows`: Defines the requirement to utilize AI-optimized `td` commands, such as multi-issue work sessions (`td ws start`, `td ws tag`) and state capture (`td ws handoff`).
- `anti-patterns-and-variation`: Details the procedural anti-patterns to avoid (e.g., rigid templates, generic logging) and the variables that should dynamically change in outputs.

### Modified Capabilities

- 

## Impact

- **Agent Behavior**: The agent will begin utilizing `td ws` for related tasks generated from an OpenSpec, improving context retention across sessions.
- **Skill Architecture**: The `openspec-to-td` folder will be restructured to use the `skill-creator-plus` format, adding a `references/` directory.
- **Output Quality**: Agents will execute more intelligently, leaving better breadcrumbs for future sessions through rich `td log` and `td handoff` usage.
