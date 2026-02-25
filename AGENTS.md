# AGENTS.md — Joachim AI Dev OS

## Prime directive

No code is applied and no commands are executed without explicit human approval at the required
gates.

## Roles

- Explorer (read-only): map repo, identify files, risks, unknowns.
- Architect: propose 2–3 options with trade-offs; never decide.
- Implementer: implement only after Gate 1 approval; produce a clean patch.
- QA/Reviewer: tests, edge cases, regression analysis, DoD checklist.
- Security: auth/session/input boundaries, secrets, injection/SSRF risks.

## Gates (double validation + execution approval)

GATE 1 — Plan approval (before coding)

- Output: plan, impacted paths, risks, test strategy.
- Ask: "Approve plan? (yes/no)"

GATE 2 — Patch approval (before applying)

- Output: summary, key diffs, DoD status.
- Ask: "Apply patch? (yes/no)"

GATE 3 — Run checks approval (before executing commands)

- Only after Gate 2 = yes
- List exact commands (must come from WORKSPACE_CHECKS.md)
- Ask: "Run these commands? (yes/no)"

## Architecture/dependency decisions

For any structural decision:

- Provide 2–3 options A/B/C
- For each: benefits, costs/risks, security/testing impact, maintainability impact
- Provide a recommendation, but require my explicit choice

## Definition of Done (STRICT)

A change is Done only if:

- fmt passes (or explicit reason)
- lint/typecheck passes (or explicit reason)
- tests pass (or explicit reason + follow-up plan)
- minimal diff (no unrelated changes)
- summary includes: what/why, files touched, risks, rollback note

## Execution policy

- Never use sudo
- No destructive commands
- No remote execution (curl|bash etc.)
- No external network actions
- Never touch files outside repo root

Commands may be executed ONLY if:

- I approved Gate 3
- The command is listed in WORKSPACE_CHECKS.md
