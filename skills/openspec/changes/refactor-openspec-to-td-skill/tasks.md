## 1. Preparation & Restructuring

- [x] 1.1 Create the `references/` directory within `skills/openspec-to-td/`
- [x] 1.2 Copy `skills/td-task-management/references/ai_agent_workflows.md` into `skills/openspec-to-td/references/` or ensure it can be universally loaded by the agent.
- [x] 1.3 Move existing verbose templates, priority logic, and dependency rules from `SKILL.md` into appropriate files in `skills/openspec-to-td/references/`

## 2. Implement Core Mental Model (SKILL.md)

- [x] 2.1 Rewrite the introduction of `SKILL.md` to establish the boundary between defining specifications (OpenSpec) and tracking execution state (td)
- [x] 2.2 Add instructions requiring the use of `td ws start` and `td ws tag` to group generated OpenSpec tasks into manageable multi-issue work sessions
- [x] 2.3 Add instructions mandating the agent to perform a `td ws handoff` (with relevant flags) at the end of its interaction

## 3. Anti-Patterns & Output Variation (SKILL.md)

- [x] 3.1 Define the anti-pattern: "Blindly mapping 1:1 without context" in the "bad/why bad/better" structure
- [x] 3.2 Define the anti-pattern: "Failing to use structure logs or handoffs (e.g. logging 'fixed stuff')" in the "bad/why bad/better" structure
- [x] 3.3 Add the Variation Guidance section, instructing the agent to dynamically group, title, and structure the tasks it generates rather than relying on a rigid loop

## 4. Final Validation & Cleanup

- [x] 4.1 Ensure the main `SKILL.md` contains clear directives to read the documentation in the newly created `references/` directory
- [x] 4.2 Validate the refactored skill using `scripts/analyze_skill.py skills/openspec-to-td/`
- [x] 4.3 Ensure the length of `SKILL.md` is comfortably under 500 lines
