# Joachim AI Dev OS Template

This repository is a starter template for human-gated AI collaboration. It is designed so planning,
patching, and command execution are all explicitly approved.

## Purpose

- Provide a clear role-based workflow (`Explorer`, `Architect`, `Implementer`, `QA/Reviewer`,
  `Security`).
- Enforce human approval gates before coding, patch application, and command execution.
- Keep changes auditable, minimal, and safe.

## Roles

- `Explorer` (read-only): map repo, identify relevant files, risks, and unknowns.
- `Architect`: present 2-3 options with trade-offs; do not decide without explicit user choice.
- `Implementer`: implement only after Gate 1 approval; produce a clean patch.
- `QA/Reviewer`: validate behavior, edge cases, regressions, and DoD.
- `Security`: review auth/session/input boundaries, secrets, injection/SSRF risks.

## Gate Workflow

All work follows a strict approval sequence:

1. `GATE 1 - Plan approval (before coding)`

- Output: plan, impacted paths, risks, test strategy.
- Ask exactly: `Approve plan? (yes/no)`

2. `GATE 2 - Patch approval (before applying)`

- Output: summary, key diffs, DoD status.
- Ask exactly: `Apply patch? (yes/no)`

3. `GATE 3 - Run checks approval (before executing commands)`

- Only after Gate 2 is `yes`.
- List exact commands from `WORKSPACE_CHECKS.md`.
- Ask exactly: `Run these commands? (yes/no)`

## Definition of Done (Strict)

A change is done only if:

- `fmt` passes (or explicit reason).
- `lint/typecheck` passes (or explicit reason).
- `tests` pass (or explicit reason plus follow-up plan).
- Diff is minimal (no unrelated changes).
- Summary includes: what/why, files touched, risks, rollback note.

## Execution Policy

- Never use `sudo`.
- No destructive commands.
- No remote execution (`curl|bash`, etc.).
- No external network actions.
- Never touch files outside repo root.
- Commands may execute only when:
  - Gate 3 is approved.
  - The command is listed in `WORKSPACE_CHECKS.md`.

## Repository Layout

- `AGENTS.md`: core operating policy and gate definitions.
- `WORKSPACE_CHECKS.md`: allowed command catalog (source of truth for checks).
- `agents/prompts/`: role-specific prompt templates.
  - `explorer.md`
  - `architect.md`
  - `implementer.md`
  - `qa.md`
  - `security.md`
- `.codex/config.toml`: local Codex configuration placeholder.

## Recommended Session Flow

1. Run `Explorer` to gather context and identify unknowns.
2. Run `Architect` to provide A/B/C options and explicit recommendation.
3. Get human choice, then produce Gate 1 plan.
4. Run `Implementer` only after Gate 1 is approved.
5. Request Gate 2 before applying patch.
6. Request Gate 3 before running any checks.
7. Run `QA/Reviewer` and `Security` review before final sign-off.

## Quick Start

1. Read `AGENTS.md`.
2. Choose role and task scope.
3. Follow gate prompts exactly.
4. Use only commands listed in `WORKSPACE_CHECKS.md` and only after Gate 3 approval.

## How to Add a New Service

1. Create the service directory and manifest (`package.json`, `Cargo.toml`, etc.).
2. Add exactly one service entry in `WORKSPACE_CHECKS.md` under `Entries`.
3. Fill all fields: `path`, `stack`, `install`, `fmt`, `build`, `lint`, `type`, `test`.
4. Use exact runnable commands for checks; use `N/A` only when a check truly does not apply.
5. If a new entry or command is needed, propose it and wait for human approval before adding it.
